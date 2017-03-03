Highlights {#Highlights}
----------

-   Fixes a major cache performance issue introduced in 1.5.14
-   Fixes a potential infinite-loop with certain LDAP layouts

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (3):

-   Plug memory leaks in LDAP provider
-   RFC2307bis initgroups: fix nested groups processing
-   Steal result onto mem\_ctx in
    sdap\_initgr\_nested\_get\_direct\_parents

Stephen Gallagher (4):

-   Bumping version to sssd 1.5.15
-   RESPONDER: Fix segfault in sss\_packet\_send()
-   SYSDB: Update sysdb version to latest
-   Updating translation files for release

