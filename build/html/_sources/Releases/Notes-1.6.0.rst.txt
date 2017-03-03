Highlights
----------

-  Add host access control support for LDAP (similar to pam\_host\_attr)
-  Finer-grained control on principals used with Kerberos (such as for
   FAST or validation)
-  Added a new tool ``sss_cache`` to allow selective expiring of cached
   entries
-  Added support for LDAP DEREF and ASQ controls

   -  This will result in a marked speedup when dealing with initgroups
      requests of users in many groups

-  Added access control features for Novell Directory Server
-  FreeIPA dynamic DNS update now checks first to see if an update is
   needed

   -  Previously we would always issue an update upon any 'going online'
      event

-  Complete rewrite of the HBAC library
-  New libraries: libipa\_hbac and libipa\_hbac-python

Detailed Changelog since 1.5.1
------------------------------

Gowrishankar Rajaiyan (2):

-  removing password option functionality
-  updating sss\_obfuscate man page accordingly

Jakub Hrozek (92):

-  Use realm for basedn instead of IPA domain
-  Reset server status after timeout
-  Prevent segfault in failover code
-  Always expire host name resolution
-  Run callbacks if server IP changes
-  Mention Samba libraries URLs in BUILD.txt
-  Fix LDAP search filter for nested initgroups
-  Add originalDN to fake groups
-  Use fake groups during IPA schema initgroups
-  Return from functions in LDAP provider after marking request as
   failed
-  Fix typo in sdap\_nested\_group\_process\_step
-  Mark transaction as done when cancelled
-  Only save members for successfully saved groups
-  Do not attempt to resolve nameless servers
-  Don't pass NULL to printf for TLS errors
-  Fix unchecked return values of pam\_add\_response
-  Remove detection of duplicates from SRV result processing
-  Use safe alignment macros for in-tree SRV record parsing
-  The systemd unit file should not require DBus
-  Provide a configuration option to use systemd unit file
-  Only check systemd unit dir if systemd is selected
-  Set same status for duplicate servers
-  Add user and group search LDAP filter options
-  Case insensitive originalDN test
-  Require openssl-devel is libcrypto backend is selected
-  Warn that some crypto features are implemented in NSS only
-  Disable libcrypto code
-  Do not leak LDAP paging controls
-  Fix order of arguments in select\_principal\_from\_keytab() call
-  Do not leak pcre context
-  Do not leak LDAP URI with high log level
-  Do not leak netgroups hash table
-  Remove unused constants from data\_provider.h
-  Use a temporary memory context in expand\_ccname\_template
-  Set c-ares to retry nameservers
-  Remove append\_attrs\_to\_array
-  Rename label in expand\_ccname\_template
-  Add a new option to override primary GID number
-  Add a new option to override home directory value
-  Add new options to override shell value
-  sdap\_get\_generic\_ext
-  Generic dereference data structures and utilities
-  Add support for Attribute Scoped Queries
-  OpenLDAP dereference searches
-  Generic dereference search
-  Change sysdb\_add\_fake\_user to add OriginalDN
-  Use fake users during RFC2307bis nested group processing
-  Refactor RFC2307bis nested group processing
-  Use dereference when processing RFC2307bis nested groups
-  Fix bad comparison in sdap\_has\_deref\_support
-  Fix uninitialized pointer read in sdap\_x\_deref\_parse\_entry
-  Fix uninitialized scalar variable in
   sdap\_nested\_group\_check\_cache
-  Separate return paths for success and failure in
   sdap\_nested\_group\_check\_cache
-  Add utility function to return IP address as string
-  Add a utility function to escape IPv6 address for use in URIs
-  Use escaped IP addresses in LDAP provider
-  Escape IPv6 IP addresses in the IPA provider
-  Make parse\_args skip extra spaces
-  Unit test for parge\_args
-  Add new resolv\_hostent data structure and utility functions
-  Resolve hosts by name from files into resolv\_hostent
-  Resolve hosts by name from DNS into resolv\_hostent
-  Switch resolver to using resolv\_hostent and honor TTL
-  Provide TTL structure names for c-ares < 1.7
-  Test NULL server hostname in fail over tests
-  Log nsupdate message
-  ipa\_dyndns: Use sockaddr\_storage for storing IP addresses
-  Provide python bindings for the HBAC evaluator library
-  Move IP adress escaping from the LDAP namespace
-  Escape IP address in kdcinfo
-  Do not hardcode default resolver timeout
-  Split reading resolver family order into a separate function
-  Allow returning arbitrary address from resolv\_hostent as string
-  Check DNS records before updating
-  Remove unused krb5\_service structure member
-  Use ares\_search instead of ares\_query for hostname resolution
-  Fixes for python HBAC bindings
-  Fix python HBAC bindings for python <= 2.4
-  Do not add a NULL host parsed from LDAP URI
-  Only print server address if one is available
-  Rename fo\_get\_server\_name to fo\_get\_server\_str\_name
-  fo\_get\_server\_name() getter for a server name
-  Fix indexing of skipped groups
-  Set gidNumber of non-posix groups to 0 even on updates
-  Explicitly ignore groups with gidNumber=0
-  Remove dead code from python HBAC bindings
-  Handle allocation error in python HBAC bindings
-  UTF8 HBAC test
-  Wrong paramater to sysdb\_attrs\_add\_uint32
-  Change the default value of ldap\_tls\_cacert in IPA provider
-  HBAC rule validation Python bindings
-  Request password control unconditionally during bind

Jan Zeleny (28):

-  Remove unused be\_check\_online() SBUS call
-  Remove unused sysdb\_attrs object
-  Fix one unlikely case of failure in sdap\_id\_op module
-  Add last usn checking after reconnection
-  Extend and move function for finding principal in keytab
-  Allow new option to specify principal for FAST
-  Don't use negative cache in netgroup lookup
-  Configuration parsing updates
-  Added originalDN to attributes with case-insensitive search
-  Modify principal selection for keytab authentication
-  Fixed lastUSN checking improvements
-  Make sysdb\_ctx\_list public structure
-  Add a function for searching netgroups with custom filter
-  Cache cleaning tool
-  Some minor fixes and changes in sysdb\_ops
-  Man page for sss\_cache
-  Added some kerberos functions for building on RHEL5
-  Fixed --debug-to-files for nss and pam services
-  Fixed wrong variable in sdap\_initgr\_nested\_store
-  Possible memory leak fixed
-  Fixed unitialized return value in match\_principal
-  Fixed unitialized pointer in select\_principal\_from\_keytab
-  Fixed uninitialized value in sss\_cache
-  Fixed copying of pam\_data structure
-  Added sysdb\_attrs\_get\_bool() function
-  Non-posix group processing - sysdb changes
-  Non-posix group processing - ldap provider and nss responder
-  Fall back to polling when inotify fails

John Hodrien (1):

-  Add vetoed\_shells option

Kaushik Banerjee (1):

-  Changing default to Default for consistency

Matthew Ife (1):

-  Replace system() function with fork and execl call.

Pierre Ossman (1):

-  Add host access control support

Simo Sorce (8):

-  Check that the socket is really ours before attempting to close it.
-  Use neutral name for functions used by both pam and nss
-  sysdb: use header defined macros instead of explicit values
-  memberof: fix calculation of replaced members
-  memberof: free delete operation apyload once done
-  clients: use poll instead of select
-  fix typos
-  sss\_client: avoid leaking file descriptors

Stephen Gallagher (96):

-  Update version to 1.5.2dev
-  Sanitize search filters for nested group lookups
-  Bumping version to 1.6.0dev
-  Wrap cleanup task in a sysdb transaction
-  Add additional indexing for sysdb
-  Make the domain argument mandatory in sss\_obfuscate
-  Gracefully handle permission errors in sss\_obfuscate
-  Make SSSDConfig API configuration readable
-  Only print "no matching service rule" when appropriate
-  Clear up -Wunused-but-set-variable warnings
-  Fix cleanup transaction
-  Fix module registration with newer LDB libraries.
-  Verify LDAP file descriptor validity
-  Minor specfile changes
-  Detect the proper location for memberof.so
-  Fix specfile for RHEL5
-  Do not attempt to use START\_TLS on SSL connections
-  Point the IPA provider at the compat tree for netgroups
-  Remove cached user entry if initgroups returns ENOENT
-  Perform initgroups lookups for all domains
-  IPA provider: remove deleted groups during initgroups()
-  Allow krb5\_realm to override ipa\_domain
-  Add krb5\_realm to the basic IPA options
-  Fix uninitialized value error in ipa\_get\_id\_options()
-  Add transifex\_client configuration
-  Add new translations from Transifex
-  Update translation sources
-  Require existence of GID number and name in group searches
-  Require existence of username, uid and gid for user enumeration
-  Add support for krb5 access provider to SSSDConfig API
-  Fix incorrect return value check
-  Create sysdb\_get\_rdn() function
-  Add sysdb\_attrs\_primary\_name()
-  Ignore aliases for users
-  RFC2307: Ignore aliases for groups
-  RFC2307bis: Ignore aliases for groups
-  Use sysdb\_attrs\_primary\_name() in
   sdap\_initgr\_nested\_store\_group
-  Add sysdb\_attrs\_primary\_name\_list() routine
-  Don't crash if we get a multivalued name without an origDN
-  Don't crash on error if \_name parameter unspecified
-  Check result of talloc\_strdup() properly
-  sss\_obfuscate: Avoid traceback on ctrl+d
-  sss\_obfuscate: abort on ctrl+c
-  Always complete the transaction in
   sdap\_process\_group\_members\_2307
-  RFC2307: Ignore zero-length member names in group lookups
-  Fall back to cn if gecos is not available
-  Never remove gecos from the sysdb cache
-  Do not throw a DP error when failing to delete a nonexistent entity
-  Add debug logging to the negative cache
-  Fix a regression with the negative cache in multi-domain
   configurations
-  Fix regression where nonexistent entries were never added to the
   negative cache
-  Don't leak memory if sysdb\_domain\_init() fails
-  Run all appropriate upgrades
-  Reopen the LDB after modifying it
-  Always generate kpasswdinfo file
-  Add value of the last USN to server configuration
-  simple provider: Don't treat primary GID lookup failures as fatal
-  Log the LDAP message type we're processing
-  Enable paging support for LDAP
-  Add ldap\_page\_size configuration option
-  Add "description" option to SSSDConfig API
-  Regular translation update
-  Fix IPA config bug with SDAP\_KRB5\_REALM
-  Fix segfault in IPA provider
-  Fix bad password caching when using automatic TGT renewal
-  Fix minor typo in error message
-  Override config file debug\_level with command-line
-  Include manpage for sss\_cache
-  Create common sss\_monitor\_init()
-  Allow changing the log level without restart
-  IPA Provider: don't fail if user is not a member of any groups
-  Build SSSD plugins without a version number
-  Build sssd utils as a libtool helper library
-  Import config.h earlier
-  Make "password" the default for ldap\_default\_authtok\_type
-  Add more detail to ldap\_uri manpage entry
-  Fix typo in initgroups negative cache check
-  Ensure that SSSD always Requires: the primary-arch sssd-client
-  Do not attempt to close() a file descriptor < 0
-  Add helper function msgs2attrs\_array
-  Add HBAC evaluator and tests
-  Add helper functions for looking up HBAC rule components
-  Remove old HBAC implementation
-  Add new HBAC lookup and evaluation routines
-  Add ipa\_hbac\_refresh option
-  Add ipa\_hbac\_treat\_deny\_as option
-  Treat NULL or empty rhost as unknown
-  Allow NULL memctx in sysdb\_custom\_subtree\_dn
-  libipa\_hbac: Support case-insensitive comparisons with UTF8
-  Fix memory leak in ipa\_hbac\_evaluate\_rules
-  Fix incorrect NULL check in ipa\_hbac\_common.c
-  Converge accept\_fd\_handler and accept\_priv\_fd\_handler
-  Require matched version and release for libipa\_hbac
-  Remove incorrect private variable
-  Add rule validator to libipa\_hbac
-  Allow LDAP to decide when an expiration warning is warranted

Sumit Bose (38):

-  Fix handling of translated man pages in spec file
-  Remove LDAP\_DEPRECATED
-  Make 'make check' look nice again
-  Introduce sysdb\_ldb\_connect()
-  Check LDB\_MODULES\_PATH for sysdb
-  Fix for generating lists of translated man pages
-  Remove renewal item if it is not re-added
-  Check ccache file for renewable TGTs at startup
-  Do not try to delete sysbd memberOf attribute
-  Fixes for dynamic DNS update
-  Add missing name to struct getent\_ctx for missing netgroup
-  Refactor set\_netgroup\_entry()
-  Change state of hash entry if netgroup cannot be parsed
-  Release handle if not connected
-  Sanitize DN when searching the original DN in the cache
-  Read only rootDSE data if rootDSE is available
-  Initialise srv\_opts even if rootDSE is missing
-  Initialise rootdse to NULL if not available
-  Return pam data to the renewal item if renewal fails
-  Add support for openldap24 package on RHEL 5.7
-  Set \_GNU\_SOURCE globally
-  Remove unused defines from configure.ac
-  Include string.h in sss\_cli.h
-  Sanitize username during initgroups call
-  Add online callback only once for TGT renewal
-  Delete cached ccache file if password is expired
-  Fix two typos
-  Add missing libsss\_util to proxy provider
-  Fix proxy provider return code for secondary missing groups
-  Do not check pwdAttribute
-  Add sockaddr\_storage to sdap\_service
-  Add sdap\_call\_conn\_cb() to call add connection callback directly
-  Use name based URI instead of IP address based URIs
-  Use ldap\_init\_fd() instead of ldap\_initialize() if available
-  Do not access state after tevent\_req\_done() is called.
-  Call ldap\_install\_tls() on ldaps connections
-  Add support for experimental features
-  Add LDAP access control based on NDS attributes

pbrezina (1):

-  silence compilation warnings on RHEL5
