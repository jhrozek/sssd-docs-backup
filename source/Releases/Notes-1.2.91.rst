Highlights
----------

-  Rewrote the internal LDB cache API. As a synchronous API it is now
   faster to access and easier to work with
-  Eugene Indenbom contributed a sizeable amount of code to the LDAP
   provider

   -  We now handle failover situations much more reliably than we did
      previously
   -  If a request fails partway through (due to a remote server ceasing
      to function) we will now restart the conversation with the next
      server in the failover list
   -  We also will now monitor the GSSAPI kerberos ticket and
      automatically renew it when appropriate, instead of waiting for a
      connection to fail

-  Support for netlink now allows us to more quickly detect situations
   where we may have come online
-  New option ``dns_discovery_domain`` allows better configuration for
   using SRV records for failover

Detailed Changelog
------------------

Alexander Gordeev (1):

-  Add explicit requests for several operational attrs

David O'Brien (1):

-  Copy-edit and format review sssd.conf

Dmitri Pal (16):

-  Adding metadata interface
-  Adding content to the metadata
-  Resolve paths for reporting purposes
-  Acess control and config change checks
-  Add ability to trace 64bit numbers
-  Fixing spec file to match version.
-  Fixing build
-  Code restructuring
-  Extending refarray interface
-  Introducing a comment object
-  Adding support for explicit 32/64 types (attempt 2).
-  Addressing initialization issues.
-  Fixing types in queue and stack interfaces
-  Fixing memory leaks in the unit test.
-  Fixing NULL dereferencing in ini\_config
-  Memory leak in case of empty value

Héctor Daniel Cabrera (1):

-  Updating ES translation

Jakub Hrozek (32):

-  Treat server names as case-insensitive in failover code
-  Do not mark a request as failed twice
-  Sort SRV replies according to RFC 2782
-  Remove freed server\_common entities from list
-  Support SRV servers in failover
-  Silence warnings with -O2
-  Fix uninitialized variable
-  Add a README file
-  Use all available servers in LDAP provider
-  Improve the offline authentication message
-  Fix memory hierarchy in the ipa timerules
-  Use service discovery in backends
-  SSSDConfigAPI fixes
-  Try all servers during Kerberos auth
-  Remove dead code from the PAM responder
-  Man page fixes
-  Don't return uninitialized value in proxy provider
-  Skip empty attributes with warning
-  Fix realm\_str dereference
-  Fix potential NULL dereference in fail\_over.c
-  Fix Incorrect NULL check in get\_server\_common()
-  Add missing break to switch statement
-  get\_uid\_from\_pid should use fstat rather than lstat
-  Remove krb5\_changepw\_principal option
-  Remove the -g option from useradd
-  Fix potential resource leak in copy\_tree\_ctx()
-  Potential memory leak in \_nss\_sss\_\*\_r()
-  Check closedir call in find\_uid
-  Print correct return code
-  Resend SIGINT as SIGTERM in services
-  Add dns\_discovery\_domain option
-  Use netlink to detect going online

Petter Reinholdtsen (2):

-  Allow
   `Debian/Ubuntu? <https://docs.pagure.org/sssd-test2/Debian/Ubuntu.html>`__
   build to pass --install-layout=deb to setup.py
-  Remove bash-isms from configure macros

Piotr Drąg (1):

-  Update Polish translation

Rui Gouveia (2):

-  Updating pt translation
-  Update pt translation

Simo Sorce (45):

-  sysdb: start conversion from async to sync
-  sysdb: use sysdb\_delete\_entry in recursive delete
-  sysdb: convert sysdb\_delete\_custom
-  sysdb: convert sysdb\_search\_entry and sysdb\_delete\_recursive
-  sysdb: convert sysdb\_search\_user\_by\_name/uid
-  sysdb: convert sysdb\_search\_group\_by\_name/gid
-  sysdb: convert sysdb\_set\_entry/user/group\_attr
-  sysdb: convert sysdb\_get\_new\_id
-  sysdb: convert sysdb\_store/add(\_basic)\_user
-  sysdb: convert sysdb\_store/add(\_basic)\_group
-  sysdb: convert sysdb\_mod/add/remove\_group\_member
-  sysdb: convert sysdb\_cache\_password
-  sysdb: convert sysdb\_search\_custom
-  sysdb: convert sysdb\_store\_custom
-  sysdb: convert sysdb\_asq\_search
-  sysdb remove sldb\_request\_send, not used anymore
-  sysdb: convert sysdb\_search\_users
-  sysdb: convert sysdb\_delete\_user
-  sysdb: delete sysdb\_delete\_group
-  sysdb: convert sysdb\_search\_groups
-  sysdb: convert sysdb\_cache\_auth
-  sysdb: remove sysdb\_check\_handle
-  tests: remove use of asynchronus transactions
-  sysdb: add synchronous transaction functions
-  proxy: complete conversion to synchronous sysdb
-  Use the sysdb synchronous transaction functions
-  Remove remaining use of sysdb\_transaction\_send
-  sysdb: remove async transactions
-  sysdb: add automatic transactions where needed
-  sysdb: convert sysdb\_getpwnam
-  sysdb: convert sysdb\_getpwuid
-  sysdb: convert sysdb\_getgrnam
-  sysdb: convert sysdb\_getgrgid
-  sysdb: convert sysdb\_get\_user\_attr
-  sysdb: convert sysdb\_enumpwent
-  sysdb: convert sysdb\_enumgrent
-  Adjust fill\_pwent and fill\_grent
-  sysdb: convert sysdb\_initgroups
-  sysdb: remove obsolete helpers from sysdb
-  sysdb: remove remaining traces of sysdb\_handle
-  sysydb: Finally stop using a common event context
-  Make groupshow synchronous.
-  tools: remove creation of event\_context
-  Better handle sdap\_handle memory from callers.
-  Avoid freeing sdap\_handle too early

Stephen Gallagher (68):

-  Support docdir and abs\_builddir
-  sysdb: convert sysdb\_delete\_entry
-  Bumping version on master to 1.2.90
-  Update translations for master branch
-  Fix merge error for sss\_userdel.c
-  Remove unused configure macro
-  Fix warning in sysdb-tests.c
-  Fix ini\_config unit test
-  Give information about ldap\_schema in the sample config
-  Make ID provider init functions clearer
-  Remove the NSS\_LIBS and KRB5\_LIBS variables from sssd.spec
-  Add dns\_resolver\_timeout option
-  Fix segfault in GSSAPI reconnect code
-  Make krb5\_kpasswd available for any krb5 provider
-  Clean up kdcinfo and kpasswdinfo files when exiting
-  Add callback when the ID provider switches from offline to online
-  Add dynamic DNS updates to FreeIPA
-  Revert "Add dynamic DNS updates to FreeIPA"
-  Properly set up SIGCHLD handlers
-  Add dynamic DNS updates to FreeIPA
-  Don't report a fatal error for an HBAC denial
-  Add a better error message for TLS failures
-  Add enumerate details to the manpage and examples
-  Revert "Copy pam data from DBus message"
-  Display name of PAM action in pam\_print\_data()
-  Make data provider id\_callback public
-  Fix error reporting for be\_pam\_handler
-  Proxy provider PAM handling in child process
-  Support password changes in chpass\_provider = proxy
-  Add ldap\_access\_filter option
-  Fix typo in Makefile
-  Fix broken build against older versions of OpenLDAP
-  Fix typo in Makefile.am
-  Disable connection callbacks when going online
-  Change default min\_id to 1
-  Allow ldap\_access\_filter values wrapped in parentheses
-  Properly handle read() and write() throughout the SSSD
-  Fix misuse of errno in find\_uid.c
-  Avoid potential NULL dereference
-  Properly handle missing originalMemberOf entry in initgroups
-  Don't leak directory access resources on errors in directory\_list()
-  Check the correct variable for NULL after creating timer
-  Properly check that the timeout event was created for cleanup/enum
-  Check return code of hash\_delete in proxy\_child\_destructor
-  Eliminate unused variable from pc\_init\_timeout()
-  Make sure to close varargs before returning from a function
-  Properly null-terminate socket path
-  Add ldap\_force\_upper\_case\_realm to example AD config
-  Don't segfault if ldap\_access\_filter is unspecified
-  Handle (ignore) unknown options in get\_domain() and get\_service()
-  Remove references to the DP service from the SSSDConfig API tests
-  Standardize on correct spelling of "principal" for krb5
-  Initialize len before looping to read the pidfile
-  Ensure that all domains are checked for users/groups
-  Refactor the negative cache
-  Move setup of filter\_users and filter\_groups to negcache.c
-  Honor filter\_users in PAM
-  Fix potential resource leak in remove\_tree\_with\_ctx()
-  Fix return value from remove\_connection\_callback() destructor
-  Protect against segfault in remove\_ldap\_connection\_callbacks
-  Drop release requirement from versions
-  Bump libini\_config version to 0.6.0
-  Replace %define with %global in example spec
-  Make RootDSE optional
-  Rename proxy\_ctx to proxy\_id\_ctx for clarity
-  Split proxy.c into smaller files
-  Add try\_inotify option
-  Release SSSD 1.2.91 (1.3.0rc1)

Sumit Bose (50):

-  Revert "Add better checks on PAM socket"
-  Use SO\_PEERCRED on the PAM socket
-  Set LDAP\_OPT\_RESTART for all LDAP connections
-  Fix a potential memory violation
-  Make the handling of fd events opaque
-  Unset authentication tokens if password change fails
-  Display a message if a password reset by root fails
-  Fix wrong return value
-  Fix a wrong return value in IPA HBAC
-  Split pam\_data utilities into a separate file
-  Create kdcinfo and kpasswdinfo file at startup
-  Compare the full service name
-  Add retry option to pam\_sss
-  Add more warnings about nearly expired passwords
-  Make Kerberos authentication a tevent\_req
-  New version of IPA auth and password migration
-  Add ldap\_krb5\_ticket\_lifetime option
-  Defer sbus\_dispatch() for 30ms during reconnect
-  Copy pam data from DBus message
-  Do not modify IPA\_DOMAIN when setting Kerberos realm
-  Handle Krb5 password expiration warning
-  Add support for delayed kinit if offline
-  Fix handling of ccache file when going offline
-  Move parse\_args() to util
-  Copy pam data from DBus message
-  Revert "Create kdcinfo and kpasswdinfo file at startup"
-  Refactor data provider callbacks
-  Add offline callbacks
-  Refactor krb5\_finalize()
-  Add run\_callbacks flag
-  Add callback to remove krb5 info files when going offline
-  Krb5 locator plugin returns KRB5\_PLUGIN\_NO\_HANDLE
-  Refactor krb5 SIGTERM handler installation
-  Add krb5 SIGTERM handler to ipa auth provider
-  Add offline callback to disconnect global SDAP handle
-  Reset run\_online\_cb flag even if there are no callbacks
-  Fix check if LDAP id provider is already initialized
-  Remove signal event if child was terminated by a signal
-  Check ipaEnabledFlag
-  Add sysdb\_attrs\_get\_string\_array()
-  Use sysdb\_attrs\_get\_string\_array() instead of
   sysdb\_attrs\_get\_el()
-  Use new schema for HBAC service checks
-  Remove service groups
-  Compare full service name
-  Unify sdap and sysdb data handling
-  Initialize pam\_data in Kerberos child.
-  Avoid a potential double-free
-  Add a missing initializer
-  Add a missing free()
-  Fix SASL authentication

Yuri Chornoivan (1):

-  Update Ukrainian translation

eindenbom (14):

-  Avoid accessing half-deallocated memory when using talloc\_zfree
   macro.
-  GSSAPI ticket expiry time is returned from ldap\_child and stored in
   sdap\_handle for future reference.
-  Added an interface to query number of configured (and currently
   resolved through SRV records) failover servers.
-  LDAP connection usage tracking, sharing and failover retry framework.
-  Add an interface to try next fail-over server after connection to the
   active server was unexpectedly dropped.
-  Use new LDAP connection framework to get user account info from LDAP.
-  Use new LDAP connection framework to get group account info from
   LDAP.
-  Use new LDAP connection framework to get user account groups from
   LDAP.
-  Use new LDAP connection framework for LDAP user and group
   enumeration.
-  Use new LDAP connection framework in LDAP access backend.
-  Use new LDAP connection framework in IPA access backend.
-  Use new LDAP connection framework in IPA dynamic DNS forwarder.
-  Remove remainder of now unused global LDAP connection handle.
-  Eliminate delayed sdap\_handle destruction after fail-over retry.
