Highlights {#Highlights}
----------

-   Support for the service map in NSS
-   Support for setting default SELinux user context from FreeIPA
-   Support for retrieving SSH user and host keys from LDAP
    (Experimental)
-   Support for caching autofs LDAP requests (Experimental)
-   Support for caching SUDO rules (Experimental)
-   Include the IPA AutoFS provider
-   Fixed several memory-corruption bugs
-   Fixed a regression in group enumeration since 1.7.0
-   Fixed a regression in the proxy provider

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (58):

-   sss\_get\_cased\_name utility function
-   Return user and group names lowercased in case insensitive domains
-   Honor case sensitive flag when creating the ccname template
-   HBAC: create empty groups with one NULL element
-   Do not call krb5\_child when changing passwords and provider went
    offline
-   IPA netgroups: Do not reuse loop iterator variable
-   Add a configure switch to specify 3rd party app libraries location
-   Export libsss\_sudo as a separate package
-   Add a new Makefile target to build RPMs with the experimental flag
-   Do not use sudo symbols in LDAP provider unconditionally
-   PAM: Fix reversed logic
-   SUDO: include the sources in the IPA provider, too
-   PAM: Do not overwrite ret
-   DP: Refactor responder\_dp\_req so it's reusable by other responders
-   SUDO: Provide a sudo DP request based on the internal\_req
-   Use the new SUDO request in DP and sudo responder
-   Fix sudo compilation on RHEL5
-   Include sudo manual pages only conditionally
-   docs: Use absolute srcdir path
-   SUDO: Provide documentation for the SUDO API
-   SYSDB: index sudoUser
-   Refactor nss\_cmd\_send\_empty
-   Use profiling Docbook XSLT only if available, fall back to normal
-   RESPONDERS: Provide a common sss\_cmd\_send\_error function
-   NSS: Use sss\_hash\_create instead of destructor
-   Fixes for sudo\_timed
-   ConfigAPI: add sudo to known services
-   SUDO: introduce a new config option --with-sudo
-   Move BUILD\_SUDO outside the generic LDAP source files
-   Fix configure with old autoconf versions
-   BUILD: Introduce a --with-autofs config option
-   SYSDB: Remove code duplication between member\_add and member\_del
-   AUTOFS: sysdb interface
-   AUTOFS: a client library
-   AUTOFS: a command-line test client
-   AUTOFS: Data Provider request
-   RESPONDERS: Refactor setent\_req\_list
-   Split the logic to check cache expiration into separate function
-   AUTOFS: responder
-   AUTOFS: LDAP provider
-   Do not call sudo functions if built without-sudo
-   Make sudo installation path configurable, install into libdir by
    default
-   Fix SSH compilation on RHEL5
-   AUTOFS: IPA provider
-   Two sssd-ldap manual pages fixes
-   Fix group enumeration
-   Only fetch SELinux string if the user is found
-   Remove setent structure when callback is called
-   Allocate setent structure on state, not on the client context
-   Fix memory hierarchy when processing nested group memberships
-   Fix case insensitive service lookups
-   End request if ldap\_parse\_result fails
-   remove unused function
-   Save errno value before calling DEBUG
-   libnl: fix the path to phy80211 subdirectory
-   AUTOFS: Invoke implicit setautomntent if needed
-   AUTOFS: Search all search bases for automounter map entries
-   AUTOFS: speed up the client by requesting multiple entries at once

Jan Cholasta (26):

-   UTIL: Provide base64 encoding and decoding functions
-   BUILD: Introduce a --with-ssh config option
-   LDAP: Add support for SSH user public keys
-   DP: Add host info handler
-   IPA: Add host info handler
-   DP: Add support for hosts in sss\_dp\_get\_account
-   SSH: Responder
-   SSH: Common client code
-   SSH: OpenSSH authorized\_keys client
-   SSH: OpenSSH known\_hosts client
-   Add methods for activating and deactivating services to SSSDConfig
-   Add ssh service to sssd.api.conf
-   SSH: Verify that names received from client are valid UTF-8 in
    responder
-   SSH: Build man pages conditionally
-   SSH: Save SSH host name aliases
-   SSH: Refactor responder and client common code
-   UTIL: Add function for atomic I/O
-   SSH: Continue connecting to SSH server even when SSSD is not running
    in sss\_ssh\_knownhostsproxy
-   SSH: Manage global known\_hosts file in the responder
-   SSH: Don't abort known\_hosts update when host search fails
-   SSH: Add more debugging messages
-   SSH: Add missing break statements to sss\_ssh\_format\_pubkey
-   SSH: Use fchmod instead of chmod on known\_hosts file
-   SSH: Replace blocking getaddrinfo call in the responder with
    asynchronous resolver code
-   SSH: Remove unused --file option of sss\_ssh\_knownhostsproxy
-   SSH: Update sss\_ssh\_knownhostsproxy manual page

Jan Zeleny (21):

-   Add info about ipa\_host\_search\_base to man page
-   Support multiple search bases in HBAC
-   Fixed wrong position of ldap\_service\_search\_base
-   Implemented support for multiple search bases in HBAC rules and
    services
-   Fixed minor memory-hierarchy-related issue in IPA HBAC
-   Add support for generic IPA config retrieval
-   Make password migration code use the IPA config retrieval code
-   Renamed some sysdb constants for their wider usage
-   Added some SELinux-related utility functions
-   Added some SELinux-related sysdb routines
-   SELinux support in PAM responder
-   SELinux support in PAM module
-   Separate the host-retrieval code from IPA HBAC to common IPA code
-   Delete unused structure in IPA access code
-   Add session target in data provider
-   Session target in IPA provider
-   Man pages for the session target and SELinux user maps fetching
-   Update shadowLastChanged attribute during LDAP password change
-   Fixed issue with netgroup update in IPA provider
-   Delete missing attributes from netgroups to be stored
-   Modifications to simplify list\_missing\_attrs

Pavel Březina (21):

-   SUDO Integration review issues
-   SUDO Integration - wrap data provider with tevent\_req
-   sysdb\_get\_bool() and sysdb\_get\_bool() functions
-   SUDO Integration - functions for manipulating with 'refreshed'
    attribute
-   SUDO Integration - periodical update of rules in data provider
-   SUDO Integration - make sysdb\_get\_sudo\_filter() more configurable
-   SUDO Integration - prepare data provider for new responder commands
-   SUDO Integration - responder command for cn=defaults
-   SUDO Integration - SUDO API can request only cn=defaults record
-   SUDO Integration - test client changed
-   SUDO Integration - manual page
-   SUDO Integration - in-memory cache in responder
-   SUDO Integration - responder 'sudo\_timed' option
-   SUDO Integration - fix offline behaviour
-   SUDO Integration - sysdb\_sudo\_check\_time() fix
-   Improve debug messages in sysdb\_sudo\_check\_time()
-   SUDO responder: check if the input is a UTF-8 string
-   Refactor sss\_result into sss\_sudo\_result
-   Redesign purging of the sudo cache
-   Honor case\_sensitive option in sudo responder
-   Move sudo\_dom\_ctx.user to local variable

Simo Sorce (11):

-   make dist fixes
-   tests: fix test group of utf8 tests
-   nsssrv: remove unused macro
-   nsssrv: add string manipulation helper
-   nsssrv: use sized\_string in fill\_pwent
-   nsssrv: use sized\_string in fill\_grent
-   util: add murmurhash3 hash function
-   Add a random + identity test for murmurhash3
-   util: Fix murmurhash3 on machines with old glibc
-   nss\_group: Cache the result from sssd when the glibc provided
    buffer is too small.
-   pam\_sss: keep selinux optional

Stephen Gallagher (73):

-   Bump version to 1.8.0
-   Add compatibility layer for Heimdal Kerberos implementation
-   Importing new translations for 1.7.0 release
-   Log fixes for sdap\_call\_conn\_cb
-   LDAP: Copy URI instead of pointing at failover service record
-   NSS: Validate input string lengths
-   NSS: Improve DEBUG messages for netgroup cache
-   Raise the debug level of two very noisy statements
-   IPA: Detect nsupdate support for the realm directive
-   NSS: Add sss\_readrep\_copy\_string
-   LDAP: Add option to disable paging control
-   SYSDB: Redundant check is redundant.
-   Fix invalid index in pidfile()
-   RESPONDER: Extend sss\_dp\_account\_send() to include extra data
-   DP: Fix bugs in sss\_dp\_get\_account\_int
-   LDAP: Improve debugging for sdap\_parse\_deref
-   Move sized\_string declaration to utils
-   UTIL: Add strtouint16
-   SYSDB: Move add\_string and add\_ulong to sysdb\_private.h
-   DP: Handle parsing extra results in be\_get\_account\_info
-   SYSDB: Add sysdb routines for manipulating service entries
-   SYSDB: Add indexes for servicePort and serviceProtocol
-   NSS: Add client support for services (non-enumeration)
-   DP: Add support for services in dp requests
-   NSS: Add negative cache routines for services
-   NSS: Add getservbyname and getservbyport support to the NSS
    Responder
-   PROXY: add support for service lookups (non-enumeration)
-   NSS: Add client support for \[set|get|end\]servent()
-   SYSDB: add support for enumerating services
-   NSS: Add service enumeration support to NSS provider
-   PROXY: add support for enumerating services
-   Rename sss\_dp\_type to sss\_dp\_sudo\_type
-   SSSDConfigAPI: Move sssd.api.\* to /usr/share/sssd
-   SYSDB: extend sysdb\_store\_service() to accept additional
    attributes
-   SYSDB: Add sysdb\_attrs\_get\_uint16\_t
-   LDAP: Add support for service lookups (non-enum)
-   LDAP: Add enumeration support for services
-   IPA: Add support for services lookups (non-enum)
-   LDAP: Add new options for service maps
-   KRB5: Add syslog messages for Kerberos failures
-   LDAP: Do not fail if RootDSE check cannot determine search bases
-   LDAP: Fix incorrect search timeouts
-   NSS: Add individual timeouts for entry types
-   Build all experimental features during 'make distcheck'
-   Set version to 1.7.91 for 1.8.0beta1
-   Updating translatable strings for string freeze
-   Updating translations
-   Bumping version to 1.8.0 beta2
-   Remove dead code
-   Fix missing NULL check after malloc
-   Avoid uninitialized value comparison
-   Add missing breaks to switch statements
-   Fix uninitialized in\_transaction
-   Fix bad failure handling in be\_sudo\_handler()
-   Check for failure in sss\_packet\_grow()
-   Fix uninitialized value error in proxy provider
-   Ensure NULL-termination in get\_uid\_from\_pid()
-   Move sss\_ssh\_\* binaries to the main 'sssd' package
-   Always include all manpage XML files in the distribution tarball
-   Bumping version to 1.7.93 for beta 3
-   Fix missing %endif in sssd.spec.in
-   NSS: Always return the same protocol that was requested
-   LDAP: Ignore group member users that do not have name attributes
-   RESPONDERS: Allow increasing the file-descriptor limit
-   Add tool to convert debug levels
-   IPA: Add ipa\_parse\_search\_base()
-   LDAP: Properly assign orig\_dn
-   LDAP: Only use paging control on requests for multiple entries
-   LDAP: Remove unnecessary filter sanitize
-   Eliminate build-time requirement for nscd
-   PAM: Don't send PAM\_SYSTEM\_INFO message if module unset
-   Update version to 1.8.0
-   Updating translations for SSSD 1.8.0 release

Sumit Bose (1):

-   Use curly braces in pkgconfig metadata file

