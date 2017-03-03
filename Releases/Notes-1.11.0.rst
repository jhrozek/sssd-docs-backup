Highlights
----------

-  This release focuses on changes not visible to the end-user. The aim
   is to support new features used by the forthcoming version 3.3 of
   FreeIPA and targets supporting legacy (non-SSSD) clients in a setup
   where the FreeIPA server established a trust relationship with an
   Active Directory Forest.

   -  The handling of ID ranges in the providers has been changed to use
      a plugin interface where each provider can use a different plugin
   -  The libsss\_idmap library has been enhanced in several ways such
      as handling "external mappings" or supporting base RIDs other than
      0
   -  The assumption that subdomain users always have a primary
      user-private-group (UPG) has been removed
   -  When SSSD is running on the IPA server, it is able to perform
      lookups for trusted users directly against the AD server using the
      AD provider lookups including enumeration and site location

-  The sudo integration was made more robust. SSSD is now able to
   gracefully handle situations where it is not able to resolve the
   client host name or sudo rules have multiple name attributes
-  Several nested group membership bugs were fixed
-  The PAC responder was made more robust and efficient, modifying
   existing cache entries instead of always recreating them.
-  The Kerberos provider now supports the new KEYRING ccache type. This
   feature depends on yet unreleased libkrb5 and kernel patches.

Packaging changes
-----------------

-  The sssd\_pac binary was moved to the IPA and AD provider subpackages
   from the krb5-common subpackage

Tickets fixed
-------------

.. raw:: html

   <div>

`#1938 </sssd/ticket/1938>`__
    [RFE] Add a new call to libsss\_idmap to add a new mapping where the
    first RID is not 0
`#1960 </sssd/ticket/1960>`__
    [RFE] Add range type for ID mapping in AD to libsss\_idmap
`#1961 </sssd/ticket/1961>`__
    [RFE] Add plugin to LDAP provider to find new ranges
`#1962 </sssd/ticket/1962>`__
    [RFE] Integrate AD provider lookup code into IPA subdomain user
    lookup
`#1979 </sssd/ticket/1979>`__
    [RFE] Add an optional unique range identifier
`#1993 </sssd/ticket/1993>`__
    [RFE] Add a new option to denote server mode

.. raw:: html

   </div>

.. raw:: html

   <div>

`#1965 </sssd/ticket/1965>`__
    man: document that the default access provider in AD provider is
    "permit"
`#1988 </sssd/ticket/1988>`__
    [RFE] sss\_cache has no option to clear all cached entries of all
    types
`#1997 </sssd/ticket/1997>`__
    When resolving a SID, search for groups first, then users
`#1998 </sssd/ticket/1998>`__
    sssd-ad man page states that ad\_server can be an IP address even
    though SSSD doesn't support that
`#2005 </sssd/ticket/2005>`__
    SSSD filter out ldap user/group if uid/gid is zero
`#2009 </sssd/ticket/2009>`__
    Disallow or warn if full\_name\_format is set to a non-default value
    when IPA server mode is on
`#2023 </sssd/ticket/2023>`__
    AD provider in server mode follows referrals
`#2025 </sssd/ticket/2025>`__
    pysss module linking is broken

.. raw:: html

   </div>

.. raw:: html

   <div>

`#1408 </sssd/ticket/1408>`__
    It should be possible to use uid/gid defined in AD instead of SIDs
`#1821 </sssd/ticket/1821>`__
    Allow using UIDs and GIDs from AD in trust case
`#1881 </sssd/ticket/1881>`__
    Determine how to map SID to UID/GID based on IdM server
    configuration
`#1942 </sssd/ticket/1942>`__
    convert enumeration timer to be\_ptask
`#1963 </sssd/ticket/1963>`__
    [RFE] Implement or Improve enumeration
`#1964 </sssd/ticket/1964>`__
    [RFE] Enhance IPA SRV plugin to do AD site lookups as well
`#1996 </sssd/ticket/1996>`__
    PAC responder: update cached user object instead of deleting and
    recreating them
`#2027 </sssd/ticket/2027>`__
    Domain Users memberships removed in subsequent lookups in
    server\_mode
`#2032 </sssd/ticket/2032>`__
    sssd sees gid as 0 for AD trust posix users causing lookup failures
`#2035 </sssd/ticket/2035>`__
    amend the docs of sss\_nss\_getnamebysid to make it clear it only
    works for id\_provider=ad
`#2044 </sssd/ticket/2044>`__
    Update sssd-ad manpage to reflect "trust between domains in single
    forest are supported"
`#2057 </sssd/ticket/2057>`__
    Data provider endianess bug
`#2059 </sssd/ticket/2059>`__
    sss\_packet\_grow: wrong use of module to pad data

.. raw:: html

   </div>

Detailed changelog
------------------

-  Alexander Bokovoy (3):

   -  build: fix dependencies for pysss module
   -  pysss: add pysss.getgrouplist(username)
   -  pysss: prevent crashing when group is unresolvable

-  Jakub Hrozek (58):

   -  Updating the version for the 1.10.1 release
   -  Bump version to track 1.11 development
   -  IPA: Add a server mode option
   -  LDAP: Add utility function sdap\_copy\_map
   -  AD: decouple ad\_id\_ctx initialization
   -  AD: initialize failover with custom realm, domain and failover
      service
   -  IPA: Initialize server mode ctx if server mode is on
   -  AD: Move storing sdap\_domain for subdomain to generic LDAP code
   -  IPA: Create and remove AD id\_ctx for subdomains discovered in
      server mode
   -  IPA: Look up AD users directly if IPA server mode is on
   -  Updating translations for the 1.11 beta1 release
   -  Bumping the version for the 1.11 beta2 release
   -  RPM: Move sssd\_pac to the krb5-common subpackage
   -  DB: sysdb\_search\_user\_by\_name: search by both name and alias
   -  LDAP: When resolving a SID, search for groups first, then users
   -  RPM: Require libsss\_idmap from sssd-common
   -  MAN: clarify the default access provider for AD
   -  MAN: IP addresss does not work when used for ad\_server
   -  MAN: Clarify the min\_id/max\_id limits further
   -  Remove unused be\_ctx->sigchld\_ctx
   -  IPA: warn if full\_name\_format is customized in server mode
   -  AD: Set the bool value same as default value in opts
   -  Fix the default FQDN format
   -  SUDO: realloc with sizeof(uint32\_t) when adding uint32\_t
   -  KRB5: Do not send PAC in server mode
   -  LDAP: Use domain-specific name where appropriate
   -  Updating translations for the 1.11 beta2 release
   -  Bumping the version for the 1.11 beta3 release
   -  Use GID if subdomain is not MPG
   -  PAM: Check negcache when searching for fully qualified users, too
   -  PAM: Set negcache if user is not found after provider check
   -  Use the correct resolv timeout
   -  Remove unused constant
   -  AD: Use the correct include guard
   -  UTIL: Remove obsolete compat macros
   -  KRB5: Formatting changes
   -  KRB5: Do not log to syslog on each login
   -  MAN: AD provider only supports trusted domains from the same
      forest
   -  PAC: Skip SIDs that cannot be resolved to domain
   -  IPA: Enable AD sites when in server mode
   -  DB: Update sss\_domain\_info with new updated data
   -  DB: remove unused realm parameter from
      sysdb\_master\_domain\_add\_info
   -  LDAP: Add enum\_{users,groups}\_recv to follow the tevent\_req
      style
   -  LDAP: Remove unused constant
   -  LDAP: Move the ldap enum request to its own reusable module
   -  LDAP: Convert enumeration to the ptask API
   -  LDAP: Make cleanup synchronous
   -  LDAP: Make the cleanup task reusable for subdomains
   -  LDAP: Make sdap\_id\_setup\_tasks reusable for subdomains
   -  SYSDB: Store enumerate flag for subdomain
   -  Read enumerate state for subdomains from cache
   -  Add a new option to control subdomain enumeration
   -  IPA: enable enumeration if parent domain enumerates in server mode
   -  NSS: Descend into subdomains if enumerate=true
   -  IPA: Add forgotten declaration
   -  DP: Use the correct type for DBus boolean
   -  Updating translations for the 1.11.0 release
   -  Updating the version for the 1.11.0 release

-  Jim Collins (1):

   -  ldap: only update shadowLastChange when password change is
      successful

-  Lukas Slebodnik (35):

   -  BUILD: Use pkg-config to detect cmocka
   -  Return right directory name for dircache
   -  Use conditional build for retrieving ccache.
   -  Remove unused function parameter
   -  Every time use permissive control in function memberof\_mod.
   -  Fix clang format string warning.
   -  Use functionm ldb\_dn\_get\_linearized to format struct ldb\_dn
   -  Add mising argument required by format string
   -  Remove unused memory context from function unpack\_authtok
   -  Fix warnings: uninitialized variable
   -  Fix autotols warnings: macro xyz not found in library
   -  Fix possible dereference of a NULL pointer.
   -  Every time release allocated memory in function
      py\_sss\_getgrouplist
   -  Prevent using uninitialized "group\_name" in done section.
   -  Remove unused memory context
   -  SSH: Ensure that cmd\_ctx->name will not be NULL.
   -  Add script make\_srpm.sh to dist tarball.
   -  NSS: allow removing entries from netgroup hash table
   -  NSS: Clear cached netgroups if a request comes in from the
      sss\_cache
   -  Enable removing nonexisting dn in sdap\_handle\_account\_info
   -  proxy: Alocate auth tokens in struct authtok\_conv
   -  Check whether servername is not empty string.
   -  Remove include recursion
   -  Remove include recursion
   -  Use brackets around macros.
   -  Fix memory leak insss\_krb5\_get\_error\_message
   -  mmap\_cache: Skip records which doesn't have same hash
   -  mmap\_cache: Use stricter check for hash keys.
   -  UTIL: Create new wraper header file sss\_endian.h
   -  CLIENT: Fix non gnu sss\_strnlen implementation
   -  MONITOR: Move function declaration out of conditional build
   -  UTIL: Explicitly include header file sys/socket.h
   -  MEMBEROF: Remove temporary workaround
   -  IPA\_HBAC: Explicitelly include header file time.h
   -  CONFIGURE: Get rid of bashism

-  Michal Zidek (16):

   -  sss\_cache: Add option to invalidate all entries
   -  Always set port status to neutral when resetting service.
   -  Missing space in debug message
   -  Remove unused constant.
   -  Set default DNS resolution timeout to 6 seconds.
   -  Lower timeout to contact DNS server
   -  resolv-tests failing with memory leak
   -  ldap, krb5: More descriptive msg on chpass failure.
   -  mmap\_cache: Check if slot and name\_ptr are not invalid.
   -  mmap\_cache: Check data->name value in client code
   -  mmap\_cache: Remove triple checks in client code.
   -  mmap\_cache: Off by one error.
   -  mmap\_cache: Use better checks for corrupted mc in responder
   -  mmap\_cache: Store corrupted mmap cache before reset
   -  mmap\_cache: Use sss\_atomic\_write\_s instead of write.
   -  pam: Bad debug message format and parameter.

-  Ondrej Kos (9):

   -  Do not copy special files when creating homedir
   -  KRB5\_CHILD: Fix handling of get\_password return code
   -  Do not try to set password when authtok\_length is zero
   -  KRB: Handle empty password gracefully
   -  KRB: Replace multiple calls with variable
   -  TOOLS: Update all services with sss\_debuglevel
   -  Clarify that getnamebysid currently works only with ipa/ad
      id\_provider
   -  AD: Cast SASL callbacks to propper type
   -  DP: Notify propperly when removing PAC responder

-  Pavel Březina (13):

   -  remove unused variable
   -  print hint about password complexity when new password is rejected
   -  dyndns timeout test: catch SIGCHLD handler events
   -  SIGCHLD handler: do not call callback when pvt data where freed
   -  Fix netgroup lookup when using fully qualified name
   -  sudo: skip rule on error instead of failing completely
   -  sudo: print better debug message when a rule has multiple cn
      values
   -  simple access provider: allow fully qualified names
   -  add simple access provider init test
   -  sudo: continue if we are unable to resolve fqdn
   -  sudo: do not fail to store the rule if we can't read usn
   -  sudo: do not strdup usn on ENOENT
   -  sss\_packet\_grow: correctly pad packet length to 512B

-  Simo Sorce (5):

   -  Add a commit template
   -  sssd\_ad: Add hackish workaround for sasl ad\_compat
   -  proxy: Allow initgroup to return NOTFOUND
   -  krb5\_common: Refactor to use a talloc temp context
   -  BUILD: Remove unnecessary patch and configure opts

-  Stephen Gallagher (14):

   -  Move pre and post scripts to sssd-common
   -  Remove sysv->systemd upgrade routines
   -  Move sssd\_pac binary to the IPA and AD providers
   -  Netgroups should ignore the 'use\_fully\_qualified\_names' setting
   -  BUILD: Fix contrib build macros to display warnings
   -  gitignore: Add Eclipse project files to ignore list
   -  KRB5: Add new #define for collection cache types
   -  KRB5: Refactor cc\_\*\_check\_existing
   -  KRB5: Only set active and valid on success
   -  KRB5: Add low-level debugging to
      sss\_get\_ccache\_name\_for\_principal
   -  KRB5: Remove unnecessary call to become\_user()
   -  KRB5: Add support for KEYRING cache type
   -  BUILD: Ignore translations when building RPMs
   -  krb5: Fetch ccname template from krb5.conf

-  Sumit Bose (36):

   -  idmap: allow first RID to be set
   -  idmap: add optional unique range id
   -  idmap: add option to indicate external\_mapping
   -  idmap: allow NULL domain sid for external mappings
   -  idmap: add calls to check if ID mapping conforms to ranges
   -  idmap: add sss\_idmap\_domain\_has\_algorithmic\_mapping
   -  Add cmocka based tests for libsss\_idmap
   -  Add now options ldap\_min\_id and ldap\_max\_id
   -  SDAP IDMAP: Add configured domain to idmap context
   -  Allow different methods to find new domains for idmapping
   -  Add sdap\_idmap\_domain\_has\_algorithmic\_mapping()
   -  Replace SDAP\_ID\_MAPPING checks with
      sdap\_idmap\_domain\_has\_algorithmic\_mapping
   -  Add ipa\_idmap\_init()
   -  Add support for new ipaRangeType attribute
   -  Replace new\_subdomain() with find\_subdomain\_by\_name()
   -  IPA: read ranges before subdomains
   -  Save mpg state for subdomains
   -  Read mpg state for subdomains from cache
   -  Fix memory context for a state member
   -  Fix memory context for hash entries
   -  ipa\_s2n\_get\_user\_done: free group\_attrs as well
   -  ipa\_s2n\_get\_user\_done: make sure ALIAS name is lower case
   -  sdap\_get\_initgr\_done: use the right SID to get a GID
   -  sdap\_save\_user: save original primary GID of subdomain users
   -  fill\_initgr: add original primary GID if available
   -  sdap\_add\_incomplete\_groups: use fully qualified name if needed
   -  save\_rfc2307bis\_user\_memberships: use fq names for subdomains
   -  sysdb\_add\_incomplete\_group: store SID string is available
   -  check\_cc\_validity: make sure \_valid is always set
   -  PAC: if user entry already exists keep it
   -  PAC: do not create users with missing GID
   -  PAC: handle non-POSIX groups in cache
   -  PAC: read user DN instead of constructing it
   -  PAC: do not fail if a single group cannot be added/removed
   -  PAC: use SID instead of GID to search for groups
   -  ipa-server-mode: add IPA group memberships to AD users

-  Yuri Chornoivan (1):

   -  Fix two minor typos
