<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Tickets Fixed](#TicketsFixed)
    3.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   Numerous manpage and translation updates
-   LDAP: Handle situations where the RootDSE isn't available
    anonymously
-   LDAP: Fix regression for users using non-standard LDAP attributes
    for user information

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1183](/sssd/ticket/1183 "sssd.conf man page does not list autofs in the list of known services"){.closed}
:   sssd.conf man page does not list autofs in the list of known
    services

[\#1219](/sssd/ticket/1219 "Warn on 'make update-po' if there are manpages not listed in po4a.cfg"){.closed}
:   Warn on 'make update-po' if there are manpages not listed in
    po4a.cfg

[\#1249](/sssd/ticket/1249 "Unable to lookup user aliases with proxy provider."){.closed}
:   Unable to lookup user aliases with proxy provider.

[\#1258](/sssd/ticket/1258 "SSSD should attempt to get the RootDSE after binding"){.closed}
:   SSSD should attempt to get the RootDSE after binding

[\#1265](/sssd/ticket/1265 "document the possible performance gains of disabling referral chasing"){.closed}
:   document the possible performance gains of disabling referral
    chasing

[\#1278](/sssd/ticket/1278 "Inadequate info in man page for "ldap_disable_paging" feature"){.closed}
:   Inadequate info in man page for "ldap\_disable\_paging" feature

[\#1290](/sssd/ticket/1290 "No info in sssd manpages for "ldap_sasl_minssf""){.closed}
:   No info in sssd manpages for "ldap\_sasl\_minssf"

[\#1295](/sssd/ticket/1295 "Fix erronous reference to the 'allow' access_provider"){.closed}
:   Fix erronous reference to the 'allow' access\_provider

[\#1300](/sssd/ticket/1300 "autofs: maximum key name must be PATH_MAX"){.closed}
:   autofs: maximum key name must be PATH\_MAX

[\#1307](/sssd/ticket/1307 "sdap_check_aliases must not error when detects the same user"){.closed}
:   sdap\_check\_aliases must not error when detects the same user

[\#1312](/sssd/ticket/1312 "group members are now lowercased in case insensitive domains"){.closed}
:   group members are now lowercased in case insensitive domains

[\#1315](/sssd/ticket/1315 "New SSSD does not fetch renewable tickets"){.closed}
:   New SSSD does not fetch renewable tickets

[\#1320](/sssd/ticket/1320 "Auth fails for user with non-default attribute names"){.closed}
:   Auth fails for user with non-default attribute names

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (14):

-   man: document that referral chasing might bring performance penalty
-   pam\_sss: improve error handling in SELinux code
-   Remove the "command" option from documentation
-   autofs: Raise the maximum key length to PATH\_MAX
-   MAN: timeout can be specified for services, too
-   MAN: document the hostid and autofs providers
-   proxy: Canonicalize user and group names
-   proxy: new option proxy\_fast\_alias
-   sdap\_check\_aliases must not error when detects the same user
-   Document sss\_tools better
-   Get the RootDSE after binding if not successfull before
-   confdb\_get\_bool needs a TALLOC\_CTX in sssd-1.8
-   Lowercase group members in case-insensitive domains
-   Read sysdb attribute name, not LDAP attribute map name

Marco Pizzoli (1):

-   Two manual pages fixes

Pavel Březina (1):

-   sudo api: check sss\_status instead of errnop in
    sss\_sudo\_send\_recv\_generic()

Stef Walter (1):

-   Fix erronous reference to the 'allow' access\_provider

Stephen Gallagher (6):

-   Bumping version to 1.8.3
-   MAN: Improve ldap\_disable\_paging documentation
-   MAN: Add ldap\_sasl\_minssf to the manpage
-   Update translation files
-   Fix typo in translation file
-   Update translations for 1.8.3 release

Yuri Chornoivan (1):

-   Fix typo: retreiving-&gt;retrieving

