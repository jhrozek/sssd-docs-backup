Highlights {#Highlights}
----------

-   Fixed a regression where the IPA provider didn't fetch User Private
    Groups correctly
-   An important bug in the GPO access control which resulted in a wrong
    principal being used was fixed
-   Several new options are available for deployments that need to
    restrict a certain PAM service from connecting to a certain SSSD
    domain. For more details, see the description of `pam_trusted_users`
    and `pam_public_domains` options in the
    [[​]{.icon}sssd.conf(5)](https://jhrozek.fedorapeople.org/sssd/1.12.2/man/sssd.conf.5.html){.ext-link}
    man page and the `domains` option in the
    [[​]{.icon}pam\_sss(8)](https://jhrozek.fedorapeople.org/sssd/1.12.2/man/pam_sss.8.html){.ext-link}
    man page.
-   When SSSD is acting as an IPA client in setup with trusted AD
    domains, it is able to return group members or full group
    memberships for users from trusted AD domains. Please note that this
    feature requires a recent (4.1 Alpha or newer) release of FreeIPA
    server
-   Suport for the 'views' feature of IPA. Please note that this feature
    requires a recent (4.1 Alpha or newer) release of FreeIPA server.
    Additionally, this feature will be improved in future versions of
    SSSD.

Packaging Changes {#PackagingChanges}
-----------------

-   Some unit tests depend on nss\_wrapper and uid\_wrapper libraries.
    These dependencies are optional, if the libraries are not detected
    during build, the tests are skipped

Documentation Changes {#DocumentationChanges}
---------------------

-   New PAM responder options `pam_trusted_users` and
    `pam_public_domains` options
-   New pam\_sss module option called `domains`
-   A new template expansion `%U` that expands into the user's User
    Principal Name
-   The default value of `ldap_user_objectsid` and
    `ldap_group_objectsid` changed from "Not set" to `objectSID` in the
    LDAP provider

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1021](/sssd/ticket/1021 "[RFE] Add domains= option to pam_sss"){.closed}
:   \[RFE\] Add domains= option to pam\_sss

[\#1644](/sssd/ticket/1644 "[RFE] Make SSSD capable of downloading GPO policies"){.closed}
:   \[RFE\] Make SSSD capable of downloading GPO policies

[\#1645](/sssd/ticket/1645 "[RFE] Leverage GPO policies to define HBAC"){.closed}
:   \[RFE\] Leverage GPO policies to define HBAC

[\#2041](/sssd/ticket/2041 "[RFE] User's home directories and shells are not taken from AD when there ..."){.closed}
:   \[RFE\] User's home directories and shells are not taken from AD
    when there is an IPA trust with AD

[\#2159](/sssd/ticket/2159 "[RFE] Support initgroups for unauthenticated AD users"){.closed}
:   \[RFE\] Support initgroups for unauthenticated AD users

[\#2340](/sssd/ticket/2340 "[RFE] User Principal Name as a template expansion for homedir mappings"){.closed}
:   \[RFE\] User Principal Name as a template expansion for homedir
    mappings

[\#2375](/sssd/ticket/2375 "[RFE] SSSD side of IPA user-views"){.closed}
:   \[RFE\] SSSD side of IPA user-views

[\#2412](/sssd/ticket/2412 "Error processing universal groups with cross-domain membership in SSSD ..."){.closed}
:   Error processing universal groups with cross-domain membership in
    SSSD server mode

[\#2435](/sssd/ticket/2435 "SSSD connection terminated after failing anonymous bind to IBM Tivoli ..."){.closed}
:   SSSD connection terminated after failing anonymous bind to IBM
    Tivoli Directory Server

[\#2437](/sssd/ticket/2437 "conflicting gpo policy settings not being resolved correctly"){.closed}
:   conflicting gpo policy settings not being resolved correctly

[\#2442](/sssd/ticket/2442 "sssd.conf man page missing subdomains_provider ad support"){.closed}
:   sssd.conf man page missing subdomains\_provider ad support

[\#2443](/sssd/ticket/2443 "Password expiration policies are not being enforced by SSSD"){.closed}
:   Password expiration policies are not being enforced by SSSD

[\#2447](/sssd/ticket/2447 "AD Provider crashes when looking up the "Domain Users" group"){.closed}
:   AD Provider crashes when looking up the "Domain Users" group

[\#2452](/sssd/ticket/2452 "authconfig crashes if case_sensitive=preserving in sssd.conf"){.closed}
:   authconfig crashes if case\_sensitive=preserving in sssd.conf

[\#2453](/sssd/ticket/2453 "group members returned in lowercase with case_sensitive=preserving"){.closed}
:   group members returned in lowercase with case\_sensitive=preserving

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Daniel Gollub (2):

-   sysdb: Write additional attrs in sysdb\_add\_user
-   PAM: Add domains= option to pam\_sss

Jakub Hrozek (22):

-   Updating version for the 1.12.2 release
-   LDAP: Always free talloc\_req
-   LDAP: Do not clobber return value when multiple controls are
    returned
-   TESTS: Add a case-insensitive group search sysdb test
-   MAN: AD is allowed value of subdomains\_provider
-   tests: Add a test for storing custom attrs with automatic ID
-   TESTS: Add a unit test for matching the secondary objectclass
-   IPA: Use GC for group lookups in server mode
-   AD: Add a missing break statement to the GPO code
-   LDAP: Do not require a dereference control to be retuned in a reply
-   MAN: Document the domains option of pam\_sss
-   MONITOR: Make internal functions static
-   SYSDB: move sysdb\_get\_real\_name() from sysdb.c to sysdb\_search.c
-   BUILD: Use \$(MKDIR\_P) in Makefile.am
-   MAN: Build the sss\_rpcidmapd man page conditionally
-   UTIL: Do not depend on monitor code
-   MONITOR: Remove useless memory contexts
-   UTIL: Move become\_user outside krb5 tree
-   BUILD: Detect nss\_wrapper and uid\_wrapper during configure
-   TESTS: Add a test to change user IDs
-   UTIL: Always write capaths
-   Updating the translations for the 1.12.2 release

Jan Engelhardt (1):

-   build: call AC\_BUILD\_AUX\_DIR before anything else

Lukas Slebodnik (14):

-   CI: Add missing debian dependency
-   CI: Use default config for mock build
-   GPO: Use argument ndg\_flags instead of constant
-   GPO: remove unused talloc contexts
-   DP: Print a type as hexadecimal number in debug message.
-   SDAP: Suppress warning maybe-uninitialized
-   TOOLS: Fix warning Value stored to is never read
-   SDAP: Fix warning Value stored to is never read
-   SDAP: test return value of sysdb\_search\_services
-   PAC: Check return value of function hash\_entries
-   IPA: Fix error handling after talloc\_ber\_flatten
-   GPO: fail if there is problem with storing gpo into sysdb
-   GPO: Fail if we cannot retrieve gpo from cache.
-   GPO: Do not use output argument if function failed

Michal Zidek (5):

-   Add alternative objectClass to group attribute maps
-   Use the alternative objectclass in group maps.
-   sssd.api.conf: Declare case\_sensitive as string
-   nss: Preserve case of group members
-   LDAP: Change defaults for ldap\_user/group\_objectsid

Nikolai Kondrashov (11):

-   TESTS: Free hbac\_info
-   TESTS: Free compiled regexes in krb5\_utils-tests
-   TESTS: Free link paths in symlink tests
-   TESTS: Free retrieved sid in test\_getsidbyname
-   CI: Preserve mock config timestamps
-   CI: Don't run dlopen-tests under Valgrind
-   CI: Add Valgrind suppression support
-   CI: Suppress all detected Valgrind issues
-   CI: Enforce Valgrind check
-   CI: Remove disabling of Valgrind gdb invocation
-   CI: Don't say Valgrind is ignored in README.md

Pavel Březina (8):

-   sysdb\_get\_user\_attr: use fqn for subdomain users
-   tests: add test for sysdb\_get\_user\_attr with subdomain user
-   sss\_get\_domain\_name: check for fq name first
-   tests: add test for sss\_get\_domain\_name
-   Add sysdb\_search\_\[user|group\]\_override\_attrs\_by\_name
-   Add sysdb\_get\_user\_attr\_with\_views
-   IFP: support views
-   sudo: support views

Pavel Reichl (5):

-   Fix debug messages - trailing '.'
-   PAM: new options pam\_trusted\_users & pam\_public\_domains
-   SDAP: move deciding of tls usage into new function
-   SDAP: check that connection is open before bind
-   NSS: UPN as a template expansion for homedir mappings

Stephen Gallagher (4):

-   UTIL: Do not change SSSD domains in get\_domains\_head
-   krb5: make get\_primary() a public call
-   AD GPO: Fix incorrect sAMAccountName selection
-   AD GPO: Fix incorrect return of EACCES

Sumit Bose (32):

-   name2sid: Check negative cache for users and groups
-   sysdb: sysdb\_search\_group\_by\_name should work like
    sysdb\_search\_user\_by\_name
-   IPA: add support for new extdom plugin version
-   pam: sub-domain authentication fix
-   add\_v1\_group\_data: fix for empty members list
-   nss: add SSS\_NSS\_GETORIGBYNAME request
-   sss\_nss\_idmap: add sss\_nss\_getorigbyname()
-   sysdb: add sysdb\_update\_view\_name()
-   Add sdap\_deref\_search\_with\_filter\_send()
-   IPA: make IPA ID context available to extdom client code
-   IPA: add view support and get view name
-   views: add ipa\_get\_ad\_override\_send()
-   sysdb: add sysdb\_store\_override
-   sysdb: add sysdb\_attrs\_add\_val\_safe() and
    sysdb\_attrs\_add\_string\_safe()
-   sysdb: sysdb\_apply\_default\_override
-   views: get overrides during user and group lookups
-   views: search overrides for user and group requests
-   confdb: add has\_views and view\_name to sss\_domain\_info
-   new\_subdomain: copy view data from parent
-   sysdb: add view data to domains
-   sysdb: add overide lookup calls
-   sysdb: add sysdb\_getpwnam/uid\_with\_views()
-   sysdb: add
    sss\_view\_ldb\_msg\_find\_element/attr\_as\_string/uint64
-   nss: add view support for getpwnam/getpwuid requests
-   sysdb: add sysdb\_initgroups\_with\_views()
-   nss: add view support to initgroups request
-   sysdb: add sysdb\_getgrnam\_with\_views and
    sysdb\_getgrgid\_with\_views
-   nss: add view support for getgr\* requests
-   sid2name: return name without views applied
-   pam: make pam responder aware if views
-   sysdb: add sysdb\_enumpw/grent\_with\_views()
-   nss: make enumeration requests aware of views

Yassir Elley (1):

-   AD-GPO resolve conflicting policy settings correctly

