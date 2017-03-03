Highlights {#Highlights}
----------

-   Fixed the IPA provider (which was segfaulting at start)
-   Fixed a bug in the SSSDConfig API causing some options to revert to
    their defaults
    -   This impacted the Authconfig UI
-   Ensure that SASL binds to LDAP auto-retry when interrupted by a
    signal

Detailed Changelog {#DetailedChangelog}
------------------

Eugene Indenbom (1):

-   Add krb5\_kpasswd to IPA provider

Jakub Hrozek (3):

-   Regression test against RHBZ [\#576856]{.missing .ticket}
-   Fixes for path\_utils
-   Unit tests for path\_utils

Piotr Drąg (1):

-   Update PL translation for 1.1.1

Stephen Gallagher (6):

-   Fix path\_utils\_ut segfault
-   Allow arbitrary-length PAM messages
-   Add regression test for
    [[​]{.icon}https://fedorahosted.org/sssd/ticket/441](https://fedorahosted.org/sssd/ticket/441){.ext-link}
-   Do not revert options to defaults in SSSDConfig.get\_domain()
-   Update translation files for 1.1.1 release
-   Update version to 1.1.1

Sumit Bose (3):

-   Fix kinit after password change
-   Set LDAP\_OPT\_RESTART for ldap\_sasl\_interactive\_bind\_s()
-   Fix LDAP search paths for IPA HBAC

