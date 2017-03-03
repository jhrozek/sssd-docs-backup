Highlights {#Highlights}
----------

-   Fixes a major cache performance issue introduced in 1.6.2
-   Fixes a potential infinite-loop with certain LDAP layouts

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (4):

-   Plug memory leaks in LDAP provider
-   RFC2307bis initgroups: fix nested groups processing
-   Steal result onto mem\_ctx in
    sdap\_initgr\_nested\_get\_direct\_parents
-   Use LDAPDerefSpec properly

Jan Zeleny (1):

-   Handle group renaming correctly

Stephen Gallagher (5):

-   Bumping version to 1.6.3
-   RESPONDER: Fix segfault in sss\_packet\_send()
-   SYSDB: add index for nameAlias
-   Fix bad backport of group rename patch
-   Update translation files for release

