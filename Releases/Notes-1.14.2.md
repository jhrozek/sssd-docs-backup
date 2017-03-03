Highlights {#Highlights}
----------

-   Several more regressions caused by cache refactoring to use
    qualified names internally were fixed, including a regression that
    prevented the `krb5_map_user` option from working correctly.
-   A regression when logging in with a smart card using the GDM login
    manager was fixed
-   SSSD now removes the internal timestamp on startup cache when the
    persistent cache is removed. This enables admins to follow their
    existing workflow of just removing the persistent cache and start
    from a fresh slate
-   Several fixes to the sssd-secrets responder are present in this
    release
-   A bug in the autofs responder that prevented automounter maps from
    being returned when sssd\_be was offline was fixed
-   A similar bug in the NSS responder that prevented netgroups from
    being returned when sssd\_be was offline was fixed
-   Disabling the netlink integration can now be done with a new option
    `disable_netlink`. Previously, the netlink integration could be
    disabled with a sssd command line switch, which is being deprecated
    in this release.
-   The internal watchdog no longer kills sssd processes in case time
    shifts during sssd runtime
-   The fail over code is able to cope with concurrent SRV resolution
    requests better in this release
-   The proxy provider gained a new option `proxy_max_children` that
    allows the administrator to control the maximum number of child
    helper processes that authenticate users with `auth_provider=proxy`
-   The InfoPipe D-Bus responder exports the UUIDs of user and group
    objects through a uniqueID property

Packaging Changes {#PackagingChanges}
-----------------

-   The private pipe directory permissions were changed from 0700
    to 0750. The restrictive permissions we causing SELinux
    `dac_override` denials
-   The Python packages for python2 were renamed from python-package to
    python2-package with backwards-compatible Provides and Obsoletes
-   The sssd-common subpackage contains a new manual page
    `sssd-secrets(5)`
-   The sssd-tools subpackage explicitly Requires `/sbin/service` on
    platforms that don't support systemd in order to be able to restart
    sssd from the `sssctl` tool

Documentation Changes {#DocumentationChanges}
---------------------

-   The `kill_service` option that was no longer useful after we moved
    from in-process pings to watchdog was removed
-   The `--disable-netlink` `sssd(8)` command-line option was removed in
    favor of `[sssd]` section option `disable_netlink`
-   The `proxy_max_children` option was added. Please see the highlights
    section for more details.
-   The `sssd-secrets` responder gained a man page in this release.
-   Two new options `containers_nest_level` and `max_secrets` options
    were added to the `sssd-secrets` responder. The former allows the
    administrator to configure the maximum nesting level of secrets
    containers, the latter allows the administrator to configure the
    maximum number of secrets that can be stored. Please note that both
    option apply to the local secrets provider only.
-   The `sssd-ldap` man page didn't specify different default for user
    and group name LDAP attribute default for the AD provider. This
    documentation bug was fixed.

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#2813](/sssd/ticket/2813 "man page for sss_override command provides irrelevant information for ..."){.closed}
:   man page for sss\_override command provides irrelevant information
    for --debug option

[\#2841](/sssd/ticket/2841 "sssd stores and returns incorrect information about empty netgroup ..."){.closed}
:   sssd stores and returns incorrect information about empty netgroup
    (ldap-server: 389-ds)

[\#3051](/sssd/ticket/3051 "Move the diag_cmd option so that it's usable by the watchdog."){.closed}
:   Move the diag\_cmd option so that it's usable by the watchdog.

[\#3052](/sssd/ticket/3052 "Remove the no longer used kill_service command"){.closed}
:   Remove the no longer used kill\_service command

[\#3053](/sssd/ticket/3053 "The sssd-secrets responder needs a manpage"){.closed}
:   The sssd-secrets responder needs a manpage

[\#3054](/sssd/ticket/3054 "Create integration tests for the sssd-secrets responder"){.closed}
:   Create integration tests for the sssd-secrets responder

[\#3056](/sssd/ticket/3056 "The sssctl tool should restart the service with systemd's dbus API"){.closed}
:   The sssctl tool should restart the service with systemd's dbus API

[\#3107](/sssd/ticket/3107 "Python SSSD Config API deletes an item during iteration"){.closed}
:   Python SSSD Config API deletes an item during iteration

[\#3123](/sssd/ticket/3123 "Netgroup resolution doesn't work offline"){.closed}
:   Netgroup resolution doesn't work offline

[\#3125](/sssd/ticket/3125 "secrets responder throws an internal error when trying to delete a ..."){.closed}
:   secrets responder throws an internal error when trying to delete a
    non-existent secret

[\#3127](/sssd/ticket/3127 "SSSD qualifies principal twice in IPA-AD trust if the principal attribute ..."){.closed}
:   SSSD qualifies principal twice in IPA-AD trust if the principal
    attribute doesn't exist on the AD side

[\#3128](/sssd/ticket/3128 "throw away the timestamp cache if re-initializing the persistent cache"){.closed}
:   throw away the timestamp cache if re-initializing the persistent
    cache

[\#3134](/sssd/ticket/3134 "sssd is not able to authenticate with alias"){.closed}
:   sssd is not able to authenticate with alias

[\#3137](/sssd/ticket/3137 "secrets: creating a secret in a container doesn't work"){.closed}
:   secrets: creating a secret in a container doesn't work

[\#3140](/sssd/ticket/3140 "autofs map resolution doesn't work offline"){.closed}
:   autofs map resolution doesn't work offline

[\#3142](/sssd/ticket/3142 "expose disabling the netlink support as a sssd.conf option"){.closed}
:   expose disabling the netlink support as a sssd.conf option

[\#3143](/sssd/ticket/3143 "selinux avc denial for vsftp login as ipa user"){.closed}
:   selinux avc denial for vsftp login as ipa user

[\#3144](/sssd/ticket/3144 "Review and update SSSD's wiki pages for 1.14.2 release"){.closed}
:   Review and update SSSD's wiki pages for 1.14.2 release

[\#3145](/sssd/ticket/3145 "Update sssd-sudo man page to reflect native sudo support"){.closed}
:   Update sssd-sudo man page to reflect native sudo support

[\#3154](/sssd/ticket/3154 "sssd exits if clock is adjusted backwards after boot"){.closed}
:   sssd exits if clock is adjusted backwards after boot

[\#3163](/sssd/ticket/3163 "resolving IPA nested user group is broken in 1.14"){.closed}
:   resolving IPA nested user group is broken in 1.14

[\#3165](/sssd/ticket/3165 "login using gdm calls for gdm-smartcard when smartcard authentication is ..."){.closed}
:   login using gdm calls for gdm-smartcard when smartcard
    authentication is not enabled

[\#3167](/sssd/ticket/3167 "SECRETS: Deleting a container that has children should fail"){.closed}
:   SECRETS: Deleting a container that has children should fail

[\#3168](/sssd/ticket/3168 "secrets: Add a configurable depth limit for containers"){.closed}
:   secrets: Add a configurable depth limit for containers

[\#3172](/sssd/ticket/3172 "Access denied for user when access_provider = krb5 is set in sssd.conf"){.closed}
:   Access denied for user when access\_provider = krb5 is set in
    sssd.conf

[\#3173](/sssd/ticket/3173 "unable to create group in sssd cache"){.closed}
:   unable to create group in sssd cache

[\#3174](/sssd/ticket/3174 "Clock skew makes SSSD return System Error"){.closed}
:   Clock skew makes SSSD return System Error

[\#3175](/sssd/ticket/3175 "sss_groupshow does not work"){.closed}
:   sss\_groupshow does not work

[\#3178](/sssd/ticket/3178 "unable to add local user in sssd to a group in sssd"){.closed}
:   unable to add local user in sssd to a group in sssd

[\#3179](/sssd/ticket/3179 "sss_override fails to export"){.closed}
:   sss\_override fails to export

[\#3180](/sssd/ticket/3180 "sss_cache -r option does not print error message if more than one argument ..."){.closed}
:   sss\_cache -r option does not print error message if more than one
    argument is supplied

[\#3181](/sssd/ticket/3181 "libwbclient-sssd: update interface to version 0.13"){.closed}
:   libwbclient-sssd: update interface to version 0.13

[\#3184](/sssd/ticket/3184 "sss_groupshow <user> fails with error "No such group in local domain. ..."){.closed}
:   sss\_groupshow &lt;user&gt; fails with error "No such group in local
    domain. Printing groups only allowed in local domain"

[\#3185](/sssd/ticket/3185 "SSSD goes offline when the LDAP server returns sizelimit exceeded"){.closed}
:   SSSD goes offline when the LDAP server returns sizelimit exceeded

[\#3188](/sssd/ticket/3188 "krb5_map_user doesn't seem effective anymore"){.closed}
:   krb5\_map\_user doesn't seem effective anymore

[\#3194](/sssd/ticket/3194 "[RFE] Make GETSIDBYNAME and GETORIGBYNAME request aware of UPNs and ..."){.closed}
:   \[RFE\] Make GETSIDBYNAME and GETORIGBYNAME request aware of UPNs
    and aliases

[\#3205](/sssd/ticket/3205 "Typo In SSSD-AD Man Page"){.closed}
:   Typo In SSSD-AD Man Page

[\#3207](/sssd/ticket/3207 "SSSD logs error upon adding [secrets] section."){.closed}
:   SSSD logs error upon adding \[secrets\] section.

[\#3212](/sssd/ticket/3212 "secrets: 500 internal server error when proxy is defined but not running"){.closed}
:   secrets: 500 internal server error when proxy is defined but not
    running

[\#3213](/sssd/ticket/3213 "IPA: Uninitialized variable during subdomain check"){.closed}
:   IPA: Uninitialized variable during subdomain check

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Fabiano Fidêncio (24):

-   PROXY: Use the fqname when converting to lowercase
-   SYSDB: Rework sysdb\_cache\_connect()
-   SYSDB: Remove the timestamp cache for a newly created cache
-   SECRETS: Return ENOENT when\_deleting a non-existent secret
-   PROXY: Remove lowercase attribute from save\_user()
-   PROXY: Remove cache\_timeout attribute from save\_user()
-   PROXY: Remove cache\_timeout attribute from save\_group()
-   PROXY: Mention that save\_user()'s parameters are already qualified
-   PROXY: Share common code of save\_{group,user}()
-   BUILD: Add a few more targets for intg tests
-   BUILD: Clean up prerelease targets
-   BUILD: Fix typo in intgcheck-run rule
-   MONITOR: Remove leftovers from diag\_cmd
-   MONITOR: Remove leftovers from kill\_service
-   SECRETS: Search by the right type when checking containers
-   SECRETS: Don't remove a container when it has children
-   CONFIG: Add secrets responder to the allowed sections
-   CONFIG: Add secrets provider options
-   SECRETS: Make functions from local.c static
-   SECRETS: Use a tmp\_context on local\_db\_check\_containers()
-   SECRETS: Add a configurable depth limit for nested containers
-   SECRETS: Add a configurable limit of secrets that can be stored
-   TESTS: Remove a leftover debug message
-   TESTS: Fix check for py bindings in dlopen tests

Jakub Hrozek (35):

-   Updating the version for the 1.14.2 release
-   CONFIG: selinux\_provider is a valid provider type
-   CONFIG: session\_provider does not exist anymore
-   IPA: Parse qualified names when guessing AD user principal
-   MONITOR: Remove the no longer used diag\_cmd command
-   MONITOR: Remove the no longer used kill\_service command
-   WATCHDOG: define and use \_MAX\_TICKS as 3
-   SECRETS: Make internal function static
-   SECRETS: Make reading the config options more uniform
-   netlink: Don't define USE\_GNU
-   MAN: Document the ldap\_user\_primary\_group option
-   TOOLS: Fix a typo in groupadd()
-   KRB5: Send the output username, not internal fqname to krb5\_child
-   KRB5: Return ERR\_NETWORK\_IO on clock skew
-   LDAP: Return partial results from adminlimit exceeded
-   TESTS: Add integration tests for the sssd-secrets
-   AUTOFS: Fix offline resolution of autofs maps
-   NSS: Fix offline resolution of netgroups
-   TESTS: Test offline netgroups resolution
-   tests: Add a regression test for upstream ticket
    [\#3131](https://fedorahosted.org/sssd/ticket/3131 "defect: DNS resolver in sssd is buggy (closed: fixed)"){.closed
    .ticket}
-   MAN: sssd-secrets documentation
-   CONFIG: List allowed secrets responder options
-   SECRETS: Add DEBUG messages to the sssd-secrets provider
-   SECRETS: Use a better data type for ret
-   SECRETS: Fix a typo in function name
-   SECRETS: Use HTTP error code 504 when a proxy server cannot be
    reached
-   IPA: Initialize a boolean control value
-   tests: Add tests for sidbyname NSS operation
-   tests: Add tests for getorig by UPN NSS op
-   BUILD: Detect the path of the "service" executable
-   BUILD: Only search for service in /sbin and /usr/sbin
-   BUILD: Not having /sbin/service is not fatal
-   RPM: Require initscripts on non-systemd platforms
-   sssctl: Fix a typo in preprocessor macro
-   Updating the translations for the 1.14.2 release

Justin Stephenson (4):

-   MONITOR: Remove --disable-netlink command-line option
-   MONITOR: Add disable\_netlink option
-   MAN: sssd-sudo manual update IPA native LDAP tree support
-   sss\_cache: improve option argument handling

Lukas Slebodnik (16):

-   sssd\_netgroup.py: Resolve nested netgroups
-   BUILD: Allow to read private pipes for root
-   SPEC: Fix typo in Summary
-   SYSDB: Fix uninitialized scalar variable
-   BUILD: Remove leftover after sysdb refactoring
-   PROXY: Use right name in ldap filter
-   SYSDB: Fix error handling in sysdb\_get\_user\_members\_recursively
-   DEBUG: Apend line feed to messages from libsemanage
-   SYSDB: Suppress warning from clang static analyser
-   SDAP: Fix settig paging attribute in sdap\_get\_generic\_ext\_send
-   Remove double semicolon at the end of line
-   TESTS: Add simple test for double semicolon
-   SSSDConfig: Do not fail with nonexisting domains/services
-   SPEC: Rename python packages using macro %python\_provide
-   BUILD: intgcheck need to fail if pytest fails
-   CI: Remove dlopen-test from valgrind blacklist

Michal Židek (12):

-   TOOLS: sss\_groupshow did not work
-   TESTS: sss\_groupadd/groupshow regressions
-   TOOLS: use internal fqdn for DN
-   TESTS: Test for sss\_user/groupmod -a
-   TOOLS: sss\_mc\_refresh\_nested\_group short/fqname usage
-   TESTS: Add FQDN variants for some tests
-   TOOLS: sss\_override without name override
-   TEST: Add regression test for ticket
    [\#3179](https://fedorahosted.org/sssd/ticket/3179 "defect: sss_override fails to export (closed: fixed)"){.closed
    .ticket}
-   TOOLS: sss\_groupshow fails to show MPG
-   TESTS: sss\_groupshow with MPG
-   MAN: Typo in id mapping explanation
-   MAN: Wrong defaults for AD provider

Pavel Březina (7):

-   watchdog: cope with time shift
-   dyndns: fix typo and unify ipa with ad debug message when off
-   failover: proceed normally when no new server is found
-   sss\_override: improve --debug description
-   man page: fix language in debug level description
-   sssctl: use systemd D-Bus API
-   sssctl: call service with absolute path

Petr Cech (4):

-   LDAP: Fixing of removing netgroup from cache
-   INTG: Adding support for netgroups to ldap\_ent
-   INTG: Tests for ldap nested netgroups
-   PROXY: Adding proxy\_max\_children option

Petr Čech (5):

-   SYSDB: Removing of unused parameter
-   TESTS: Fixing of 'const' warnings in sbus tests
-   MAKEFILE: Fixing CFLAGS in some tests
-   KRB5: Fixing FQ name of user in krb5\_setup()
-   TESTS: Adding intg. tests on nested groups

Sumit Bose (8):

-   sdap\_initgr\_nested\_get\_membership\_diff: use fully-qualified
    names
-   p11: only set PKCS11\_LOGIN\_TOKEN\_NAME if gdm-smartcard is used
-   p11: return a fully-qualified name
-   pam\_sss: check PKCS11\_LOGIN\_TOKEN\_NAME
-   PAM: call free only when memory is expected to be allocated
-   nss: allow UPNs in SSS\_NSS\_GETSIDBYNAME and
    SSS\_NSS\_GETORIGBYNAME
-   libwbclient-sssd: update interface to version 0.13
-   LDAP: Removing of member link from group

Thomas Equeter (1):

-   IFP: expose user and group unique IDs through DBus

