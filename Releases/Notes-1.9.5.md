Highlights {#Highlights}
----------

-   This release focused mainly on fixing regressions compared to the
    1.8 series and bugfixes for features introduced in the 1.9 release
    cycle. The release also includes one security fix
-   Includes a fix for
    [[​]{.icon}CVE-2013-0287](https://lists.fedorahosted.org/pipermail/sssd-devel/2013-March/014066.html){.ext-link}:
    A simple access provider flaw prevents intended ACL use when SSSD is
    configured as an Active Directory client
-   Fixed spurious password expiration warning that was printed on login
    with the Kerberos back end
-   A new option ldap\_rfc2307\_fallback\_to\_local\_users was added. If
    this option is set to true, SSSD is be able to resolve local group
    members of LDAP groups.
-   Fixed an indexing bug that prevented the contents of autofs maps
    from being returned to the automounter deamon in case the map
    contained a large number of entries
-   Several fixes for safer handling of Kerberos credential caches for
    cases where the ccache is set to be stored in a DIR: type

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1020](/sssd/ticket/1020 "SSSD does not list local user's group membership defined in LDAP"){.closed}
:   SSSD does not list local user's group membership defined in LDAP

[\#1512](/sssd/ticket/1512 "[sssd[krb5_child[PID]]]: Credential cache directory /run/user/UID/ccdir ..."){.closed}
:   \[sssd\[krb5\_child\[PID\]\]\]: Credential cache directory
    /run/user/UID/ccdir does not exist

[\#1737](/sssd/ticket/1737 "Misleading example in the man page"){.closed}
:   Misleading example in the man page

[\#1739](/sssd/ticket/1739 "sssd is not serving large automount maps reliably"){.closed}
:   sssd is not serving large automount maps reliably

[\#1755](/sssd/ticket/1755 "Saving dereferenced groups fails if a nested group member is outside ..."){.closed}
:   Saving dereferenced groups fails if a nested group member is outside
    nesting limit

[\#1791](/sssd/ticket/1791 "Unchecked return value in files.c"){.closed}
:   Unchecked return value in files.c

[\#1795](/sssd/ticket/1795 "names of domain_realm mapping files in SSSD contain dots"){.closed}
:   names of domain\_realm mapping files in SSSD contain dots

[\#1799](/sssd/ticket/1799 "sssd_be crashes sometimes"){.closed}
:   sssd\_be crashes sometimes

[\#1808](/sssd/ticket/1808 "pwd_expiration_warning has wrong default for Kerberos"){.closed}
:   pwd\_expiration\_warning has wrong default for Kerberos

[\#1817](/sssd/ticket/1817 "sssd pam write_selinux_login_file creating the temp file for SELinux data ..."){.closed}
:   sssd pam write\_selinux\_login\_file creating the temp file for
    SELinux data failed

[\#1818](/sssd/ticket/1818 "LDAP provider doesn't save binary attributes correctly"){.closed}
:   LDAP provider doesn't save binary attributes correctly

[\#1822](/sssd/ticket/1822 "krbcc dir creation issue with MIT krb5 1.11"){.closed}
:   krbcc dir creation issue with MIT krb5 1.11

[\#1826](/sssd/ticket/1826 "sssd etas 99% CPU and runs out of file descriptors when clearing cache"){.closed}
:   sssd etas 99% CPU and runs out of file descriptors when clearing
    cache

[\#1841](/sssd/ticket/1841 "document what does access_provider=ad do"){.closed}
:   document what does access\_provider=ad do

[\#1868](/sssd/ticket/1868 "sssd fails with readonly /etc/selinux/targeted/logins"){.closed}
:   sssd fails with readonly /etc/selinux/targeted/logins

[\#1869](/sssd/ticket/1869 "pam responder segfaults if the client disconnects before the operation ..."){.closed}
:   pam responder segfaults if the client disconnects before the
    operation finishes

[\#1880](/sssd/ticket/1880 "Simple access control always denies uppercased users in case insensitive ..."){.closed}
:   Simple access control always denies uppercased users in case
    insensitive domain

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (16):

-   Bump the version to 1.9.5, reset release in RPMs to 0
-   Don't use srcdir with tests
-   Fix the krb5 password expiration warning
-   Remove enumerate=true from man sssd-ldap
-   Don't treat 0 as default for pam\_pwd\_expiration warning
-   Provide a be\_get\_account\_info\_send function
-   Add unit tests for simple access test by groups
-   Do not compile main() in DP if UNIT\_TESTING is defined
-   Resolve GIDs in the simple access provider
-   Document what does access\_provider=ad do
-   Allocate PAM DP request data on responder context
-   krb5: include backwards compatible declaration of krb5\_trace\_info
-   Fix simple access group control in case-insensitive domains
-   LDAP: do not invalidate pointer with realloc while processing ghost
    users
-   tests: Link the simple access tests with -ldl
-   Updating the translations for the 1.9.5 release

Jan Engelhardt (1):

-   sysdb: try dealing with binary-content attributes

Kamil Dudka (1):

-   sssd-1.8.0: work around a bug in cov-build from Coverity

Lukas Slebodnik (1):

-   Fix krbcc dir creation issue with MIT krb5 1.11

Michal Zidek (4):

-   Unchecked return value in files.c
-   File descriptor leak in nss responder.
-   Debug message in sss\_mc\_create\_file.
-   sssd fails with readonly SELinux login files

Pavel Březina (6):

-   krb: recreate ccache if it was deleted
-   subdomains: replace invalid characters with underscore in krb5
    mapping file name
-   sdap\_fill\_memberships: continue if a member is not foud in sysdb
-   autofs: fix invalid header 'number of entries' in packet
-   if selinux is disabled, ignore that selogin dir is missing
-   krb5-utils-tests: remove invalid condition

Simo Sorce (1):

-   ldap: Fallback option for rfc2307 schema

Stephen Gallagher (2):

-   Fix minor grammar error in log
-   NSS: Add original homedir to home directory template options

