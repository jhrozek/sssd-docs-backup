Highlights {#Highlights}
----------

-   Fixes for support of FreeIPA v2
-   Fixes for failover if DNS entries change
-   Improved sss\_obfuscate tool with better interactive mode
-   Fix several crash bugs
-   Don't attempt to use START\_TLS over SSL. Some LDAP servers can't
    handle this
-   Delete users from the local cache if initgroups calls return 'no
    such user' (previously only worked for getpwnam/getpwuid)
-   Use new Transifex.net translations
-   Better support for automatic TGT renewal (now survives restart)
-   Netgroup fixes

Detailed Changelog {#DetailedChangelog}
------------------

Gowrishankar Rajaiyan (2):

-   removing password option functionality
-   updating sss\_obfuscate man page accordingly

Jakub Hrozek (6):

-   Use realm for basedn instead of IPA domain
-   Reset server status after timeout
-   Prevent segfault in failover code
-   Always expire host name resolution
-   Run callbacks if server IP changes
-   Mention Samba libraries URLs in BUILD.txt

Simo Sorce (1):

-   Check that the socket is really ours before attempting to close it.

Stephen Gallagher (16):

-   Update version to 1.5.2dev
-   Sanitize search filters for nested group lookups
-   Make the domain argument mandatory in sss\_obfuscate
-   Gracefully handle permission errors in sss\_obfuscate
-   Make SSSDConfig API configuration readable
-   Only print "no matching service rule" when appropriate
-   Verify LDAP file descriptor validity
-   Do not attempt to use START\_TLS on SSL connections
-   Point the IPA provider at the compat tree for netgroups
-   Remove cached user entry if initgroups returns ENOENT
-   Perform initgroups lookups for all domains
-   IPA provider: remove deleted groups during initgroups()
-   Allow krb5\_realm to override ipa\_domain
-   Add krb5\_realm to the basic IPA options
-   Fix uninitialized value error in ipa\_get\_id\_options()
-   Updating translations for 1.5.2 release

Sumit Bose (9):

-   Fix for generating lists of translated man pages
-   Remove renewal item if it is not re-added
-   Check ccache file for renewable TGTs at startup
-   Do not try to delete sysbd memberOf attribute
-   Fixes for dynamic DNS update
-   Add missing name to struct getent\_ctx for missing netgroup
-   Refactor set\_netgroup\_entry()
-   Change state of hash entry if netgroup cannot be parsed
-   Release handle if not connected

