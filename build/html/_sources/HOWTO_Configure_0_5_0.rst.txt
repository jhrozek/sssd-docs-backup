.. raw:: html

   <div class="wiki-toc">

#. 

   #. `About <#About>`__
   #. `Installation <#Installation>`__
   #. `Running SSSD <#RunningSSSD>`__
   #. `Configuration <#Configuration>`__

      #. `Configure NSS for fetching user and group
         information <#ConfigureNSSforfetchinguserandgroupinformation>`__
      #. `Configure PAM for
         authentication <#ConfigurePAMforauthentication>`__
      #. `SSSD daemon configuration <#SSSDdaemonconfiguration>`__

   #. `Configuring services <#Configuringservices>`__

      #. `General configuration
         options <#Generalconfigurationoptions>`__
      #. `NSS configuration options <#NSSconfigurationoptions>`__

   #. `Configuring domains <#Configuringdomains>`__

      #. `Domain configuration options <#Domainconfigurationoptions>`__
      #. `Options valid for proxy
         domains <#Optionsvalidforproxydomains>`__
      #. `The LOCAL domain <#TheLOCALdomain>`__

   #. `Domain configuration examples <#Domainconfigurationexamples>`__

      #. `Example 1: A LOCAL domain that proxies to
         files <#Example1:ALOCALdomainthatproxiestofiles>`__

         #. `PAM config for the proxied LOCAL
            domain <#PAMconfigfortheproxiedLOCALdomain>`__

      #. `Example 2: A standalone LOCAL
         domain <#Example2:AstandaloneLOCALdomain>`__
      #. `Example 3: An LDAP domain using the proxy data
         provider <#Example3:AnLDAPdomainusingtheproxydataprovider>`__

         #. `PAM config for the LDAP
            domain <#PAMconfigfortheLDAPdomain>`__

      #. `Example 4: Authenticating against a native LDAP
         domain <#Example4:AuthenticatingagainstanativeLDAPdomain>`__
      #. `Example 5: Authenticating against a Kerberos
         server <#Example5:AuthenticatingagainstaKerberosserver>`__

.. raw:: html

   </div>

About
-----

SSSD provides a set of daemons to manage access to remote directories
and authentication mechanisms, it provides an NSS and PAM interface
toward the system and a pluggable backend system to connect to multiple
different account sources. It is also the basis to provide client
auditing and policy services for projects like FreeIPA.

SSSD takes advantage of the common set of tools. More information about
those tools can be found
`here. <https://docs.pagure.org/sssd-test2/WikiPage/SSSDTools.html>`__

This page is intended to outline a series of steps needed to install and
configure SSSD. It is aimed at Fedora primarily in terms of commands and
config file placement, but in general, things should work on other
distributions, too.

More information about SSSD can be found on its `​project
page <https://fedorahosted.org/sssd/>`__ or on the Fedora 11 `​Feature
Page <http://fedoraproject.org/wiki/Features/SSSD>`__.

This document was last updated for the 0.5.0 release of SSSD.

Installation
------------

On Fedora (since F11), all that is needed is:

.. code:: wiki

    yum install sssd

If you're using another distribution or want to get the latest bits from
the git repository, clone the SSSD repository:

.. code:: wiki

    git-clone https://pagure.io/SSSD/sssd.git sssd.git
    cd sssd.git

You can now build and install SSSD locally. The complete process is
described into great detail in a text file ``BUILD.txt`` in sssd's
source tree.

Another option is to build and install RPMs from the git tree, issue:

.. code:: wiki

    make rpms

For this to work, you'll also need to have git, and all the build
requirements of SSSD installed. The built RPMs will be in the
``rpmbuild/RPMS`` subdirectory.

Running SSSD
------------

To start the deamon, just start the sssd service:

.. code:: wiki

    service sssd start

For debugging, it may be more comfortable to run the daemon in
foreground:

.. code:: wiki

    /usr/sbin/sssd -i

Another option that might be of interest especially for testing a
configuration is ``-d/--debug-level``, that tells sssd to print more
debug information according to debug level specified. The debug level
can also be specified per-service (see below).

Configuration
-------------

The configuration of the deamon itself is done via editing
``/etc/sssd/sssd.conf``. The file has a ini-style syntax - the file
consists of sections that in turn consist of key=value pairs. If you
need to use more values, separate them with commas. For example:

.. code:: wiki

    [section]
    key = value
    key2 = val,val2

A comment starts with a hash sign (``#``) or a semicolon (``;``). The
data types used are string, integer and bool (with values of
``TRUE/FALSE``).

It is also possible to use an alternate config file by using the
``-c/--config`` parameter of sssd.

For more information on configuring SSSD, see the ``sssd.conf(5)`` man
page that comes with SSSD.

Configure NSS for fetching user and group information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to configure your system to use sssd for user information, SSSD
provides a new *nss\_sss* NSS module. To use it, you need to configure
NSS to use the *sss* name database along the classic UNIX file database.
Edit your ``/etc/nsswitch.conf``:

.. code:: wiki

    passwd:     files sss
    group:      files sss

Configure PAM for authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configuring PAM should be done with extreme care. A mistake or typo in
the PAM config file can lock you out of the system completely. Always
backup your config files before doing any changes and keep a session
open in order to be able to revert changes you do.

Enable the use of the SSSD for PAM. If you are changing the default PAM
config on Fedora, it should look like:

.. code:: wiki

    #%PAM-1.0
    auth        required      pam_env.so
    auth        sufficient    pam_fprintd.so
    auth        sufficient    pam_unix.so nullok
    auth        sufficient    pam_sss.so use_first_pass
    auth        requisite     pam_succeed_if.so uid >= 500 quiet
    auth        required      pam_deny.so

    account     required      pam_unix.so broken_shadow
    account     sufficient    pam_sss.so
    account     sufficient    pam_localuser.so
    account     sufficient    pam_succeed_if.so uid < 500 quiet
    account     required      pam_permit.so

    password    requisite     pam_cracklib.so try_first_pass retry=3
    password    sufficient    pam_unix.so sha512 shadow nullok use_authtok
    password    sufficient    pam_sss.so use_first_pass
    password    required      pam_deny.so

    session     optional      pam_keyinit.so revoke
    session     required      pam_limits.so
    session     [success=1 default=ignore] pam_succeed_if.so service in crond quiet use_uid
    session     sufficient    pam_unix.so
    session     required      pam_sss.so

If your operating system provides a tool to configure PAM, e.g.
authconfig for Fedora based systems, you can use this, too. Select LDAP
authentication with this tool and then substitute pam\_ldap.so by
pam\_sss.so in all files below /etc/pam.d or in /etc/pam.conf.

Recent PAM implementations allow to include PAM configurations, e.g.

.. code:: wiki

    ...
    session     include      system-auth
    session     optional     pam_console.so
    ...

If you use includes please note that in the example above
pam\_console.so is not executed if a sufficient condition from
system-auth returns PAM\_SUCCESS.

Some of the later examples use a proxy auth provider between pam\_sss
and other PAM modules using the ``pam-target`` configuration directive
that references a file in ``/etc/pam.d``. It is important **not** to
include ``pam_sss.so`` modules in these proxied targets, otherwise the
PAM stack may go into a loop.

SSSD daemon configuration
~~~~~~~~~~~~~~~~~~~~~~~~~

I suggest that you start with the ``/etc/sssd/sssd.conf`` file that
comes with the Fedora RPMs as most of the stuff is already there. The
source distribution contains an example config file in the
``server/examples`` subdirectory.

Configuring services
--------------------

Individual pieces of SSSD functionality are provided by special SSSD
services that are started and stopped together with SSSD. The services
provided by SSSD have their own configuration inside
``[services/<NAME>]`` sections. The ``[services]`` section also lists
the services that are active and should be started when sssd starts
within the ``activeServices`` directive.

We use several services in this HOWTO - NSS, Data Provider, PAM and a
service called monitor that watches over other services, starts or
restarts them as needed.

-  An NSS provider service that answers NSS requests from the
   ``nss_sss`` module
-  A PAM provider service that manages a PAM conversation through the
   ``pam_sss`` PAM module
-  A data provider front-end service for populating cache data from
   back-ends

.. code:: wiki

    [services]
    description = Local Service Configuration
    activeServices = nss, dp, pam

    [services/monitor]
    description = Service Monitor Configuration
    sbusTimeout = 30

    [services/dp]
    description = Data Provider Configuration

    [services/pam]
    description = PAM Responder Configuration

    [services/nss]
    description = NSS Responder Configuration
    filterGroups = root
    filterUsers = root

The following subsections list only the most important configuration
optiosn. See the ``sssd.conf(5)`` manual page that is shipped with SSSD
for all the configuration options available.

General configuration options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**debug-level** (integer)
    This is a per-service setting (that is, it can appear in any of
    [services/<NAME>] sections that sets the debug level for that
    service.
**reconnection\_retries** (integer)
    Number of times services should attempt to reconnect in the event of
    a Data Provider crash or restart before they give up

NSS configuration options
~~~~~~~~~~~~~~~~~~~~~~~~~

**EnumCacheTimeout** (integer)
    How long should ``nss_sss`` cache enumerations (requests for info
    about all users)
**EntryCacheTimeout** (integer)
    How long should ``nss_sss`` cache positive cache hits (that is,
    queries for valid database entries) before asking the backend again
**EntryNegativeTimeout** (integer)
    How long should ``nss_sss`` cache negative cache hits (that is,
    queries for invalid database entries, like nonexitent ones) before
    asking the backend again
**filterUsers**, **filterGroups** (string)
    Exclude certain users from being fetched from the ``sss`` NSS
    database. This is particularly useful for system accounts like root.
**filterUsersInGroups** (bool)
    If you want filtered user still be group members set this option to
    false.

Configuring domains
-------------------

A domain is a database containing user information. SSSD can use more
domains at the same time, but at least one must be configured or SSSD
won't start. Using SSSD domains, it is possible to use several LDAP
servers providing several unique namespaces.

Add new domains configurations into ``[domains/<NAME>]`` sections. Then
add the list of domains (in the order you want them to be queried) in
the 'domains' attribute of the domains section. For example, to use only
``LOCAL`` domain:

.. code:: wiki

    [domains]
    description = Domains served by SSSD
    domains = LOCAL

The following subsections will list examples of configuring different
types of domains.

Domain configuration options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These configuration options can be present in a domain configuration
section, that is, in a section called ``[domains/<NAME>]``.

**minId,maxId** (integer)
    UID limits for the domain. If a domain contains entry that is
    outside these limits, it is ignored
**magicPrivateGroups** (bool)
    By using the Magic Private Groups option, you are imposing two
    limitations to the ID space and name space:

    #. users and groups share a common name space, there can never be a
       group with a same name as a user
    #. users and groups share a common ID space, there can never be a
       group with a same ID as a user

Using Magic Private groups bring the benefit of better Windows
Interoperability (in Windows, the ID and name spaces are unique) and
also avoids creating a group for every user, thus cluttering the group
space. Also, for NSS calls, every user is actually returned as user's
private group without having to explicitly create the group, thus having
the same effect as User Private Groups

**enumerate** (integer)
    Determines if a domain can be enumerated. This parameter can have
    one of the following values:

    -  1 = Enumerate users
    -  2 = Enumerate groups
    -  3 = Enumerate both

**timeout** (integer)
    Timeout in seconds for this particular domain. Raising this timeout
    might prove useful for slower backends like distant LDAP servers.
    The default is 0 (no timeout).
**cache-credentials** (bool)
    Determines if user credentials are also cached in the local LDB
    cache
**legacy** (bool)
    A legacy domain is a strictly POSIX domain in terms of attributes it
    has, also groups can't be nested.
**store-legacy-passwords** (bool)
    Whether to also store passwords in a legacy domain
**provider** (string)
    The Data Provider backend to use for this domain. Currently
    supported backends are:

    -  proxy: Support a legacy NSS provider
    -  local: SSSD internal local provider
    -  ldap: ldap provider
    -  files: Support for legacy /etc/passwd and /etc/shadow

**useFullyQualifiedNames** (bool)
    If set to TRUE, all requests to this domain must use fully qualified
    names. For example, if used in LOCAL domain that contains a "test"
    user, ``getent passwd test`` wouldn't find the user while
    ``getent passwd test@LOCAL`` would
**auth-module** (string)
    The authentication module used for the domain. Supported auth
    modules are:

    -  ldap for native LDAP authentication. See sssd-ldap(5) for more
       information on configuring LDAP.
    -  krb5 for Kerberos authentication. See sssd-krb5(5) for more
       information on configuring Kerberos.
    -  proxy for relaying authentication to some other PAM target.

Options valid for proxy domains
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**pam-target** (string)
    The proxy target PAM proxies to. If not set, a default setting of
    ``sssd_pam_proxy_default`` is used.
**libName** (string)
    The name of NSS library. The NSS functions searched for in the
    library are in the form of ``_nss_$(libName)_$(function)``, for
    example ``_nss_files_getpwent``.

The LOCAL domain
~~~~~~~~~~~~~~~~

There is a special domain in SSSD named *LOCAL*. Its backend is stored
on disk in a format called *LDB*, an on-disk LDAP-like database. This
domain can be used together with classic UNIX files
(``/etc/passwd, /etc/shadow``) or completely substitute it.

One difference in comparison with the classic files is that groups in
the LOCAL backend can be nested (only non-legacy LOCAL backend, see
below). The LOCAL domain is also meant to contain additional user
information such as user picture or keyboard settings.

To manage users in the LOCAL backend, SSSD comes with a set of tools
that resemble their shadow-utils counterparts in names as well as
parameters. The tools include *sss\_useradd*, *sss\_groupadd* for adding
users and groups, *sss\_userdel*, *sss\_groupdel* for removing them and
*sss\_usermod*, *sss\_groupmod* for changing their attributes. You can
see details about tools usage by running them with the ``--help``
argument.

Domain configuration examples
-----------------------------

Example 1: A LOCAL domain that proxies to files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example ``LOCAL`` domain that proxies to ``/etc/passwd`` and
``/etc/group`` files. This configuration is meant mostly as a migration
path to be able to store additional information about users while still
keeping ``/etc/passwd`` authoritative.

.. code:: wiki

    [domains/LOCAL]
    description = LOCAL migration domain
    enumerate = 3
    minId = 500
    magicPrivateGroups = FALSE
    legacy = TRUE

    provider = files

Note that the "files" provider is really an alias for

.. code:: wiki

    provider = proxy
    libName = files

PAM config for the proxied LOCAL domain
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To enable authentication via the PAM stack, add these options to the
domain config:

.. code:: wiki

    auth-module = proxy
    pam-target = sssdproxylocal

This way, the authentication requests will be proxied via file
``/etc/pam.d/sssdproxylocal`` that will provide the usual module
interfaces.

This is how the ``/etc/pam.d/sssdproxylocal`` file should look like:

.. code:: wiki

    auth        required      pam_unix.so
    account     required      pam_unix.so
    password    required      pam_unix.so
    session     required      pam_unix.so

Example 2: A standalone LOCAL domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Put the following definition of LOCAL domain into your sssd config file:

.. code:: wiki

    [domains/LOCAL]
    description = LOCAL Users domain
    enumerate = 3
    minId = 500
    maxId = 999
    legacy = FALSE
    magicPrivateGroups = TRUE
    provider = local

Now, add a LOCAL user using sssd management tools:

.. code:: wiki

    sss_useradd testuser1

Note that contrary to useradd from shadow-utils sss\_useradd does not
create home directory of the new user. One option to create it might be
using *pam\_mkhomedir*.

If you configured NSS to use the SSS domain, you should be able to
request the user information now:

.. code:: wiki

    getent passwd testuser1@LOCAL

Changing the user's password and logging in should be also possible now:

.. code:: wiki

    passwd testuser1
    ssh testuser1@localhost

Example 3: An LDAP domain using the proxy data provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configuring a domain that uses user information in LDAP requires a
running LDAP server and your machine configured as an LDAP client for
that server. For example, for a server running on ldap.example.com with
base of "dc=example,dc=com" using simple bind authentication, your
/etc/ldap.conf would include the following:

.. code:: wiki

    base dc=example,dc=com
    uri ldap://ldap.example.com:389
    ssl no

The domain configuration in sssd config would look like this:

.. code:: wiki

    [domains/LDAP]
    description = Proxy request to our LDAP server
    enumerate = 3
    minId = 1000
    legacy = TRUE
    provider = proxy
    libName = ldap
    cache-credentials = TRUE

Also, don't forget to add the domain to the list of active domains:

.. code:: wiki

    domains = LOCAL,LDAP

You should be able to authenticate using LDAP credentials:

.. code:: wiki

    ssh ldapuser@localhost

Now comes the fun part - the caching mechanism. Measure the time to get
information about user from the LDAP server:

.. code:: wiki

    time getent passwd ldapuser

OK, it may have taken even few seconds, depending on the connection to
your LDAP server. Do the same again:

.. code:: wiki

    time getent passwd ldapuser

The second ``getent`` should return almost immediatelly, leveraging the
caching mechanism.

Go to your LDAP server and turn it off (or shutdown the network). You
should still be able to get information from the cache, even log in
using the LDAP credentials - that is possible because the credentials
are cached in LDB, the same on-disk LDAP database that is used for
storing LOCAL accounts.

.. code:: wiki

    service network stop
    getent passwd ldapuser
    ssh ldapuser@localhost

The results are retreived from cache *after* the timeout interval.

PAM config for the LDAP domain
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To enable authentication via the PAM stack, add these options to the
domain config:

.. code:: wiki

    auth-module = proxy
    pam-target = sssdproxyldap

This way, the authentication requests will be proxied via file
``/etc/pam.d/sssdproxyldap`` that will provide the usual module
interfaces.

This is how the ``/etc/pam.d/sssdproxyldap`` file should look like:

.. code:: wiki

    auth        required      pam_ldap.so
    account     required      pam_ldap.so
    password    required      pam_ldap.so
    session     required      pam_ldap.so

Example 4: Authenticating against a native LDAP domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Similarly to configuring a proxy LDAP domain, a native LDAP domain
requires a running LDAP server to authenticate against. The client
configuration is done in ``/etc/sssd/sssd.conf``.

The domain configuration in sssd config would look like this:

.. code:: wiki

    [domains/LDAP]
    description = A native LDAP domain
    enumerate = 3
    legacy = TRUE
    cache-credentials = TRUE

    provider = ldap

    auth-module = ldap
    ldapUri = ldap://ldap.mydomain.org
    userSearchBase = dc=mydomain,dc=org
    tls_reqcert = demand

All the parameters for a native LDAP domain are described in the
``sssd-ldap(5)`` manual page.

Example 5: Authenticating against a Kerberos server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to set up Kerberos authentication, you need to know the address
of your KDC and the Kerberos realm. Using these parameters, the
configuration is very simple:

.. code:: wiki

    [domains/KRBDOMAIN]
    auth-module = krb5
    krb5KDCIP = 192.168.1.1
    krb5REALM = EXAMPLE.COM

All the parameters for a configuring Kerberos authentication are
described in the ``sssd-krb5(5)`` manual page.
