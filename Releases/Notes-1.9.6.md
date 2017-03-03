Highlights {#Highlights}
----------

-   This release focused primarily on bug fixing and stabilization. Only
    minor features were added
-   A new ignore\_group\_members option was added. This option can be
    used to suppress downloading group members on group lookups, making
    the group lookups much faster for environments that do not need to
    know the group members.
-   A new option ldap\_rfc2307\_fallback\_to\_local\_users was added. If
    this option is set to true, SSSD is be able to resolve local group
    members of LDAP groups.
-   A new option ldap\_disable\_range\_retrieval was added. Switching
    this option to True skips large Active Directory groups that might
    otherwise take a long time to download and process.
-   A new option refresh\_expired\_interval was added. This option
    allows to configure a background task that would automatically
    refresh entries that are nearing their expiration time. In this
    release, only refreshing netgroups is implemented.
-   Multiple crasher bugs in the fast in-memory cache were fixed
-   Several commits improved portability of SSSD's build system,
    allowing for easier builds on non-Linux platforms

Tickets Fixed {#TicketsFixed}
-------------

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1893](https://fedorahosted.org/sssd/ticket/1893){.ext-link} -
    Enabling enumeration causes sssd\_be process to utilize 100% of the
    CPU
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1890](https://fedorahosted.org/sssd/ticket/1890){.ext-link} -
    SSSD doesn't display warning for last grace login.
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1733](https://fedorahosted.org/sssd/ticket/1733){.ext-link} -
    \[RFE\] support autoconfiguring SUDO with ipa provider and compat
    tree
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1912](https://fedorahosted.org/sssd/ticket/1912){.ext-link} -
    SUDO is not working for users from trusted AD domain
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1823](https://fedorahosted.org/sssd/ticket/1823){.ext-link} -
    getgrnam / getgrgid for large user groups is too slow due to range
    retrieval functionality
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1376](https://fedorahosted.org/sssd/ticket/1376){.ext-link} -
    \[RFE\] Add support for suppressing group members
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1886](https://fedorahosted.org/sssd/ticket/1886){.ext-link} -
    If previous SRV query failed, the next try might not be retried in
    some cases
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1947](https://fedorahosted.org/sssd/ticket/1947){.ext-link} -
    \[abrt\] sssd-1.10.0-4.fc19.beta1: get\_server\_status: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1806](https://fedorahosted.org/sssd/ticket/1806){.ext-link} -
    sssd\_be goes to 99% CPU and causes significant login delays when
    client is under load
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1693](https://fedorahosted.org/sssd/ticket/1693){.ext-link} -
    sudoHost mismatch response is incorrect sometimes
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1933](https://fedorahosted.org/sssd/ticket/1933){.ext-link} -
    sssd fails to resolve hosts/services once the network is up
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1846](https://fedorahosted.org/sssd/ticket/1846){.ext-link} -
    cyclic group memberships may not work depending on order of
    operations
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2031](https://fedorahosted.org/sssd/ticket/2031){.ext-link} -
    sssd fails instead of skipping when a sudo ldap filter returns
    entries with multiple CNs
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1932](https://fedorahosted.org/sssd/ticket/1932){.ext-link} -
    sssd\_be crashing with nested ldap groups contain a dangling member
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1759](https://fedorahosted.org/sssd/ticket/1759){.ext-link} -
    sss\_cache -N/-n should invalidate the hash table in sssd\_nss
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2005](https://fedorahosted.org/sssd/ticket/2005){.ext-link} -
    SSSD filter out ldap user/group if uid/gid is zero
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1980](https://fedorahosted.org/sssd/ticket/1980){.ext-link} -
    SSSD service randomly dies
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1986](https://fedorahosted.org/sssd/ticket/1986){.ext-link} -
    SYSV init script should use @sbindir@
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1959](https://fedorahosted.org/sssd/ticket/1959){.ext-link} -
    Enhance sssd init script so that it would source a configuration
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1966](https://fedorahosted.org/sssd/ticket/1966){.ext-link} -
    SSSD failover doesn't work if the first DNS server in resolv.conf is
    unavailable
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1899](https://fedorahosted.org/sssd/ticket/1899){.ext-link} -
    resolv-tests failing with memory leak
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2018](https://fedorahosted.org/sssd/ticket/2018){.ext-link} -
    sssd\_nss terminated with segmentation fault
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1891](https://fedorahosted.org/sssd/ticket/1891){.ext-link} -
    unite periodic refresh API
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1713](https://fedorahosted.org/sssd/ticket/1713){.ext-link} -
    \[RFE\] Add a task to the SSSD to periodically refresh cached
    entries
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2029](https://fedorahosted.org/sssd/ticket/2029){.ext-link} -
    passwd returns "Authentication token manipulation error" when
    entering wrong current password
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1827](https://fedorahosted.org/sssd/ticket/1827){.ext-link} -
    Cannot change expired password of an AD user
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1825](https://fedorahosted.org/sssd/ticket/1825){.ext-link} -
    Invalid assignment to enum
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2059](https://fedorahosted.org/sssd/ticket/2059){.ext-link} -
    sss\_packet\_grow: wrong use of module to pad data
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2049](https://fedorahosted.org/sssd/ticket/2049){.ext-link} -
    sssd\_nss core dumps under load
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2057](https://fedorahosted.org/sssd/ticket/2057){.ext-link} -
    Data provider endianess bug
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1992](https://fedorahosted.org/sssd/ticket/1992){.ext-link} -
    AD dyndns update crashed after attempting to update a standalone DNS
    server
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1892](https://fedorahosted.org/sssd/ticket/1892){.ext-link} -
    In IPA AD trust setup, the sssd logs throws
    'sysdb\_search\_user\_by\_name failed' error when AD user tries to
    login via ipa client.
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2126](https://fedorahosted.org/sssd/ticket/2126){.ext-link} -
    sssd\_be segfault when authenticating against active directory

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (10):

-   Bump the version for the 1.9.6 release
-   Only try to relink ghost users if we're not enumerating
-   Display the last grace warning, too
-   IPA: Do not download or store the member attribute of host groups
-   LDAP: Fix crash when processing nested groups
-   MAN: Clarify the min\_id/max\_id limits further
-   Set default DNS resolution timeout to 6 seconds.
-   DP: Use the correct type for DBus boolean
-   Make IPA SELinux provider aware of subdomain users
-   Updating Transifex URL
-   Updating translations for the 1.9.6 release

Lukas Slebodnik (31):

-   SUDO: IPA provider
-   Removing unused functions.
-   Adding option to disable retrieving large AD groups.
-   Every time use permissive control in function memberof\_mod.
-   NSS: allow removing entries from netgroup hash table
-   NSS: Clear cached netgroups if a request comes in from the
    sss\_cache
-   Do not call sss\_cmd\_done in function check\_cache.
-   Handle too many results from getnetgr.
-   Removing unused parameter type from
    sudosrv\_get\_sudorules\_query\_cache()
-   mmap\_cache: Skip records which doesn't have same hash
-   mmap\_cache: Use stricter check for hash keys.
-   UTIL: Create new wraper header file sss\_endian.h
-   CLIENT: Fix non gnu sss\_strnlen implementation
-   MONITOR: Move function declaration out of conditional build
-   UTIL: Explicitly include header file sys/socket.h
-   MEMBEROF: Remove temporary workaround
-   IPA\_HBAC: Explicitelly include header file time.h
-   CONFIGURE: Get rid of bashism
-   Include sys/types.h for types id\_t and uid\_t
-   UTIL: Use standard maximum value of type size\_t
-   mmap\_cache: Do not remove record from chain twice
-   AUTOTOOLS: Add -LLIBDIR to PYTHON\_LIBS
-   AUTOTOOLS: Add missing AC\_MSG\_RESULT
-   AUTOMAKE: Use portable way to link with dlopen
-   AUTOMAKE: Use portable way to link with gettext
-   AUTOTOOLS: Add directories for searching ldap headers and libs
-   AUTOTOOLS: Refactor unicode library detection
-   AUTOTOOLS: add check for type intptr\_t
-   AUTOTOOLS: Use pkg-config to detect libraries.
-   AUTOTOOLS: More robust detection of inotify.
-   AUTOTOOLS: Fix warnings: macro xyz not found in library

Michal Zidek (13):

-   Always set port status to neutral when resetting service.
-   Lower timeout to contact DNS server
-   resolv-tests failing with memory leak
-   mmap\_cache: Check if slot and name\_ptr are not invalid.
-   ldap, krb5: More descriptive msg on chpass failure.
-   mmap\_cache: Check data-&gt;name value in client code
-   mmap\_cache: Remove triple checks in client code.
-   mmap\_cache: Off by one error.
-   mmap\_cache: Use better checks for corrupted mc in responder
-   mmap\_cache: Store corrupted mmap cache before reset
-   Rename \_SSS\_MC\_SPECIAL
-   man sssd: Add note about SSS\_NSS\_USE\_MEMCACHE
-   Check slot validity before MC\_SLOT\_TO\_PTR.

Paul B. Henson (1):

-   Add ignore\_group\_members option.

Pavel Březina (16):

-   sudo responder: use fully qualified name for subdomain users
-   failover: set state-&gt;out when meta server remains in
    SRV\_RESOLVE\_ERROR
-   collapse\_srv\_lookup may free the server, make it clear from the
    API
-   failover: if expanded server is marked as neutral, invoke srv
    collapse
-   sudo responder: use different callback for oob refresh
-   sudo: skip rule on error instead of failing completely
-   sudo: print better debug message when a rule has multiple cn values
-   init script: source /etc/sysconfig/sssd
-   back end: periodic task API
-   back end: periodical refresh of expired records API
-   back end: add refresh expired records periodic task
-   providers: refresh expired netgroups
-   print hint about password complexity when new password is rejected
-   sss\_packet\_grow: correctly pad packet length to 512B
-   SIGCHLD handler: do not call callback when pvt data was freed
-   is\_dn(): free dn

Simo Sorce (1):

-   Add a commit template

Stephen Gallagher (1):

-   Configure SYSV init scripts properly

Sumit Bose (2):

-   sdap\_get\_generic\_ext\_send: check if we a re still connected
-   be\_spy\_create: free be\_req and not the long living data

