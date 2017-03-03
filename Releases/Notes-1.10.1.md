Highlights {#Highlights}
----------

-   Another case where the dircache might have been created with the UID
    of root was fixed
-   Fixed a crash in case the dynamic DNS update timed out
-   Several packaging bugs that were introduced as a result of splitting
    out the providers into separate subpackages was fixed
-   The SRV resolution status is now correctly reset after receiving
    notification about changed network conditions

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1778](/sssd/ticket/1778 "Do not copy special files when creating a home directory from a skeldir"){.closed}
:   Do not copy special files when creating a home directory from a
    skeldir

[\#1814](/sssd/ticket/1814 "Empty Kerberos passwords handled incorrectly"){.closed}
:   Empty Kerberos passwords handled incorrectly

[\#1827](/sssd/ticket/1827 "Cannot change expired password of an AD user"){.closed}
:   Cannot change expired password of an AD user

[\#1846](/sssd/ticket/1846 "cyclic group memberships may not work depending on order of operations"){.closed}
:   cyclic group memberships may not work depending on order of
    operations

[\#1933](/sssd/ticket/1933 "sssd fails to resolve hosts/services once the network is up"){.closed}
:   sssd fails to resolve hosts/services once the network is up

[\#1935](/sssd/ticket/1935 "Several translated man pages are malformed"){.closed}
:   Several translated man pages are malformed

[\#1984](/sssd/ticket/1984 "sssd-common requires libndr due to pac responder dependency"){.closed}
:   sssd-common requires libndr due to pac responder dependency

[\#1992](/sssd/ticket/1992 "AD dyndns update crashed after attempting to update a standalone DNS ..."){.closed}
:   AD dyndns update crashed after attempting to update a standalone DNS
    server

[\#1999](/sssd/ticket/1999 "shadowLastChange updates even when PAM reports password change failed"){.closed}
:   shadowLastChange updates even when PAM reports password change
    failed

[\#2002](/sssd/ticket/2002 "cc_residual_is_used might not work correctly with dircache"){.closed}
:   cc\_residual\_is\_used might not work correctly with dircache

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (5):

-   Updating the version for the 1.10.1 release
-   RPM: Move sssd\_pac to the krb5-common subpackage
-   DB: sysdb\_search\_user\_by\_name: search by both name and alias
-   RPM: Require libsss\_idmap from sssd-common
-   Updating translations for the 1.10.1 release

Jim Collins (1):

-   ldap: only update shadowLastChange when password change is
    successful

Lukas Slebodnik (2):

-   Return right directory name for dircache
-   Every time use permissive control in function memberof\_mod.

Michal Zidek (1):

-   Always set port status to neutral when resetting service.

Ondrej Kos (5):

-   Do not copy special files when creating homedir
-   KRB5\_CHILD: Fix handling of get\_password return code
-   Do not try to set password when authtok\_length is zero
-   KRB: Handle empty password gracefully
-   KRB: Replace multiple calls with variable

Pavel Březina (3):

-   print hint about password complexity when new password is rejected
-   dyndns timeout test: catch SIGCHLD handler events
-   SIGCHLD handler: do not call callback when pvt data where freed

Stephen Gallagher (3):

-   Move pre and post scripts to sssd-common
-   Remove sysv-&gt;systemd upgrade routines
-   Move sssd\_pac binary to the IPA and AD providers

Packaging Changes {#PackagingChanges}
-----------------

-   The sssd\_pac binary is now owned by the IPA and AD providers
-   The sysv-&gt;systemd upgrade routines were removed
-   Several packaging fixes

