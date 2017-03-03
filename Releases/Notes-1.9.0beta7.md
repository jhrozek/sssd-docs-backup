Highlights {#Highlights}
----------

-   This is a bugfix release. No new features have been added. The most
    important bugs fixed include:
-   Fixed security bug CVE-2012-3462 - HBAC rules were ignored when the
    SELinux login context support was enabled
-   Mutexes in the nss\_sss module are now released correctly if one
    thread in a multithreaded application is cancelled while the mutex
    is locked
-   The fail over code works correctly when the IPA provider is not able
    to establish a GSSAPI-encrypted connection to an IPA server
-   The SSSD correctly accepts -1 as a valid value of the shadow
    attributes
-   When the SSSD is unable to resolve a host name, it tries the next
    configured server now instead of going offline
-   The default SELinux login context for IPA users was changed to
    unconfined\_t when there are no rules on the server
-   A file descriptor leak in cases the SSSD was unable to establish SSL
    connection to an LDAP server was fixed

Packaging Changes {#PackagingChanges}
-----------------

-   A new Python wrapper around the murmur hash library has been
    introduced. It is only useful to the FreeIPA server at the moment.

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#734](/sssd/ticket/734 "on reconnect we need to detect that a ipa/ds server has been reinitialized"){.closed}
:   on reconnect we need to detect that a ipa/ds server has been
    reinitialized

[\#1156](/sssd/ticket/1156 "Do not use "goto" to jump backwards in the proxy code"){.closed}
:   Do not use "goto" to jump backwards in the proxy code

[\#1194](/sssd/ticket/1194 "when nesting limit is reached, the LDAP provider tries to establish link ..."){.closed}
:   when nesting limit is reached, the LDAP provider tries to establish
    link to members outside the nesting limit

[\#1365](/sssd/ticket/1365 "ipv6 address with square brackets doesn't work for krb5_server"){.closed}
:   ipv6 address with square brackets doesn't work for krb5\_server

[\#1388](/sssd/ticket/1388 "domain.remove_provider() does not work"){.closed}
:   domain.remove\_provider() does not work

[\#1390](/sssd/ticket/1390 "Add support for nested automount maps"){.closed}
:   Add support for nested automount maps

[\#1393](/sssd/ticket/1393 "shadow attributes should accept -1"){.closed}
:   shadow attributes should accept -1

[\#1396](/sssd/ticket/1396 "Kerberos validation algorithm is insufficient for cross-realm trusts"){.closed}
:   Kerberos validation algorithm is insufficient for cross-realm trusts

[\#1415](/sssd/ticket/1415 "Group lookups no longer work when fastcache cannot be initialized"){.closed}
:   Group lookups no longer work when fastcache cannot be initialized

[\#1416](/sssd/ticket/1416 "sssd_be crashes on using inappropriate keytab file"){.closed}
:   sssd\_be crashes on using inappropriate keytab file

[\#1430](/sssd/ticket/1430 "Password change prompt doesn't appear when "User must change password on ..."){.closed}
:   Password change prompt doesn't appear when "User must change
    password on next logon" is set for a AD user.

[\#1436](/sssd/ticket/1436 "LOCAL domain lookups don't work"){.closed}
:   LOCAL domain lookups don't work

[\#1446](/sssd/ticket/1446 "sssd does not try another server when unable to resolve hostname"){.closed}
:   sssd does not try another server when unable to resolve hostname

[\#1447](/sssd/ticket/1447 "Fail over does not work correctly when IPA server is establishing a ..."){.closed}
:   Fail over does not work correctly when IPA server is establishing a
    GSSAPI-encrypted LDAP connection

[\#1453](/sssd/ticket/1453 "proxy provider: value stored to status is never read in get_pw_name"){.closed}
:   proxy provider: value stored to status is never read in
    get\_pw\_name

[\#1455](/sssd/ticket/1455 "SELinux code must fall back to default only if there are no rules on the ..."){.closed}
:   SELinux code must fall back to default only if there are no rules on
    the server

[\#1456](/sssd/ticket/1456 "Attempt to close the same file stream twice"){.closed}
:   Attempt to close the same file stream twice

[\#1457](/sssd/ticket/1457 "Insecure temporary file in IPA subdomain provider"){.closed}
:   Insecure temporary file in IPA subdomain provider

[\#1459](/sssd/ticket/1459 "SRV servers are always marked as back up"){.closed}
:   SRV servers are always marked as back up

[\#1460](/sssd/ticket/1460 "SSSD thread issue can cause the application to not get any identity ..."){.closed}
:   SSSD thread issue can cause the application to not get any identity
    information

[\#1470](/sssd/ticket/1470 "FreeIPA HBAC rules ignored when FreeIPA and SSSD are configured to set ..."){.closed}
:   FreeIPA HBAC rules ignored when FreeIPA and SSSD are configured to
    set SELinux user context

[\#1472](/sssd/ticket/1472 "Duplicate detection in fail over does not work"){.closed}
:   Duplicate detection in fail over does not work

[\#1478](/sssd/ticket/1478 "ldap_autofs_* options missing from ..."){.closed}
:   ldap\_autofs\_\* options missing from
    /usr/share/sssd/sssd.api.d/sssd-ldap.conf

[\#1480](/sssd/ticket/1480 "1.9.0b6 does not build with SELinux disabled"){.closed}
:   1.9.0b6 does not build with SELinux disabled

[\#1488](/sssd/ticket/1488 "Segfault in IPA subdomain provider"){.closed}
:   Segfault in IPA subdomain provider

[\#1490](/sssd/ticket/1490 "SSSD does not close TCP connections when SSL fails"){.closed}
:   SSSD does not close TCP connections when SSL fails

[\#1491](/sssd/ticket/1491 "Consolidate functions that make a realm upper-case"){.closed}
:   Consolidate functions that make a realm upper-case

[\#1492](/sssd/ticket/1492 "There is no /etc/selinux/targeted/logins on RHEL5"){.closed}
:   There is no /etc/selinux/targeted/logins on RHEL5

[\#1500](/sssd/ticket/1500 "SSSD's default ccache location needs to be updated (again), and the man ..."){.closed}
:   SSSD's default ccache location needs to be updated (again), and the
    man pages should reflect it

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Ariel Barria (1):

-   SIGUSR2 should force SSSD to reread resolv.conf as well

Jakub Hrozek (32):

-   Bumping version for the 1.9.0 release
-   Don't call fo\_set\_{server,port}\_status for SRV servers
-   Fix the version number
-   SYSDB: Check the return value
-   SYSDB: Use ldb\_msg\_add\_string for simple string additions
-   Failover: Return last tried server if it's still being tried
-   Subdomains: Send the DP reply in the correct format
-   Always mark SRV servers as primary
-   Allocate on top of a talloc context, not NULL
-   Abort PAM access phase if HBAC does not return PAM\_SUCCESS
-   Change default for ldap\_idmap\_range\_min to 200000
-   Don't use server after SRV data collapsed
-   Document entry\_cache\_autofs\_timeout
-   Add autofs-related options to configAPI
-   sss\_client: Group lookups should work even when fastcache cannot be
    initialized
-   FO: Don't retry the same server if it's not working
-   FO: Return EAGAIN if there are more servers to try
-   KRB5: Only return PAM error for unreachable kpasswd when performing
    chpass
-   Build SELinux code in responder conditionally
-   Do not try to remove the temp login file if already renamed
-   Only create the SELinux login file if there are mappings on the
    server
-   Fix compilation error in Python murmurhash bindings
-   Process all groups from a single nesting level
-   Use PTHREAD\_MUTEX\_ROBUST to avoid deadlock in the client
-   RPM: Switch the default ccache location
-   RPM: Always include the patch file
-   Check if the SELinux login directory exists
-   SYSDB: Commit transaction in sysdb\_store\_user
-   SYSDB: Abort unit test if sysdb\_getpwnam fails
-   Retry the next server if bind during LDAP auth times out
-   Don't terminate the same connection twice
-   Update translations for 1.9.0 beta 7 release

Jan Cholasta (3):

-   SSH: Return error code in SSH utility functions
-   SSH: Simplify public key formatting function
-   SSH: Add support for OpenSSH-style public keys

Michal Zidek (10):

-   Return value of fread in src/tools/sss\_debuglevel.c no longer
    ignored.
-   Change default value of ldap\_sasl\_string to host/hostname@REALM in
    man page.
-   SRV resolution for backup servers should not be permitted.
-   When ldap\_group\_nesting\_level was reached, the LDAP provider
    tried to link group members with groups outside nesting limit.
-   Duplicate detection in fail over did not work.
-   Typo in debug message (SSSd -&gt; SSSD).
-   Unify usage of sysdb transactions
-   Fix: IPv6 address with square brackets doesn't work.
-   Adding -std=gnu99 flag.
-   Unify usage of sysdb transactions (part 2).

Nick Guay (1):

-   remove duplicate sss\_obfuscate reference in seealso manpage section

Ondrej Kos (5):

-   Removed unused variable assignment
-   Replaced "id\_max" & "id\_min"
-   Backward GOTOs rewritten into do-while loops.
-   AD context was set to null due to type mismatch
-   Consolidation of functions that make realm upper-case

Pavel Březina (12):

-   tests: build sysdb ssh tests conditionally
-   shadow attributes can contain -1
-   Add end of line to debug message
-   monitor: set debug level when unable to load configuration
-   Remove redefinition of some SYSDB\_\* macros
-   Rename SYSDB\_SUDO\_CACHE\_AT\_OC to SYSDB\_SUDO\_CACHE\_OC
-   Remove SYSDB\_SUDO\_CACHE\_OC from attribute lists
-   Fix LOCAL domain lookups
-   Close LDAP connection when unable to install TLS
-   Unbreak build on RHEL5: replace ldap\_destroy() with
    ldap\_unbind\_ext()
-   Remove compilation warning: ret may be uninitialized
-   Clean up cache on server reinitialization

Stephen Gallagher (6):

-   SSSDConfig: Fix nonfunctional SSSDDomain.remove\_provider()
-   IPA: Do not attempt to close the same file twice
-   IPA: Securely set umask for mkstemp in subdomain provider
-   MAN: Fix minor typo in ldap\_search\_base section
-   MAN: Improve description of ldap\_\*\_search\_base options
-   SYSDB: Make sysdb\_attrs\_get\_el\_int() public

Sumit Bose (5):

-   Add python bindings for murmurhash3
-   accept\_fd\_handler: add missing return
-   Fix fallback in validate\_tgt()
-   Use new debug levels in validate\_tgt()
-   Check flat names when searching for sub-domains as well

Yuri Chornoivan (1):

-   Fix various typos in documentation.

