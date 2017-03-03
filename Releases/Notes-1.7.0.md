Highlights {#Highlights}
----------

-   Support for case-insensitive domains
-   Support for multiple search bases in the LDAP provider
-   Support for the native FreeIPA netgroup implementation
-   Reliability improvements to the process monitor
-   New DEBUG facility with more consistent log levels
-   New tool to change debug log levels without restarting SSSD
-   SSSD will now disconnect from LDAP server when idle
-   FreeIPA HBAC rules can choose to ignore srchost options for
    significant performance gains
-   Assorted performance improvements in the LDAP provider (reducing
    disk-writes to the cache)
-   **Experimental** support for looking up SUDO rules in ldap
    -   Not built by default
    -   Requires unreleased sudo binary. Very preliminary functionality.
-   **Experimental** support for Heimdal Kerberos implementation (buggy)

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (89):

-   pyhbac: Do not convert int to bool
-   Fix returning groups when gidNumber attribute is not ordered
-   Prevent segfault if vetoed\_shells are specified without
    allowed\_shells
-   Remove unused temporary context
-   Handle errno properly in set\_debug\_file\_from\_fd()
-   Do not delete requests inside hash\_iterate loop
-   Handle timeout during sss\_ldap\_init\_send
-   IPA dyndns: do not segfault if the server cannot be resolved
-   Return the first value of name if the multivalued name attribute
    does not match RDN
-   Add LDAP provider option to set LDAP\_OPT\_X\_SASL\_NOCANON
-   Use the default Kerberos realm for LDAP with GSSAPI auth
-   Fix moving to next entry in deref code
-   Allow turning dereference off by setting the threshold to 0
-   Change libnl monitor callback to only signal going online
-   Discard carrier messages from non-ethernet devices
-   Subscribe to netlink route and addr messages
-   Improve error message for LDAP password constraint violation
-   Keep deref controls until the whole request is finished
-   Fix uninitialized pointer read in
    sdap\_gssapi\_get\_default\_realm()
-   Fix wrong buffer size in has\_phy\_80211\_subdir()
-   Multiline macro cleanup
-   IPA access: hostname comparison should be case-insensitive
-   Add sysdb interface to get name aliases
-   Add a sysdb\_get\_direct\_parents function
-   Store name aliases for users, groups
-   Return users and groups based on alias
-   Use explicit base 10 for converting strings to integers
-   Fix typo in sysdb\_get\_direct\_parents
-   Add option to follow symlinks to check\_file()
-   Append PID to sbus server socket name, let clients use a symlink
-   Streamline the example config
-   Check if dp\_requests hash table exists before using it
-   Fix off-by-one error in remove\_socket\_symlink()
-   Report on errno, not return code in create\_socket\_symlink
-   Add a missing break
-   Sanitize DN in sysdb\_get\_direct\_parents
-   gitignore additions
-   Utility functions for LDAP nested schema initgroups
-   Use fewer transactions during RFC2307bis initgroups
-   Use fewer transactions during IPA initgroups
-   Cancel transactions correctly during initgroups
-   Plug memory leaks in LDAP provider
-   Plug memory leaks in sysdb\_ops
-   Do not leak hash table iterator during proxy auth
-   resolver: Free the whole hostent structure
-   RFC2307bis initgroups: fix nested groups processing
-   Steal result onto mem\_ctx in
    sdap\_initgr\_nested\_get\_direct\_parents
-   Use LDAPDerefSpec properly
-   Remove confusing do-while loop
-   Fix segfault in sdap\_get\_initgr\_user
-   Use correct state struct in sdap\_initgr\_rfc2307bis\_next\_base
-   configAPI: Fix removing in old domain when saving a new domain
-   Squash transactions in sdap\_initgr\_common\_store
-   Use one transaction instead of two during RFC2307bis group
    processing
-   Prevent printing NULL in several places of LDAP provider
-   Cleanup: Remove unused parameters
-   Fix sdap\_id\_ctx/ipa\_id\_ctx mismatch in IPA provider
-   Provide means of forcing TLS and GSSAPI enabled/disabled for sdap
    connections
-   IPA migration fixes
-   Fix two small bugs in group dereferencing
-   Use dereference during IPA provider initgroups
-   Pass the correct private data into Data Provider callback
-   Always attempt to connect in sdap\_async\_sys\_connect\_done
-   LDAP provider: Error while setting the nocanon option should not be
    fatal
-   Cancel ping\_check if service goes away
-   sss\_utf8\_tolower utility function+unit tests
-   Responders: Split getting domain by name into separate function
-   Canonicalize username in PAM provider
-   Use the case sensitivity flag in responders
-   Refactor saving sdap entities
-   sysdb\_get\_real\_name helper function
-   Use the case sensitivity flag in the LDAP provider
-   Use the case sensitivity flag in the simple access provider
-   Use the case sensitivity flag in the proxy provider
-   Export the function to convert ldb\_result to sysdb\_attrs
-   SUDO Integration - sysdb interface
-   SUDO Integration - LDAP provider - save sudo rules functions
-   SUDO Integration - responder - get sudo rules logic
-   DP: Remove processed callbacks
-   Pass client context to sss\_dp\_get\_account\_send
-   Pass sdap\_id\_ctx to online check from IPA provider
-   Error out if local domain is case insensitive
-   Resolver: Introduce a per-request timeout
-   Do not touch resolve\_service\_state in fo\_resolve\_service\_done
-   Failover: Introduce a per-service timeout
-   Save original memberof, not memberof
-   sss\_get\_cased\_name utility function
-   Return user and group names lowercased in case insensitive domains
-   Honor case sensitive flag when creating the ccname template

Jan Zeleny (37):

-   sysdb refactoring: renamed ctx variable to sysdb
-   Added sysdb\_ctx\_get\_domain function
-   sysdb refactoring: deleted domain variables in sysdb API
-   sysdb refactoring: memory context deleted
-   Remaining memory context variables renamed
-   sdap\_async\_accounts.c split
-   Confusing part of code cleared out
-   Moved some functions in sdap\_async\_groups
-   Moved some functions in sdap\_async\_initgroups
-   Fixed bad logic in processing netgroups in LDAP provider
-   man page fix (lists are comma-separated)
-   Fixed timeout handling in responders
-   Added krb5\_fast\_principal to SSSDConfig API
-   Cleanup of unused function in ldap access provider
-   Add wrapper for krb5\_get\_init\_creds\_opt\_set\_canonicalize
-   Add support to request canonicalization on krb AS requests
-   Support to request canonicalization in LDAP/IPA provider
-   Handle group renaming correctly
-   Fixed possible resource leak in get\_uid\_from\_pid()
-   Fixed possible resource leak in create\_mail\_spool()
-   Fixed empty loginShell in proxy provider
-   Fixed unchecked value of setenv() in check\_and\_export\_options()
-   Renamed some LDAP routines
-   Modified sdap\_parse\_search\_base()
-   Added and modified options for IPA netgroups
-   New IPA ID context
-   Added support for fetching netgroups in IPA provider
-   Added IPA account info handler
-   Fixed a typo in sysdb\_upgrade\_07() declaration
-   Fixed uninitialized pointer read in netgroups processing
-   Fixed logically dead code in netgroup processing
-   Add ipa\_hbac\_support\_srchost option to IPA provider
-   Fixed an error in macro for merging double linked lists
-   Fixed incorrect return code in PAM client
-   Add ldap\_sasl\_minssf option
-   Fixed IPA netgroup processing
-   Deleted declaration of nss\_get\_dom()

Krzysztof Klimonda (1):

-   Fix FTBFS related to -Werror=format-security

Marko Myllynen (4):

-   Add missing options to sssd.api.conf
-   Unbreak ./configure
-   Update sssd-example.conf
-   Typo fixes

Pavel Březina (35):

-   debug\_timestamps fixes
-   Fixed implicit declaration of function 'time' in
    src/sss\_client/common.c.
-   New DEBUG facility - new levels
-   New DEBUG facility - modified DEBUG
-   New DEBUG facility - conversion
-   New DEBUG facility - man pages
-   New DEBUG facility - unit tests
-   New DEBUG facility - SSSDBG\_UNRESOLVED changed from -1 to 0
-   --debug-timestamps=1 is not passed to providers
-   sss\_ldap\_err2string() - function created
-   sss\_ldap\_err2string() - ldap\_err2string() to
    sss\_ldap\_err2string()
-   sss\_debuglevel - change the debug levels on the fly
-   DEBUG timestamps offer higher precision
-   DEBUG timestamps offer higher precision - man page updated
-   DEBUG timestamps offer higher precision - unit tests updated
-   DEBUG timestamps offer higher precision - SSSDConfig updated
-   Added quiet option to pam\_sss
-   SysDB commands that save lastUpdate allows this value to be passed
    in
-   Fixes debug-tests.c coverity issues: NEGATIVE\_RETURNS,
    FORWARD\_NULL
-   sss\_cli.h - fix: function declaration after the header guard
-   Added sssd --version option
-   Added sss\_ldap\_dn\_in\_search\_bases()
-   Support search bases in RFC2307bis enumeration
-   Support search bases in netgroup members translation
-   SUDO integration - client common interface
-   SUDO integration - data provider backend handler
-   SUDO Integration - LDAP configuration options
-   SUDO integration - LDAP provider
-   SUDO Integration - responder
-   SUDO Integration - API for sudo
-   SUDO Integration - pseudo client for testing
-   Logically dead code in sdap\_nested\_group\_lookup\_group
-   Use of uninitialized value in sss\_ldap\_dn\_in\_search\_bases
-   SUDO Integration - be\_sudo\_req removed from sudo\_ctx
-   SUDO Integration - fixed memory leak in sdap\_sudo\_handler()

Pavel Zuna (2):

-   Fix small bug where TALLOC\_CTX could end up unfreed.
-   Add common SIGCHLD handling for providers.

Ralf Haferkamp (1):

-   Allow the O\_NONBLOCK flag to be reset correctly

Simo Sorce (1):

-   Set more strict permissions on keyring

Stephen Gallagher (74):

-   Bumping version to 1.7.0
-   Revert "Allow LDAP to decide when an expiration warning is
    warranted"
-   Rename sssd.conf to sssd-example.conf
-   Include the configuration file as a %ghost entry
-   Remove private shared object Provides: for pysss.so and pyhbac.so
-   Cancel sysdb upgrade transaction if commit fails
-   Fix potential double-free issue
-   Fix broken RHEL5 build
-   Use sysdb attribute name for GID, not LDAP attribute
-   HBAC: Handle saving groups that have no members
-   HBAC: Use of hostgroups for targethost or sourcehost was broken
-   HBAC: Properly skip all non-group memberOf entries
-   Add option to specify the kerberos replay cache dir
-   Fix typo in %configure
-   Remove all libtool .la files from RPM
-   Improve documentation of libipa\_hbac
-   Add libipa\_hbac documentation to the -devel package
-   MONITOR: Correctly detect lack of response from services
-   Do not build documentation on RHEL 5
-   Fix typo in specfile
-   MAN: Add more information about internal credential storage
-   Enable the midpoint cache update by default
-   HBAC: fix typos preventing proper hostgroup evaluation
-   SYSDB: New source file for sysdb upgrade routines
-   HBAC: Do not save member/memberOf links
-   HBAC: Use originalMember for identifying servicegroups
-   HBAC: Use originalMember for identifying hostgroups
-   BUILDSYS: Fix --without-manpages
-   TOOLS: Do not leak pid\_file handle on error
-   MONITOR: fix timeout conversion
-   Updating translation files
-   SSSDConfig: Handle integer parsing more leniently
-   Remove unused sdap\_options attributes
-   Fix size return for split\_on\_separator()
-   Make sdap\_get\_id\_specific\_filter() more strict
-   LDAP: Add parser for multiple search bases
-   LDAP: Support multiple user search bases (non-enumeration)
-   LDAP: Support multiple netgroup search bases
-   LDAP: Support multiple group search bases (non-enumeration, RFC2307)
-   LDAP: Add multiple search bases for initgroups (users)
-   LDAP: Add multiple search bases for initgroups (RFC2307 groups)
-   LDAP: Add multiple search bases for initgroups (RFC2307bis groups)
-   LDAP: Update manpages with multiple search base information
-   LDAP: Convert ldap\_\*\_search\_filter
-   LDAP: Add support for multiple search bases for user enumeration
-   LDAP: Add support for multiple search bases for group enumeration
-   RESPONDER: Fix segfault in sss\_packet\_send()
-   SYSDB: add index for nameAlias
-   Periodic translation file update
-   LDAP: Remove redundant groups from the lookup list
-   SBUS: Fix DEBUG log matching
-   RESPONDER: Ensure that all input strings are valid UTF-8
-   SYSDB: Make ENOENT log messages less threatening
-   Fix broken build due to commit of IPA netgroup support
-   Add -fno-strict-aliasing
-   LDAP: Try next failover server on any error
-   RESPONDER: Refactor DP requests into tevent\_req style
-   Allow using Glib for UTF8 support
-   Ignore NULL-terminator when checking UTF8-validity
-   LDAP: Fix missing break statements in force\_tls
-   Ignore NULL-terminator when checking UTF8-validity for netgroups
-   Fix potential resource leak in backup\_file.c
-   Fix uninitialized value error in ipa\_netgroups.c
-   Add sdap\_connection\_expire\_timeout option
-   Update spec file to build with Glib on RHEL 5
-   Fix typo in IPA SSSDConfig file
-   Move child\_common routines to util
-   Reorder pidfile() function to guarantee NULL-termination
-   Securely set umask when using mkstemp
-   Update translations for string freeze
-   MONITOR: use sigchld handler for monitoring SSSD services
-   PAM: make initgroups timeout work across multiple clients
-   Add compatibility layer for Heimdal Kerberos implementation
-   Importing new translations for 1.7.0 release

Sumit Bose (2):

-   Improve password policy error code and message
-   Do not access memory out of bounds

Thorsten Scherf (1):

-   Fixed translation bug

Yuri Chornoivan (2):

-   Fix two man page typos
-   Fix typos in manual pages

