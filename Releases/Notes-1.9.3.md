Highlights {#Highlights}
----------

-   This release focused mainly on fixing regressions compared to the
    1.8 series and bugfixes for features introduced in the 1.9 release
    cycle
-   Many fixes related to deployments where the SSSD is running as a
    client of IPA server with trust relation established with an Active
    Directory server
-   Multiple fixes related to correct reporting of group memberships,
    especially in setups that use nested groups
-   Fixed a bug that prevented upgrade from the 1.8 series if the cache
    contained nested groups before the upgrade
-   Restarting the responders is more robust for cases where the machine
    is under heavy load during back end restart
-   The default\_shell option can now be also set per-domain in addition
    to global setting

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1345](/sssd/ticket/1345 "sssd does not warn into sssd.log for broken configurations"){.closed}
:   sssd does not warn into sssd.log for broken configurations

[\#1357](/sssd/ticket/1357 "Init script reports complete before sssd is actually working"){.closed}
:   Init script reports complete before sssd is actually working

[\#1437](/sssd/ticket/1437 "upstream spec should use systemd where available"){.closed}
:   upstream spec should use systemd where available

[\#1482](/sssd/ticket/1482 ""fullName" in sysdb doesn't match with the "name" ldap attribute on AD ..."){.closed}
:   "fullName" in sysdb doesn't match with the "name" ldap attribute on
    AD Server

[\#1528](/sssd/ticket/1528 "SSSD_NSS failure to gracefully restart after sbus failure"){.closed}
:   SSSD\_NSS failure to gracefully restart after sbus failure

[\#1581](/sssd/ticket/1581 "sssd_be crashes while looking up users"){.closed}
:   sssd\_be crashes while looking up users

[\#1583](/sssd/ticket/1583 "Allow setting the default_shell per-domain"){.closed}
:   Allow setting the default\_shell per-domain

[\#1584](/sssd/ticket/1584 "invalidating the memcache with sss_cache doesn't work if the sssd is not ..."){.closed}
:   invalidating the memcache with sss\_cache doesn't work if the sssd
    is not running

[\#1589](/sssd/ticket/1589 "sss_cache says 'Wrong DB version'"){.closed}
:   sss\_cache says 'Wrong DB version'

[\#1590](/sssd/ticket/1590 "sssd does not resolve group names from AD"){.closed}
:   sssd does not resolve group names from AD

[\#1593](/sssd/ticket/1593 "Silence the DEBUG messages when ID mapping code skips a built-in group"){.closed}
:   Silence the DEBUG messages when ID mapping code skips a built-in
    group

[\#1594](/sssd/ticket/1594 "ldap_child crashes on using invalid keytab during gssapi connection"){.closed}
:   ldap\_child crashes on using invalid keytab during gssapi connection

[\#1595](/sssd/ticket/1595 "Password authentication with users coming via AD trust"){.closed}
:   Password authentication with users coming via AD trust

[\#1596](/sssd/ticket/1596 "Sudo smart refresh doesn't occur on time"){.closed}
:   Sudo smart refresh doesn't occur on time

[\#1600](/sssd/ticket/1600 "The sssd_nss process grows the memory consumption over time"){.closed}
:   The sssd\_nss process grows the memory consumption over time

[\#1601](/sssd/ticket/1601 "A wrong callback used causes getgrgid to not work for trusted domains"){.closed}
:   A wrong callback used causes getgrgid to not work for trusted
    domains

[\#1602](/sssd/ticket/1602 "provider is forcibly killed with SIGKILL instead of SIGTERM if it's not ..."){.closed}
:   provider is forcibly killed with SIGKILL instead of SIGTERM if it's
    not responding

[\#1604](/sssd/ticket/1604 "sssd not granting access for AD trusted user in HBAC rule"){.closed}
:   sssd not granting access for AD trusted user in HBAC rule

[\#1606](/sssd/ticket/1606 "SSSD starts multiple processes due to syntax error in ldap_uri"){.closed}
:   SSSD starts multiple processes due to syntax error in ldap\_uri

[\#1608](/sssd/ticket/1608 "sss_cache: Multiple domains not handled properly"){.closed}
:   sss\_cache: Multiple domains not handled properly

[\#1610](/sssd/ticket/1610 "subdomains: Invalid sub-domain request type."){.closed}
:   subdomains: Invalid sub-domain request type.

[\#1611](/sssd/ticket/1611 "authconfig chokes on sssd.conf with chpass_provider directive"){.closed}
:   authconfig chokes on sssd.conf with chpass\_provider directive

[\#1612](/sssd/ticket/1612 "Nested groups are not retrieved appropriately from cache"){.closed}
:   Nested groups are not retrieved appropriately from cache

[\#1613](/sssd/ticket/1613 "ipa client setup should configure host properly in a trust is in place"){.closed}
:   ipa client setup should configure host properly in a trust is in
    place

[\#1614](/sssd/ticket/1614 "User appears twice on looking up a nested group"){.closed}
:   User appears twice on looking up a nested group

[\#1615](/sssd/ticket/1615 "IPA client cannot change AD Trusted User password"){.closed}
:   IPA client cannot change AD Trusted User password

[\#1616](/sssd/ticket/1616 "sudo failing for ad trusted user in IPA environment"){.closed}
:   sudo failing for ad trusted user in IPA environment

[\#1619](/sssd/ticket/1619 "pam: fd leak when writing the selinux login file in the pam responder"){.closed}
:   pam: fd leak when writing the selinux login file in the pam
    responder

[\#1623](/sssd/ticket/1623 "Man page issue to list  'force_timeout' as an option for the [sssd] ..."){.closed}
:   Man page issue to list 'force\_timeout' as an option for the
    \[sssd\] section

[\#1628](/sssd/ticket/1628 "user id lookup fails using proxy provider"){.closed}
:   user id lookup fails using proxy provider

[\#1629](/sssd/ticket/1629 "subdomains code does not save the proper user/group name"){.closed}
:   subdomains code does not save the proper user/group name

[\#1631](/sssd/ticket/1631 "sysdb upgrade failed converting db to 0.11"){.closed}
:   sysdb upgrade failed converting db to 0.11

[\#1636](/sssd/ticket/1636 "offline authentication failure always returns System Error"){.closed}
:   offline authentication failure always returns System Error

[\#1638](/sssd/ticket/1638 "password expiry warning message doesn't appear during auth"){.closed}
:   password expiry warning message doesn't appear during auth

[\#1640](/sssd/ticket/1640 ""defaults" entry ignored"){.closed}
:   "defaults" entry ignored

[\#1647](/sssd/ticket/1647 "LDAP provider fails to save empty groups"){.closed}
:   LDAP provider fails to save empty groups

[\#1649](/sssd/ticket/1649 "ldap_connection_expire_timeout doesn't expire ldap connections"){.closed}
:   ldap\_connection\_expire\_timeout doesn't expire ldap connections

[\#1650](/sssd/ticket/1650 "Wrong variable check in sudosrv_parse_query_send"){.closed}
:   Wrong variable check in sudosrv\_parse\_query\_send

[\#1651](/sssd/ticket/1651 "Unchecked return value from waitpid()"){.closed}
:   Unchecked return value from waitpid()

[\#1652](/sssd/ticket/1652 "updating top-level group does not reflect ghost members correctly"){.closed}
:   updating top-level group does not reflect ghost members correctly

[\#1657](/sssd/ticket/1657 "SIGSEGV in IPA provider when ldap_sasl_authid is not set"){.closed}
:   SIGSEGV in IPA provider when ldap\_sasl\_authid is not set

[\#1658](/sssd/ticket/1658 "ipa password auth failing for user principal name when shorter than IPA ..."){.closed}
:   ipa password auth failing for user principal name when shorter than
    IPA Realm name

[\#1661](/sssd/ticket/1661 "Allow backward compatible regex for domain / realm search in sssd 1.9"){.closed}
:   Allow backward compatible regex for domain / realm search in sssd
    1.9

[\#1668](/sssd/ticket/1668 "delete operation is not implemented for ghost users"){.closed}
:   delete operation is not implemented for ghost users

[\#1669](/sssd/ticket/1669 "sssd hangs at startup with broken configurations"){.closed}
:   sssd hangs at startup with broken configurations

[\#1671](/sssd/ticket/1671 "mmap cache needs update after db changes"){.closed}
:   mmap cache needs update after db changes

[\#1674](/sssd/ticket/1674 "Explicit null dereferenced"){.closed}
:   Explicit null dereferenced

[\#1675](/sssd/ticket/1675 "SSSD crashes when c-ares returns success but an empty hostent during the ..."){.closed}
:   SSSD crashes when c-ares returns success but an empty hostent during
    the DNS update

[\#1683](/sssd/ticket/1683 "arithmetic bug in the SSSD causes netgroup midpoint refresh to be always ..."){.closed}
:   arithmetic bug in the SSSD causes netgroup midpoint refresh to be
    always set to 10 seconds

[\#1684](/sssd/ticket/1684 "Dereference after null check in sss_idmap_sid_to_unix"){.closed}
:   Dereference after null check in sss\_idmap\_sid\_to\_unix

[\#1686](/sssd/ticket/1686 "sssd crashes during start if id_provider is not mentioned"){.closed}
:   sssd crashes during start if id\_provider is not mentioned

[\#1688](/sssd/ticket/1688 "sssd_sudo prints wrong debug message when notBefore or notAfter attribute ..."){.closed}
:   sssd\_sudo prints wrong debug message when notBefore or notAfter
    attribute is missing

[\#1695](/sssd/ticket/1695 "user is not removed from group membership during initgroups"){.closed}
:   user is not removed from group membership during initgroups

</div>

Packaging Changes {#PackagingChanges}
-----------------

-   The sss\_cache has been moved from sss-tools subpackage to the main
    sssd package
-   The upstream RPM uses a systemd unit file by default, rather than a
    SystemV init script
-   Several rpmlint warnings have been fixed in the upstream spec file

Detailed Changelog {#DetailedChangelog}
------------------

Ariel O. Barria (1):

-   Monitor quit when not exists no process no stops

Jakub Hrozek (42):

-   Updating the version for the 1.9.3 release
-   LDAP: Check validity of naming\_context
-   Allow setting the default\_shell option per-domain as well
-   KRB5: Return error when principal selection fails
-   Free the internal DP request
-   LDAP: Fix off-by-one error when saving ghost users
-   Monitor: read the correct SIGKILL timeout for providers, too
-   PAM: Do not leak fd after SELinux context file is written
-   Do not always return PAM\_SYSTEM\_ERR when offline krb5
    authentication fails
-   KRB5: Rename variable to avoid shadowing a global declaration
-   Only build extract\_and\_send\_pac on platforms that support it
-   Include the auth\_utils.h header in the distribution
-   SYSDB: Do not touch the member attribute during conversion to ghost
    users
-   Provide AM\_COND\_IF-combatible implementation for old automake
    systems
-   LDAP: Expire even non authenticated connections
-   SUDO: Fix wrong variable check
-   SERVER: Check the return value of waitpid
-   LDAP: Allocate the temporary context on NULL, not memctx
-   LDAP: Fix saving empty groups
-   LDAP: use the correct memory context
-   LDAP: Refactor saving ghost users
-   Restart services with a delay in case they are restarted too often
-   MAN: document the ldap\_sasl\_realm option
-   LDAP: Provide a common sdap\_set\_sasl\_options init function
-   LDAP: Checking the principal should not be considered fatal
-   LDAP: Make it possible to use full principal in ldap\_sasl\_authid
    again
-   SYSDB: Use the add\_string convenience functions for managing ghost
    user attribute
-   LDAP: Only convert direct parents' ghost attribute to member
-   MONITOR: Fix off-by-one error in add\_string\_to\_list
-   Handle compiling FQDN regular expression with old pcre gracefully
-   MEMBEROF: Do not add the ghost attribute to self
-   TESTS: Test ghosts users in the RFC2307 schema
-   NSS: Fix netgroup midpoint cache refresh
-   LDAP: Continue adjusting group membership even if there is nothing
    to add
-   MEMBEROF: Implement delete operation for ghost users
-   MEMBEROF: split processing the member modify into a separate
    function
-   MEMBEROF: Split the del ghost attribute op into a reusable function
-   MEMBEROF: Split the add ghost operation into a separate function
-   MEMBEROF: Implement the modify operation for ghost users
-   MEMBEROF: Keep inherited ghost users around on modify operation
-   RESOLV: return ENOENT if the address list is empty
-   Updating the translations for the 1.9.3 release

Jan Cholasta (3):

-   Use systemd by default on Fedora 16+
-   Fix errors reported by rpmlint
-   MAN: Move ssh\_known\_hosts\_timeout documentation to the correct
    section

Michal Zidek (11):

-   sss\_cache: Multiple domains not handled properly
-   util: Added new file util\_lock.c
-   sss\_cache: Remove fastcache even if sssd is not running.
-   util\_lock.c: sss\_br\_lock\_file accepted invalid parameter value
-   debug: print fatal and critical errors if debug level is unresolved
-   sss\_cache: Small refactor.
-   Uninitialized pointer read
-   idmap: Silence DEBUG messages when dealing with built-in SIDs.
-   Null pointer dereferenced.
-   Dereference after null check in sss\_idmap\_sid\_to\_unix
-   Missing parameter in DEBUG message.

Ondrej Kos (4):

-   MAN: sssd-simple - suggest awarness of empty rules
-   Display more information on DB version crash
-   LDAP: fix uninitialized variable
-   SYSDB: Don't operate with aliases same as name

Pavel Březina (23):

-   sudo: do not fail if usn value is zero but full refresh is completed
-   sudo refresh: handle errors properly
-   authconfig: allow chpass\_provider = proxy
-   add SSSDBG\_IMPORTANT\_INFO macro
-   fix indendation, coding style and debug levels in server.c
-   make monitor\_quit() usable outside signal handler
-   exit original process after sssd is initialized
-   create pid file immediately after fork again
-   do not default fullname to gecos when schema = ad
-   sss\_dp\_get\_domains\_send(): handle subreq error correctly
-   subdomains: check request type on one place only
-   backend: add PAC to the list of known clients
-   sudo: fix missing parameter in two debug messages
-   use tmp\_ctx in sudosrv\_get\_sudorules\_from\_cache()
-   sudo: support users from subdomains
-   sudo: do not send domain name with username
-   sudo: print how many rules we are refreshing or returning
-   sudo: store rules with no sudoHost attribute
-   fix SIGSEGV in IPA provider when ldap\_sasl\_authid is not set
-   avoid versioning libsss\_sudo
-   warn user if password is about to expire
-   do not crash when id\_provider is not set
-   sudo: print rule name if notBefore or notAfter attribute is missing

Simo Sorce (9):

-   Simplify writing db update functions
-   Refactor the way subdomain accounts are saved
-   Handle conversion to fully qualified usernames
-   mmap cache: public functions to invalidate records
-   Hook to perform a mmap cache update from sssd\_nss
-   Hook for mmap cache update on initgroup calls
-   Add backchannel NSS provider query on initgr calls
-   Always append rctx as private data
-   Add memory barrier to mmap cache client code loop

Stephen Gallagher (9):

-   LDAP: Better debug logging when saving groups
-   RPMS: Move sss\_cache tool to main package
-   Monitor: Better debugging for ping timeouts
-   MAN: Specify the correct location for the force\_timeout option
-   SSSDConfig: Locate the force\_timeout option in the correct sections
-   MAN: Fix validation error caused by bad 'ca' translation
-   SUDO: Remove unused variable
-   BUILD: Temporary workaround for Kerberos build
-   IPA: Handle bad results from c-ares lookup

Sumit Bose (34):

-   Fix two errors in the nss responder
-   subdomain-id: Generate homedir only for users not groups
-   pac responder: fix copy-and-paste error
-   sysdb: look for ranges in the parent tree
-   pac responder: use only lower case user name
-   pac responder: add user principal and name alias to cached user
    object
-   krb5\_auth\_send: check for sub-domains
-   sysdb: add sysdb\_base\_dn()
-   check\_ccache\_files: search sub-domains as well
-   Add replacement for krb5\_find\_authdata()
-   krb5\_auth: check if principal belongs to a different realm
-   krb5\_auth: send different\_realm flag to krb5\_child
-   krb5\_child: send PAC to PAC responder
-   krb5\_mod\_ccname: replace wrong memory context
-   krb5\_child: send back the client principal
-   Add new call find\_or\_guess\_upn()
-   Use find\_or\_guess\_upn() where needed
-   krb5\_auth: update with correct UPN if needed
-   sss\_parse\_name\_for\_domains: always return the canonical domain
    name
-   Make sub-domains case-insensitive
-   Clarify debug message about initgroups and subdomains
-   Do not remove a group if it has members from subdomains
-   Add diff\_gid\_lists() with test
-   Add pac\_user\_get\_grp\_info() to read current group memberships
-   Get lists of GIDs to be added and deleted and use them
-   Store the original group DN in the subdomain user object
-   Add string\_in\_list() and add\_string\_to\_list() with tests
-   Always start PAC responder if IPA ID provider is configured
-   Run IPA subdomain provider if IPA ID provider is configured
-   Do not save HBAC rules in subdomain subtree
-   Just use the service name with krb5\_get\_init\_creds\_password()
-   Fix compare\_principal\_realm() check
-   Disable canonicalization during password changes
-   KRB5: Work around const warning for krb5 releases older than 1.11

Timo Aaltonen (1):

-   link sss\_ssh\_authorizedkeys and sss\_ssh\_knownhostsproxy with
    -lpthread

