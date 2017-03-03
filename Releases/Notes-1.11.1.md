Highlights {#Highlights}
----------

-   This release contains mainly bug fixes in the Active Directory
    provider and setups where the SSSD is running on an IPA server
    instance. In particular:
    -   Several cases where offline authentication did not work
        correctly for users from Active Directory domains were fixed
    -   Fixed a resolver bug that caused the SSSD to only look up AAAA
        records for trusted Active Directory servers
    -   SSSD is now able to resolve users from trusted AD domains using
        their POSIX attributes
-   The simple access provider now allows the administrator to specify
    users or groups from trusted domains in the access or deny lists
-   Handling of Kerberos credential caches was made simpler and more
    robust

Packaging Changes {#PackagingChanges}
-----------------

-   A new subpackage sssd-common-pac was added to work around a
    packaging bug. Previous SSSD versions would own the PAC responder by
    both the IPA and AD providers, which is not permitted by the Fedora
    packaging guidelines.
-   The configure.ac changes need `libltdl-dev` installed as an
    additional build dependency on Ubuntu and Debian systems in order to
    make the `LT_LIB_DLLOAD` macro available

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1945](/sssd/ticket/1945 "Enable printf format string checking in function debug_fn"){.closed}
:   Enable printf format string checking in function debug\_fn

[\#2001](/sssd/ticket/2001 "Implement heuristics to use Global Catalog servers from local DNS domain ..."){.closed}
:   Implement heuristics to use Global Catalog servers from local DNS
    domain first

[\#2007](/sssd/ticket/2007 "sss_debuglevel did not increase verbosity in sssd_pac.log"){.closed}
:   sss\_debuglevel did not increase verbosity in sssd\_pac.log

[\#2034](/sssd/ticket/2034 "[RFE] simple access provider: support subdomain users and groups"){.closed}
:   \[RFE\] simple access provider: support subdomain users and groups

[\#2060](/sssd/ticket/2060 "Cached credentials aren't working with sssd-ad UPN logins"){.closed}
:   Cached credentials aren't working with sssd-ad UPN logins

[\#2063](/sssd/ticket/2063 "sssd-ad unable to resolve names in other domains possibly UPN related"){.closed}
:   sssd-ad unable to resolve names in other domains possibly UPN
    related

[\#2066](/sssd/ticket/2066 "ad: invalid handling of Domain Users group for subdomain user"){.closed}
:   ad: invalid handling of Domain Users group for subdomain user

[\#2067](/sssd/ticket/2067 "Carry on if detecting the flat name fails"){.closed}
:   Carry on if detecting the flat name fails

[\#2068](/sssd/ticket/2068 "Initial enumeration in the AD provider does not work"){.closed}
:   Initial enumeration in the AD provider does not work

[\#2070](/sssd/ticket/2070 "The present sssd-ad is unable to pull RFC2307 attributes from all domains ..."){.closed}
:   The present sssd-ad is unable to pull RFC2307 attributes from all
    domains in a forest

[\#2075](/sssd/ticket/2075 "sssd fails to retrieve netgroups with multiple CN attributes"){.closed}
:   sssd fails to retrieve netgroups with multiple CN attributes

[\#2076](/sssd/ticket/2076 "Fix expand_ccname_template libkrb5 style expansion and add tests"){.closed}
:   Fix expand\_ccname\_template libkrb5 style expansion and add tests

[\#2079](/sssd/ticket/2079 "SSSD subdomains provider does not resolve SRV records correctly when DNS ..."){.closed}
:   SSSD subdomains provider does not resolve SRV records correctly when
    DNS name of the server is different from domain/realm name of IPA
    install in IPA server mode

[\#2080](/sssd/ticket/2080 "When in IPA server mode, SSSD should map trusted forest subdomains to root ..."){.closed}
:   When in IPA server mode, SSSD should map trusted forest subdomains
    to root domain realm

[\#2085](/sssd/ticket/2085 "man sssd-sudo: improve description of necessary configuration"){.closed}
:   man sssd-sudo: improve description of necessary configuration

[\#2087](/sssd/ticket/2087 "The multicast check is wrong in the sudo source code getting the host info"){.closed}
:   The multicast check is wrong in the sudo source code getting the
    host info

[\#2090](/sssd/ticket/2090 "getpwuid and getgrgid do not use the negative cache"){.closed}
:   getpwuid and getgrgid do not use the negative cache

[\#2091](/sssd/ticket/2091 "Document that server side password policies always takes precedence"){.closed}
:   Document that server side password policies always takes precedence

[\#2093](/sssd/ticket/2093 "sssd should write capaths for IPA trusted forests' subdomains"){.closed}
:   sssd should write capaths for IPA trusted forests' subdomains

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (24):

-   Updating the version for 1.11.1 release
-   PROXY: Handle empty GECOS
-   MAN: Document that sss\_cache should be run after changing the cache
    timeout
-   AD: Rename parametrized \#define
-   LDAP: Store cleanup timestamp after initial cleanup
-   Remove unused code
-   TESTS: Remove unused variable
-   KRB5: Call umask before mkstemp in the krb5 child code
-   AD: async request to retrieve master domain info
-   LDAP: sdap\_id\_setup\_tasks accepts a custom enum request
-   AD: Download master domain info when enumerating
-   AD: Failure to get flat name is not fatal
-   Convert IN\_MULTICAST parameter to host order
-   NSS: Set UID and GID to negative cache after searching all domains
-   NSS: Failure to store entry negative cache should not be fatal
-   KRB5: Fix bad comparison
-   IPA: Ignore dns\_discovery\_domain in server mode
-   KRB5: Return ERR\_NETWORK\_IO when trusted AD server can't be
    resolved
-   KRB5: Use the correct domain when authenticating with cached
    password
-   LDAP: Require ID numbers when ID mapping is off
-   LDAP: Allow searching subdomain during RFC2307bis initgroups
-   AD: talk to GC first even for local domain objects
-   MAN: Document that POSIX attributes must be replicated to GC
-   Updating the translations for the 1.11.1 release

Lukas Slebodnik (38):

-   AUTOMAKE: Add missing escaped newline
-   Include sys/types.h for types id\_t and uid\_t
-   UTIL: Use standard maximum value of type size\_t
-   KRB5: Fix warning declaration shadows global declaration
-   Fix warning missing arguments
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
-   krb5: Fix warning sometimes uninitialized
-   Fix formating of variables with type: long
-   Fix formating of variables with type: unsigned long
-   Fix formating of variables with type: int
-   Fix pointer formatting
-   Use the same variable type like in struct ldb\_message\_element
-   Fix formating of variables with type: ssize\_t
-   Fix formating of variables with type: size\_t
-   Adding new header for printf formating macros
-   Fix formating of variables with type: key\_serial\_t
-   Fix formating of variables with type: rlim\_t
-   Fix formating of variables with type defined in stdint.h
-   Fix formating of variables with type: time\_t
-   Fix formating of variables with ber\_ type
-   Fix warning: data argument not used by format string
-   Use right formating to print string
-   Fix formating of variables with type: id\_t
-   Fix formating of variables with type: uid\_t
-   Fix formating of variables with type: gid\_t
-   Enable printf format string checking
-   KRB: Remove unused memory context
-   KRB: Remove unused function parameters
-   LDAP: Use primary cn to search netgroup

Michal Zidek (4):

-   Rename SAFEALIGN macros
-   Rename \_SSS\_MC\_SPECIAL
-   man sssd: Add note about SSS\_NSS\_USE\_MEMCACHE
-   Check slot validity before MC\_SLOT\_TO\_PTR.

Nikolai Kondrashov (1):

-   Fix reference to sssd-krb5 man page

Ondrej Kos (2):

-   DB: Add user/group lookup by SID
-   DB: Rise search functions debug levels

Pavel Březina (22):

-   Fix czech specific character in my name
-   krb5\_utils tests: fix some typos
-   resolv\_sort\_srv\_reply: remove unnecessary mem\_ctx
-   fo srv: add priority to fo\_server\_info
-   utils: add is\_host\_in\_domain()
-   ad srv: prefer servers that are in the same domain as client
-   sysdb\_search\_group\_by\_gid: obtain gid instead of uid
-   is\_dn(): free dn
-   util: add sss\_idmap\_talloc\[\_free\]
-   simple access tests: fix typos
-   simple provider: support subdomain users
-   util: add find\_subdomain\_by\_sid()
-   util: add find\_subdomain\_by\_object\_name()
-   simple provider: support subdomain groups
-   simple access test: initialize be\_ctx for all tests
-   simple provider: obey case sensitivity for subdomain users and
    groups
-   man: improve sssd-sudo manual page
-   man: server side password policies always takes precedence
-   util: add get\_domains\_head()
-   sysdb: get\_sysdb\_grouplist() can return either names or dn
-   sysdb: sysdb\_update\_members can take either name or dn
-   ad: store group in correct tree on initgroups via tokenGroups

Simo Sorce (18):

-   Makefile: Fix sssd\_be targets
-   krb5: Ingnore unknown expansion sequences
-   tests: Add dlopen test to make sure modules works
-   krb5: Add calls to change and restore credentials
-   krb5: Add helper to destroy ccache as user
-   krb5: Use krb5\_cc\_destroy to remove old ccaches
-   krb5: Replace type-specific ccache/principal check
-   krb5: Move determination of user being active
-   krb5: move template check to initializzation
-   krb5: Make check\_for\_valid\_tgt() static
-   krb5: Use new function to validate ccaches
-   krb5: Unify function to create ccache files
-   krb5: Remove unused ccache backend infrastructure
-   krb5: Remove unused function
-   krb5: Add file/dir path precheck
-   krb5\_child: Simplify ccache creation
-   krb5: Remove unused helper functions
-   krb5: Be more lenient on failures for old ccache

Stephen Gallagher (1):

-   RPM: Add new subpackage for PAC responder

Sumit Bose (7):

-   dyndns: do not modify global family\_order
-   sdap\_domain\_add: remove too strict consistency check
-   krb5: save canonical upn to sysdb
-   krb5: do not expand enterprise principals is offline
-   IPA: store forest name for forest member domains
-   ipa\_server\_mode: write capaths to krb5 include file
-   Do not return DP\_ERR\_FATAL in case of success

