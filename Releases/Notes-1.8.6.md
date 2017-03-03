<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Tickets Fixed](#TicketsFixed)
    3.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   A security bug assigned CVE-2013-0219 was fixed - TOCTOU race
    conditions when creating or removing home directories for users in
    local domain
-   A security bug assigned CVE-2013-0220 was fixed - out-of-bounds
    reads in autofs and ssh responder
-   Handle servers that return an empty string as the value of
    namingContext, in particular Novell eDirectory
-   The netgroup midpoint cache refresh works as documented in the
    manual page
-   The sssd\_pam responder processes pending requests after reconnect

Tickets Fixed {#TicketsFixed}
-------------

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1542](https://fedorahosted.org/sssd/ticket/1542){.ext-link}
    User authentication using LDAP doesn't work
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1581](https://fedorahosted.org/sssd/ticket/1581){.ext-link}
    sssd\_be crashes while looking up users
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1717](https://fedorahosted.org/sssd/ticket/1717){.ext-link}
    Limit requests coalescing in time
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1683](https://fedorahosted.org/sssd/ticket/1683){.ext-link}
    arithmetic bug in the SSSD causes netgroup midpoint refresh to be
    always set to 10 seconds
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1655](https://fedorahosted.org/sssd/ticket/1655){.ext-link}
    Login fails - sssd\_be module polling fd indefinitely and gets
    killed
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1781](https://fedorahosted.org/sssd/ticket/1781){.ext-link}
    sssd: Out-of-bounds read flaws in autofs and ssh services responders
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1528](https://fedorahosted.org/sssd/ticket/1528){.ext-link}
    SSSD\_NSS failure to gracefully restart after sbus failure
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1783](https://fedorahosted.org/sssd/ticket/1783){.ext-link}
    Group lookup fails and takes \~60s to return to shell if member dn
    is incorrect
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1782](https://fedorahosted.org/sssd/ticket/1782){.ext-link}
    TOCTOU race conditions by copying and removing directory trees

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (9):

-   Updating the version for the 1.8.6 release
-   Initialize Kerberos ticket renewal in the IPA provider
-   LDAP: Check validity of naming\_context
-   Free the internal DP request
-   Do not always return PAM\_SYSTEM\_ERR when offline krb5
    authentication fails
-   NSS: Fix netgroup midpoint cache refresh
-   TOOLS: Use openat/unlinkat when removing the homedir
-   TOOLS: Compile on old platforms such as RHEL5
-   Include the auth\_utils.h header in the distribution

Jan Cholasta (1):

-   Check that strings do not go beyond the end of the packet body in
    autofs and SSH requests.

Ondrej Kos (2):

-   Restart services with a delay in case they are restarted too often
-   TOOLS: Use file descriptor to avoid races when creating a home
    directory

Pavel Březina (1):

-   nested groups: fix group lookup hangs if member dn is incorrect

Simo Sorce (2):

-   responder\_dp: Add timeout to side requets
-   sssd\_pam: Cleanup requests cache on sbus reconect

Stephen Gallagher (1):

-   LDAP: Handle empty namingContexts values safely

Timo Aaltonen (1):

-   link sss\_ssh\_authorizedkeys and sss\_ssh\_knownhostsproxy with
    -lpthread

