Highlights
----------

-  The IPA provider now supports logins with enterprise principals (also
   known as additional UPN suffixes). This functionality also enabled
   Active Directory users from trusted AD domains who use an additional
   UPN suffix to log in. Please note that this feature requires a recent
   IPA server.
-  When a user name is overriden in an IPA domain, resolving a group
   these users are a member of now returns the overriden user names
-  Users can be looked up by and log in with their e-mail address as an
   identifier. In order to do so, an attribute that represents the
   user's e-mail address is fetched by default. This attribute can by
   customized by setting the ``ldap_user_email`` configuration option.
-  A new ``ad_enabled_domains`` option was added. This option lets the
   administrator select domains that SSSD should attempt to reach in the
   AD forest SSSD is joined to. This option is useful for deployments
   where not all domains are reachable on the network level, yet the
   administrator needs to access some trusted domains and therefore
   disabling the subdomains provider completely is not desirable.
-  The ``sssctl`` tool has two new commands ``active-server`` and
   ``servers`` that allow the administrator to observe the server that
   SSSD is bound to and the servers that SSSD autodiscovered
-  SSSD used to fail to start when an attribute name is present in both
   the default SSSD attribute map and the custom
   ``ldap_user_extra_attrs`` map
-  GPO policy procesing no longer fails if the gPCMachineExtensionNames
   attribute only contains whitespaces
-  Several commits fix regressions related to switching all user and
   group names to fully qualified format, such as running ``initgroups``
   for a user who is only a member of a primary group
-  Several patches fix regressions caused by splitting the database into
   two ldb files, such as when user attributes change without increasing
   the ``modifyTimestamp`` attribute value
-  systemd unit files are now shipped for the sssd-secrets responder,
   allowing the responder to be socket-activated. To do so,
   administrators should enable the ``sssd-secrets.socket`` and
   ``sssd-secrets.service`` systemd units.
-  The ``sssd`` binary has a new switch ``--disable-netlink`` that lets
   sssd skip messages from the kernel's netlink interface.
-  A crash when entries with special characters such as '(' were
   requested was fixed
-  The ``ldap_rfc_2307_fallback_to_local_users`` option was broken in
   the previous version. This release fixes the functionality.

Packaging Changes
-----------------

-  The NFS ID-mapping plugin was moved to its own subpackage

Documentation Changes
---------------------

-  A new option ``ad_enabled_domains`` was added
-  A new LDAP attribute mapping for e-mail addresses called
   ``ldap_user_email`` was added

Tickets Fixed
-------------

.. raw:: html

   <div>

`#2789 </sssd/ticket/2789>`__
    Warn if ad\_server contains IP address
`#2828 </sssd/ticket/2828>`__
    Add an option to disable checking for trusted domains in the
    subdomains provider
`#2856 </sssd/ticket/2856>`__
    [RFE] Allow users to authenticate with alternative names
`#2860 </sssd/ticket/2860>`__
    Add support for disabling netlink use
`#2948 </sssd/ticket/2948>`__
    Handle overriden name of members in the memberUid attribute
`#2958 </sssd/ticket/2958>`__
    Support multiple principals for IPA users
`#2978 </sssd/ticket/2978>`__
    pid file name decalration is duplicated
`#2987 </sssd/ticket/2987>`__
    Improve information about krb5\_keytab & ldap\_krb5\_keytab option
    in sssd man pages
`#3009 </sssd/ticket/3009>`__
    sssd fails to mark a connection as bad on searches that time out
`#3018 </sssd/ticket/3018>`__
    Detect of IPA server can handle enterprise principals
`#3024 </sssd/ticket/3024>`__
    sssd-common brings in nfs-utils
`#3064 </sssd/ticket/3064>`__
    incorrect dataExpireTimestamp setting in the timestamps cache
`#3068 </sssd/ticket/3068>`__
    fixes to the initial config schema implementation
`#3069 </sssd/ticket/3069>`__
    The sssctl tool should provide information about active and
    available servers
`#3072 </sssd/ticket/3072>`__
    task: Add a 1.14 upstream repo
`#3077 </sssd/ticket/3077>`__
    sssd does not work under non-root user
`#3084 </sssd/ticket/3084>`__
    DP: Don't pass empty string, but NULL to providers
`#3086 </sssd/ticket/3086>`__
    tools: sssctl config-check and sssctl cache ignore --help
`#3087 </sssd/ticket/3087>`__
    tools: make sssctl command names consistent
`#3088 </sssd/ticket/3088>`__
    Review and update SSSD's wiki pages for 1.14.1 release
`#3089 </sssd/ticket/3089>`__
    Error message "Failed to retrieve users" is sometimes misleading
`#3090 </sssd/ticket/3090>`__
    Don't print message about trust direction on clients
`#3091 </sssd/ticket/3091>`__
    remove DEBUG(SSSDBG\_TRACE\_INTERNAL, "Trace: ldap\_result found
    nothing!\\n");
`#3093 </sssd/ticket/3093>`__
    Missing nested groups in user groups
`#3094 </sssd/ticket/3094>`__
    SELINUX\_getpeercon failed [-1][Unknown error -1].
`#3096 </sssd/ticket/3096>`__
    sssctl: Time stamps without time zone information
`#3101 </sssd/ticket/3101>`__
    sssd does not start if sub-domain user is used with simple access
    provider
`#3109 </sssd/ticket/3109>`__
    Wrong pam error code returned for password change in offline mode
`#3110 </sssd/ticket/3110>`__
    Access denied after activating user in 389ds
`#3111 </sssd/ticket/3111>`__
    sssd doesn't start on IPA client if IPA server VM is paused
`#3120 </sssd/ticket/3120>`__
    SSSD fails to start when ldap\_user\_extra\_attrs contains mail
`#3121 </sssd/ticket/3121>`__
    [abrt] [faf] sssd: unknown function(): /usr/libexec/sssd/sssd\_nss
    killed by 11
`#3122 </sssd/ticket/3122>`__
    Do not check local users with disabled local\_negative\_timeout
`#3130 </sssd/ticket/3130>`__
    Better error message if sssctl is ran w/o activating the IFP
    responder
`#3132 </sssd/ticket/3132>`__
    check return value of sysdb\_search\_user\_by\_upn()

.. raw:: html

   </div>

Detailed Changelog
------------------

Dan Lavu (1):

-  MAN: Update description of sssctl

Fabiano Fidêncio (5):

-  sssctl: Use localtime for time stamps
-  RESPONDERS: Decrease debug level for failures in
   SELINUX\_getpeercon()
-  RESPONDERS: Show a bit more info in case of SELINUX\_getpeercon()
   failure
-  RESPONDERS: Pass errno to strerror() when SELINUX\_getpeercon() fails
-  SDAP: Don't log an op failure when no users are found

Jakub Hrozek (18):

-  Updating the version for the 1.14.1 release
-  FO: Set port to NOT\_WORKING when trying a next server
-  LDAP: Fix storing initgroups for users with no supplementary groups
-  LDAP: Use FQDN when linking parent LDAP groups
-  SYSDB: Fix setting dataExpireTimestamp if sysdb is supposed to set
   the current time
-  PAM: Do not act on ldb\_message in case of a failure
-  IPA: Check the return value of sss\_parse\_internal\_fqname
-  SIMPLE: Do not parse names on startup
-  SIMPLE: Fail on any error parsing the access control list
-  SIMPLE: Make the DP handlers testable
-  TESTS: Use the DP handlers in simple provider tests, add more tests
-  CONFIG: full\_name\_format is an allowed option for all domains
-  CONFIG: re\_expression is an allowed option for all domains
-  SPEC: Own the secrets DB path
-  UTIL: Use sss\_atomic\_read\_s in generate\_csprng\_buffer
-  SECRETS: Use sss\_atomic\_read/write for better readability
-  BUILD: Ship systemd service file for sssd-secrets
-  Updating the translations for the 1.14.1 release

Justin Stephenson (4):

-  Make resolv\_is\_address() function public and create some basic
   tests
-  Warn if IP address is used as option for ipa\_server/ad\_server
-  Monitor: Add support for disabling netlink
-  SSSCTL: More helpful error message when
   `InfoPipe? <https://docs.pagure.org/sssd-test2/InfoPipe.html>`__ is
   disabled

Lukas Slebodnik (37):

-  sssctl: Fix error handling after memory allocation failure
-  sssctl: Fix format string for size\_t
-  doxygen: Fix path to header file ipa\_hbac.h
-  ipa\_hbac: Fix documentation for hbac\_enable\_debug
-  sssctl: Fix warning maybe-uninitialized
-  nss-srv-tests: Fix prototype of wrapped ncache functions
-  TOOLS: Prevent dereference of null pointer
-  sysdb-tests: Fix cast from pointer to integer
-  SPEC: Move nfsidmap plugin to separate package
-  test\_utils: Clean files after sss\_write\_krb5\_conf\_snippet
-  CI: Use /bin/sh as a CONFIG SHELL
-  SECRETS: Log message for failures with removing file
-  Amend debug messages after failure of unlink
-  SYSDB: Do not try to modify ts cache for unsupported DNs
-  SDAP: sanitize member name before using in filter
-  SDAP: sysdb\_search\_users does not set users\_count for failures
-  SYSDB: Sanitize dn in sysdb\_get\_user\_members\_recursively
-  LDAP: Fix Dereference after NULL check
-  NSS: Do not check local users with disabled local\_negative\_timeout
-  config\_schema: Add ldap\_user\_email to schema
-  intg: Make location of sssd nss module configurable
-  intg: Allow to test netgroups
-  NSS: Use correct name for invalidating memory cache
-  SYSDB: Avoid optimisation with modifyTimestamp for users
-  dyndns-tests: Fix false positive failures
-  LDAP: Log autofs rfc2307 config changes only with enabled responder
-  DP: Add log message for get account info
-  ds.py: Do not call teardown in destructor
-  test\_local\_domain: Restore correct env variable
-  intg: rename test with enumeration
-  test\_enumeration: Remove test without enumeration
-  intg: create ldap test without enumeration
-  sssd\_id.py: Primary group should be returned for initgroups
-  intg: Fix pep8 warnings
-  test\_ldap: test nested membership with rfc2307bis
-  test\_ldap: test resolving of names with special characters
-  intg: Test extra attributes duplicate

Michal Židek (13):

-  sssctl: config-check access check report
-  config: override\_space is monitor's option
-  config: Fix user\_attributes
-  config: Allow timeout for all sevices
-  config: Add config\_file\_version to schema
-  dyndns: Add checks for NULL
-  sdap: Fix ldap\_rfc\_2307\_fallback\_to\_local\_users
-  sss\_ini: Change debug level of config error msgs
-  sssctl: Consistent commands naming
-  tools: Add missing gettext macro
-  sssctl: Generic help for cache-upgrade and config-check
-  gpo: gPCMachineExtensionNames with just whitespaces
-  sdap: Skip exact duplicates when extending maps

Pavel Březina (17):

-  sssctl: move filter creation to separate function
-  sssctl: improve readability of a condition
-  DP: rename be\_acct\_req to dp\_id\_data
-  DP: Initialize D-Bus as soon as possible
-  utils: add remove\_subtree
-  sssctl: use internal API to remove files
-  rdp: add ability to forward reply to the client request
-  sbus: add sbus\_request\_reply\_error()
-  sbus: add utility function to simplify message and reply handling
-  sssctl: use talloc with sifp
-  failover: mark subdomain service with sd\_ prefix
-  sssctl: print active server and server list
-  sifp: fix coverity warning
-  sbus: allow freeing msg through dbus api when using talloc
-  PROXY: Do not abuse data provider interface
-  DP: Remove old data provider interface
-  NSS: Remove unused functions

Petr Cech (18):

-  SYSDB: Fixing DB update
-  PROVIDERS: Setting right {u,g}id if unprivileged
-  SYSDB: Removing of duplication of sysdb\_ts\_cache\_attrs
-  test\_utils: Fixing assignment discards 'const' qualifier
-  LDAP: Changing of confusing debug message
-  IPA: Changing of confusing debug message
-  Revert "LDAP: Lookup services by all protocols unless a protocol is
   specified"
-  PROVIDER: Conversion empty string from D-Bus to NULL
-  LDAP: Fixing wrong pam error code for passwd
-  UTILS: Fixing duplication of pid file declaration
-  AD\_PROVIDER: Add ad\_enabled\_domains option
-  AD\_PROVIDER: Initializing of ad\_enabled\_domains
-  AD\_PROVIDER: ad\_enabled\_domains - only master
-  AD\_PROVIDER: ad\_enabled\_domains - other then master
-  TESTS: Adding tests for ad\_enabled\_domains option
-  LDAP: Adding support for SIGTERM signal
-  LDAP: Adding SIGTERM signal before SIGKILL
-  LDAP: Adding SIGCHLD callback

Sumit Bose (33):

-  views: allow override added for non-default views at runtime
-  IPA: read ipaNTAdditionalSuffixes for master and trusted domains
-  sysdb: add UPN suffix support for the master domain
-  sysdb: make subdomain calls aware of upn\_suffixes
-  DP: add dp\_get\_module\_data()
-  IPA: add ipa\_init\_get\_krb5\_auth\_ctx()
-  IPA: enable enterprise principals if server supports them
-  IPA: fix [capaths] output
-  UTIL: make domain mapping content testable
-  tests: add tests for sss\_get\_domain\_mappings\_content()
-  AD: avoid memory leak in netlogon\_get\_domain\_info() and make it
   public
-  AD: netlogon\_get\_domain\_info() allow missing arguments and empty
   results
-  tests: add tests for netlogon\_get\_domain\_info
-  AD: replace ad\_get\_client\_site\_parse\_ndr() with
   netlogon\_get\_domain\_info()
-  sysdb\_master\_domain\_add\_info: properly set do\_update
-  IPA: make ipa\_resolve\_user\_list\_{send\|recv} public and allow AD
   users
-  IPA: expand ghost members of AD groups in server-mode
-  sysdb: add sysdb\_get\_user\_members\_recursively()
-  views: properly override group member names
-  IPA: fix lookup by UPN for subdomains
-  LDAP: allow multiple user principals
-  LDAP: new attribute option ldap\_user\_email
-  sysdb: include email in UPN searches
-  LDAP: include email in UPN searches
-  NSS: add user email to fill\_orig()
-  utils: add is\_email\_from\_domain()
-  LDAP/IPA: add local email address to aliases
-  NSS: continue with UPN/email search if name was not found
-  PAM: continue with UPN/email search if name was not found
-  NSS: use different neg cache name for UPN searches
-  PAM: Fix domain for UPN based lookups
-  SDAP: add special handling for IPA Kerberos enterprise principal
   strings
-  SDAP: add enterprise principal strings for user searches

Thorsten Scherf (1):

-  Fixed some typos in man pages
