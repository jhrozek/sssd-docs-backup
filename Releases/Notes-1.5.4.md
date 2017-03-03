Highlights {#Highlights}
----------

-   Fixes for Active Directory when not all users and groups have POSIX
    attributes
-   Fixes for handling users and groups that have name aliases (aliases
    are ignored)
-   Fix group memberships after initgroups in the IPA provider

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (4):

-   Fix LDAP search filter for nested initgroups
-   Add originalDN to fake groups
-   Use fake groups during IPA schema initgroups
-   Return from functions in LDAP provider after marking request as
    failed

Stephen Gallagher (19):

-   Update version to 1.5.4
-   Require existence of GID number and name in group searches
-   Require existence of username, uid and gid for user enumeration
-   Add support for krb5 access provider to SSSDConfig API
-   Fix incorrect return value check
-   Create sysdb\_get\_rdn() function
-   Add sysdb\_attrs\_primary\_name()
-   Ignore aliases for users
-   RFC2307: Ignore aliases for groups
-   RFC2307bis: Ignore aliases for groups
-   Use sysdb\_attrs\_primary\_name() in
    sdap\_initgr\_nested\_store\_group
-   Add sysdb\_attrs\_primary\_name\_list() routine
-   Don't crash if we get a multivalued name without an origDN
-   Don't crash on error if \_name parameter unspecified
-   Check result of talloc\_strdup() properly
-   sss\_obfuscate: Avoid traceback on ctrl+d
-   sss\_obfuscate: abort on ctrl+c
-   Add transifex\_client configuration
-   Adding new translations

Sumit Bose (1):

-   Sanitize DN when searching the original DN in the cache

