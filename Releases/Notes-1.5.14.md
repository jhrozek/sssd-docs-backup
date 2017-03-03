Highlights {#Highlights}
----------

-   Improved handling of users and groups with multi-valued name
    attributes (aliases)
-   Performance enhancements
    -   Initgroups on RFC2307bis/FreeIPA
    -   HBAC rule processing
-   Improved process-hang detection and restarting
-   Enabled the midpoint cache refresh by default (fewer cache misses on
    commonly-used entries)
-   Cleaned up the example configuration

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (22):

-   Improve error message for LDAP password constraint violation
-   Fix uninitialized pointer read in
    sdap\_gssapi\_get\_default\_realm()
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
-   Do not delete requests inside hash\_iterate loop
-   Check if dp\_requests hash table exists before using it
-   Fix off-by-one error in remove\_socket\_symlink()
-   Report on errno, not return code in create\_socket\_symlink
-   Add a missing break
-   Sanitize DN in sysdb\_get\_direct\_parents
-   gitignore additions
-   Utility functions for LDAP nested schema initgroups
-   Use fewer transactions during RFC2307bis initgroups
-   Use fewer transactions during IPA initgroups

Jan Zeleny (2):

-   man page fix (lists are comma-separated)
-   Fixed timeout handling in responders

Marko Myllynen (3):

-   Add missing options to sssd.api.conf
-   Unbreak ./configure
-   Update sssd-example.conf

Pavel Březina (3):

-   sss\_ldap\_err2string() - function created
-   sss\_ldap\_err2string() - ldap\_err2string() to
    sss\_ldap\_err2string()
-   Added quiet option to pam\_sss

Stephen Gallagher (17):

-   Bumping version to 1.5.14
-   Add option to specify the kerberos replay cache dir
-   Fix typo in %configure
-   Remove all libtool .la files from RPM
-   Improve documentation of libipa\_hbac
-   Add libipa\_hbac documentation to the -devel package
-   MONITOR: Correctly detect lack of response from services
-   Do not build documentation on RHEL 5
-   Fix typo in specfile
-   MAN: Add more information about internal credential storage
-   HBAC: fix typos preventing proper hostgroup evaluation
-   HBAC: Do not save member/memberOf links
-   HBAC: Use originalMember for identifying servicegroups
-   HBAC: Use originalMember for identifying hostgroups
-   BUILDSYS: Fix --without-manpages
-   MONITOR: fix timeout conversion
-   Updating translation files

Sumit Bose (1):

-   Do not access memory out of bounds

