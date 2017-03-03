<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Tickets Fixed](#TicketsFixed)
    3.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   Fix a bug causing AD servers not to fail over properly when the KDC
    on the primary server is down
-   Fix an endianness bug on big-endian systems when looking up services
-   Fix a segfault dealing with nested groups
-   Make the nowait cache updates work for netgroups
-   Fix a regression that broke domains with
    `use_fully_qualified_names = True`

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1206](/sssd/ticket/1206 "RHEL5 detection in sssd.spec.in does not work"){.closed}
:   RHEL5 detection in sssd.spec.in does not work

[\#1321](/sssd/ticket/1321 "Warning in debug log about nscd"){.closed}
:   Warning in debug log about nscd

[\#1322](/sssd/ticket/1322 "Special-case LDAP_SIZELIMIT_EXCEEDED when handling ldap return codes"){.closed}
:   Special-case LDAP\_SIZELIMIT\_EXCEEDED when handling ldap return
    codes

[\#1324](/sssd/ticket/1324 "LDAP provider needs to use all available servers for GSSAPI if the child ..."){.closed}
:   LDAP provider needs to use all available servers for GSSAPI if the
    child times out

[\#1325](/sssd/ticket/1325 "heimdal:  configure: Kerberos locator plugin cannot be build"){.closed}
:   heimdal: configure: Kerberos locator plugin cannot be build

[\#1329](/sssd/ticket/1329 "Group enumeration fails in proxy provider"){.closed}
:   Group enumeration fails in proxy provider

[\#1333](/sssd/ticket/1333 "Potential NULL dereference in proxy provider"){.closed}
:   Potential NULL dereference in proxy provider

[\#1335](/sssd/ticket/1335 "sss_groupadd no longer detects duplicate GID numbers"){.closed}
:   sss\_groupadd no longer detects duplicate GID numbers

[\#1338](/sssd/ticket/1338 "sssd does not provide maps for automounter when custom schema is being ..."){.closed}
:   sssd does not provide maps for automounter when custom schema is
    being used

[\#1340](/sssd/ticket/1340 "SSSD netgroups do not honor entry_cache_nowait_percentage"){.closed}
:   SSSD netgroups do not honor entry\_cache\_nowait\_percentage

[\#1343](/sssd/ticket/1343 "sssd_be crashed with SIGSEGV in _tevent_schedule_immediate()"){.closed}
:   sssd\_be crashed with SIGSEGV in \_tevent\_schedule\_immediate()

[\#1344](/sssd/ticket/1344 "Loading of selinux user maps broken"){.closed}
:   Loading of selinux user maps broken

[\#1348](/sssd/ticket/1348 "Service lookups by port number doesn't work on s390x/ppc64 arches"){.closed}
:   Service lookups by port number doesn't work on s390x/ppc64 arches

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Ariel Barria (2):

-   Potential NULL dereference in proxy provider
-   Warn to syslog when dereference requests fail

Jakub Hrozek (11):

-   Special-case LDAP\_SIZELIMIT\_EXCEEDED
-   Kerberos locator: Include the correct krb5.h header file
-   krb5 locator: Do not leak addrinfo
-   Try all KDCs when getting TGT for LDAP
-   Send the correct enumeration request
-   SYSDB: Handle user and group renames better
-   Use the sysdb attribute name, not LDAP attribute name
-   LDAP nested groups: Do not process callback with \_post deep in the
    nested structure
-   Use sized\_string correctly in FQDN domains
-   Send 16bit protocol numbers from the sss\_client
-   Revert the client packet length, too, after reverting the packet
    protocol

Jan Engelhardt (1):

-   build: resolve link failure

Jan Zeleny (1):

-   Fixed issue in SELinux user maps

Stef Walter (3):

-   Limit krb5\_get\_init\_creds\_keytab() to etypes in keytab
-   If canon'ing principals, write ccache with updated default principal
-   Remove erroneous failure message in find\_principal\_in\_keytab

Stephen Gallagher (7):

-   Bump version to 1.8.4
-   murmurhash: Relax inline requirement
-   RPM: Allow running 'make rpms' on RHEL 5 machines
-   NSS: Expire in-memory netgroup cache before the nowait timeout
-   KRB5: Avoid NULL-dereference with empty keytab
-   NSS: Restore original protocol for getservbyport
-   Updating translations for 1.8.4 release

