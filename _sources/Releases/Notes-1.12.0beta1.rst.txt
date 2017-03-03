.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Packaging Changes <#PackagingChanges>`__
   #. `Documentation Changes <#DocumentationChanges>`__
   #. `Tickets Fixed <#TicketsFixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

-  A new responder, called InfoPipe was added. This responder provides a
   public D-Bus interface accessible over the system bus. In this
   release, methods for retrieving user attributes and list of groups
   were added as well as objects representing SSSD domains and
   processes. The next 1.12.x releases will publish objects representing
   users and groups, too.
-  SSSD provides an ID-mapping plugin for cifs-utils so that Windows
   SIDs can be mapped onto POSIX IDs and/or names without requiring
   Winbind and using the same code as the SSSD uses for identity
   information.
-  Added a new library called ``sss_sifp`` that provides a simple
   synchronous API for communication with our new InfoPipe responder
   over the system bus.
-  journald can now be used to store debug logs. The journald support is
   not enabled by default. In order to enable it, compile SSSD with
   ``--with-syslog=journald``.
-  First phase of Group Policy-based access control for the AD provider
   was added. At the moment, the gpo-ldap component that downloads the
   list of GPOs that apply for the specific client has been implemented.
   The gpo-smb component that retrieves the group policy files and
   determines the access control check results based on those files is
   expected to be implemented in one of the next 1.12.x releases

Packaging Changes
-----------------

-  The sssd\_sifp library and the InfoPipe responder are packaged in
   their own subpackages

Documentation Changes
---------------------

-  The new InfoPipe responder has several configuration options. Refer
   to the ``sssd-ifp`` manual page for details.
-  A new option ``offline_timeout`` was added. This option allows the
   administrator to configure how often should SSSD attempt to reconnect
   when in offline mode
-  The LDAP provider has a new option ``ldap_user_extra_attrs`` that
   enables the administrator to extend the map of attributes downloaded
   when looking up a user. These custom attributes can then be retrieved
   with the new DBus API.
-  The automounter master map name can now be configured with a new
   option ``ldap_autofs_map_master_name``.
-  A new option ``ad_gpo_access_control`` is available to let the user
   configure the behaviour of the GPO access control feature.

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1096 </sssd/ticket/1096>`__
    Clock skew in krb5 auth should result in offline operation, not
    failure
`#1187 </sssd/ticket/1187>`__
    Delete IPA specific attribute mappings from man page
`#1366 </sssd/ticket/1366>`__
    [RFE] Optimize RFC2307bis lookups when user and group search bases
    do not overlap
`#1451 </sssd/ticket/1451>`__
    Update manpage with the minimal value expected for
    ldap\_idmap\_range\_size
`#1534 </sssd/ticket/1534>`__
    [RFE] Integrate SSSD with CIFS client
`#1585 </sssd/ticket/1585>`__
    [RFE] Add a check to pam\_sss to ensure that
    authtok\_type=SSS\_AUTHTOK\_TYPE\_PASSWORD is \\0 terminated
`#1718 </sssd/ticket/1718>`__
    Offline mode timeout not documented
`#1866 </sssd/ticket/1866>`__
    SSSD changes primary creds on authentication
`#1885 </sssd/ticket/1885>`__
    Use a shorter retry timeout for SRV queries in cases the query
    cannot be resolved (negative timeout)
`#1918 </sssd/ticket/1918>`__
    Undocument and deprecate ipa\_hbac\_support\_srchost
`#1923 </sssd/ticket/1923>`__
    Create tickets to track unit test enhancements
`#2022 </sssd/ticket/2022>`__
    Review Fedora 20 system wide changes and file corresponging tickets
    if they affect SSSD
`#2024 </sssd/ticket/2024>`__
    Create unit test for nested groups
`#2037 </sssd/ticket/2037>`__
    nondescriptive error message when ccache directory has wrong
    permissions
`#2040 </sssd/ticket/2040>`__
    Enable ad\_compat sasl option
`#2061 </sssd/ticket/2061>`__
    ccache mangament simplification
`#2072 </sssd/ticket/2072>`__
    [RFE] Provide an experimental DBus responder to retrieve custom
    attributes from SSSD cache
`#2073 </sssd/ticket/2073>`__
    [RFE] Extend the LDAP backend to retrieve extended set of attributes
`#2084 </sssd/ticket/2084>`__
    check for active sessions not troll proc for uids
`#2094 </sssd/ticket/2094>`__
    find uid tests fail
`#2097 </sssd/ticket/2097>`__
    Build library libsss\_test\_common in test phase
`#2125 </sssd/ticket/2125>`__
    cifsidmap support should be optional
`#2162 </sssd/ticket/2162>`__
    [RFE] warn to syslog if an unresponsive subprocess is terminated
`#2171 </sssd/ticket/2171>`__
    Do not start multiple backends for the same domain
`#2179 </sssd/ticket/2179>`__
    Sssd dyndns update fails for addresses from different networks
`#2195 </sssd/ticket/2195>`__
    [RFE] Send debug logs to journald by default
`#2198 </sssd/ticket/2198>`__
    remove unused tmp\_ctx in async\_resolv.c
`#2210 </sssd/ticket/2210>`__
    convert ad\_account\_can\_shortcut to returning boolean
`#2225 </sssd/ticket/2225>`__
    PO files changed during build
`#2227 </sssd/ticket/2227>`__
    [RFE] Expose domain object over DBus
`#2234 </sssd/ticket/2234>`__
    autogenerate introspection
`#2254 </sssd/ticket/2254>`__
    [RFE] Create a library to simplify usage of D-Bus responder
`#2258 </sssd/ticket/2258>`__
    [src/providers/krb5/krb5\_common.c:418] ->
    [src/providers/krb5/krb5\_common.c:418]: (style) Same expression on
    both sides of '\|\|'.
`#2288 </sssd/ticket/2288>`__
    sssd is crashing after several quick invokes of automount -m
`#2290 </sssd/ticket/2290>`__
    The DBus responder should not spawn a client socket
`#2291 </sssd/ticket/2291>`__
    make distcheck fails
`#2304 </sssd/ticket/2304>`__
    refactor splitting the selinux priority list
`#2313 </sssd/ticket/2313>`__
    consider going offline on KRB5KRB\_ERR\_GENERIC error instead of
    System Error
`#2319 </sssd/ticket/2319>`__
    provide a compatible definition of ck\_assert\_uint\_eq
`#2321 </sssd/ticket/2321>`__
    daemon FAILS to start with config file set to mode 400
`#2331 </sssd/ticket/2331>`__
    sssd should also filter out S-1-18

.. raw:: html

   </div>

Detailed Changelog
------------------

Please note this detailed changelog contains only changes since the
latest stable version, which was
`​1.11.5.1 <https://docs.pagure.org/sssd-test2/Releases/Notes-1.11.5.1.html>`__.

Alexander Bokovoy (2):

-  ipa subdomains provider: make sure search by SID works for homedir
-  well known sids: Windows Server 2012 new asserted identity SIDs

Benjamin Franzke (3):

-  Add CIFS idmap plugin
-  BUILD: Use OPENLDAP\_CFLAGS instead of LDAP\_CFLAGS
-  BUILD: Link libsss\_krb5\_common.so to libkeyutils.so

Chris Leick (1):

-  German translation update

Cove Schneider (1):

-  Add ldap\_autofs\_map\_master\_name option

Jakub Hrozek (86):

-  Bump version to track 1.12 development
-  Add journald support
-  BE: Log domain name to journald if available
-  MAN: Fix provider man page subtitle
-  LDAP: Deprecate ldap\_{user,group}\_search\_filter
-  Check return values of setenv and unsetenv
-  MAN: Fix refsect-id
-  Include external headers with #include <foo.h>
-  Remove unused constants
-  IPA: Do not enable IPA sites in server mode
-  Remove duplicate declaration
-  UTIL: Move sss\_parse\_name\_for\_domains declaration to util.h
-  NSS: Use new safealign macros in NSS responder
-  UTIL: Free log message when using journald
-  Remove unused variable
-  PAC: Free config attribute when it's processed
-  Merge ipa\_selinux\_common.c and ipa\_selinux.c
-  SYSDB: Drop the sysdb\_ctx parameter from the autofs API
-  SYSDB: Drop the sysdb\_ctx parameter from SELinux functions
-  SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_idmap module
-  SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_sudo.c module
-  KRB5: Go offline in case of clock skew
-  MAN: Add a link explaining different LDAP scopes
-  MAN: Remove unused experimental file
-  NSS: Compare bool with false, not 0
-  Fix a trivial typo
-  LDAP: Fix a debug message
-  NSS: Fix DEBUG formatting of cmdctx->id
-  DEBUG: Fix build without journald
-  NSS: Continue if there is no port
-  Fix DEBUG message formatting
-  IFP: Fix a typo in the Makefile
-  IFP: Re-add the
   `InfoPipe? <https://docs.pagure.org/sssd-test2/InfoPipe.html>`__
   server
-  IFP: Connect to the system bus
-  tests: Don't set the check fork mode explicitly
-  SBUS: Generate introspection from the interface meta structure
-  ConfigAPI: Add two missing AD options
-  Add a unit test for sss\_parse\_name\_for\_domains
-  Minor fixes for sss\_parse\_name\_for\_domains
-  SBUS: Create an sbus\_method\_meta instance for Introspection
-  RESPONDER: Fix a wrong DEBUG message
-  DP: Remove unused 'force' parameter from the subdomain handler
-  TESTS: Create a default sss\_names\_ctx in create\_dom\_test\_ctx
-  TESTS: Split a separate common\_mock\_resp\_dp module
-  RESPONDERS: Add a new request sss\_parse\_inp\_send
-  KRB5: Print a verbose error message on failure reading the keytab
-  LDAP: Fix off-by-one bug in sdap\_copy\_opts
-  LDAP: Make it possible to extend an attribute map
-  IFP: Close memstream handle in introspect destructor
-  LDAP: Check the LDAP handle before using it
-  SBUS: several trivial style fixes
-  SBUS: Fix error handling condition
-  SBUS: Add a convenience function sbus\_error\_new
-  SBUS: Split out dbus\_conn\_send
-  SBUS: Add SBUS\_CONN\_TYPE\_SYSBUS
-  SBUS: Add an async request to retrieve the caller ID
-  SBUS: Refactor sbus\_message\_handler to retrieve caller ID
-  IFP: Add utility functions
-  IFP: use a list of allowed\_uids for authentication
-  IFP: Initialize negative cache timeout
-  IFP: Add
   `GetUserAttrs? <https://docs.pagure.org/sssd-test2/GetUserAttrs.html>`__
   call
-  AD: Do not remove non-root domains when looking up root domain
-  IFP: Per-attribute ACL for users
-  SBUS: Allow registering paths with fallback
-  SYSDB: return SYSDB\_NAME from sysdb\_initgroups
-  IFP: Add a
   `GetGroupsList? <https://docs.pagure.org/sssd-test2/GetGroupsList.html>`__
   method
-  AD: Initialize user\_map\_cnt in server mode
-  IFP: Add utility functions to escape and unescape object paths
-  IFP: Add a unit test for ifp\_reply\_objpath
-  SBUS: Utility function sbus\_request\_return\_as\_variant
-  IFP: Allow Set, Get and
   `GetAll? <https://docs.pagure.org/sssd-test2/GetAll.html>`__ from
   DBus.Properties
-  SBUS: Implement org.freedesktop.DBus.Properties.Get for primitive
   types
-  SBUS: Return / if an object path getter returns NULL
-  SBUS: Add several error constant definitions
-  SBUS: Add org.freedesktop.DBus.Properties.Get to Introspection
-  IFP: Support multiple interfaces on sysbus
-  SBUS: Add utility function sbus\_add\_variant\_to\_dict
-  SBUS: Consolidate VTABLE\_FUNC definitions in sssd\_dbus\_meta.h
-  SBUS: Implement
   org.freedesktop.DBus.Properties.\ `GetAll? <https://docs.pagure.org/sssd-test2/GetAll.html>`__
   for primitive types
-  SBUS: Add
   org.freedesktop.DBus.Properties.\ `GetAll? <https://docs.pagure.org/sssd-test2/GetAll.html>`__
   to Introspection
-  TESTS: check allocation result
-  TESTS: check dbus mock result
-  IFP: Add
   `ListDomains? <https://docs.pagure.org/sssd-test2/ListDomains.html>`__
   and
   `FindDomainByName? <https://docs.pagure.org/sssd-test2/FindDomainByName.html>`__
-  tests: Add test for confdb\_list\_all\_domain\_names
-  tests: Add test for get\_known\_services
-  BUILD: Disable dbus tests when running distcheck

Lukas Slebodnik (106):

-  Add missing new line in DEBUG message
-  RESPONDER: Use right function prototype
-  Revert "mmap\_cache: Skip records which doesn't have same hash"
-  mmap\_cache: Use two chains for hash collision.
-  Include right header file
-  Include header file in implementation module.
-  IPA: Remove unused memory context.
-  BUILD: Explicitly link libsss\_ad.so with sasl libs
-  BUILD: Change error message if missing cifsimap.h
-  monitor: return right error code
-  TESTS: Remove test dir after successful tests
-  Remove unused parameter from sss\_selinux\_extract\_user
-  Remove unused parameter from get\_user\_dn
-  Remove unused parameter from sdap\_save\_user
-  Remove unused parameter from sdap\_get\_members\_with\_primary\_gid
-  Remove unused parameter from sdap\_store\_group\_with\_gid
-  Remove unused parameter from sdap\_add\_group\_member\_2307
-  Remove unused parameter from sdap\_process\_missing\_member\_2307
-  Remove unused parameter from sdap\_save\_netgroup
-  Remove unused parameter from krb5\_auth\_cache\_creds
-  Remove unused parameter from krb5\_auth\_store\_creds
-  Remove unused parameter from mod\_groups\_member
-  Remove unused parameter from usermod
-  Remove unused parameter from groupmod
-  Remove unused parameter from useradd
-  Remove unused parameter from groupadd
-  Remove unused parameter from invalidate\_entry
-  Remove unused parameter from search\_autofsmaps
-  Remove unused parameter from seed\_domain\_user\_info
-  Remove unused parameter from sudosrv\_get\_sudorules\_query\_cache
-  Remove unused parameter from delete\_user
-  Remove unused parameter from save\_user
-  Remove unused parameter from save\_netgroup
-  Remove unused memory context in proxy
-  Remove unused parameter from ipa\_save\_netgroup
-  Remove unused parameter from group\_show\_mpg
-  Remove unused parameter from group\_show\_trim\_memberof
-  AUTOMAKE: Don't build libsss\_test\_common every time
-  SYSDB: Sanitize filter before sysdb\_search\_groups
-  SYSDB: Sanitize filter before removing ghost attrs
-  TESTS: Fix build with older version of check framework
-  TESTS: Fix authtok test for zero length string.
-  CLIENT: Remove unused macros
-  AD: Remove unused memory contexts
-  memberof: Removed unused parameter from mbof\_fill\_vals\_array.
-  Makefile: Remove unused libraries
-  test\_dyndns: Test right variable after allocation.
-  IPA: explicitly link libsss\_ipa with selinux library
-  Translation: Move german translation to right directory
-  SPEC: Fix packaging rpms on OSes without systemd
-  DEBUG: Fix crash after fallback from journal log
-  Fix warning unused variable ap\_fallback
-  KRB5: Fix condition for empty string
-  NSS: Fix warning access array with index then check
-  TEST: Fix warning invalid printf argument type
-  Remove unused structures.
-  TEST: Use unique directory for negcache test
-  PAM: Test return value of strdup
-  TEST: Remove unused argument sysdb\_path
-  TEST: Use right domain name in negcache test
-  TEST: Do not clean up if test fail.
-  hbac-test: Use defined macros instead of strings
-  TESTS: Remove unused macros
-  KRB: Prevent dereference of a null pointer
-  UTIL: Hide implementation details about unicode libraries.
-  Use pattern #elif defined(identifier)
-  BUILD: Enable additional compiler warnings
-  AUTOFS: terminate array after the last entry
-  krb5\_child: Remove unused krb5\_context from set\_changepw\_options
-  Remove unused argument from resolv\_gethostbyname\_dns\_parse
-  Fix warning zero-length gnu\_printf format string
-  krb5\_child: Fix use after free in debug message
-  BUILD: Link libsss\_ldap\_common.so to libsss\_idmap.so
-  BUILD: Move file find\_uid.c into libsss\_util.so
-  BUILD: Move file sss\_krb5.c into libsss\_krb5\_common.so
-  BUILD: Move duplicated files from providers to
   libsss\_ldap\_common.so
-  TEST: Add untested libraries into dlopen test
-  TEST: Some macros aren't defined in older version of check.
-  CRYPTO: Fix access to uninitialized data
-  SPEC: Remove duplicate sssd\_ifp.
-  TEST: Link ipa\_ldap\_opt test with openldap libs
-  UTIL: Use constant instead of value for stdin.
-  MONITOR: Fix start up with empty standard input
-  SPEC: Add libsss\_ad\_common.so to the package sssd-ad
-  TEST: Refactor test\_io
-  BUILD: Make samba4 libraries optional
-  SBUS: Fix warning declaration shadows a global declaration
-  PAM: Fix problem with missing declaration.
-  PAM: macro PAM\_DATA\_REPLACE isn't available in openpam.
-  CRYPTO: Use unprefixed version of function stpncpy
-  CONFIGURE: Remove duplicate detection of pam
-  Remove unused parameter from ifp\_user\_get\_attr\_handle\_reply
-  Remove unused parameter from ifp\_user\_get\_groups\_reply
-  resolv: Do not try to free addrinfo in case of error
-  AUTOCONF: Move detection of samba libraries to one file
-  SBUS: Define DBUS\_ERROR\_INIT for old version of dbus
-  SBUS: Include config.h for enabling function in stdio.h
-  UTIL: Fix order of header files.
-  LDAP: Don't use macro \_XOPEN\_SOURCE for extra features
-  UTIL: Include netinet/in.h for ip adress macros
-  TEST: Test empty results from functions sysdb\_search\_\*
-  sss\_autofs: Check return value of autofs make request
-  sss\_autofs: Do not try to free empty autofs context
-  Don't use macro \_XOPEN\_SOURCE for function strptime
-  TEST: Add libsss\_simpleifp.so to dlopen test
-  man: Substitute entity values for entity references

Michal Zidek (25):

-  nss: Wrong debug message.
-  util: Add functions to check if IP addresses is special
-  dyndns: Use check\_ipvX\_addr functions
-  sdap\_async\_sudo\_hostinfo.c: Use check\_ipvX\_addr
-  tests: Silence alignment warning in tests.
-  responder: Access packet header using SAFEALIGN macros.
-  confdb: Make offline timeout configurable
-  SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_search module
-  SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_services module
-  SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_ssh module
-  SYSDB: Drop the sysdb\_ctx parameter - module sysdb\_ops (part 1)
-  SYSDB: Drop the sysdb\_ctx parameter - module sysdb\_ops (part 2)
-  SYSDB: Drop redundant sysdb\_ctx parameter from sysdb.c
-  sss\_client: Use SAFEALIGN\_SETMEM\_<type> macros where appropriate.
-  krb5: Alignment warning reported by clang
-  monitor: Stop using unnecessary helper pointer.
-  Missing parameter name in declaration.
-  Fix parameter name.
-  sss\_client: Use SAFEALIGN\_COPY\_<type> macros where appropriate.
-  responder: Use SAFEALIGN macro when checking pam data validity.
-  Properly align buffer when storing pointers.
-  responder: Use SAFEALIGN macros where appropriate.
-  Remove dead code from ipa\_get\_selinux\_recv
-  mmap: Get errno when unlink fails
-  ipa\_selinux: Put SELinux map order related variables into structure

Nikolai Kondrashov (20):

-  dyndns: Update PTR records separately
-  Add cscope inverted index files to .gitignore
-  Update debug levels in sss\_semanage\_error\_callback
-  Move DEBUG macro body to debug\_fn
-  Remove extra flushing from debug message output
-  Cleanup debug\_fn
-  Make DEBUG macro definition variadic
-  Make DEBUG macro invocations variadic
-  Fixup DEBUG macro invocations update
-  Update DEBUG\* invocations to use new levels
-  Update debug level in sysdb\_check\_upgrade\_02
-  Remove DEBUG macro support for old debug levels
-  Use HW instead of processor name as build arch
-  Use functions, not aliases in bashrc\_sssd
-  Handle unbound variables in bashrc\_sssd
-  Clarify CFLAGS handling in bashrc\_sssd
-  Remove --with-distro-version
-  build: Don't assume systemd implies journald
-  build: List test extensions
-  build: Switch to AM\_DISTCHECK\_CONFIGURE\_FLAGS

Ondrej Kos (2):

-  MAN: Remove IPA specific LDAP settings
-  IPA: Deprecate ipa\_hbac\_support\_srchost option

Pallavi Jha (5):

-  added null checks to authtok module
-  permament is corrected to permanent
-  cmocka unit test for authtok module added
-  Unit-test-for-negcache-module-added
-  cmocka-unit-test-for-functions-getpwuid\*-added

Pavel Březina (37):

-  resolv\_gethostbyname\_dns\_parse(): remove tmp\_ctx
-  sdap: move non async functions from sdap\_async.c to sdap\_utils.c
-  sdap: move non async functions from sdap\_async\_connection.c to
   sdap\_utils.c
-  sdap: move sdap\_get\_id\_specific\_filter() to sdap\_utils.c
-  ldap: move options related content from ldap\_common.c to
   ldap\_options.c
-  ldap: move domain related content from ldap\_common.c to
   sdap\_domain.c
-  make make\_realm\_upper\_case() static
-  tests: add confdb\_path to sss\_test\_ctx
-  tests: mock SDAP
-  tests: mock sysdb users and groups
-  tests: prepare makefile for provider related unit tests
-  tests: new macro sss\_will\_return\_always
-  tests: nested groups unit test
-  tests: don't print debug message when test dir does not exist
-  ad\_account\_can\_shortcut(): return bool instead of errno
-  IFP: do not create client socket
-  sbus\_tests: fix missing invoker in initializer
-  sbus request: fix error initialization
-  SBUS: remove unused variables
-  sss\_config: the code
-  sss\_config: build
-  sss\_config: unit tests
-  sss\_config: build only when IFP is allowed
-  IFP: Add a utility function to reply with an object path
-  SBUS: Utility function sbus\_request\_return\_array\_as\_variant
-  SBUS: Return empty string if a string getter returns NULL
-  SBUS: Add utility function sbus\_add\_array\_as\_variant\_to\_dict
-  IFP: Implement domain getters
-  confdb: add confdb\_list\_all\_domain\_names()
-  utils: add get\_known\_services()
-  IFP: Implement SSSD components
-  sss\_sifp: introduce API
-  sss\_sifp: implement API
-  sss\_sifp: build
-  sss\_sifp: unit tests
-  sss\_sifp: add support for string dictionary
-  sss\_sifp: add shortcuts for common use cases

Pavel Reichl (27):

-  Include ext headers with #include <foo.h> - cont
-  monitor: use-after-free bugfix
-  monitor: monitor\_kill\_service - refactor
-  monitor: memory-leak bug
-  monitor: syslog when process killed by monitor
-  SYSDB: typos & debug macro constants
-  SYSDB: missing conversion of LDB error to errno
-  SYSDB: simplification of condition in if statement
-  CONFDB: fail if there are domains with same name
-  MAN: new general options section
-  MAN: Option name typo in sssd-krb5
-  refactor calls of sss\_parse\_name
-  KRB5: log message - wrong permissions on ccache dir
-  MAN: minimal value expected for ldap\_idmap\_range\_size
-  PAC: fix clang warning
-  failover: Shorter retry time for failed SRV
-  SDAP: augmented logging for group saving
-  KRB: do not check ccache directory for GID
-  KRB5: Go offline in case of generic error
-  Monitor: fix message wrong perm. mode on config file
-  util: Fix 'wrong mode' debug message
-  AD Provider: bug-fix uninitialized variable
-  AD Provider: bugfix use-after-free
-  TEST: Remove unused variable
-  TEST: fix warning in sbus\_codegen\_tests
-  TEST: unused variable
-  TEST: simple\_access & sysdb tests - cleanup

Simo Sorce (7):

-  util: Use systemd-login to check user sessions
-  util: Allways fall back to old find\_uid method
-  Signals: Remove unused functions
-  Signals: Remove empty sig\_hup
-  Signals: Refactor termination of processes
-  util: Change file check fns to use a mode mask
-  confdb: Change file checks for config file

Stef Walter (18):

-  Update .gitignore for 'make check' built files
-  util: Fix const cast failures when building with -Werror
-  util: A safe printf for user provided format strings
-  NSS: Don't use printf(3) on user provided strings.
-  sbus: Add meta data structures and code generator
-  sbus: Add sbus\_vtable and update codegen to support it
-  nss: Stop using one DBus interface with totally different methods
-  sbus: Rework sbus to use interface metadata and vtables
-  sbus: Generate constants from interface definitions
-  sbus: Use constants to make dbus calls
-  sbus: Add struct sbus\_request to represent a DBus invocation
-  sbus: Refactor how we export DBus interfaces
-  sbus: Make sbus\_new\_server() work for non-priveleged processes
-  sbus\_tests: Add some testing of dispatch and handler code
-  sbus: Add the sbus\_request\_parse\_or\_finish() method
-  sbus: Add type-safe DBus method handlers and finish functions
-  sbus\_codegen\_tests: Add test case type-safe handler args
-  SBUS: Start implementing property access

Stephen Gallagher (4):

-  DEBUG: Allow debug\_fn to process FILE and LINE
-  DEBUG: Enable sending structured debug logs to journald
-  BUILD: Build with journald support by default on Fedora
-  BUILD: Simplify enabling journald on installed systems

Sumit Bose (19):

-  Do not set HAVE\_SYSTEMD\_LOGIN if libsystemd-login is not available
-  Spec file changes for cifs-utils plugin
-  Enhance/add unit tests for find\_subdomain\_by\_sid/name
-  Replace prog\_DEPENDENCIES with EXTRA\_prog\_DEPENDENCIES
-  Add sss\_packet\_get\_status()
-  sss\_names\_init: allow empty domain name
-  nss: save global name configuration to the nss context
-  Add sss\_tc\_fqname2()
-  Add utility to handle Well-Known SIDs
-  nss-srv-tests: check packet status
-  nss: check for Well-Known SIDs in SID based requests
-  Update CIFS plugin for Well-Known SID support
-  rfc2307bis\_nested\_groups\_send: reuse search base
-  config API: read only specific files from schemaplugindir
-  config API: prepend source dir search path for tests
-  krb5\_child: remove unused option lifetime\_str from
   k5c\_setup\_fast()
-  krb5-child: extract lifetime settings into set\_lifetime\_options()
-  Make LDAP extra attributes available to IPA and AD
-  contrib: add
   `BuildRequires? <https://docs.pagure.org/sssd-test2/BuildRequires.html>`__
   libsmbclient-devel to spec file

Yassir Elley (4):

-  ad\_access\_filter man page typo
-  Implemented LDAP component of GPO-based access control
-  AD-GPO: Remove dependency on libsamba-security
-  AD-GPO: add libsmbclient to makefiles
