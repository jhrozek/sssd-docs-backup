Highlights {#Highlights}
----------

-   New, more consistent config file format
-   Improvements to SSL/TLS setup in the LDAP provider
-   Support for configuring the location of the credential cache in
    Kerberos
-   Better handling of bad configuration files
-   Support for asynchronous cache refreshes
-   New, faster enumeration logic
-   SSS tools made more reliable
-   New Python API for managing native SSSD users
-   Improvements for building on older platforms
-   Many other bugfixes and stability improvements

Detailed Changes Since 0.5.0 {#DetailedChangesSince0.5.0}
----------------------------

Dmitri Pal (8):

-   ELAPI sinks and providers
-   ELAPI Adding file provider and CSV format
-   ELAPI Laying foundation for the async processing
-   COLLECTION Copy collection flat with concatenated names
-   COLLECTION Improvements to copy functions
-   COLLECTION Functions to deal with hash
-   ELAPI Better separation from collection internals.
-   INI Error handling and interface cleanup

Jakub Hrozek (17):

-   Remove shadow-utils support from tools
-   Small changes to the example config and manpage
-   Add copyright notices
-   ELAPI: Fix dispatcher structure initialization
-   Add binaries and backup files to .gitignore
-   Refactor tools code
-   Decouple synchronous sysdb interface from tools
-   Provide python bindings for sysdb
-   Use syslog for logging error conditions in SSSD
-   ELAPI: fix varargs call, update unit tests
-   ELAPI: Ticket 161: Initialize structures with calloc instead of
    enumerating members
-   Allow entering parent groups as FQDN
-   Remove provider=files
-   Manpages update
-   script to upgrade config to v2
-   Send debug messages to logfile
-   Convert the example config to v2 format, upgrade config on update
    only

Jeff Schroeder (1):

-   Add documentation for installing build dependencies

Piotr Drąg (1):

-   Add pl translation

Ralf Haferkamp (2):

-   Fix initgroups search filter when using rfc2307bis
-   Avoid crash when timestamp is NULL

Simo Sorce (30):

-   Use the correct structure.
-   Initial support for multiple schema types
-   Always save using member/memberOf
-   Fix group replies when using member/memberof
-   Upgrade database to 0.2
-   Remove redunant function and always pass attrs.
-   Make enumeration an independent task
-   Speed-up enumerations.
-   Correctly handle DbusWatch behavior.
-   Turn enumeration into a boolean value
-   Honor enumerate option in ldap\_id
-   Fix proxy enumeration
-   Fix two possible uninitialized values
-   Split database in multiple files
-   Tools are allowed to touch only the 'local' domain
-   Fix Ldap id backend offline code
-   Fix memory mishandling.
-   Fix ldap enumeration async task
-   Fix getgrnam and getgrgid calls
-   Complete the removal of "legacy" option.
-   Update documentation and examples
-   Make the offline status backend-global
-   Turn ldap driver options into multitype
-   Fix copy&paste error.
-   Better handle groups w/o members
-   Fix copy&paste of wrong structure
-   Don't try to use initgroups\_dyn if not available
-   Handle suspend cases
-   Split out an sssd-clients package
-   Let backend respond while fetching large results

Stephen Gallagher (26):

-   Move RPM specfiles into contrib/
-   Consolidate cache lookups in the NSS
-   Add support for the EntryCacheNoWaitRefreshTimeout
-   Check for valid min and max IDs in confdb\_get\_domains
-   Update manpage to reflect new syntax for enumerate
-   Add strtoint32 and strtouint32 convenience functions
-   Properly detect negative/invalid values for the minId and maxId
-   Remove unused event context argument from confdb\_init
-   Read the configuration parsing before daemonization
-   Fix first-time confdb generation
-   Add 'make tests' target
-   Add strtoint32 and strtouint32 tests
-   Print error message when connection to the config db fails
-   Exit if the sssd is launched as a user other than root
-   Include m4 directories in tarball
-   Allow rerunning autoreconf from the tarball
-   Add PRERELEASE\_VERSION variable for use in sssd.spec.in
-   Add missing updates to LINGUAS for pl translation
-   Add missing reference to sssd-ldap(5) in sssd.conf(5) manpage
-   Include groupSearchBase in sssd-ldap(5) manpage
-   Several fixes and enhancements for config file processing
-   Make configure script compatible with older python versions
-   Revert "Use syslog for logging error conditions in SSSD"
-   Temporarily disable automatic config file reread
-   Upgrade confdb to version 2
-   Update version to 0.6.0

Sumit Bose (31):

-   removed unused header file
-   do not show server messages to user
-   fix internal order of ldap user mapping options
-   add configure check for errno\_t
-   send SSSD\_REALM and SSSD\_KDCIP environment to the client
-   check if gid attribute is empty
-   stop processing a domain if no provider is given
-   check if libpcre version is above or below 7
-   remove the concept of a backend name
-   configure cleanups
-   fix libdbus configure check
-   initialize sockaddr\_in structure
-   add change password target to krb5 backend
-   use fork+exec for kerberos helper
-   Let the PAM client send its PID
-   remove unused client locale from PAM protocol
-   make cli\_pid mandatory and increase version number of pam protocol
-   add krb5ccache\_dir and krb5ccname\_template option
-   fix the wrong usage of an offset
-   added child timeout handler
-   Check if SSL/TLS handler is already in place
-   use getaddrinfo to resolve IP address of KDC
-   add a man page for pam\_sss
-   toggle debug output of sssd\_krb5\_locator\_plugin with an
    environment variable
-   add new config options ldap\_tls\_cacert and ldap\_tls\_cacertdir
-   fix possible short reads in kerberos provider
-   remove krb5\_try\_simple\_upn option and make it a default fallback
-   add defines for large file support to standard CFLAGS
-   more fixes for older libpcre versions
-   Cleanups for library linking
-   added support for older MIT kerberos versions

