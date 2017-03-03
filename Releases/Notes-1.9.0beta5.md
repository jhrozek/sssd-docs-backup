<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Tickets Fixed](#TicketsFixed)
    3.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   Many fixes for the support for setting default SELinux user context
    from FreeIPA, most notably fixed the specificity evaluation
-   Fixed an incorrect default in the krb5\_canonicalize option of the
    AD provider which was preventing password change operation
-   The shadowLastChange attribute value is now correctly updated with
    the number of days since the Epoch, not seconds

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1360](/sssd/ticket/1360 "format of file for pam_selinux is incorrect"){.closed}
:   format of file for pam\_selinux is incorrect

[\#1379](/sssd/ticket/1379 "Possible use of uninitialized values"){.closed}
:   Possible use of uninitialized values

[\#1395](/sssd/ticket/1395 "SELinux rule matching ignores specificity requirement"){.closed}
:   SELinux rule matching ignores specificity requirement

[\#1417](/sssd/ticket/1417 "Several unowned directories"){.closed}
:   Several unowned directories

[\#1419](/sssd/ticket/1419 "sssd incorrectly sets shadowLastChange in seconds not days"){.closed}
:   sssd incorrectly sets shadowLastChange in seconds not days

[\#1421](/sssd/ticket/1421 "selinux rules are never deleted from sysdb"){.closed}
:   selinux rules are never deleted from sysdb

[\#1422](/sssd/ticket/1422 "When ldap_sasl_minssf is assigned large values, appropriate error message ..."){.closed}
:   When ldap\_sasl\_minssf is assigned large values, appropriate error
    message should be logged sssd\_DOMAIN log

[\#1431](/sssd/ticket/1431 "Set "krb5_canonicalize = False" for password change to work"){.closed}
:   Set "krb5\_canonicalize = False" for password change to work

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (9):

-   Bumping version to 1.9.0 beta 5
-   Add newline to DEBUG messages
-   RPM: Own several directories
-   Add missing "%" to specfile
-   IPA: Download defaults even if there are no SELinux mappings
-   SYSDB: Delete SELinux mappings
-   IPA: Return and save all SELinux rules in the provider
-   PAM: Fix off-by-one-error in the SELinux session code
-   Update translations for 1.9.0 beta 5 release

Jan Vcelak (1):

-   LDAP: Properly cast type for MINSSF value

Jan Zeleny (3):

-   Fixed wrong number in shadowLastChange
-   Add function sysdb\_attrs\_copy\_values()
-   Modify priority evaluation in SELinux user maps

Michal Zidek (2):

-   Fixed: Unchecked return value from dp\_opt\_set\_int.
-   Fixed: Uninitialized value in krb5\_child-test if ccname was
    specified.

Nick Guay (1):

-   Fix uninitialized values

Pavel Březina (2):

-   resolv\_gethostbyname\_send: strdup hostname to work properly when
    hostname is allocated on stack
-   sudo test client: avoid SIGSEGV when run without arguments

Stephen Gallagher (2):

-   AD: Add missing DP option terminator
-   AD: Fix defaults for krb5\_canonicalize

Yuri Chornoivan (1):

-   Fix typo: exhasution-&gt;exhaustion.

