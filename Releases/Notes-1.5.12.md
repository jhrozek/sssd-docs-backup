Highlights {#Highlights}
----------

-   Fixes a regression introduced in 1.5.11 with hostname resolution
-   Fixes an issue where sssd\_pam would leak file descriptors until
    resource exhaustion
-   Complete rewrite of the FreeIPA Host-Based Access Control (HBAC)
    resolver
-   New shared library for HBAC access-control
-   Fixes for password expiration handling with LDAP auth
-   New option to veto certain centrally-managed shells (Patch by John
    Hodrien)

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (18):

-   Use ares\_search instead of ares\_query for hostname resolution
-   Do not add a NULL host parsed from LDAP URI
-   Only print server address if one is available
-   Fix indexing of skipped groups
-   Set gidNumber of non-posix groups to 0 even on updates
-   Explicitly ignore groups with gidNumber=0
-   Wrong paramater to sysdb\_attrs\_add\_uint32
-   Change the default value of ldap\_tls\_cacert in IPA provider
-   Provide python bindings for the HBAC evaluator library
-   Fixes for python HBAC bindings
-   Fix python HBAC bindings for python &lt;= 2.4
-   Remove dead code from python HBAC bindings
-   Handle allocation error in python HBAC bindings
-   UTF8 HBAC test
-   HBAC rule validation Python bindings
-   Request password control unconditionally during bind
-   pyhbac: Do not convert int to bool
-   Fix returning groups when gidNumber attribute is not ordered

John Hodrien (1):

-   Add vetoed\_shells option

Simo Sorce (1):

-   sss\_client: avoid leaking file descriptors

Stephen Gallagher (19):

-   Bumping version to 1.5.12
-   Remove incorrect private variable
-   Add helper function msgs2attrs\_array
-   Add HBAC evaluator and tests
-   Add helper functions for looking up HBAC rule components
-   Remove old HBAC implementation
-   Add new HBAC lookup and evaluation routines
-   Add ipa\_hbac\_refresh option
-   Add ipa\_hbac\_treat\_deny\_as option
-   Treat NULL or empty rhost as unknown
-   libipa\_hbac: Support case-insensitive comparisons with UTF8
-   Fix memory leak in ipa\_hbac\_evaluate\_rules
-   Fix incorrect NULL check in ipa\_hbac\_common.c
-   Require matched version and release for libipa\_hbac
-   Add rule validator to libipa\_hbac
-   Allow LDAP to decide when an expiration warning is warranted
-   Update translation files for SSSD 1.5.12 release
-   Revert "Allow LDAP to decide when an expiration warning is
    warranted"
-   Updating translations for SSSD 1.5.12 release

