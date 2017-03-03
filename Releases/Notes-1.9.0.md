Highlights {#Highlights}
----------

### New Features {#NewFeatures}

-   Add a new AD provider to improve integration with Active Directory
    2008 R2 or later servers
    -   Support for ID-mapping when connecting to Active Directory
    -   Support for handling very large (&gt; 1500 users) groups in
        Active Directory
-   The SSSD is able to act as an IPA client in cases where the IPA
    server has established a trust setup with an Active Directory server
    -   Support for sub-domains for dealing with trust relationships
    -   Add a new PAC responder for dealing with cross-realm Kerberos
        trusts
    -   The IPA authentication provider now supports subdomains
    -   In scenarios, where the SSSD is acting as an IPA client, it is
        able to discover and save the DNS domain-Kerberos realm mappings
        between an IPA server and a trusted Active Directory server.
-   Add a new fast in-memory cache to speed up lookups of cached data on
    repeated requests
-   Many fixes for the support for setting default SELinux user context
    from FreeIPA, most notably fixed the specificity evaluation
-   Add support for the Kerberos DIR cache for storing multiple TGTs
    automatically
-   SUDO integration was completely rewritten. The new implementation
    works with multiple domains and uses an improved refresh mechanism
    to download only the necessary rules
-   The SSSD supports the concept of a Primary Server and a Back Up
    Server. If the SSSD switches to a back up server because a primary
    server is not available, it would later try to re-establish a
    connection to the primary server.
-   Add native support for autofs to the IPA provider
-   A new command-line tool sss\_seed is available. This tool is able to
    prime the internal cache with a user record and a cached password to
    support the scenario when a user needs to log in to the client
    before the network connection to the centralized identity source is
    established, such as the first log in to a new machine.
-   A new option, override\_shell was added. If this option is set, all
    users managed by SSSD will have their shell set to its value.

### Important Fixes and Enhancements {#ImportantFixesandEnhancements}

-   Major performance enhancement when storing large groups in the cache
-   Major performance enhancement when performing initgroups() against
    Active Directory
-   Terminate idle connections to the NSS and PAM responders
-   The shadowLastChange attribute value is now correctly updated with
    the number of days since the Epoch, not seconds
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
-   Potential crash when one of two parallel requests would expire the
    list of servers resolved from a SRV query
-   Fixed a crash that occured when a service was requested by both name
    and protocol

### Packaging Changes {#PackagingChanges}

-   SSSDConfig data file default locations can now be set during
    configure for easier packaging
-   Switch from libunistring to glib2 for unicode support
-   A new Python wrapper around the murmur hash library has been
    introduced. It is only useful to the FreeIPA server at the moment.
-   a new binary, called sss\_seed is available. The binary is installed
    to /usr/sbin/sss\_seed by default and includes its own manual page.
-   The SSSD uses a new directory to store the DNS domain - Kerberos
    realm mappings. The default location is
    /var/lib/sss/pubconf/krb5.include.d

Tickets fixes {#Ticketsfixes}
-------------

<div>

[\#866](/sssd/ticket/866 "Support TLS_KEY for unlocking password-protected NSS databases"){.closed}
:   Support TLS\_KEY for unlocking password-protected NSS databases

[\#881](/sssd/ticket/881 "[RFE] support the equivalent of kinit -C in sssd as an option"){.closed}
:   \[RFE\] support the equivalent of kinit -C in sssd as an option

[\#920](/sssd/ticket/920 "Bad debug message when adding services without explicit ..."){.closed}
:   Bad debug message when adding services without explicit
    dns\_discovery\_domain

[\#966](/sssd/ticket/966 "include Samba prefork code in SSSD build system"){.closed}
:   include Samba prefork code in SSSD build system

[\#1118](/sssd/ticket/1118 "Support exclusion of attributes when building attribute list from map"){.closed}
:   Support exclusion of attributes when building attribute list from
    map

[\#1120](/sssd/ticket/1120 "Cleanup of the provider code - SYSDB_* constants"){.closed}
:   Cleanup of the provider code - SYSDB\_\* constants

[\#1153](/sssd/ticket/1153 "Offline(network disconnect) authentication using proxy provider crashes ..."){.closed}
:   Offline(network disconnect) authentication using proxy provider
    crashes sssd.

[\#1180](/sssd/ticket/1180 "Manpage for ldap_sasl_mech should be made more clear"){.closed}
:   Manpage for ldap\_sasl\_mech should be made more clear

[\#1225](/sssd/ticket/1225 "RFE: Add more debug information into the krb5_child and ldap_child ..."){.closed}
:   RFE: Add more debug information into the krb5\_child and ldap\_child
    processes

[\#1266](/sssd/ticket/1266 "Potential NULL-dereference in sss_nss_mc_get_record"){.closed}
:   Potential NULL-dereference in sss\_nss\_mc\_get\_record

[\#1267](/sssd/ticket/1267 "Use of unininitialized value in fill_grent"){.closed}
:   Use of unininitialized value in fill\_grent

[\#1310](/sssd/ticket/1310 "System error when trying to sudo"){.closed}
:   System error when trying to sudo

[\#1311](/sssd/ticket/1311 "sss_cache does not remove entries from the fastcache"){.closed}
:   sss\_cache does not remove entries from the fastcache

[\#1317](/sssd/ticket/1317 "Detect LDAPDerefRes in configure script"){.closed}
:   Detect LDAPDerefRes in configure script

[\#1341](/sssd/ticket/1341 "add AD-specific autofs mapping for the AD schema"){.closed}
:   add AD-specific autofs mapping for the AD schema

[\#1347](/sssd/ticket/1347 "protocol fallback when resolving SRV queries does not work properly"){.closed}
:   protocol fallback when resolving SRV queries does not work properly

[\#1355](/sssd/ticket/1355 "ldap_schema = ad performance issue"){.closed}
:   ldap\_schema = ad performance issue

[\#1384](/sssd/ticket/1384 "SSSD should move away unaccessible ccache files"){.closed}
:   SSSD should move away unaccessible ccache files

[\#1387](/sssd/ticket/1387 "sssd_ldap fails to properly authenticate to the disrectory for sudo ..."){.closed}
:   sssd\_ldap fails to properly authenticate to the disrectory for sudo
    queries

[\#1394](/sssd/ticket/1394 "sssd_krb5_locator_plugin man pages found in sssd rpm."){.closed}
:   sssd\_krb5\_locator\_plugin man pages found in sssd rpm.

[\#1399](/sssd/ticket/1399 "sasl_bind_send returns with -2 [Local error] when trying to connect to ..."){.closed}
:   sasl\_bind\_send returns with -2 \[Local error\] when trying to
    connect to LDAP server using GSSAPI

[\#1402](/sssd/ticket/1402 "sssd_nss segfault detected during ipa-server-install."){.closed}
:   sssd\_nss segfault detected during ipa-server-install.

[\#1411](/sssd/ticket/1411 "Uninitialized value in krb5_child-test if ccname is specified"){.closed}
:   Uninitialized value in krb5\_child-test if ccname is specified

[\#1423](/sssd/ticket/1423 "Examine all uses of ldap_set_option() for endianness issues"){.closed}
:   Examine all uses of ldap\_set\_option() for endianness issues

[\#1426](/sssd/ticket/1426 "ignoring return value of ‘fread’ in sss_debuglevel"){.closed}
:   ignoring return value of ‘fread’ in sss\_debuglevel

[\#1428](/sssd/ticket/1428 "SELinux login file is not recreated during offline login"){.closed}
:   SELinux login file is not recreated during offline login

[\#1434](/sssd/ticket/1434 "Typo in logging when ldap search base is not set"){.closed}
:   Typo in logging when ldap search base is not set

[\#1440](/sssd/ticket/1440 "SSSD fails to store users if any of the requested attribute is empty."){.closed}
:   SSSD fails to store users if any of the requested attribute is
    empty.

[\#1487](/sssd/ticket/1487 "yum remove sssd does not remove files in  var/lib/sss/mc/"){.closed}
:   yum remove sssd does not remove files in var/lib/sss/mc/

[\#1506](/sssd/ticket/1506 "autofs entries with the same key collide"){.closed}
:   autofs entries with the same key collide

[\#1517](/sssd/ticket/1517 "subdomain discovery is too noisy"){.closed}
:   subdomain discovery is too noisy

[\#1521](/sssd/ticket/1521 "Missing Primary Server doesn't default to service lookup"){.closed}
:   Missing Primary Server doesn't default to service lookup

[\#1524](/sssd/ticket/1524 "Add provider specific default regular expressions for parsing user names"){.closed}
:   Add provider specific default regular expressions for parsing user
    names

[\#1526](/sssd/ticket/1526 "SSSD does not auto renew kerberos credentials when auth_provider is 'ipa'"){.closed}
:   SSSD does not auto renew kerberos credentials when auth\_provider is
    'ipa'

[\#1530](/sssd/ticket/1530 "ldap_idmap_autorid_compat not working with tokenGroups"){.closed}
:   ldap\_idmap\_autorid\_compat not working with tokenGroups

[\#1556](/sssd/ticket/1556 "check the principal using select_principal_from_keytab in LDAP provider ..."){.closed}
:   check the principal using select\_principal\_from\_keytab in LDAP
    provider when using GSSAPI

</div>

<div>

[\#1331](/sssd/ticket/1331 "Off-by-one error in sss_hmac_sha1"){.closed}
:   Off-by-one error in sss\_hmac\_sha1

[\#1364](/sssd/ticket/1364 "[abrt] sssd-1.8.3-11.fc16: set_server_common_status: Process ..."){.closed}
:   \[abrt\] sssd-1.8.3-11.fc16: set\_server\_common\_status: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)

[\#1438](/sssd/ticket/1438 "SSSD crashes at boot time"){.closed}
:   SSSD crashes at boot time

[\#1452](/sssd/ticket/1452 "Authentication fails if kpasswd cannot be resolved"){.closed}
:   Authentication fails if kpasswd cannot be resolved

[\#1454](/sssd/ticket/1454 "if allocation fails, sss_mmap_cache_init may dereference NULL pointer"){.closed}
:   if allocation fails, sss\_mmap\_cache\_init may dereference NULL
    pointer

[\#1458](/sssd/ticket/1458 "Full sudo refresh is scheduled even if there is no sudo responder"){.closed}
:   Full sudo refresh is scheduled even if there is no sudo responder

[\#1466](/sssd/ticket/1466 "Proxy: Cannot retrieve an user after a group he is a member of was ..."){.closed}
:   Proxy: Cannot retrieve an user after a group he is a member of was
    retrieved

[\#1467](/sssd/ticket/1467 "enumeration is broken in the proxy provider"){.closed}
:   enumeration is broken in the proxy provider

[\#1479](/sssd/ticket/1479 "Hbac logs show wrong rule name granting access"){.closed}
:   Hbac logs show wrong rule name granting access

[\#1486](/sssd/ticket/1486 "[abrt] sssd-1.8.4-14.fc17: sss_ldap_init_send: Process ..."){.closed}
:   \[abrt\] sssd-1.8.4-14.fc17: sss\_ldap\_init\_send: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)

[\#1496](/sssd/ticket/1496 "[abrt] sssd-1.8.4-14.fc17: ldap_pvt_sasl_getmechs: Process ..."){.closed}
:   \[abrt\] sssd-1.8.4-14.fc17: ldap\_pvt\_sasl\_getmechs: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)

[\#1505](/sssd/ticket/1505 "sudo with sss backend should use ipa_hostname"){.closed}
:   sudo with sss backend should use ipa\_hostname

[\#1509](/sssd/ticket/1509 "libsss_sudo is not updated when yum update sssd is called"){.closed}
:   libsss\_sudo is not updated when yum update sssd is called

[\#1513](/sssd/ticket/1513 "Change the processing of the SELinux default map"){.closed}
:   Change the processing of the SELinux default map

[\#1515](/sssd/ticket/1515 "pam_sss report System Error on wrong password"){.closed}
:   pam\_sss report System Error on wrong password

[\#1516](/sssd/ticket/1516 "krb5_mod_ccname should cancel the transaction at one place only"){.closed}
:   krb5\_mod\_ccname should cancel the transaction at one place only

[\#1519](/sssd/ticket/1519 "membership of IPA hostgroups is not evaluated when treating them as ..."){.closed}
:   membership of IPA hostgroups is not evaluated when treating them as
    netgroups

</div>

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

<div>

[\#1461](/sssd/ticket/1461 "Replace "id_max, id_min" to "max_id, min_id" in manpage section of ID ..."){.closed}
:   Replace "id\_max, id\_min" to "max\_id, min\_id" in manpage section
    of ID MAPPING

[\#1462](/sssd/ticket/1462 "Change default for ldap_idmap_range_min to 200000"){.closed}
:   Change default for ldap\_idmap\_range\_min to 200000

[\#1463](/sssd/ticket/1463 "SRV support and duplicate detection in the back up list"){.closed}
:   SRV support and duplicate detection in the back up list

[\#1464](/sssd/ticket/1464 "Manpage for ldap_sasl_authid needs to show correct default"){.closed}
:   Manpage for ldap\_sasl\_authid needs to show correct default

[\#1473](/sssd/ticket/1473 "description of ldap_*_search_base options is missing details"){.closed}
:   description of ldap\_\*\_search\_base options is missing details

</div>

<div>

[\#904](/sssd/ticket/904 "Create tool to seed a user for first-boot"){.closed}
:   Create tool to seed a user for first-boot

[\#1087](/sssd/ticket/1087 "RFE: Allow Forcing User Shell"){.closed}
:   RFE: Allow Forcing User Shell

[\#1128](/sssd/ticket/1128 "Introduce the concept of a Primary Server in SSSD"){.closed}
:   Introduce the concept of a Primary Server in SSSD

[\#1185](/sssd/ticket/1185 "[Feature] AD Extensions"){.closed}
:   \[Feature\] AD Extensions

[\#1318](/sssd/ticket/1318 "RFE: make the NSS memory cache timeout configurable"){.closed}
:   RFE: make the NSS memory cache timeout configurable

[\#1368](/sssd/ticket/1368 "Missing hostid and subdomains sections in sssd-ipa.conf"){.closed}
:   Missing hostid and subdomains sections in sssd-ipa.conf

[\#1380](/sssd/ticket/1380 "domain_realm mappings manipulation by sssd"){.closed}
:   domain\_realm mappings manipulation by sssd

[\#1418](/sssd/ticket/1418 "document how sudo works with sssd"){.closed}
:   document how sudo works with sssd

[\#1420](/sssd/ticket/1420 "sudo: provide automatic configuration of machine hostnames"){.closed}
:   sudo: provide automatic configuration of machine hostnames

[\#1427](/sssd/ticket/1427 "Don't refersh HBAC rules when looking up SELinux rules"){.closed}
:   Don't refersh HBAC rules when looking up SELinux rules

[\#1429](/sssd/ticket/1429 "IPA session code returns error when SELinux mapping rule links to an HBAC ..."){.closed}
:   IPA session code returns error when SELinux mapping rule links to an
    HBAC rule

[\#1432](/sssd/ticket/1432 "Mention AD Provider in manpage of sssd.conf"){.closed}
:   Mention AD Provider in manpage of sssd.conf

[\#1433](/sssd/ticket/1433 "Suggested additions to manpage of sssd-ad"){.closed}
:   Suggested additions to manpage of sssd-ad

[\#1435](/sssd/ticket/1435 "SELinux specifity does not work with HBAC rules"){.closed}
:   SELinux specifity does not work with HBAC rules

[\#1439](/sssd/ticket/1439 "sss_pam needs to write out SELinux login file during the account phase"){.closed}
:   sss\_pam needs to write out SELinux login file during the account
    phase

[\#1445](/sssd/ticket/1445 "The SELinux login file needs to be created by the responder, not PAM ..."){.closed}
:   The SELinux login file needs to be created by the responder, not PAM
    module

[\#1448](/sssd/ticket/1448 "sss_seed tool review issues"){.closed}
:   sss\_seed tool review issues

</div>

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

<div>

[\#1239](/sssd/ticket/1239 "[RFE] sudo: send username and uid while requesting default options"){.closed}
:   \[RFE\] sudo: send username and uid while requesting default options

[\#1299](/sssd/ticket/1299 "Per domain formats for qualified user names"){.closed}
:   Per domain formats for qualified user names

[\#1352](/sssd/ticket/1352 "[RFE] Add the subdomain functionality to IPA auth provider"){.closed}
:   \[RFE\] Add the subdomain functionality to IPA auth provider

[\#1377](/sssd/ticket/1377 "[RFE] Add AD provider"){.closed}
:   \[RFE\] Add AD provider

[\#1382](/sssd/ticket/1382 "pac responder interface needs checks"){.closed}
:   pac responder interface needs checks

[\#1385](/sssd/ticket/1385 "heimdal: compile time diference"){.closed}
:   heimdal: compile time diference

[\#1398](/sssd/ticket/1398 "Dependency issue while "yum update libsss_sudo""){.closed}
:   Dependency issue while "yum update libsss\_sudo"

[\#1403](/sssd/ticket/1403 "Combine keytab options for AD provider"){.closed}
:   Combine keytab options for AD provider

[\#1404](/sssd/ticket/1404 "AD provider should default to case-insensitive operation"){.closed}
:   AD provider should default to case-insensitive operation

[\#1407](/sssd/ticket/1407 "Revert sssd patch for limiting enctypes to keytab"){.closed}
:   Revert sssd patch for limiting enctypes to keytab

[\#1409](/sssd/ticket/1409 "Resource leak in sssdpac_import_authdata"){.closed}
:   Resource leak in sssdpac\_import\_authdata

[\#1410](/sssd/ticket/1410 "Dead code in ipa_subdomains_handler_done()"){.closed}
:   Dead code in ipa\_subdomains\_handler\_done()

[\#1412](/sssd/ticket/1412 "Starting SSSD with a domain using the LOCAL provider segfaults the ..."){.closed}
:   Starting SSSD with a domain using the LOCAL provider segfaults the
    responders

</div>

<div>

[\#1163](/sssd/ticket/1163 "[Feature] SSSD AD Integration Feature (Cross Realm Kerberos Trusts)"){.closed}
:   \[Feature\] SSSD AD Integration Feature (Cross Realm Kerberos
    Trusts)

[\#1354](/sssd/ticket/1354 "Add support for terminating idle connections in sssd_nss"){.closed}
:   Add support for terminating idle connections in sssd\_nss

[\#1383](/sssd/ticket/1383 "sssd_nss segfaults performing netgroup lookups without a specified domain"){.closed}
:   sssd\_nss segfaults performing netgroup lookups without a specified
    domain

</div>

<div>

[\#974](/sssd/ticket/974 "[RFE] Support DIR: credential caches for multiple TGT support"){.closed}
:   \[RFE\] Support DIR: credential caches for multiple TGT support

[\#984](/sssd/ticket/984 "RFE: sssd should support Netscape LDAP password expiration controls"){.closed}
:   RFE: sssd should support Netscape LDAP password expiration controls

[\#1213](/sssd/ticket/1213 "Warn to syslog when dereference requests fail"){.closed}
:   Warn to syslog when dereference requests fail

[\#1240](/sssd/ticket/1240 "sudo: contact data provider only once"){.closed}
:   sudo: contact data provider only once

[\#1255](/sssd/ticket/1255 "RFE: change the way we deal with fake users"){.closed}
:   RFE: change the way we deal with fake users

[\#1256](/sssd/ticket/1256 "Document the expectations about ghost users showing in the lookups"){.closed}
:   Document the expectations about ghost users showing in the lookups

[\#1330](/sssd/ticket/1330 "Potential NULL dereference in sss_krb5_read_etypes_for_keytab"){.closed}
:   Potential NULL dereference in sss\_krb5\_read\_etypes\_for\_keytab

[\#1336](/sssd/ticket/1336 "Please only use named parameters in translatable strings"){.closed}
:   Please only use named parameters in translatable strings

[\#1337](/sssd/ticket/1337 "Minor typos in SSSD messages and man pages"){.closed}
:   Minor typos in SSSD messages and man pages

[\#1346](/sssd/ticket/1346 "in-memory cache causes nss to segfault if it cannot be initialized ..."){.closed}
:   in-memory cache causes nss to segfault if it cannot be initialized
    properly

[\#1367](/sssd/ticket/1367 "Optimize AD memberOf lookups with LDAP_MATCHING_RULE_IN_CHAIN"){.closed}
:   Optimize AD memberOf lookups with LDAP\_MATCHING\_RULE\_IN\_CHAIN

</div>

<div>

[\#357](/sssd/ticket/357 "SSSD should provide fast in memory cache to provide similar functionality ..."){.closed}
:   SSSD should provide fast in memory cache to provide similar
    functionality as NSCD currently provides

[\#783](/sssd/ticket/783 "Support range retrievals"){.closed}
:   Support range retrievals

[\#887](/sssd/ticket/887 "Implement mechanism to fetch and store domain info"){.closed}
:   Implement mechanism to fetch and store domain info

[\#917](/sssd/ticket/917 "Document sss_tools better"){.closed}
:   Document sss\_tools better

[\#949](/sssd/ticket/949 "Filter out inappropriate IP addresses from IPA dynamic DNS update"){.closed}
:   Filter out inappropriate IP addresses from IPA dynamic DNS update

[\#996](/sssd/ticket/996 "RFE: Allow Constructing uid from Active Directory objectSid"){.closed}
:   RFE: Allow Constructing uid from Active Directory objectSid

[\#1031](/sssd/ticket/1031 "[RFE] Implement "AD friendly" schema mapping"){.closed}
:   \[RFE\] Implement "AD friendly" schema mapping

[\#1064](/sssd/ticket/1064 "Sub-Domains: define new get_domains method"){.closed}
:   Sub-Domains: define new get\_domains method

[\#1065](/sssd/ticket/1065 "Sub-Domains: implement new get_domains method in IPA provider"){.closed}
:   Sub-Domains: implement new get\_domains method in IPA provider

[\#1067](/sssd/ticket/1067 "Sub-Domains: add new get_domains method to responders"){.closed}
:   Sub-Domains: add new get\_domains method to responders

[\#1114](/sssd/ticket/1114 "get_uid_from_pid() perfoms an improper read"){.closed}
:   get\_uid\_from\_pid() perfoms an improper read

[\#1119](/sssd/ticket/1119 "Monitor SIGKILL time should be configurable"){.closed}
:   Monitor SIGKILL time should be configurable

[\#1140](/sssd/ticket/1140 "RFE Request for including pam_pwd_expiration_warning = 0 in sssd.conf"){.closed}
:   RFE Request for including pam\_pwd\_expiration\_warning = 0 in
    sssd.conf

[\#1170](/sssd/ticket/1170 "sss_cache should support invalidating services and autofs maps"){.closed}
:   sss\_cache should support invalidating services and autofs maps

[\#1172](/sssd/ticket/1172 "Bad check for id_provider=local and access_provider=permit"){.closed}
:   Bad check for id\_provider=local and access\_provider=permit

[\#1174](/sssd/ticket/1174 "sssd.conf has wrong defaults for the "command" parameter"){.closed}
:   sssd.conf has wrong defaults for the "command" parameter

[\#1176](/sssd/ticket/1176 "SSH: Add dp_get_host_send to common responder code"){.closed}
:   SSH: Add dp\_get\_host\_send to common responder code

[\#1181](/sssd/ticket/1181 "Typos in sssd manual"){.closed}
:   Typos in sssd manual

[\#1203](/sssd/ticket/1203 "Hash the hostname/port information in the known_hosts file."){.closed}
:   Hash the hostname/port information in the known\_hosts file.

[\#1209](/sssd/ticket/1209 "Convert all read and write loops to use atomic I/O function"){.closed}
:   Convert all read and write loops to use atomic I/O function

[\#1233](/sssd/ticket/1233 "Memory leak in sss_sudo_send_recv_generic"){.closed}
:   Memory leak in sss\_sudo\_send\_recv\_generic

[\#1250](/sssd/ticket/1250 "Add default home directory mapping"){.closed}
:   Add default home directory mapping

[\#1271](/sssd/ticket/1271 "Stop using HTML_FOOTER_DESCRIPTION in doxygen docs"){.closed}
:   Stop using HTML\_FOOTER\_DESCRIPTION in doxygen docs

[\#1281](/sssd/ticket/1281 "Add unit test for compatibility of ldap options between schemas"){.closed}
:   Add unit test for compatibility of ldap options between schemas

[\#1289](/sssd/ticket/1289 "Create a way to define a default shell for cases when there no shell"){.closed}
:   Create a way to define a default shell for cases when there no shell

[\#1297](/sssd/ticket/1297 "Use keytab to select etypes for krb5_get_init_creds_keytab()"){.closed}
:   Use keytab to select etypes for krb5\_get\_init\_creds\_keytab()

[\#1298](/sssd/ticket/1298 "Invalid cache file created when canoning principals during ..."){.closed}
:   Invalid cache file created when canoning principals during
    krb5\_get\_init\_creds\_keytab()

[\#1301](/sssd/ticket/1301 "sss_cache does nothing when executed without any options."){.closed}
:   sss\_cache does nothing when executed without any options.

[\#1305](/sssd/ticket/1305 "sss_cache should return a warning/error while validating unknown ..."){.closed}
:   sss\_cache should return a warning/error while validating unknown
    user/group

[\#1306](/sssd/ticket/1306 "sss_cache should return an error, when executed against inactive domains"){.closed}
:   sss\_cache should return an error, when executed against inactive
    domains

[\#1313](/sssd/ticket/1313 "exec_child, execv and friends don't return success"){.closed}
:   exec\_child, execv and friends don't return success

[\#1316](/sssd/ticket/1316 "kpasswd server status set to working when Kerberos auth succeeds"){.closed}
:   kpasswd server status set to working when Kerberos auth succeeds

[\#1565](/sssd/ticket/1565 "SSSD stops working due to memory problems"){.closed}
:   SSSD stops working due to memory problems

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Ariel Barria (6):

-   Bad check for id\_provider=local and access\_provider=permit
-   Potential NULL dereference in proxy provider
-   Warn to syslog when dereference requests fail
-   Clarify how comments work in sssd.conf
-   SIGUSR2 should force SSSD to reread resolv.conf as well
-   Missing resolv.conf should be non-fatal

George
[McCollister?](https://docs.pagure.org/sssd-test2/McCollister.html){.missing
.wiki} (1):

-   libcrypto fully implemented

Jakub Hrozek (205):

-   Fix SSH compilation on RHEL5
-   AUTOFS: IPA provider
-   Two sssd-ldap manual pages fixes
-   Fix group enumeration
-   Only fetch SELinux string if the user is found
-   Remove setent structure when callback is called
-   Allocate setent structure on state, not on the client context
-   Fix memory hierarchy when processing nested group memberships
-   Fix case insensitive service lookups
-   Include the fd\_limit configuration option
-   End request if ldap\_parse\_result fails
-   remove unused function
-   Save errno value before calling DEBUG
-   libnl: fix the path to phy80211 subdirectory
-   AUTOFS: Invoke implicit setautomntent if needed
-   AUTOFS: Search all search bases for automounter map entries
-   AUTOFS: speed up the client by requesting multiple entries at once
-   Use proper errno code
-   Only do one cycle when resolving a server
-   krb5\_child: set debugging sooner
-   Search netgroups by alias, too
-   Detect cycle in the fail over on subsequent resolve requests only
-   Autofs: operate on contents of double-pointer, not address
-   Only free returned values on success
-   Save original name into the in-memory cache
-   Handle errors from lookup\_netgr\_step gracefully
-   Fix nested groups processing
-   Fix netgroup error handling
-   Handle empty elements in proxy netgroups:
-   Fix uninitialized variable
-   Free entry found in negative cache
-   Make the string\_equal() function public
-   Save alias of the primary name, too
-   NSS: Look for services with correct case when cache is updated
-   AUTOFS: fix copy-and-paste bug in the autofs client
-   LDAP services: Keep the protocol around
-   Silence Coverity warning in the autofs test tool
-   Return correct resolv\_status on resolver timeout
-   Add sss\_get\_cased\_name\_list utility function
-   LDAP services: Save lowercased protocol names in case-insensitive
    domains
-   Proxy services: Save lowercased protocol names and aliases in
    case-insensitive domains
-   Fix off-by-one error in principal selection
-   Catch cases where D-Bus connection is NULL
-   Use HTML\_TIMESTAMP instead of HTML\_FOOTER\_DESCRIPTION
-   Fix regression in SSSDConfig.py
-   netlink integration: ensure that interface name is NULL-terminated
-   Remove forgotten DEBUG message
-   autofs: load the correct option
-   man: document that referral chasing might bring performance penalty
-   Prevent printing NULL from DEBUG messages
-   Do not call sdap\_auth if not needed
-   pam\_sss: improve error handling in SELinux code
-   Remove the "command" option from documentation
-   Add sysdb\_set\_service\_attr and sysdb\_set\_autofsmap\_attr
-   sss\_cache: support invalidating services and autofs maps
-   autofs: Raise the maximum key length to PATH\_MAX
-   sss\_cache: Better error reporting
-   MAN: timeout can be specified for services, too
-   MAN: document the hostid and autofs providers
-   proxy: Canonicalize user and group names
-   proxy: new option proxy\_fast\_alias
-   Free controls in sdap\_rebind\_proc
-   Make the monitor SIGKILL time configurable
-   sdap\_check\_aliases must not error when detects the same user
-   sss\_atomic\_io: Do not fail reads with EPIPE if there is not enough
    data to read
-   Move atomic io function to a separate module
-   Convert read and write operations to sss\_atomic\_read
-   Document sss\_tools better
-   Warn on 'make update-po' if there are manpages not listed in
    po4a.cfg
-   Test RFC2307bis and RFC2307 option maps
-   Get the RootDSE after binding if not successfull before
-   Lowercase group members in case-insensitive domains
-   NSS: Only return data from initgroups once
-   SUDO: Return ret, not EOK
-   SYSDB: return EOK if empty message is passed into get\_rm\_msg
-   SYSDB: check return value
-   SSH: return NULL on error in
    ssh\_host\_pubkeys\_format\_known\_host\_plain
-   SERVER: use the correct return code of sss\_atomic\_write\_s
-   LDAP: check return value of sysdb\_attrs\_get\_el
-   RESPONDER: check return value from confdb\_get\_int
-   PYHBAC: Return NULL on failure
-   PAM\_SSS: report error code if write fails
-   NSS: Check return code of sss\_mmap\_cache\_gr\_store
-   IPA netgroups: return EOK when there are no netgroups to process
-   ipa\_get\_config\_send: remove unused assignment
-   HBAC: Prevent NULL dereference in hbac\_evaluate
-   DP: return correct error message when subdomains back end target is
    not configured
-   NSS: fix returning group from cache
-   SSS\_DEBUGLEVEL: silence analyzer warnings
-   PROXY: return correct return codes
-   IPA: Check return values
-   AUTOFS: remove unused assignments
-   Rename split\_service\_name\_filter
-   SSH: Add dp\_get\_host\_send to common responder code
-   Read sysdb attribute name, not LDAP attribute map name
-   Kerberos locator: Include the correct krb5.h header file
-   Special-case LDAP\_SIZELIMIT\_EXCEEDED
-   krb5 locator: Do not leak addrinfo
-   Only reset kpasswd server status when performing a chpass operation
-   Try all KDCs when getting TGT for LDAP
-   Send the correct enumeration request
-   subdomains: Fix error handling in Data Provider
-   Filter out IP addresses inappropriate for DNS forward records
-   sysdb: return proper error code from sysdb\_sudo\_purge\_all
-   SYSDB: Handle user and group renames better
-   NSS: keep a pointer to body after body is reallocated
-   Use sized\_string correctly in FQDN domains
-   Use the sysdb attribute name, not LDAP attribute name
-   LDAP nested groups: Do not process callback with \_post deep in the
    nested structure
-   Send 16bit protocol numbers from the sss\_client
-   Revert the client packet length, too, after reverting the packet
    protocol
-   Fix the default sssd.conf path
-   Fix the 0.11 sysdb upgrade
-   sss\_names\_init: Report correct error code if allocation failed
-   Two small krb5\_child fixes
-   Provide more debugging in krb5\_child and ldap\_child
-   Allow redefining the KRB5\_CHILD path
-   Split parse\_krb5\_child\_response so it can be reused
-   Add a krb5\_child test tool
-   Residual util functions
-   Handle trailing slash in the ccname template
-   Add a credential cache back end structure
-   Add support for storing credential caches in the DIR: back end
-   Use Kerberos context in KRB5\_DEBUG
-   Make krb5\_ccname\_template and krb5\_ccachedir configurable
-   Print based on pointer contents not address
-   Cast uid\_t to unsigned long long in DEBUG messages
-   Update translations for 1.9.0 beta 4 release
-   Bumping version to 1.9.0 beta 5
-   Add newline to DEBUG messages
-   RPM: Own several directories
-   Add missing "%" to specfile
-   IPA: Download defaults even if there are no SELinux mappings
-   SYSDB: Delete SELinux mappings
-   IPA: Return and save all SELinux rules in the provider
-   PAM: Fix off-by-one-error in the SELinux session code
-   Update translations for 1.9.0 beta 5 release
-   Bumping version to 1.9.0 beta 6
-   Fix sysdb\_search\_selinux\_usermap\_by\_username return value
-   Fix SSSDConfigTest
-   Fix bad check
-   Create a domain-realm mapping for krb5.conf to be included
-   Update translations for 1.9.0 beta 6 release
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
-   Bumping version for the 1.9.0 beta 7 release
-   libsss\_sudo should have a versioned dependency on SSSD
-   KRB5: cancel the sysdb transaction on one place only
-   KRB5: Return PAM\_AUTH\_ERR on incorrect password
-   RPM:
    [BuildRequire?](https://docs.pagure.org/sssd-test2/BuildRequire.html){.missing
    .wiki} selinux-policy-targeted
-   SYSDB: NULL-terminate the output of sysdb\_get\_{ranges,subdomains}
-   KRB5: Add a missing string argument
-   NSS: Fix off-by-one error in parse\_getservbyname
-   FO: Check server validity before setting status
-   DB: Always write the SELinux object to sysdb
-   SELinux: Always use the default if it exists on the server
-   Updating the translations for the 1.9.0 RC1 release
-   Updating the version for the RC1 release
-   KRB5 child: Don't return System Error on empty password
-   KRB5 child: handle more error codes gracefully
-   DB: Cancel transaction in sysdb\_store\_user if sysdb\_add\_user
    fails
-   Mark the fastcache files in the spec file as %ghost
-   autofs, sudo, ssh and PAC are not experimental anymore
-   AUTOFS: Do not fail if search base is not provided
-   AUTOFS: Add sysdb tests
-   AUTOFS: Add entry objects below map objects
-   AUTOFS: Use both key and value in entry RDN
-   AUTOFS: convert the existing autofs entries during a sysdb upgrade
-   SYSDB: Remove unnecessary domain parameter from several sysdb calls
-   DB: Use TALLOC\_CTX for talloc context
-   KRB5: Recover gracefully if the ccache file could not be reused
-   Detect LDAPDerefRes in configure script
-   RPM: Create ghost files during install
-   Set the version number to 1.9.0 for the release
-   Updating translations for the 1.9.0 release

Jan Cholasta (29):

-   Add methods for activating and deactivating services to SSSDConfig
-   Add ssh service to sssd.api.conf
-   SSH: Verify that names received from client are valid UTF-8 in
    responder
-   SSH: Build man pages conditionally
-   SSH: Save SSH host name aliases
-   SSH: Refactor responder and client common code
-   UTIL: Add function for atomic I/O
-   SSH: Continue connecting to SSH server even when SSSD is not running
    in sss\_ssh\_knownhostsproxy
-   SSH: Manage global known\_hosts file in the responder
-   SSH: Don't abort known\_hosts update when host search fails
-   SSH: Add more debugging messages
-   SSH: Add missing break statements to sss\_ssh\_format\_pubkey
-   SSH: Use fchmod instead of chmod on known\_hosts file
-   SSH: Replace blocking getaddrinfo call in the responder with
    asynchronous resolver code
-   SSH: Remove unused --file option of sss\_ssh\_knownhostsproxy
-   SSH: Update sss\_ssh\_knownhostsproxy manual page
-   Include missing source files to the list of source files which
    contain translatable strings
-   SSH: Allow clients to explicitly specify host alias
-   SSH: Canonicalize host name and do reverse DNS lookup in
    sss\_ssh\_knownhostsproxy
-   SSH: Fix infinite loop in sss\_ssh\_knownhostsproxy
-   UTIL: Add HMAC-SHA-1 function
-   SSH: Add support for hashed known\_hosts
-   SSH: Update sss\_ssh\_knownhostsproxy manual page
-   SSH: Supress error message output in sss\_ssh\_knownhostsproxy
-   SSH: Don't abort connection in sss\_ssh\_knownhostsproxy when DNS
    records are missing
-   SSH: Return error code in SSH utility functions
-   SSH: Simplify public key formatting function
-   SSH: Add support for OpenSSH-style public keys
-   SSH: Fix possible infinite loop when updating known\_hosts

Jan Engelhardt (1):

-   build: resolve link failure

Jan Vcelak (1):

-   LDAP: Properly cast type for MINSSF value

Jan Zeleny (87):

-   Fixed issue with netgroup update in IPA provider
-   Don't give memory context in confdb where not needed
-   IPA hosts refactoring
-   SELinux related attributes added to config API
-   Delete missing attributes from netgroups to be stored
-   Modifications to simplify list\_missing\_attrs
-   Fix the script path
-   Fixed uninitialized pointer in SSH known host proxy
-   Fixed uninitialized pointer in SSH authorized keys client
-   Add umask before mkstemp() call in SSH responder
-   Fixed resource leak in ssh client code
-   Removed a block of dead code in sdap\_async\_groups.c
-   Removed unused block of code is sdap\_fill\_memberships()
-   Removed unused function sysdb\_attrs\_users\_from\_ldb\_vals()
-   Fixed memory context in sdap\_fill\_memberships()
-   Fixed minor memory leak in ldap provider
-   Sysdb routines for subdomains
-   Add some utility functions for subdomains
-   Add conn\_name to allow different names for domains and connections
-   Responder part of the subdomain retrieval work
-   Modified responder\_get\_domain()
-   Retrieve subdomains if there is a request for fully qualified user
-   Ask for subdomains in responder in the first request after startup
-   New config option for subdomains
-   Moved expand\_homedir\_template() from NSS responder to utility code
-   Add ID operations in subdomains
-   Send PAM requests for subdomains to the right provider
-   Basic support for subdomains in auth provider
-   Carry sysdb context and domain info in be\_req structure
-   Accept be\_req instead if be\_ctx in LDAP access provider
-   Detect subdomain request in IPA access provider
-   Utilize sysdb context within be\_req in HBAC
-   Two fixes in responder subdomain code
-   Modify behavior of pam\_pwd\_expiration\_warning
-   Fixed two minor memory leaks
-   Fixed issue in SELinux user maps
-   Ghost members - add the ghost attribute to sysdb
-   Ghost members - support in LDAP provider
-   Ghost members - support in proxy provider
-   Ghost members - modifications in sysdb
-   Ghost members - modifications in memberof plugin
-   Ghost members - sysdb upgrade routine
-   Ghost members - NSS responder changes
-   Ghost members - removed sdap\_check\_aliases()
-   Ghost members - modified sss\_groupshow
-   Ghost members - various small changes
-   Add support for filtering atributes
-   Utilize attribute exclusion in LDAP initgroups
-   Fixed setting of debug level in test suite
-   IPA subdomains - ask for information about master domain
-   Allow fast memcache timeout to be configurable
-   Fix an issue in ghost users
-   Provide "service filter" for SELinux context
-   Fixed debug message in sdap\_save\_group()
-   Fix possible segfault in sdap\_save\_group()
-   PAC responder: add some utility functions
-   PAC responder: test suite
-   Fix re\_expression matching with subdomains
-   SELinux user maps: pick just one map
-   Fixed wrong number in shadowLastChange
-   Add function sysdb\_attrs\_copy\_values()
-   Modify priority evaluation in SELinux user maps
-   Added some DEBUG statements into SELinux related code
-   Extend category support in SELinux user maps
-   Remove ipa\_selinux\_map\_merge()
-   Fix linking of HBAC rules and SELinux user maps
-   Provide counter of possible matches in SELinux IPA provider
-   Always free request in data provider PAM callback
-   Renamed session provider to selinux provider
-   Move SELinux processing from session to account PAM stack
-   Remove unused member of be\_req
-   Write SELinux config files in responder instead of PAM module
-   Modify hbac\_get\_cached\_rules() so it can be used outside of HBAC
    code
-   Support fetching of HBAC rules from sysdb in SELinux code
-   Support fetching of host from sysdb in SELinux code
-   Primary server support: introduce concept of reconnection
-   Primary server support: basic support in failover code
-   Primary server support: support for "disconnecting" connections in
    LDAP
-   Primary server support: IPA adaptation
-   Primary server support: krb5 adaptation
-   Primary server support: LDAP adaptation
-   Primary server support: AD adaptation
-   Primary server support: man page, failover section
-   Primary server support: new option in ldap provider
-   Primary server support: new options in krb5 provider
-   Primary server support: new option in IPA provider
-   Primary server support: new option in AD provider

Joshua Roys (1):

-   Simple implementation of Netscape password warning expiration
    control

Marco Pizzoli (1):

-   Two manual pages fixes

Michal Zidek (18):

-   Fixed: Unchecked return value from dp\_opt\_set\_int.
-   Fixed: Uninitialized value in krb5\_child-test if ccname was
    specified.
-   Added unit test for sysdb\_ssh.c
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
-   LDB\_ERR\_INVALID\_ATTRIBUTE\_SYNTAX added to
    sysdb\_error\_to\_errno.
-   SSSD fails to store users if any of the requested attribute is
    empty.
-   tools\_util.h provides signal\_sssd function.
-   sss\_cache tool invalidates records in memory cache.
-   Bad debug message when no dns\_discovery\_domain specified.

Nick Guay (4):

-   added DEBUG messages to krb5\_child and ldap\_child
-   Fix uninitialized values
-   First-boot sss\_seed tool
-   remove duplicate sss\_obfuscate reference in seealso manpage section

Ondrej Kos (7):

-   Removed unused variable assignment
-   Replaced "id\_max" & "id\_min"
-   Backward GOTOs rewritten into do-while loops.
-   AD context was set to null due to type mismatch
-   Consolidation of functions that make realm upper-case
-   Out-of-bounds read fix in hmac-sha-1
-   Add more debuginfo into ldap\_child

Pavel Březina (96):

-   Improve debug messages in sysdb\_sudo\_check\_time()
-   SUDO responder: check if the input is a UTF-8 string
-   Refactor sss\_result into sss\_sudo\_result
-   Redesign purging of the sudo cache
-   Honor case\_sensitive option in sudo responder
-   Move sudo\_dom\_ctx.user to local variable
-   Hide --debug option in sss\_debuglevel
-   Two memory leaks in sss\_sudo\_get\_values
-   Missing debug message if sdap\_sudo\_refresh\_set\_timer fails
-   Use of unininitialized value in sudosrv\_cache\_set\_entry and
    sudosrv\_cache\_lookup\_internal
-   Use of unininitialized value in sss\_sudo\_parse\_response
-   Potential NULL-dereference in sudosrv\_cmd\_get\_sudorules
-   sudo api: check sss\_status instead of errnop in
    sss\_sudo\_send\_recv\_generic()
-   Install and uninstall all documentation
-   fix copy and paste error in comment
-   Fix typo in debug message
-   sudo api: remove EOK
-   sudo responder: remove code duplication in commands
-   sudo responder: get rid of dctx where possible
-   sudo sysdb: make sysdb\_get\_sudo\_user\_info more configurable
-   sudo api: send uid, username and domainname
-   sudo responder: change protocol version to 1
-   libsss\_sudo: bump version to 2:0:1
-   sudo responder: discard in-memory cache
-   sudo ldap provider: move async routines to sdap\_async\_sudo.c
-   sudo ldap provider: give sdap\_sudo\_refresh\_send() search and
    purge filters
-   confdb: add entry\_cache\_sudo\_timeout option
-   sudo ldap provider: add sysdb ctx in sdap\_sudo\_refresh\_state
-   sudo ldap provider: add domain info in sdap\_sudo\_refresh\_state
-   sudo ldap provider: add expiration time to each rule
-   sysdb: add getter/setter for last sudo full refresh time
-   sudo ldap provider: provide API for full refresh
-   sudo ldap provider: add support for on demand full refresh
-   sudo ldap provider: provide API for refresh of specific rules
-   sudo ldap provider: add support for on demand refresh of specific
    rules
-   sudo backend - support only on demand full refresh
-   sudo backend - add support for on demand refresh of specific rules
-   sudo provider: add ldap\_sudo\_full\_refresh\_interval
-   sudo provider: remove old timer
-   sudo ldap provider: add new timer API
-   sysdb: remove sudo\_set/get\_refreshed
-   sudo ldap provider: support periodical full refresh
-   ldap provider: add sudo usn value
-   sudo ldap provider: find highest USN
-   sudo ldap provider: add sdap\_sudo\_set\_usn()
-   sudo ldap provider: remember highest usn after full refresh
-   sudo ldap provider: add smart refresh API
-   sudo ldap provider: when sysdb filter is NULL remove downloaded
    rules
-   sudo provider: add ldap\_sudo\_smart\_refresh\_interval
-   sudo ldap provider: add periodical smart refresh API
-   sudo ldap provider: support periodical smart refresh
-   sudo responder: new request enum type
-   sudo sysdb: add expiration time to the filter
-   sudo responder: allow fetching only expired rules in
    sudosrv\_get\_sudorules\_query\_cache()
-   sudo responder: update dp interface
-   sudo responder: refresh expired rules
-   sudo ldap provider: return number of downloaded rules in
    sdap\_sudo\_refresh\_recv()
-   sudo ldap provider: notify responder when an expired rule has been
    deleted
-   sudo responder: schedule OOB full refresh when expired rule is
    deleted
-   sudo: clean up
-   sudo ldap provider: modify highest USN in
    sdap\_sudo\_rules\_refresh\_done()
-   sdap\_sudo.c: move \_recv after \_done
-   sudo ldap provider: pass sudo\_ctx instead of id\_ctx
-   sudo: add host info options
-   sudo ldap provider: load host filter configuration on init
-   sudo ldap provider: mark sdap\_sudo\_setup\_periodical\_refresh() as
    static
-   sudo ldap provider: do per-host updates
-   sudo ldap provider: support autoconfiguration of IP addresses
-   sudo: manpage updated
-   resolv\_gethostbyname\_send: strdup hostname to work properly when
    hostname is allocated on stack
-   sudo test client: avoid SIGSEGV when run without arguments
-   sdap\_sudo.c: add missing end of line in few debug messages
-   add hostid and subdomains sections in sssd-ipa.conf
-   manpage: seealso - include ssh conditionally
-   tests: allow changing cwd in all tests
-   manpage: sssd-sudo - documents how sudo works with sssd
-   sudo ldap provider: support autoconfiguration of hostnames
-   Unbreak SASL
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
-   netgroup: resolve hostgroup membership correctly
-   be\_process\_init(): free ctx on error
-   backend: initialize sudo only when it is enabled in services
-   Failover: use \_srv\_ when no primary server is defined
-   rpm: put localized sssd\_krb5\_locator\_plugin manpages into client
-   sdap\_add\_incomplete\_groups(): fix ret may be uninitialized
    warning

Rambaldi (2):

-   heimdal: fix compile error in krb5-child-test
-   heimdal: use sss\_krb5\_princ\_realm to access realm

Shantanu Goel (4):

-   Set return errno to the value prior to calling close().
-   Log message if close() fails in destructor.
-   Do not send SIGPIPE on disconnection
-   Add support for terminating idle connections

Simo Sorce (31):

-   nss\_group: Cache the result from sssd when the glibc provided
    buffer is too small.
-   pam\_sss: keep selinux optional
-   Use the correct hash table for pending requests
-   util: Helper headers for shared memory cache
-   nsssrv: shared memory cache server initialization
-   nsssrv: Add memory cache record handling utils
-   nsssrv: add handling of memory cache passwd map
-   sss\_client: Add common shared memory cache utils
-   sss\_client: shared memory cache passwd map support
-   nsssrv: add handling of memory cache group map
-   sss\_client: shared memory cache group map support
-   Do not leak file descriptors in client libs.
-   Add close on exec support for old platforms
-   Fix segfault when sudo is not configured.
-   Change subdomain\_info
-   tests: Remove useless consts
-   80 columns police
-   Fix double semi-colons
-   Fix wrong elements used in comparison
-   Use ldb\_msg\_add\_string with bare strings
-   Fix return error and debug message
-   Make structure initializer more readable
-   80 col and style fixes
-   Use a more tractable name for subdomain request
-   Add realm paramter to subdomain list
-   Expose an initializer function from subdomain
-   Change refreshing of subdomains
-   Limit refreshes keeping track of last refresh time
-   Add online callback to enumerate subdomains
-   Add automatic periodic retrieval of subdomains
-   Remove obsolete comment

Stef Walter (10):

-   Fix erronous reference to the 'allow' access\_provider
-   execv, excvp and exec\_child never return EOK
-   If canon'ing principals, write ccache with updated default principal
-   Remove erroneous failure message in find\_principal\_in\_keytab
-   Limit krb5\_get\_init\_creds\_keytab() to etypes in keytab
-   Clearer documentation for use\_fully\_qualified\_names
-   Make re\_expression and full\_name\_format per domain options
-   Move some debug lines to new debug log levels
-   Fix crash when interface doesn't have an address
-   Revert commit
    [4c157ecedd52602f75574605ef48d0c48e9bfbe8](https://fedorahosted.org/sssd/changeset/4c157ecedd52602f75574605ef48d0c48e9bfbe8/ "Limit krb5_get_init_creds_keytab() to etypes in keytab

     * Load the ..."){.changeset}

Stephen Gallagher (178):

-   Set version to 1.9dev
-   Updating translatable strings for string freeze
-   Updating translations
-   Remove dead code
-   Fix missing NULL check after malloc
-   Avoid uninitialized value comparison
-   Add missing breaks to switch statements
-   Fix uninitialized in\_transaction
-   Fix bad failure handling in be\_sudo\_handler()
-   Check for failure in sss\_packet\_grow()
-   Fix uninitialized value error in proxy provider
-   Ensure NULL-termination in get\_uid\_from\_pid()
-   Move sss\_ssh\_\* binaries to the main 'sssd' package
-   Always include all manpage XML files in the distribution tarball
-   Fix missing %endif in sssd.spec.in
-   NSS: Always return the same protocol that was requested
-   LDAP: Ignore group member users that do not have name attributes
-   RESPONDERS: Allow increasing the file-descriptor limit
-   RESPONDERS: Make the fd\_limit setting configurable
-   Add tool to convert debug levels
-   IPA: Add ipa\_parse\_search\_base()
-   LDAP: Properly assign orig\_dn
-   LDAP: Only use paging control on requests for multiple entries
-   LDAP: Remove unnecessary filter sanitize
-   Eliminate build-time requirement for nscd
-   PAM: Don't send PAM\_SYSTEM\_INFO message if module unset
-   Fix typo in autofs option description
-   Include the debug\_level upgrade tool in the tarball
-   Include new manpages in translations
-   Fix typo in script name
-   Handle cases where UID is -1
-   IPA: Set the DNS discovery domain to match ipa\_domain
-   IPA: Fix segfault with srchost functionality enabled
-   DP: Reorganize memory hierarchy of requests
-   Prune python provides correctly
-   Make RPM spec more explicit
-   Build experimental features by default in RPMs
-   Properly terminate GIT\_CHECKOUT
-   LDAP: Make sdap\_access\_send/recv public
-   IPA: Check nsAccountLock during PAM\_ACCT\_MGMT
-   PROXY: Create fake user entries for group lookups
-   SSH: Fix missing semicolon
-   IPA: Initialize hbac\_ctx to NULL
-   i18n: Remove empty translations
-   LDAP: Add AD 2008r2 schema
-   IPA: Allow service lookups
-   SYSDB: Save only lowercased aliases in case-insensitive domains
-   LDAP: Errors retrieving the RootDSE should not be fatal
-   NSS: Fix debug message
-   Start SSSD earlier and stop it later
-   LDAP: Add better error logging when ldap\_result() fails
-   LDAP: Fix memory leaks in synchronous\_tls\_setup
-   BUILDSYS: Create common libs for LDAP and KRB5 sources
-   Put dp\_option maps in their own file
-   Add terminator for dp\_option
-   Add better dp\_option tests
-   Add terminator for sdap\_attr\_map
-   Add better tests for sdap\_attr compability
-   Remove old compatibility tests
-   Fix building manpages in parallel build dirs
-   Clean up log messages about keytab\_name
-   MAN: Improve ldap\_disable\_paging documentation
-   MAN: Add ldap\_sasl\_minssf to the manpage
-   Fix linker issue with pam\_sss
-   murmurhash: Relax inline requirement
-   Handle endianness issues on older systems
-   SYSDB: Handle upgrade script failures better
-   LDAP: Add objectSID config option
-   LDAP: Add id-mapping option
-   SYSDB: Add sysdb routines for ID-mapping
-   LDAP: Add helper routines for ID-mapping
-   LDAP: Add ID mapping range settings
-   LDAP: Initialize ID mapping when configured
-   LDAP: Enable looking up ID-mapped users by name
-   LDAP: Add autorid compatibility mode
-   LDAP: Allow setting a default domain for id-mapping slice 0
-   LDAP: Add routine to extract domain SID from an object SID
-   LDAP: Allow automatically-provisioning a domain and range
-   LDAP: Enable looking up id-mapped users by UID
-   LDAP: Allow looking up ID-mapped groups by name
-   LDAP: Enable looking up id-mapped groups by GID
-   LDAP: Map the user's primaryGroupID
-   LDAP: Add helper routine to convert LDAP blob to SID string
-   LDAP: Do not remove uidNumber and gidNumber attributes when saving
    id-mapped entries
-   LDAP: Add helper function to map IDs
-   LDAP: Treat groups with unmappable SIDs as non-POSIX groups
-   MAN: Add manpage for ID mapping
-   LDAP: Add support for enumeration of ID-mapped users and groups
-   SSSDConfigAPI: Fix missing option in tests
-   NSS: Add fallback\_homedir option
-   NSS: Add default\_shell option
-   SYSDB: Add better error logging to sysdb\_set\_entry\_attr()
-   LDAP: Add attr\_count return value to build\_attrs\_from\_map()
-   LDAP: Handle very large Active Directory groups
-   Updating translations for 1.9.0 beta 1 release
-   Bumping version to 1.8.91 for 1.9.0 beta 1 release
-   Bumping version ton 1.8.92 for beta 2 development
-   RPM: Allow running 'make rpms' on RHEL 5 machines
-   NSS: Expire in-memory netgroup cache before the nowait timeout
-   Always use positional arguments in translatable strings
-   KRB5: Avoid NULL-dereference with empty keytab
-   Update translation sources
-   NSS: Fix segfault when mmap cache cannot be initialized
-   NSS: Restore original protocol for getservbyport
-   SSSDConfig: Make SSSDConfig a package
-   SSSDConfig: Make default config and schema file locations
    configurable
-   PAM: Better pam\_reply message
-   SYSDB: Reduce noise level of debug messages in lookups
-   LDAP: Remove redundant check
-   LDAP: Fix incorrect switch statement in sdap\_get\_initgr\_done()
-   LDAP: Add helper function to get list of a user's groups from sysdb
-   LDAP: Make sdap\_initgr\_common\_store() non-static
-   LDAP: Add ldap\_\*\_use\_matching\_rule\_in\_chain options
-   LDAP: Add support for AD chain matching extension in group lookups
-   LDAP: Add support for AD chain matching extension in initgroups
-   LDAP: Auto-detect support for the ldap match rule
-   LDAP: Fix missing variable in debug message
-   SSS\_CLIENT: Fix uninitialized value error
-   Fix compilation on older little-endian systems
-   KRB5: Update DEBUG macros for create\_ccache\_dir and
    find\_ccdir\_parent\_data
-   KRB5: Auto-detect DIR cache support in configure
-   KRB5: Avoid shadowing dirname
-   Updating translations for 1.9.0 beta 2 release
-   Bumping version to 1.9.0 beta 3
-   Fix typo breaking DIR cache detection
-   Make the client idle timeout configurable
-   UTILS: Fix segfault due to sss\_parse\_name\_for\_domains
-   BUILD: Change default unicode library to glib2
-   Update translations for 1.9.0 beta 3 release
-   Bumping version to 1.9.0 beta 4
-   TESTS: Print messages when LDAP options do not match
-   DEBUG: Log to syslog if we are unable to open a debug fd
-   KRB5: Initialize the credential cache type properly
-   IPA: Don't hang onto memory longer than necessary
-   LDAP: Print extended failure message for SASL bind
-   MAN: Unify "SEE ALSO" sections
-   KRB5: Some logging enhancements for krb5\_child
-   KRB5\_LOCATOR: Print the filename that couldn't be opened
-   KRB5: Drop memctx parameter of krb5\_try\_kdcip
-   KRB5: Create a common init routine for krb5\_child options
-   LDAP: Rename user and group maps for AD
-   AD: Add AD identity provider
-   AD: Add AD auth and chpass providers
-   AD: Add AD access-control provider
-   AD: Add AD provider to the spec file
-   AD: use krb5\_keytab for validation and GSSAPI
-   AD: Add manpages and SSSDConfig entries
-   CONFDB: Add the ability to set a boolean value in the confdb
-   AD: Force case-insensitive operation in AD provider
-   Fix use-after-free
-   Fix uninitialized variable
-   Fix potential NULL-dereference
-   Fix potential NULL-dereference
-   Fix incorrect return value in tests
-   Fix potential NULL-dereference
-   Fix uninitialized value return
-   Fix uninitialized memcpy error
-   Avoid NULL-dereference in error-handling
-   Add missing return value check
-   Check for errors from krb5\_unparse\_name
-   Fix incorrect error-check
-   Fix segfault when using local provider
-   AD: Add missing DP option terminator
-   AD: Fix defaults for krb5\_canonicalize
-   MAN: List all available backends for provider options
-   MAN: Improvements to the AD provider manpage
-   NSS: Add override\_shell option
-   SYSDB: Add log message for unexpected LDB errors
-   SSSDConfig: Fix nonfunctional SSSDDomain.remove\_provider()
-   IPA: Do not attempt to close the same file twice
-   IPA: Securely set umask for mkstemp in subdomain provider
-   MAN: Fix minor typo in ldap\_search\_base section
-   MAN: Improve description of ldap\_\*\_search\_base options
-   SYSDB: Make sysdb\_attrs\_get\_el\_int() public
-   AD: autorid compatibility should recommend the use of default domain
-   AD: Detect domain controller compatibility version
-   AD: Optimize initgroups lookups with tokenGroups
-   AD: Handle sysdb lookup failure during tokenGroups processing

Sumit Bose (40):

-   Use curly braces in pkgconfig metadata file
-   Keep sysdb context in domain info struct
-   Remove sysdb\_get\_ctx\_from\_list()
-   Always initialize the returned data in sss\_krb5\_princ\_realm()
-   Add idmap library
-   Check sub-domains in nss\_cmd\_get{pwuid|grgid}\_search()
-   data provider: added subdomains
-   IPA: Add get-domains target
-   Add domain name to get\_account\_info request
-   Add s2n extended operation
-   Allow different SID representations in libidmap
-   Fix typo in spec file
-   Fix endian issue in SID conversion
-   Rename struct dom\_sid to struct sss\_dom\_sid
-   Fix libsss\_hbac library version
-   sss\_idmap: add support for samba struct dom\_sid
-   sss\_idmap: fix typo which prevents sub auth larger then 2^31^
-   PAC responder: add basic infrastructure
-   PAC responder: add the core functionality
-   PAC responder: support in spec file
-   PAC client: add basic support in common client code
-   PAC client: add krb5 authdata plugin
-   Add support for ID ranges
-   Add range support to PAC responder
-   Try to build PAC responder only if all dependencies are available
-   Build pac responder tests only if pac responder is build
-   Add man page section for the PAC responder
-   Set default for subdomain\_homedir
-   Fix SSSDConfigTest for separate build directories
-   Set file descriptor limits in pac responder
-   Remove resource leak in sssdpac\_import\_authdata
-   Remove dead code in ipa\_subdomains\_handler\_done()
-   pac responder: limit access by checking UIDs
-   Add python bindings for murmurhash3
-   accept\_fd\_handler: add missing return
-   Fix fallback in validate\_tgt()
-   Use new debug levels in validate\_tgt()
-   Check flat names when searching for sub-domains as well
-   Add provider specific default regular expressions
-   Make subdomain discovery less noisy

Ville Skyttä (1):

-   Require and call ldconfig from subpackages if appropriate

Yuri Chornoivan (5):

-   fix typos in manual
-   Fix typo: retreiving-&gt;retrieving
-   Fix typos in message and man pages.
-   Fix typo: exhasution-&gt;exhaustion.
-   Fix various typos in documentation.

