Highlights {#Highlights}
----------

-   This pre-release does not bring substantial changes visible to the
    end-user. It is intended to be part of the development of FreeIPA
    3.3 and its focus of supporting legacy (non-SSSD) clients in a setup
    where IPA server established a trust relationship with an Active
    Directory clients.
-   Includes several fixes related to setup where the SSSD is running on
    IPA client in a special "server mode".
-   The default DNS timeouts have been tweaked in order to allow the
    c-ares resolver to cycle through all available name servers
-   The pysss module now contains a new method `getgroupslist` that
    provides a Python interface to the POSIX `getgroupslist(3)` call
-   The sss\_debuglevel tool is now able to change debug level of all
    responders, including PAC or autofs

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1965](/sssd/ticket/1965 "man: document that the default access provider in AD provider is "permit""){.closed}
:   man: document that the default access provider in AD provider is
    "permit"

[\#1988](/sssd/ticket/1988 "[RFE] sss_cache has no option to clear all cached entries of all types"){.closed}
:   \[RFE\] sss\_cache has no option to clear all cached entries of all
    types

[\#1997](/sssd/ticket/1997 "When resolving a SID, search for groups first, then users"){.closed}
:   When resolving a SID, search for groups first, then users

[\#1998](/sssd/ticket/1998 "sssd-ad man page states that ad_server can be an IP address even though ..."){.closed}
:   sssd-ad man page states that ad\_server can be an IP address even
    though SSSD doesn't support that

[\#2005](/sssd/ticket/2005 "SSSD filter out ldap user/group if uid/gid is zero"){.closed}
:   SSSD filter out ldap user/group if uid/gid is zero

[\#2009](/sssd/ticket/2009 "Disallow or warn if full_name_format is set to a non-default value when ..."){.closed}
:   Disallow or warn if full\_name\_format is set to a non-default value
    when IPA server mode is on

[\#2023](/sssd/ticket/2023 "AD provider in server mode follows referrals"){.closed}
:   AD provider in server mode follows referrals

[\#2025](/sssd/ticket/2025 "pysss module linking is broken"){.closed}
:   pysss module linking is broken

</div>

Documentation Changes {#DocumentationChanges}
---------------------

-   The `dns_resolver_timeout` option default value was changed from 5
    to 6 seconds. At the same time, the timeout that controls how long
    the internal resolver communicates with a single DNS server was
    changed to 2 seconds. This change would allow the resolver to cycle
    through up to 3 nameservers until the `dns_resolver_timeout` fires.
-   the `sss_cache` utility gained a new option `-E`. This option is a
    shortcut to tell `sss_cache` to invalidate all entries in the cache.
    Please note that invalidating sudo rules is still not implemented as
    it requires cooperation with the back end as well.

Detailed Changelog {#DetailedChangelog}
------------------

This changelog does not include commits already released in 1.10.1
release. To see all changes since 1.11 beta2, run
`git shortlog sssd-1_11_0_beta1..sssd-1_11_0_beta2` from a directory
that contains the SSSD git checkout.

Alexander Bokovoy (3):

-   build: fix dependencies for pysss module
-   pysss: add pysss.getgrouplist(username)
-   pysss: prevent crashing when group is unresolvable

Jakub Hrozek (13):

-   Bumping the version for the 1.11 beta2 release
-   LDAP: When resolving a SID, search for groups first, then users
-   MAN: clarify the default access provider for AD
-   MAN: IP addresss does not work when used for ad\_server
-   MAN: Clarify the min\_id/max\_id limits further
-   Remove unused be\_ctx-&gt;sigchld\_ctx
-   IPA: warn if full\_name\_format is customized in server mode
-   AD: Set the bool value same as default value in opts
-   Fix the default FQDN format
-   SUDO: realloc with sizeof(uint32\_t) when adding uint32\_t
-   KRB5: Do not send PAC in server mode
-   LDAP: Use domain-specific name where appropriate
-   Updating translations for the 1.11 beta2 release

Lukas Slebodnik (11):

-   BUILD: Use pkg-config to detect cmocka
-   Use conditional build for retrieving ccache.
-   Remove unused function parameter
-   Fix clang format string warning.
-   Use functionm ldb\_dn\_get\_linearized to format struct ldb\_dn
-   Add mising argument required by format string
-   Remove unused memory context from function unpack\_authtok
-   Fix warnings: uninitialized variable
-   Fix autotols warnings: macro xyz not found in library
-   Fix possible dereference of a NULL pointer.
-   Every time release allocated memory in function
    py\_sss\_getgrouplist

Michal Zidek (5):

-   sss\_cache: Add option to invalidate all entries
-   Missing space in debug message
-   Remove unused constant.
-   Set default DNS resolution timeout to 6 seconds.
-   Lower timeout to contact DNS server

Ondrej Kos (1):

-   TOOLS: Update all services with sss\_debuglevel

Pavel Březina (1):

-   remove unused variable

