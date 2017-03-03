SSSD Release 0.5.0 {#SSSDRelease0.5.0}
------------------

### Highlights {#Highlights}

The most significant changes since 0.4.0 are:

-   The addition of the Kerberos 5 authentication provider
-   The addition of the native LDAP identity provider
-   Support for building on Debian and Ubuntu
-   Improved caching mechanism to reduce server load
-   Includes the fix released for CVE-2009-2410 in SSSD 0.4.1 and many
    other bugfixes.

### Detailed changes since 0.4.0 {#Detailedchangessince0.4.0}

Dmitri Pal (21):

-   Adding INSERT into collection functionality.
-   FORMATTING - minor cleanup of the unit test.
-   Queue and stack APIs using collection.
-   New deletion unit test.
-   Changing function names for collection API.
-   Adding wrappers to free data in INI API.
-   Fixing build issues
-   COLLECTION Removing static placeholder structure.
-   COLLECTION Adding flat traversal & copy
-   COLLECTION Fixed: iterator\_up and insert\_into\_current
-   ELAPI First part of the interface
-   INI Refactoring code a bit
-   COLLECTION Add remove item functions
-   COLLECTION Improving searches
-   COLLECTION & INI Cleanup
-   INI Simple fix to properly process multi value config parameters.
-   ELAPI Next round of functionality - logging part of the interface
-   TRACE: Making sure trace is safe to output NULL strings
-   ELAPI: Adding concept of targets
-   COMMON Fixes to return values, errno, leaks
-   ELAPI Shortening names

Jakub Hrozek (23):

-   fix shadow-utils base path
-   PRINT and ERROR macros
-   Gettextize the sss\_ tools
-   Check for root before initializing
-   Fix saving new nextID
-   Async DNS integration
-   Add ares helpers into sssd
-   Add async resolver tests
-   Improve error messages
-   Add ignore\_not\_found parameter to sysdb delete functions
-   Use correct return codes
-   Notify user when deleting nonexistent user or group
-   Correct check for local domain in tools
-   Consolidate tevent helpers
-   Fix adding to groups on user creation
-   Move parsing of names and domains into util/
-   Parse fully qualified names in tools
-   Add configure checks for docbook XSL templates and XML tools
-   Make child processes exit when parent dies
-   Tools ID range fixes
-   Make "files" a reserved word for legacy local domain
-   Disallow all operations outside domains, fix deleting cache for
    files
-   Fix sysdb tests

John Dennis (1):

-   add path\_utils filesystem path manipulation utility functions

Simo Sorce (40):

-   Link crypt functions only to sssd binaries
-   Fix warnings in stress-tests.c
-   Turn sssd\_mem\_takeover into sssd\_mem\_attach
-   Rename sysdb\_req to sysdb\_handle.
-   Rework transaction code to use tevent\_req
-   Convert proxy internals to tevent\_req style
-   Clean up warnings in common/
-   Cleanup warnings in client and server code
-   Add dumb way to clean up .X files
-   Expose sysdb function to parse sysdb\_attrs
-   Add async helper functions
-   Use async helpers for ldap auth module
-   Unify password caching ops in sysdb
-   Implement the ldap identity module.
-   Start rationalizing user tools a bit
-   Instrument memberof for debugging
-   Add option to add timestamps to debug output
-   Raise debug level for version negotiation
-   Rework the engine that deals with openldap libraries
-   Fix race condition that was causing segfaults
-   Fix search replies getting ignored
-   Fix race condition in sdap code
-   Fix broken ifndefs
-   Cleanups
-   Refactor some code around watches and timeouts
-   Remove redundant memory contexts
-   Cosmetic changes
-   merge server and connection structures
-   Simplify interfaces initialization
-   Do not fail enumerations because of range checks
-   Minor fixes
-   Change services identification mechanism
-   Prevent races between dp startup and others
-   Change the why DP clients identify
-   Fix reversal of parent and member in groupmod
-   Fix reconnection code
-   Catch possible bad input passed in by glibc
-   Add debug statements to sysdb\_ops
-   Relax memberof constraints a bit
-   Do not fail enumerations if a single store fails

Stephen Gallagher (52):

-   Treat a missing provider entry as a config error
-   Update version to 0.4.1
-   Fix invalid pointer error in ldb\_debug\_messages
-   Remove unnecessary .la cleanup from sssd.spec.in
-   Add missing configure check for getpgrp
-   Remove extra implementation of password\_destructor
-   Make SysV script install executable
-   Add --with-aux-info config option to SSSD daemon
-   Add --with-aux-info config option to SSS client
-   Control sssd\_be exported functions
-   Control sss\_client exports
-   Create gettext framework for SSSD daemon
-   Do not treat warnings as errors
-   Add configure check for PCRE &gt;= 7
-   Allow the use of custom CFLAGS on the make command line
-   Fix segfault in update\_monitor\_config
-   Protect against segfault in service\_signal\_reload
-   Implement \_pam\_overwrite\_n(n,x) for older systems
-   Add pam\_sss\_macros.h to "make dist"
-   Remove redundant libPath option from proxy provider
-   Eliminate segfault on first start-up
-   Build all SSSD components with warnings enabled
-   Run libcollection unit tests with 'make check'
-   Run ini\_config unit test with "make check"
-   Improvements to config file updates
-   Monitor resolv.conf for changes
-   Implement resInit for monitor, NSS, PAM, DP and the backends
-   Fix typo in elapi's Makefile.am that breaks 'make dist'
-   Remove unused InfoPipe and PolicyKit code
-   Add 'make srpms' target
-   Minor cleanups in monitor.c
-   Address CVE-2009-2410
-   Build and run tests with 'make check'
-   Revert build-breaking libsss\_util\_la change.
-   Make socket paths a compile-time option
-   Fix monitor ping timeout
-   Eliminate unnecessary explicit timeout for DP account requests
-   Don't go to the backend for identical cache entry requests
-   Refactor responder\_dp.c
-   Fix broken build
-   Ensure that only one local domain is configured
-   Remove unneeded binary objects from the replace directory
-   Eliminate the --with-tests configure flag
-   Make the LOCAL provider always use MagicPrivateGroups
-   Add m4 directory at root
-   Fix usage of \$(builddir) in SSSD
-   Remove 'color-tests' from AM\_INIT\_AUTOMAKE
-   Support gettext &gt;= 0.14 instead of 0.17
-   Support Docbook 4.4
-   Ensure nextID doesn't reuse an existing local UID or GID
-   Fix accidentally forcing MPGs on for all domains
-   Update version to 0.5.0

Sumit Bose (24):

-   fix detection of authentication against LOCAL domain
-   added kerberos locator plugin
-   added kerberos backend with tevent\_req event handling
-   let .gitignore only filter autogenerated m4 files
-   check pending\_return after dbus\_connection\_send\_with\_reply
-   fixed a double talloc\_free error
-   fixed some typos which prevented password caching
-   fix return code of krb5 child to indicate that the kdc is
    unavailable
-   fixed typos and a potential memory leak
-   add a short explanation about the used debug levels
-   fixed the default value for tls\_reqcert
-   let krb5 backend safe valid credentials for offline authentication
-   add infrastructure to handle new backend targets
-   add handling of the new backend targets to proxy backend
-   added LDAP change password backend target
-   cleanup of pam\_sss
-   fix return value of confdb\_get\_domains
-   added missing hash\_create which was remove by a previous patch
-   enable usage of defaultBindDn
-   use stored upn if available
-   fix handling of filtersUsers in groups
-   store additional LDAP attributes
-   extended the documentation of LDAP backend
-   some UPN handling fixes

