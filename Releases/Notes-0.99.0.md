Highlights {#Highlights}
----------

-   Enhanced IPA provider with host-based access control support
-   Added server failover feature
-   Vast performance enhancements to enumerations
-   Performance enhancements to offline user lookups
-   Improvements to the SSSDConfig API and configuration upgrade
    scripts. They will now retain comments and ordering.
-   Several new translations

Known Bugs {#KnownBugs}
----------

-   Nested groups are known to be broken in 0.99. A fix is basically
    ready, but was too late for inclusion in this release. This will be
    fixed before the 1.0 release.

Detailed changes since 0.7.1 {#Detailedchangessince0.7.1}
----------------------------

Bouska (1):

-   Add French translation to sss\_client

Jakub Hrozek (17):

-   Fix migration script for pre-0.5 local domains
-   Do not migrate Data Provider
-   Free the PCRE regexp with destructor
-   Do not delete users, groups outside domain range
-   Add missing include
-   IPA time rules parsing routines
-   Fix regression in error message when deleting groups
-   Assorted manpage fixes
-   Make the password field configurable in NSS
-   Add Simo's ipachangeconf
-   SSSDChangeConf - a wrapper around ipachangeconf
-   Change the upgrade script to use ipachangeconf
-   Convert SSSDConfig API to ipachangeconf
-   SSSDConfigAPI fixes
-   upgrade\_config fixes for SSSD 0.6 and later
-   Split helpers for child processes
-   Get TGT in a child process.

Martin Nagy (5):

-   Add missing include file to files-tests.c
-   Fix a bad free in async\_resolv.c
-   Add DLIST\_FOR\_EACH() macro
-   Add simple reference counting wrappers for talloc
-   Add fail over utility functions

Piotr Drąg (1):

-   Updating polish translation for 0.7.0

Simo Sorce (48):

-   Copy option overrides.
-   Read the right buffer, avoids potential segfaults
-   Add IPA conf template
-   Zero pointers on free
-   Use standard coding practice to set last login
-   Fix segfault
-   Add proper support for IPA/AD schemas
-   Move responsibility for entry expiration timeout
-   Kill the ldap connection when we go offline
-   Tidy up ipa options
-   Add support to get rootDSE from the LDAP server.
-   Fix segfault when SASL is not used at all
-   Rename sdap\_id\_map to sdap\_attr\_map
-   Make available method to quickly retrive string
-   Make useful function more broadly available.
-   Store the original memberof attributes if any
-   Unify parse routines, use maps in generic searches
-   Fix and enhance initgroups call
-   Unify code to use the generic search interface
-   Reorganize ldap id provider files
-   Split async helpers in multiple files
-   Always set last update and expire time
-   Fix build
-   Fix ldap driver
-   Check return, zero free hostent, adhere to style
-   Fix enumerations
-   Fix tevent\_req error checking.
-   Refactor delete functions and add a few
-   Add cleanup task
-   Try to fix offline logins
-   Fix double free case.
-   Fix check\_cache bug in dealing with the callback
-   Change var name to make its use more clear.
-   Fix crash due to uninitialized timeout variable
-   Change initgroups code to use and check the cache
-   Change the pam code to perform an initgroups call
-   Store initgr expire time on initgr call
-   Failover fixes and additions
-   Better behavior on cleanup
-   Correctly escape DN value.
-   Add reference to sssd-krb5 man page.
-   Optimize sysdb\_enumgrent
-   Filter by id range before actually storing entries.
-   Raise some timeouts
-   Add initial failover support for ldap and ipa
-   Fix ticket
    [\#289](https://fedorahosted.org/sssd/ticket/289 "defect: Filter User Now Getting Returned as  Member of a Group - Change in ... (closed: fixed)"){.closed
    .ticket}
-   Fix internal options numbers test
-   In IPA, the realm is always the domain uppercased.

Stephen Gallagher (32):

-   Remove DP from example configuration
-   Remove \[dp\] section from example config
-   Fix sssd.api.conf with correct entry\_cache\_timeout
-   Clean up warnings in dhash tests
-   Make config\_file\_version a hidden setting in SSSDConfig API
-   Remove magic\_private\_groups from SSSDConfig API schema
-   Add support for option descriptions to SSSDConfig API
-   Localize SSSDConfig strings
-   Add complete pydoc for SSSDConfig API
-   Add Requires: cyrus-sasl-gssapi
-   Simplify debug\_fn()
-   Add configure check for sasl.h
-   Update midpoint refresh logic to be relative to cache timeout
-   Increase the sbus dispatch DEBUG level to 9
-   Build files.c only for tools
-   Clean up unused dependencies
-   Update sssd.spec to use only the required KRB5\_LIBS and NSS\_LIBS
-   Fix segfault on unknown user/domain
-   Fix Requires: sssd-client line in specfile
-   Make the sysdb user and group names case-sensitive
-   Upgrade cache and local databases to case-sensitive names
-   Update translatable strings
-   Fix sysdb upgrade bug
-   Add empty NL translation
-   Only display errors in unit tests
-   Update PL translation
-   Update NL translation
-   Make backend request type a bitfield
-   Speed up user requests while offline
-   Update translation strings for string freeze
-   Fix bug with bad ldb pkg-config files
-   Update version to 0.99.0

Sumit Bose (32):

-   store original DN with cached group objects if available
-   added a ASQ search API for sysdb
-   Allow sysdb\_search\_entry request to return more than one result
-   Add AM\_CFLAGS to unit tests
-   Fix compiler warnings in krb5\_utils-tests.
-   remove old sysdb file before starting tests
-   set ipa\_hostname if not given in config file
-   Make debug message less irritating.
-   add sysdb\_delete\_recursive request to sysdb API
-   Add sysdb\_attrs\_replace\_name to sysdb API.
-   Fix for a seg fault during recursive delete
-   add replacements for missing Kerberos calls
-   Check is ccache structure is initialized before calling
    krb5\_cc\_destroy
-   added access module of IPA provider
-   Simplify krb5 child handler
-   Add check for access-time rules to ipa\_access.
-   Add support for host, source host and user category
-   Fix inconsistent use of krb5\_ccname\_template
-   Fixes for proxy provider
-   Make 'permit' the default for the access target
-   Fix option name krb5\_changepw\_principal
-   Validate Kerberos credentials with local keytab
-   Improve handling of ccache files
-   Add ipa\_auth
-   Enhance check for remote hosts
-   Add ldap\_pwd\_policy option
-   Read KDC info from file instead from environment
-   Really check return value from pam\_set\_item
-   Use ldb modules from build root for tests
-   Make ldb lib dir configurable
-   Fix an internal error when cache\_credentials=FALSE
-   Remove unneeded debugging code

deneb (1):

-   Add Italian translation for sss\_client

noriko (1):

-   Adding Japanese translation

raven (1):

-   Update PL translation

