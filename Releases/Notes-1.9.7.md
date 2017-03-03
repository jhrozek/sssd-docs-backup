Highlights {#Highlights}
----------

-   This release is the last supported upstream release in the 1.9.x
    series. Users of sssd-1.9 are advised to upgrade to sssd-1.11
-   A memory leak in the netgroup code of the NSS responder was fixed
-   Subdomains inherit min\_id/max\_id limits of parent domains. The
    user-visible effect of this bug was that adding system users or
    groups with shadow-utils took too long.
-   The default\_domain\_suffix is ignored in the autofs responder,
    making it possible to use default\_domain\_suffix along with autofs
    integration
-   Several fixes related to Kerberos DIR cache support were backported
    from later releases

Tickets Fixed {#TicketsFixed}
-------------

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1936](https://fedorahosted.org/sssd/ticket/1936){.ext-link} -
    GSSAPI working only on first login
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2153](https://fedorahosted.org/sssd/ticket/2153){.ext-link} -
    If both IPA and LDAP are set up with enumeration on, two enum tasks
    are running
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2170](https://fedorahosted.org/sssd/ticket/2170){.ext-link} -
    sssd\_nss grows memory footprint when netgroups are requested
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2157](https://fedorahosted.org/sssd/ticket/2157){.ext-link} -
    sssd\_be segfaults if empty grop is resolved using
    ad\_matching\_rule
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2077](https://fedorahosted.org/sssd/ticket/2077){.ext-link} -
    \[RFE\] If originalDN is not available during LDAP auth, the SSSD
    should look it up
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2051](https://fedorahosted.org/sssd/ticket/2051){.ext-link} -
    Do not fail if initgroups returns NOT\_FOUND
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2123](https://fedorahosted.org/sssd/ticket/2123){.ext-link} -
    Creating system accounts on a IdM client takes up to 10 minutes when
    AD trust is configured in the IdM.

Detailed Changelog {#DetailedChangelog}
------------------

Aron Parsons (1):

-   do not use default\_domain\_suffix with autofs

Jakub Hrozek (7):

-   Bumping the version for 1.9.7
-   Inherit ID limits of parent domains if set
-   PROXY: Handle empty GECOS
-   LDAP: Split out a request to search for a user w/o saving
-   LDAP: Search for original DN during auth if it's missing
-   LDAP: Initialize user count for AD matching rule
-   Updating translations for the 1.9.7 release

Lukas Slebodnik (6):

-   NSS: Fix memory leak in sss\_setnetgrent
-   AUTOTOOLS: krb5 1.12 is also supported krb5 libs
-   LDAP: Setup periodic task only once.
-   Fix wrong detection of krb5 ccname
-   Every time return directory for krb5 cache collection.
-   Do not switch to credentials everytime.

Simo Sorce (1):

-   proxy: Allow initgroup to return NOTFOUND

