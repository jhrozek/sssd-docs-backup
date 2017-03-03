Highlights {#Highlights}
----------

-   Fixes a bug in the failover code that prevented the SSSD from
    detecting when it went back online
-   Fixes a bug causing long (sometimes multiple-minute) waits for NSS
    requests
-   Several segfault bugfixes

Detailed Changelog {#DetailedChangelog}
------------------

David O'Brien (1):

-   Copy-edit, mainly fixing typos and English

Martin Nagy (4):

-   Re-create c-ares channels if /etc/resolv.conf is modified
-   Make periodic checks for DNS timeouts
-   Don't recursively call ares\_process\_fd() from fd\_event()
-   Make sure callbacks never retry when ares channel is destroyed

Simo Sorce (1):

-   Fix
    [\#382](https://fedorahosted.org/sssd/ticket/382 "defect: sssd_be segfault (closed: fixed)"){.closed
    .ticket}, a segfault bug in the memberof plugin.

Stephen Gallagher (4):

-   Update SV translation
-   Remove local and kerberos providers from the access\_provider list
-   Explicitly set async DNS timeout
-   Update version to 1.0.2

