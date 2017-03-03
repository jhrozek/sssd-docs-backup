.. raw:: html

   <div class="wiki-toc">

#. 

   #. `About <#About>`__
   #. `Installation <#Installation>`__
   #. `Upgrading from a previous
      version <#Upgradingfromapreviousversion>`__
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
      #. `Options valid for proxy identity
         domains <#Optionsvalidforproxyidentitydomains>`__
      #. `The LOCAL provider <#TheLOCALprovider>`__

   #. `Domain configuration examples <#Domainconfigurationexamples>`__

      #. `Example 1: A standalone LOCAL
         domain <#Example1:AstandaloneLOCALdomain>`__
      #. `Example 2: Authenticating against a native LDAP
         domain <#Example2:AuthenticatingagainstanativeLDAPdomain>`__
      #. `Example 3: Authenticating against a Kerberos
         server <#Example3:AuthenticatingagainstaKerberosserver>`__

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
page <https://fedorahosted.org/sssd/>`__.

This document is being updated for the development version of SSSD.

Installation
------------

On Fedora (since F11), all that is needed is:

.. code:: wiki

    yum install sssd

If you're using another distribution or want to get the latest bits from
the git repository, clone the SSSD repository:

.. code:: wiki

    git clone https://pagure.io/SSSD/sssd.git sssd.git
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

Upgrading from a previous version
---------------------------------

Starting from version 0.6.0, SSSD uses a different and simplified
configuration file format. Existing config files need to be migrated to
the new format and SSSD provides a script to automate the migration
process.

If you are using RPMs, the script will be run automatically when
upgrading the package to the new version. Your ``/etc/sssd/sssd.conf``
config file will be upgraded in-place, copying the old one to
``/etc/sssd/sssd.conf.bak``.

If you need to run the script manually, perhaps when using SSSD built
from source, the synopsis is as follows:

.. code:: wiki

        upgrade_config.py [-f FILE] [-o OUTFILE] [--verbose] [--no-backup]

When not given, both ``FILE`` and ``OUTFILE`` default to
``/etc/sssd/sssd.conf``, performing the conversion in-place and copying
the original to ``/etc/sssd/sssd.conf.bak``. Adding the ``--no-backup``
option would turn off producing the backup files.

Running SSSD
------------

To start the daemon, just start the sssd service:

.. code:: wiki

    service sssd start

For debugging, it may be more comfortable to run the daemon in
foreground:

.. code:: wiki

    /usr/sbin/sssd -i

Another option that might be of interest especially for testing a
configuration is ``-d/--debug-level``, that tells sssd to print more
debug information according to debug level specified. The debug level
can also be specified per-service (see below). Timestamps can be added
to the debug information by specifying '--debug-timestamps'

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
NSS to use the *sss* name database along with the classic UNIX file
database. Edit your ``/etc/nsswitch.conf``:

.. code:: wiki

    passwd:     files sss
    group:      files sss

The recent glibc versions also include an ``initgroups`` database. In
order for the initgroups operation (which is performed during login) to
function correctly, either append the ``sss`` module to the
``initgroups`` line, too:

.. code:: wiki

    initgroups: files sss

Or comment out the ``initgroups`` line altogether.

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
    # This file is auto-generated.
    # User changes will be destroyed the next time authconfig is run.
    auth        required      pam_env.so
    auth        sufficient    pam_unix.so nullok try_first_pass
    auth        requisite     pam_succeed_if.so uid >= 500 quiet
    auth        sufficient    pam_sss.so use_first_pass
    auth        required      pam_deny.so

    account     required      pam_unix.so broken_shadow
    account     sufficient    pam_localuser.so
    account     sufficient    pam_succeed_if.so uid < 500 quiet
    account     [default=bad success=ok user_unknown=ignore] pam_sss.so
    account     required      pam_permit.so

    password    requisite     pam_cracklib.so try_first_pass retry=3
    password    sufficient    pam_unix.so sha512 shadow nullok try_first_pass use_authtok
    password    sufficient    pam_sss.so use_authtok
    password    required      pam_deny.so

    session     required      pam_mkhomedir.so umask=0022 skel=/etc/skel/
    session     optional      pam_keyinit.so revoke
    session     required      pam_limits.so
    session     [success=1 default=ignore] pam_succeed_if.so service in crond quiet use_uid
    session     sufficient    pam_sss.so
    session     required      pam_unix.so

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
comes with the Fedora RPMs as it contains comments to aid you. The
source distribution contains an example config file in the
``server/examples`` subdirectory.

Configuring services
--------------------

Individual pieces of SSSD functionality are provided by special SSSD
services that are started and stopped together with SSSD. The services
provided by SSSD have their own configuration sections. The ``[sssd]``
section also lists the services that are active and should be started
when sssd starts within the ``services`` directive.

At present, we use three services in this HOWTO - NSS, PAM and a service
called monitor that watches over other services, starts or restarts them
as needed.

-  An NSS provider service that answers NSS requests from the
   ``nss_sss`` module
-  A PAM provider service that manages a PAM conversation through the
   ``pam_sss`` PAM module
-  The monitor service maintains the other processes and restarts them
   if they die. Its options are specified in the [sssd] section

.. code:: wiki

    [sssd]
    services = nss, pam
    sbus_timeout = 30

    [nss]
    filter_users = root
    filter_groups = root

The following subsections list only the most important configuration
optiosn. See the ``sssd.conf(5)`` manual page that is shipped with SSSD
for all the configuration options available.

General configuration options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**debug\_level** (integer)
    This is a per-service setting (that is, it can appear in any of the
    service sections and sets the debug level for that service.
**reconnection\_retries** (integer)
    Number of times services should attempt to reconnect in the event of
    a Data Provider Backend crash or restart before they give up

NSS configuration options
~~~~~~~~~~~~~~~~~~~~~~~~~

**enum\_cache\_timeout** (integer)
    How long should ``nss_sss`` cache enumerations (requests for info
    about all users)
**entry\_cache\_nowait\_timeout** (integer)
    How long should nss\_sss return cached entries before initiating an
    out-of-band cache refresh (0 disables this feature)
**entry\_negative\_timeout** (integer)
    How long should ``nss_sss`` cache negative cache hits (that is,
    queries for invalid database entries, like nonexitent ones) before
    asking the backend again
**filter\_users**, **filter\_groups** (string)
    Exclude certain users from being fetched from the ``sss`` NSS
    database. This is particularly useful for system accounts like root.
**filter\_users\_in\_groups** (bool)
    If you want filtered user still be group members set this option to
    false.

Configuring domains
-------------------

A domain is a database containing user information. SSSD can use more
domains at the same time, but at least one must be configured or SSSD
won't start. Using SSSD domains, it is possible to use several LDAP
servers providing several unique namespaces.

Add new domains configurations into ``[domain/<NAME>]`` sections. Then
add the list of domains (in the order you want them to be queried) in
the 'domains' attribute of the domains section. For example, to use only
``LOCAL`` domain:

.. code:: wiki

    [sssd]
    domains = LOCAL

The following subsections will list examples of configuring different
types of domains.

Domain configuration options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These configuration options can be present in a domain configuration
section, that is, in a section called ``[domain/<NAME>]``.

**min\_id, max\_id** (integer)
    UID limits for the domain. If a domain contains entry that is
    outside these limits, it is ignored
**enumerate** (bool)
    Determines if a domain can be enumerated. This parameter affects
    enumerating of both users and groups.
**timeout** (integer)
    Timeout in seconds for this particular domain. Raising this timeout
    might prove useful for slower backends like distant LDAP servers.
    The default is 0 (no timeout).
**cache\_credentials** (bool)
    Determines if user credentials are also cached in the local LDB
    cache
**store\_legacy\_passwords** (bool)
    Whether to also store passwords in a legacy domain
**id\_provider** (string)
    The Data Provider identity backend to use for this domain. Currently
    supported identity backends are:

    -  proxy: Support a legacy NSS provider (e.g. nss\_nis)
    -  local: SSSD internal local provider
    -  ldap: ldap provider

**entry\_cache\_timeout** (integer)
    How long should the domain's Data Provider cache positive cache hits
    (that is, queries for valid database entries) before asking the
    database again
**use\_fully\_qualified\_names** (bool)
    If set to TRUE, all requests to this domain must use fully qualified
    names. For example, if used in LOCAL domain that contains a "test"
    user, ``getent passwd test`` wouldn't find the user while
    ``getent passwd test@LOCAL`` would
**auth\_provider** (string)
    The authentication provider used for the domain. Supported auth
    providers are:

    -  ldap for native LDAP authentication. See sssd-ldap(5) for more
       information on configuring LDAP.
    -  krb5 for Kerberos authentication. See sssd-krb5(5) for more
       information on configuring Kerberos.
    -  proxy for relaying authentication to some other PAM target.

Options valid for proxy identity domains
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**proxy\_pam\_target** (string)
    The proxy target PAM proxies to. If not set, a default setting of
    ``sssd_pam_proxy_default`` is used.
**proxy lib\_name** (string)
    The name of NSS library. The NSS functions searched for in the
    library are in the form of ``_nss_$(libName)_$(function)``, for
    example ``_nss_nis_getpwent``.

The LOCAL provider
~~~~~~~~~~~~~~~~~~

There is a special identity and authentication provider in SSSD named
*local*. Its backend is stored on disk in a format called *LDB*, an
on-disk LDAP-like database.

One difference in comparison with the classic files is that groups in
the LOCAL backend can be nested. The LOCAL domain is also meant to
contain additional user information such as user picture or keyboard
settings.

Instead of using User Private Groups (where a group is created for every
user), which is usually the default in files-based scheme, the LOCAL
domain uses a concept called Magic Private Groups. By using the Magic
Private Groups option, you are imposing two limitations to the ID space
and name space:

#. users and groups share a common name space, there can never be a
   separate group with a same name as a user
#. users and groups share a common ID space, there can never be a group
   with a same ID as a user

Using Magic Private groups bring the benefit of better Windows
Interoperability (in Windows, the ID and name spaces are unique) and
also avoids creating a group for every user, thus cluttering the group
space. Also, for NSS calls, every user is actually returned a user's
private group without having to explicitly create the group, thus having
the same effect as User Private Groups

To manage users in the LOCAL backend, SSSD comes with a set of tools
that resemble their shadow-utils counterparts in names as well as
parameters. The tools include *sss\_useradd*, *sss\_groupadd* for adding
users and groups, *sss\_userdel*, *sss\_groupdel* for removing them and
*sss\_usermod*, *sss\_groupmod* for changing their attributes. You can
see details about tools usage by running them with the ``--help``
argument.

Domain configuration examples
-----------------------------

Example 1: A standalone LOCAL domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Put the following definition of LOCAL domain into your sssd config file:

.. code:: wiki

    # LOCAL Users domain
    [domain/LOCAL]
    enumerate = TRUE
    min_id = 500
    max_id = 999
    id_provider = local
    auth_provider = local

Now, add a LOCAL user using sssd management tools:

.. code:: wiki

    sss_useradd testuser1

A home directory for the new user will be created. Refer to
``sss_useradd`` and ``sssd.conf`` manual pages for more documentation on
the subject.

If you configured NSS to use the SSS domain, you should be able to
request the user information now:

.. code:: wiki

    getent passwd testuser1@LOCAL

Changing the user's password and logging in should be also possible now:

.. code:: wiki

    passwd testuser1
    ssh testuser1@localhost

Example 2: Authenticating against a native LDAP domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A native LDAP domain requires a running LDAP server to authenticate
against. The client configuration is done in ``/etc/sssd/sssd.conf``.

If you want to **authenticate** against an LDAP server **TLS/SSL is
required**. sssd does not support authentication over an unencrypted
channel. If the LDAP server is used only as an identify provider, an
encrypted channel is not needed.

The domain configuration in sssd config would look like this:

.. code:: wiki

    # A native LDAP domain
    [domain/LDAP]
    enumerate = true
    cache_credentials = TRUE

    id_provider = ldap
    auth_provider = ldap
    chpass_provider = ldap

    ldap_uri = ldap://ldap.mydomain.org
    ldap_user_search_base = dc=mydomain,dc=org
    tls_reqcert = demand
    ldap_tls_cacert = /etc/pki/tls/certs/ca-bundle.crt

All the parameters for a native LDAP domain are described in the
``sssd-ldap(5)`` manual page.

Example 3: Authenticating against a Kerberos server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to set up Kerberos authentication, you need to know the address
of your KDC and the Kerberos realm. Using these parameters, the
configuration is very simple:

.. code:: wiki

    # A domain with identities provided by LDAP and authentication by Kerberos
    [domain/KRBDOMAIN]
    enumerate = false
    id_provider = ldap
    chpass_provider = krb5
    ldap_uri = ldap://ldap.mydomain.org
    ldap_user_search_base = dc=mydomain,dc=org
    tls_reqcert = demand
    ldap_tls_cacert = /etc/pki/tls/certs/ca-bundle.crt

    auth_provider = krb5
    krb5_kdcip = 192.168.1.1
    krb5_realm = EXAMPLE.COM
    krb5_changepw_principal = kadmin/changepw
    krb5_ccachedir = /tmp
    krb5_ccname_template = FILE:%d/krb5cc_%U_XXXXXX
    krb5_auth_timeout = 15

All the parameters for a configuring Kerberos authentication are
described in the ``sssd-krb5(5)`` manual page.
