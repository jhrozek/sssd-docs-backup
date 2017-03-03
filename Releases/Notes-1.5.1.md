Highlights {#Highlights}
----------

-   Addresses CVE-2010-4341 - DoS in sssd PAM responder can prevent
    logins
-   Vast performance improvements when `enumerate = true`
-   All PAM actions will now perform a forced initgroups lookup instead
    of just a user information lookup
    -   This guarantees that all group information is available to other
        providers, such as the simple provider.
-   For backwards-compatibility, DNS lookups will also fall back to
    trying the SSSD domain name as a DNS discovery domain.
-   Support for more password expiration policies in LDAP
    -   389 Directory Server
    -   FreeIPA
    -   ActiveDirectory
-   Support for ldap\_tls\_{cert,key,cipher\_suite} config options
    -   Provided by community member Tyson Whitehead
-   Assorted bugfixes

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (1):

-   NSS obfuscation code cleanup

Piotr Drąg (2):

-   Updating pl translation
-   Updating pl translation

Stephen Gallagher (27):

-   Bumping version to 1.5.1
-   Remove unnecessary po4a BuildRequires
-   Fix boolean comparison against string
-   Work around libldb bug
-   Add missing sysdb transaction to group enumerations
-   Do not throw a DP error when a netgroup is not found
-   Fix missing hash table bug
-   Regenerate manpage po\[t\] files
-   Update manpage translations for ldap\_enumeration\_search\_timeout
-   Fix usability of sss\_obfuscate command
-   Do not force a default for debug\_level
-   Clarify nscd warning
-   Remove support for pre-1.1 netlink
-   Don't double-sanitize member DNs
-   Fix incorrect example file
-   Add the user's primary group to the initgroups lookup
-   Perform initgroups lookup for PAM
-   Add missing include file to sdap\_async\_accounts.c
-   Allow fallback to SSSD domain
-   Rename dns\_domain to discovery domain for fo\_add\_srv\_server()
-   Delete attributes that are removed from LDAP
-   Updating translation files for string freeze
-   Update translation files for string freeze
-   Add uk translation to specfile
-   Add missing gettext BuildRequires
-   Update man.stamp when the potfile or po4a.cfg is updated
-   Add option to disable TLS for LDAP auth

Sumit Bose (22):

-   Build and install translated man pages by default
-   Use the right status when resetting service discovery
-   Rename SRV\_NOT\_RESOLVED to SRV\_RESOLVE\_ERROR
-   Return groups and users from all domains during enumeration
-   Post enumeration tevent request if needed
-   Remove unused enumeration cache timeout checks
-   Convert obfuscated password once at startup
-   Add syslog message to shadow access check
-   Add syslog messages to authorized service access check
-   Validate user supplied size of data items
-   Add overflow check to SAFEALIGN\_COPY\_\*\_CHECK macros
-   Add timeout parameter to sdap\_get\_generic\_send()
-   Add ldap\_search\_enumeration\_timeout config option
-   Add LDAP expire policy based on AD attributes
-   Add LDAP expire policy base RHDS/IPA attribute
-   Add ipa\_hbac\_search\_base config option
-   Add pam\_pwd\_expiration\_warning config option
-   Use DEFAULT\_PAM\_VERBOSITY if config value cannot be retrieved
-   Fix return value check
-   Fix uninitialized value error
-   Fix nested group handling during enumeration
-   Do not fail if attributes are empty

Tyson Whitehead (1):

-   Add ldap\_tls\_{cert,key,cipher\_suite} config options

Yuri Chornoivan (6):

-   Updating uk translation
-   Add uk translation for manpages
-   Fix manpage typos
-   Updating uk manpage translation
-   Updating uk translation
-   Updating uk translation

