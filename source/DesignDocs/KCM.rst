KCM server for SSSD
===================

Related ticket(s):

-  `​https://fedorahosted.org/sssd/ticket/2887 <https://fedorahosted.org/sssd/ticket/2887>`__

External links:

-  `​MIT wiki KCM
   documentation <http://k5wiki.kerberos.org/wiki/Projects/KCM_client>`__

Having the KCM service might also enable us to solve tickets such as:

-  `​- RFE To delete kerberos tickets once the user logs
   out <https://fedorahosted.org/sssd/ticket/2551>`__
-  `​- RFE Expand kerberos ticket
   renewal <https://fedorahosted.org/sssd/ticket/1723>`__
-  `​- RFE Add a general-purpose D-Bus responder for ticket
   monitoring <https://fedorahosted.org/sssd/ticket/1497>`__

Problem statement
~~~~~~~~~~~~~~~~~

This design page describes adding a new SSSD responder, called
``sssd_kcm``. This component would manage Kerberos credential caches and
store them in SSSD's secrets storage.

Use cases
~~~~~~~~~

-  A sysadmin needs to deploy applications in containers without
   worrying about applications clobbering each other's credential caches
   in a kernel keyring as keyrings are not namespaced
-  A user wants to keep having her Kerberos ticket automatically renewed
   regardless of the ticket being acquired through a PAM conversation
   with SSSD or from the command line with kinit
-  A system admin wants to leverage a collection-aware credentials cache
   for most of applications on their systems, yet enable a legacy
   application that can only work with a FILE-based ccache to
   interoperate with them

Overview of the solution
~~~~~~~~~~~~~~~~~~~~~~~~

Over time, both libkrb5 and SSSD used different credential cache types
to store Kerberos credentials - going from a simple file-based storage
(``FILE:``) to a directory (``DIR:``) and most recently a kernel-keyring
based cache (``KEYRING:``).

Each of these caches has its own set of advantages and disadvantages.
The ``FILE`` ccache is very widely supported, but does not support
multiple primary caches. The ``DIR`` cache does, but creating and
managing the directories including proper access control can be tricky.
The ``KEYRING`` cache is not well suited for cases where multiple
semi-isolated environments might share the same kernel. Managing
credential caches' lifetime is not well solved in neither of these cache
types automatically, only with the help of a daemon like SSSD.

An interesting credentials cache that might solve the issues mentioned
above is ``KCM``. With KCM, the Kerberos caches are not stored in a
"passive" store, but managed by a daemon. In this setup, the Kerberos
library (typically used through an application, like for example,
``kinit``) is a "KCM client" and the daemon is being referred to as a
"KCM server".

Having the Kerberos credential caches managed by a daemon has several
advantages:

-  the daemon is stateful and can perform tasks like Kerberos credential
   cache renewals or reaping old ccaches. Some tasks, like renewals are
   possible already with SSSD, but only for tickets that SSSD itself
   acquired (typically via a login through ``pam_sss.so``) and tracks.
   Tickets acquired otherwise, most notably though kinit wouldn't be
   tracked and renewed.
-  since the process runs in userspace, it is subject to UID
   namespacing, `​unlike the kernel
   keyring <http://www.projectatomic.io/blog/2014/09/yet-another-reason-containers-don-t-contain-kernel-keyrings/>`__
-  unlike the kernel keyring-based cache, which is entirely dependant on
   UIDs of the caller and in a containerized environment is shared
   between all containers, the KCM server's entry point is a UNIX socket
   which can be bind-mounted to only some containers
-  the protocol between the client and the server can be extended for
   custom operations such as dumping a cache in a different format to a
   specific location. This would be beneficial for applications that
   only understand a certain Kerberos ccache type - for example, some
   legacy applications only know how to deal with a FILE-based cache,
   thus preventing the use of cache collections

Only the Heimdal Kerberos implementation currently implements a KCM
server, but both Heimdal and MIT implement the client-side operations
(in libkrb5) to manage KCM-based Kerberos ccaches. This design page
describes adding a KCM server to SSSD. While it's of course possible to
create a completely standalone daemon that would implement a KCM server,
doing so in the context of SSSD has several advantages, notably:

-  An easy access to the authentication provider of SSSD that already
   has existing and tested code to renew Kerberos credentials on user's
   behalf
-  SSSD already has a D-Bus API that could publish information about
   Kerberos tickets and for example emit signals that a graphical
   application can consume
-  SSSD has a 'secrets provider' to store data at rest. It makes sense
   to leverage this component to store Kerberos ccaches persistently

Implementation details
~~~~~~~~~~~~~~~~~~~~~~

A new SSSD responder will be added. Since accessing the Kerberos
credentials is quite an infrequent operation, the responder will be
socket-activated.

This responder would implement the same subset of the KCM protocol the
MIT client libraries implement. Contrary to Heimdal's KCM server that
just stores the credential caches in memory, the SSSD KCM server would
store the ccaches in the secrets database through the sssd-secret's
responder `​public REST
API <https://jhrozek.fedorapeople.org/sssd/1.14.2/man/sssd-secrets.5.html>`__.

For user credentials the KCM Server would use a secrets responder URI
like ``/kcm/users/1234/X`` where 1234 is the user ID and X is the
residual. The client then gets assigned a KRB5CCNAME of KCM:1234:X.
Internally in the secrets responder we will store the credential caches
under a new base DN ``cn=kcm``.

The secret responder's quota on secrets must be made modular to allow
different number of secrets per base DN (so, different number of secrets
and credentials pretty much). What to do in case the quota is reached is
debatable - we should probably first remove service (non-TGT) tickets
first for valid TGTs and if that's not possible, just fail. A failure in
this case would be no different than a failure if a disk is full when
trying to store a FILE-based ccache.

The KCM responder would renew the user credentials by starting a tevent
timer which would then contact the SSSD Data Provider for the given UID
and principal, asking for the credentials to be renewed. Another tevent
timer would reap and remove a ccache that reaches its lifetime.

In the future, SSSD-specific operations such as writing out a FILE-based
ccache might be added. The SSSD D-Bus interface would also be extended
to publish information about credentials activity (such as - a ticket
being acquired, a ticket was renewed etc)

Configuration changes
~~~~~~~~~~~~~~~~~~~~~

The SSSD KCM responder would use the same common options like other SSSD
services such as idle timeout.

We will also add a configurable KCM socket location later, which will
default to ``/var/run/.heim_org.h5l.kcm-socket`` mostly because that's
what MIT defaults to as well.

Packaging changes
~~~~~~~~~~~~~~~~~

The KCM responder will be packaged in its own subpackage called
``sssd-kcm``. This subpackage will not be installed by default, in other
words it would not be required by the sssd meta-package, but a user will
have to install this subpackage manually. Except for the KCM responder
and its documentation, the package will also contain a krb5.conf snippet
that enables the ``KCM`` ccache type, so switching to the new
credentials cache should be as easy as installing the package.

The subpackage will also handle enabling the systemd-activated socket.

How To Test
~~~~~~~~~~~

In order for the admin to start using the KCM service, the sssd-kcm
responder's systemd service must be enabled. Then, libkrb5 must also be
configured to use KCM as its default ccache type in ``/etc/krb5.conf``

.. code:: wiki

        [libdefaults]
        default_ccache_name = KCM:

After that, all common operations like kinit, kdestroy or login through
pam\_sss should just work and store their credentials in the KCM server.

The KCM server must implement access control correctly, so even trying
to access other user's KCM credentials by setting KRB5CCNAME to
``KCM:1234:RESIDUAL`` would not work (except for root).

Restarting the KCM server or rebooting the machine must persist the
tickets.

As far as automatic unit and integration testing is required, we need to
make sure that MIT's testsuite passes with Kerberos ccache defaulting to
KCM and SSSD KCM daemon running. In the SSSD upstream, we should write
integration tests that run a MIT KDC under socket\_wrapper to exercise
the KCM server.

Use-case: separating ccaches of root users in containers, SSSD is running on the host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this scenario, SSSD is running on the host and an application is
running in a container. However, the application in a container runs as
root and we want to keep its credential caches separate from the
credential caches on the host. On the other hand we want to share the
kerberos credentials between the containers.

#. Create a directory that will contain the KCM daemon socket:

   .. code:: wiki

           host # mkdir /var/run/kcm

#. Configure sssd-kcm to spawn the KCM socket there. Add the following
   to ``/etc/sssd/sssd.conf`` on the host

   .. code:: wiki

           [kcm]
           socket_path = /var/run/kcm/kcm.sock

#. Restart sssd on the host to pick up the changes and verify the socket
   is there

   .. code:: wiki

           host # systemctl restart sssd.service
           host # ls -l /var/run/kcm/
           srw-rw-rw-. 1 root root 0 Nov 25 14:08 kcm.sock

#. In order for the root user in the container to be represented as a
   different UID to the host, we need to create a subordinate UID and
   GID ranges that the ID from the containers will be mapped to. This
   range takes a required argument, which must correspond to a user that
   exists in ``/etc/passwd`` (although domain users `​will be supported
   starting with docker
   1.13 <https://github.com/docker/docker/pull/27599>`__). The
   subordinate ranges are created in ``/etc/subuid`` and ``/etc/subgid``
   on the host. Please refer to the `​docker
   documentation <https://success.docker.com/Datacenter/Apply/Introduction_to_User_Namespaces_in_Docker_Engine>`__
   for more details on Docker user namespaces. For example:

   .. code:: wiki

           host # grep jhrozek /etc/subgid
           jhrozek:50000:65536
           host # grep jhrozek /etc/subuid
           jhrozek:50000:65536

#. Configure the docker daemon to use this subordinate ID namespace by
   changing this line in ``/etc/sysconfig/docker``

   .. code:: wiki

           OPTIONS='--selinux-enabled --log-driver=journald --userns-remap=jhrozek'

#. Restart the docker service. Please note that docker stores the images
   under a per-user-namespace directory, so you'll need to pull the
   images again.

   .. code:: wiki

           host # systemctl restart docker.service

#. Start a container, bind-mounting the ``/var/run/kcm`` directory from
   the host to make the KCM socket accessible:

   .. code:: wiki

           host # docker run -t -i -h=kcmtest1 -v=/var/run/kcm:/var/run/kcm fedora /bin/bash

#. Configure the container's Kerberos config file to use ``KCM:`` as the
   credential cache. Edit ``/etc/krb5.conf`` in the container:

   .. code:: wiki

           [libdefaults]
           default_realm = IPA.TEST
           dns_lookup_realm = true
           dns_lookup_kdc = true
           rdns = false
           default_ccache_name = KCM:
           kcm_socket = /var/run/kcm/kcm.sock

           [realms]
           IPA.TEST = {
               pkinit_anchors = FILE:/etc/ipa/ca.crt
               kdc = unidirect.ipa.test
           }

#. Acquire Kerberos credentials for the ``admin`` IPA user. Note that
   despite the user's UID value in the container is 0, the UID is
   translated to 50000 on the host, which is what the KCM server then
   uses to store the credentials at

   .. code:: wiki

           [root@kcmtest1 /]# id
           uid=0(root) gid=0(root) groups=0(root)

           [root@kcmtest1 /]# kinit admin
           Password for admin@IPA.TEST: 

           [root@kcmtest1 /]# klist 
           Ticket cache: KCM:50000
           Default principal: admin@IPA.TEST

           Valid starting     Expires            Service principal
           11/25/16 15:29:38  11/26/16 15:29:37  krbtgt/IPA.TEST@IPA.TEST

#. Start another container, bind-mounting the ``/var/run/kcm`` directory
   from the host to make the KCM socket accessible:

   .. code:: wiki

           host # docker run -t -i -h=kcmtest2 -v=/var/run/kcm:/var/run/kcm fedora /bin/bash

#. Configure ``krb5.conf`` in the same manner and run klist (without
   kinit!) in the container. Note we can access the same ccache the
   first container acquired

   .. code:: wiki

           [root@kcmtest2 /]# klist 
           Ticket cache: KCM:50000
           Default principal: admin@IPA.TEST

           Valid starting     Expires            Service principal
           11/25/16 15:29:38  11/26/16 15:29:37  krbtgt/IPA.TEST@IPA.TEST

#. root on the host cannot access the same cache by default. An
   interesting property of the KCM protocol is that UID 0 can list all
   ccaches or all other UIDs, though.

   .. code:: wiki

           host # klist 
           klist: Matching credential not found

Note - if the container is running as a different user (using the
``USER`` directive specified in the container's ``Dockerfile``), then
the ID the KCM server is contacted with depends on whether ID namespaces
are used. Without the ID namespaces, the host receives the UID of the
container user as-is. If user namespaces are in effect, then the ID of
the container user is translated into the subordinate namespace. For
example, if the namespace above was still in effect, a container user
running as uid=1000 would be translated into user with uid=51000 on the
host.

Use-case: separating ccaches of containers from ccaches of the host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this use-case, SSSD is running in one container and keeps track of
ccaches in other containers that are completely separated from the host
environment. The containers must also share the credential caches
between one another.

#. Start a container that will run an SSSD instace with the KCM service.
   We name the container ``kcmserver`` and assign a volume called
   ``/kcmserver`` to this container.

   .. code:: wiki

           host# docker run -t -i --name=kcmserver -h=kcmserver -v=/kcmserver fedora /bin/bash

#. Install and configure sssd in the container. The configuration can be
   pretty minimal, but the important piece is the KCM socket in the
   Docker volume at ``/kcmserver/kcm.socket``. Please note that even the
   domain should hopefully not be required in future versions where the
   files provider will be ran by default instead.

   .. code:: wiki

           kcmserver # dnf -y install sssd-kcm
           kcmserver # cat /etc/sssd/sssd.conf
           [sssd]
           services = kcm
           domains = local

           [kcm]
           socket_path = /kcmserver/kcm.socket

           [domain/local]
           id_provider = local

#. Start another container that will represent an application. Make sure
   the container mounts the volume from the ``kcmserver`` instance.

   .. code:: wiki

           host # docker run -t -i --name=kcmclient -h=kcmclient --volumes-from=kcmserver fedora /bin/bash

#. Observe that the container mounted the volume and the volume includes
   the KCM server socket

   .. code:: wiki

           kcmclient # ll /kcmserver/kcm.socket 
           srw-rw-rw-. 1 root root 0 Nov 29 16:21 /kcmserver/kcm.socket

#. Configure ``/etc/krb5.conf`` to use ``KCM:`` as the credentials cache
   and point libkrb5 to the KCM socket

   .. code:: wiki

           kcmclient # cat /etc/krb5.conf
           # To opt out of the system crypto-policies configuration of krb5, remove the
           # symlink at /etc/krb5.conf.d/crypto-policies which will not be recreated.
           includedir /etc/krb5.conf.d/

           [logging]
           default = FILE:/var/log/krb5libs.log
           kdc = FILE:/var/log/krb5kdc.log
           admin_server = FILE:/var/log/kadmind.log

           [libdefaults]
           default_realm = IPA.TEST
           dns_lookup_realm = true
           dns_lookup_kdc = true
           rdns = false
           ticket_lifetime = 24h
           forwardable = true
           udp_preference_limit = 0
           default_ccache_name = KCM:
           kcm_socket = /kcmserver/kcm.socket


           [realms]
           IPA.TEST = {
               pkinit_anchors = FILE:/etc/ipa/ca.crt
               kdc = unidirect.ipa.test
           }

#. Acquire Kerberos credentials in the ``kcmclient`` container

   .. code:: wiki

           kcmclient # kinit admin
           Password for admin@IPA.TEST: 
           kcmclient # klist 
               Ticket cache: KCM:0
               Default principal: admin@IPA.TEST

               Valid starting     Expires            Service principal
               11/29/16 16:21:28  11/30/16 16:21:26  krbtgt/IPA.TEST@IPA.TEST

#. Observe that these credentials are not visible to the host

   .. code:: wiki

           host # klist
           klist: Matching credential not found

#. Start another container as another KCM client, configure its
   ``krb5.conf`` configuration file in the same manner. As long as this
   container runs as the same UID as the first KCM client, the
   credentials should be visible in this container immediatelly without
   having to acquire them:

   .. code:: wiki

           kcmclient # klist 
               Ticket cache: KCM:0
               Default principal: admin@IPA.TEST

               Valid starting     Expires            Service principal
               11/29/16 16:21:28  11/30/16 16:21:26  krbtgt/IPA.TEST@IPA.TEST

How To Debug
~~~~~~~~~~~~

The SSSD KCM server would use the same DEBUG facility as other SSSD
services. In order to debug the client side operations, setting the
``KRB5_TRACE`` variable might come handy.

When debugging the setup, the admin might also inspect the SSSD secrets
database (if permissable by SELinux policy) to see what credential
caches have been stored by the SSSD.

Authors
~~~~~~~

-  Jakub Hrozek <`​jhrozek@redhat.com <mailto:jhrozek@redhat.com>`__>
-  Simo Sorce <`​simo@redhat.com <mailto:simo@redhat.com>`__>
