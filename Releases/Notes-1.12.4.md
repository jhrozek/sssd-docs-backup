Highlights {#Highlights}
----------

-   This is mostly a bug fixing release with only minor enhancements
    visible to the end user
-   Contains many fixes and enhancements related to the ID views
    functionality of FreeIPA servers
-   Several fixes related to retrieving AD group membership in an IPA-AD
    trust scenario
-   Fixes a bug where the GPO access control previously didn't work at
    all if debugging was enabled in smb.conf.
-   SSSD can now be pinned to a particular AD site instead of
    autodiscovering the site
-   A regression that caused setting the SELinux context for IPA users
    to fail, was fixed
-   Fixed a potential crash caused by a double-free error when an SSSD
    service was killed by the monitor process

Packaging Changes {#PackagingChanges}
-----------------

-   Several patches that allow building the Python code in SSSD with
    python3 were merged

Documentation Changes {#DocumentationChanges}
---------------------

-   A new option `ad_site` was added. When this option is set, SSSD will
    attempt to connect to DCs from this particular AD site instead of
    looking up the site via DNS
-   The `ad_gpo_map_permit` option now also includes the `systemd-user`
    service to avoid errors in processing of the PAM session stack

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1991](/sssd/ticket/1991 "Make return codes of basic sysdb operations consistent"){.closed}
:   Make return codes of basic sysdb operations consistent

[\#2203](/sssd/ticket/2203 "Write message to syslog about users with duplicated UID"){.closed}
:   Write message to syslog about users with duplicated UID

[\#2376](/sssd/ticket/2376 "Investigate Kerberized NFS4 setup with the new NFS plugin"){.closed}
:   Investigate Kerberized NFS4 setup with the new NFS plugin

[\#2486](/sssd/ticket/2486 "[RFE] ad provider dns_discovery_domain option: kerberos discovery is not ..."){.closed}
:   \[RFE\] ad provider dns\_discovery\_domain option: kerberos
    discovery is not using this option

[\#2515](/sssd/ticket/2515 "sssd-ad: The man page description to enable GPO HBAC Policies are unclear"){.closed}
:   sssd-ad: The man page description to enable GPO HBAC Policies are
    unclear

[\#2527](/sssd/ticket/2527 "sssd.conf(5) man page gives bad advice about domains parameter"){.closed}
:   sssd.conf(5) man page gives bad advice about domains parameter

[\#2531](/sssd/ticket/2531 "sssd_be crashes in nested LDAP code with a use-after-free error"){.closed}
:   sssd\_be crashes in nested LDAP code with a use-after-free error

[\#2542](/sssd/ticket/2542 "GPO offline processing rejects access if no applicable GPOs are find in ..."){.closed}
:   GPO offline processing rejects access if no applicable GPOs are find
    in the cache

[\#2543](/sssd/ticket/2543 "GPO code fails if no LDAP URI can be resolved"){.closed}
:   GPO code fails if no LDAP URI can be resolved

[\#2544](/sssd/ticket/2544 "GPO: libsmbclient logs to stdout by default, cluttering gpo_child output"){.closed}
:   GPO: libsmbclient logs to stdout by default, cluttering gpo\_child
    output

[\#2547](/sssd/ticket/2547 "gzip: stdin: file size changed while zipping when rotating logfile"){.closed}
:   gzip: stdin: file size changed while zipping when rotating logfile

[\#2548](/sssd/ticket/2548 "Document that dyndns_iface only supports a single interface"){.closed}
:   Document that dyndns\_iface only supports a single interface

[\#2550](/sssd/ticket/2550 "libsss_simpleifp should pull sssd-dbus"){.closed}
:   libsss\_simpleifp should pull sssd-dbus

[\#2556](/sssd/ticket/2556 "add systemd-user to default gpo list"){.closed}
:   add systemd-user to default gpo list

[\#2557](/sssd/ticket/2557 "pam_sss(sshd:auth): authentication failure with user from AD"){.closed}
:   pam\_sss(sshd:auth): authentication failure with user from AD

[\#2559](/sssd/ticket/2559 "PAC responder is called after krb5_child switches to the user logging in"){.closed}
:   PAC responder is called after krb5\_child switches to the user
    logging in

[\#2560](/sssd/ticket/2560 "Users saved throug extop don't have the originalMemberOf attribute"){.closed}
:   Users saved throug extop don't have the originalMemberOf attribute

[\#2563](/sssd/ticket/2563 "Need to set different umask in selinux_child"){.closed}
:   Need to set different umask in selinux\_child

[\#2564](/sssd/ticket/2564 "selinux_child needs to setuid(0) to make libselinux work as non-root"){.closed}
:   selinux\_child needs to setuid(0) to make libselinux work as
    non-root

[\#2566](/sssd/ticket/2566 "Uncached SIDs cannot be resolved"){.closed}
:   Uncached SIDs cannot be resolved

[\#2567](/sssd/ticket/2567 "Same member saved as ghost and as member in IPA server mode"){.closed}
:   Same member saved as ghost and as member in IPA server mode

[\#2571](/sssd/ticket/2571 "IPA initgroups don't work correctly in non-default view"){.closed}
:   IPA initgroups don't work correctly in non-default view

[\#2572](/sssd/ticket/2572 "[abrt] sssd-common: talloc_abort(): sssd killed by SIGABRT"){.closed}
:   \[abrt\] sssd-common: talloc\_abort(): sssd killed by SIGABRT

[\#2586](/sssd/ticket/2586 "user_attributes missing from ifp schema"){.closed}
:   user\_attributes missing from ifp schema

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Bohuslav Kabrda (1):

-   Python3 support in SSSD

Jakub Hrozek (23):

-   Updating the version to the 1.12.4 release
-   GPO: Ignore ENOENT result from
    sysdb\_gpo\_get\_gpo\_result\_setting()
-   TESTS: Cover sysdb\_gpo.c with unit tests
-   GPO: Set libsmb debugging to stderr
-   UTIL: Allow dup-ing child pipe to a different FD
-   GPO: Don't use stdout for output in gpo\_child
-   GPO: Extract server hostname after connecting
-   krb5\_child: Return ERR\_NETWORK\_IO on KRB5\_KDCREP\_SKEW
-   Open the PAC socket from krb5\_child before dropping root
-   IPA: Use attr's dom for users, too
-   SELINUX: Call setuid(0)/setgid(0) to also set the real IDs to root
-   SELINUX: Set and reset umask when caling set\_seuser from deamon
    code
-   LDAP: Add UUID when saving incomplete groups
-   IPA: Resolve IPA user groups' overrideDN in non-default view
-   LDAP: Rename the \_res output parameter to avoid clashing with
    libresolv in tests
-   RESOLV: Add an internal function to read TTL from a DNS packet
-   resolv: Fix a typo
-   SELINUX: Check the return value of setuid and setgid
-   BUILD: Include python-test.py in the tarball
-   GPO: Better debugging for gpo\_child's mkdir
-   LDAP: Add better DEBUG messages to the cleanup task
-   LDAP: Handle ENOENT better in the cleanup task
-   Updating translations for the 1.12.4 release

Lukas Slebodnik (11):

-   logrotate: Fix warning file size changed while zipping
-   PROXY: Fix use after free
-   pysss: Fix double free
-   MONITOR: Fix double free
-   SSSDConfig: Remove unused exception name
-   SSSDConfig: Port missing parts to python3
-   Remove strict requirements of python2
-   sbus\_codegen: Port to python3
-   Add missing new lines to debug messages
-   CONFIGURE: Do not use macro AC\_PROG\_MKDIR\_P twice
-   RESPONDERS: Warn to syslog about colliding objects

Pavel Březina (1):

-   spec: sifp requires sssd-dbus

Pavel Reichl (6):

-   GPO: add systemd-user to gpo default permit list
-   MAN: dyndns\_iface supports only one interface
-   MAN: add dots as valid character in domain names
-   AD: add new option ad\_site
-   AD: support for AD site override
-   MAN: amend sss\_ssh\_authorizedkeys

Rob Crittenden (1):

-   Add user\_attributes to ifp section of API schema

Sumit Bose (24):

-   IPA: add get\_be\_acct\_req\_for\_user\_name()
-   IPA: resolve ghost members if a non-default view is applied
-   sysdb: fix group members with overridden names
-   IPA: ipa\_resolve\_user\_list\_send() take care of overrides
-   IPA: do not look up overrides on client with default view
-   IPA: make version check more precise
-   IPA: add missing break
-   IPA: process\_members() optionally return missing members list
-   IPA: rename ipa\_s2n\_get\_groups\_send() to
    ipa\_s2n\_get\_fqlist\_send()
-   IPA: resolve missing members
-   IPA: set SYSDB\_INITGR\_EXPIRE for RESP\_USER\_GROUPLIST
-   krb5: fix entry order in MEMORY keytab
-   nss: make fill\_orig() multi-value aware
-   nss: refactor fill\_orig()
-   nss: Add original DN and memberOf to origbyname request
-   views: fix GID overrride for mpg domains
-   IPA: properly handle mixed-case trusted domains
-   nss: fix SID lookups
-   sysdb: remove ghosts in all sub-domains as well
-   IPA: resolve IPA group-memberships for AD users
-   IPA: process\_members() add ghosts only once
-   ipa\_s2n\_save\_objects: properly handle fully-qualified group names
-   AD: use GC for SID requests as well
-   fill\_id() fix LE/BE issue with wrong data type

