Highlights {#Highlights}
----------

-   Fixed issues with LDAP search filters that needed to be escaped
-   Add Kerberos FAST support on platforms that support it
-   Reduced verbosity of PAM\_TEXT\_INFO messages for cached credentials
-   Added group support to the simple access provider
-   Added a Kerberos access provider to honor .k5login
-   Addressed several thread-safety issues in the sss\_client code
-   Improved support for delayed online Kerberos auth
    -   Significantly reduced time between connecting to the network/VPN
        and acquiring a TGT
-   Added feature for automatic Kerberos ticket renewal
    -   Provides the kerberos ticket for long-lived processes or cron
        jobs even when the user logs out
-   Added several new features to the LDAP access provider
    -   Support for 'shadow' access control
    -   Support for authorizedService access control
    -   Ability to mix-and-match LDAP access control features
-   Added an option for a separate password-change LDAP server for those
    platforms where LDAP referrals are not supported
-   Added support for manpage translations

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (5):

-   Always use uint32\_t for UID/GID numbers
-   Internal DNS resolver should check /etc/hosts
-   Allow protocol fallback for SRV queries
-   Make manual pages translatable
-   Add Czech translation

Jan Zeleny (1):

-   Option krb5\_server is now used to store a list of KDCs instead of
    krb5\_kdcip.

Marko Myllynen (1):

-   Fix a typo in sssd-krb5 man page

Moritz Baumann (1):

-   Fix misused SDAP\_SEARCH\_BASE

Piotr Drąg (1):

-   Updating pl translation

Simo Sorce (6):

-   sss\_client: make code thread-safe
-   Pass sdap\_id\_ctx in sdap\_id\_op functions.
-   ldap: remove variable that was never assigned nor used
-   ldap: add checks to determine if USN features are available.
-   ldap: Use USN entries if available.
-   Fix wrong test in pam\_sss

Stephen Gallagher (58):

-   Write log opening failures to the syslog
-   Improve versioning for automated builds
-   Bumping version to 1.5.0 dev
-   Fix incorrect free of req in krb5\_auth.c
-   Don't clean up groups for which a user has it as primary GID
-   Handle errors during log reopening better
-   Properly check the return value from semanage\_commit
-   Add utility function to sanitize LDAP/LDB filters
-   Add sysdb utility function for sanitizing DN
-   Sanitize search filters for the sysdb
-   Sanitize sysdb search filters in the IPA provider
-   Sanitize sysdb filters in the LDAP provider
-   Sanitize sysdb DN helpers
-   Sanitize search filters in memberOf plugin
-   Sanitize sysdb dn for memberof lookup
-   Add unit tests for users and groups with odd characters
-   Sanitize search filters in LDAP provider
-   Properly document ldap\_purge\_cache\_timeout
-   Sanitize ldap attributes in the config file
-   Fix cast warning for pam\_sss.c
-   Fix const cast warning for sysdb\_update\_members
-   Fix const cast warning in build\_attrs\_from\_map
-   Fix const cast issue with sysdb\_attrs\_users\_from\_str\_list
-   Fix const cast warning in confdb\_create\_ldif
-   Fix const cast warnings in tests
-   Fix incorrect type comparison
-   Log startup errors to syslog
-   Ensure that SSSD shuts down completely before restarting
-   Fix authentication queue code for proxy auth
-   Wait for all children to exit
-   Add signal documentation to sssd(8)
-   Print correct error messages for dp\_err\_to\_string()
-   Make default SIGTERM and SIGINT handlers use tevent
-   Resend SIGTERM if child doesn't terminate
-   Set up signal handlers before initializing sysdb
-   Make sure that sss\_obfuscate installs as executable
-   Move sss\_\* tools into their own subpackage
-   Remove IPA\_ACCESS\_TIME define
-   Add group support to the simple access provider
-   Fix timeouts for DNS resolver
-   Reschedule the fd timeout for secondary lookups
-   Eliminate possible NULL-dereference in pam\_check\_user\_search
-   Add missing break statement to sss\_hash\_create
-   Prevent uninitialized value error in monitor\_quit
-   Fix invalid sizeof in pidfile
-   Fix segfault for PAM\_TEXT\_INFO conversations
-   Fix unchecked return value in sss\_krb5\_verify\_keytab\_ex
-   Fix unsafe return condition in ipa\_access\_handler
-   Fix uninitialized value error in set\_local\_and\_remote\_host\_info
-   Fix unchecked return value in test\_sysdb\_attrs\_to\_list
-   Fix unchecked return value in set\_nonblocking
-   Start first enumeration immediately
-   Add sysdb\_has\_enumerated and sysdb\_set\_enumerated helper
    functions
-   Pass all PAM data to the LDAP access provider
-   Add authorizedService support
-   Ensure ID is checked in all domains for PAM
-   Update the ID cache for any PAM request
-   Committing new translation updates for release

Sumit Bose (79):

-   Add ldap\_deref option
-   Add some missing ldap\_memfree()
-   Download only enabled IPA HBAC rules
-   Add netgroups infrastructure to proxy provider
-   Implement netgroups for proxy provider
-   Remove all nss requests after a reconnect
-   Always use talloc\_zero() to allocate cmdctx
-   Fix double free issue
-   Allow authentication for referrals
-   Mention ding-libs in BUILD.txt
-   Fix two return value checks
-   Store krb5 auth context for other targets
-   Add infrastructure for Kerberos access provider
-   Add krb5\_get\_simple\_upn()
-   Make krb5\_setup() public
-   Add krb5\_kuserok() access check to krb5\_child
-   Make handle\_child\_\* request public
-   Call krb5\_child to check access permissions
-   Add defaultNamingContext to RootDSE attributes
-   Use (default)namingContext to set empty search bases
-   Make ldap\_search\_base a non-mandatory option
-   Review comments for namingContexts patches
-   Avoid long long in messages to PAM client use int64\_t
-   Introduce pam\_verbosity config option
-   Add missing error code
-   Fix offline detection for LDAP auth/chpass
-   Fix man page
-   Use a more efficient host search filter
-   Add SIGUSR2 to reset offline status
-   fix typo in get\_server\_status()
-   Fix a typo on setup\_netlink()
-   Daemonize by default
-   Run checks before resetting offline state
-   Fix offline detection in sdap\_cli\_connect request
-   Add check\_online method to LDAP ID provider
-   Add a special filter type to handle enumerations
-   Send authtok\_type to krb5\_child
-   Add a renew task to krb5\_child
-   Check authtok type for krb5 auth and chpass
-   Add krb5\_renewable\_lifetime option
-   Add krb5\_lifetime option
-   Add support for server-side pam response messages
-   krb5\_child returns TGT lifetime
-   Add support for automatic Kerberos ticket renewal
-   Allow krb5 lifetime values without a unit
-   Make string\_to\_shadowpw\_days() public
-   Add new account expired rule to LDAP access provider
-   Add ldap\_chpass\_uri config option
-   Refactor krb5\_child to make helpers more flexible
-   Add support for FAST in krb5 provider
-   Mark unavailable Kerberos server as PORT\_NOT\_WORKING
-   Replace krb5\_kdcip by krb5\_server in LDAP provider
-   Fix build issue with older Kerberos library
-   Remove check\_access\_time() from IPA access provider
-   Bye, bye, ipa\_timerules
-   Fix unchecked return value in sdap\_get\_msg\_dn()
-   Fix unchecked return value in sdap\_parse\_entry()
-   Remove unused newauthtok variable in LOCAL\_pam\_handler
-   Fix improper NULL check in fo\_add\_srv\_server()
-   Fix incorrect return value on failure in
    resolve\_get\_domain\_send()
-   Fix incorrect return value on failure in
    check\_and\_export\_options()
-   Fix uninitialized value error in sdap\_account\_expired\_shadow()
-   Fix uninitialized value error in setup\_test in fail\_over-tests.c
-   Fix improper bit manipulation in pam\_sss
-   Fix possible memory leak in sss\_nss\_recv\_rep()
-   Fix uninitialized value error in main() in stress-tests.c
-   Fix possible memory leak in do\_pam\_conversation
-   Fix another possible memory leak in sss\_nss\_recv\_rep()
-   Fix memory leak of library handle in proxy
-   Fix uninitialized value error in lookup\_netgr\_step()
-   Fix possible NULL-dereference in lookup\_netgr\_step()
-   Avoid multiple initializations in LDAP provider
-   Introduce sss\_hash\_create\_ex()
-   Fixes for automatic ticket renewal
-   Serialize requests of the same user in the krb5 provider
-   Update config API files
-   Add all values of a multi-valued user attribute
-   Remove unused member of a struct
-   Fix potential NULL-dereference in krb5\_auth\_done()

Yuri Chornoivan (1):

-   Updating uk translation

