Highlights {#Highlights}
----------

-   The main focus of the 1.10 release was improving the Active
    Directory integration.
    -   The Active Directory provider now includes support for
        Site-based discovery. This feature allows the Active Directory
        clients to find the most suitable Domain Controller to connect
        to.
    -   Support for dynamic DNS updates in the Active Directory
        provider. This feature enables the clients to automatically
        update or refresh their DNS records stored in the AD server.
    -   The Active Directory provider now includes support for
        retrieving identity information and authentication as users from
        trusted domains in the same forest. The SSSD looks up the
        information using the Global Catalog.
    -   The group memberships for Active Directory users can optionally
        be read from the PAC during login. If the PAC is not available
        (such as when group membership is requested for a user who has
        never logged in), the SSSD falls back to using tokenGroups. To
        enable this feature, add `pac` to the list of configured
        services in the `[sssd]` section of the `sssd.conf` config file.
    -   The Active Directory provider is able to autodiscover the
        NetBIOS (flat) name of the domain it connects to. The NetBIOS
        name is discovered automatically on startup.
    -   The support for Enterprise Kerberos principals was added.
        Currently the enterprise principals are only enabled by default
        in the Active Directory provider
-   A new library, called libsss\_nss\_idmap was introduced. This
    library allows the user to convert Windows Security Identifiers
    (SIDs) to names and vice versa. The library also includes Python
    bindings.
-   A new option `ipa_dyndns_ttl` was added, allowing the client to set
    a custom TTL on IPA dynamic DNS updates
-   A new `ignore_group_members option` was added. This option can be
    used to suppress downloading group members on group lookups, making
    the group lookups much faster for environments that do not need to
    know the group members.
-   A new option `ldap_rfc2307_fallback_to_local_users` was added. If
    this option is set to true, SSSD is able to resolve local group
    members of LDAP groups.
-   The `subdomain_homedir` configuration option gained a new template
    expansion `%F` that expands to the flat name (NetBIOS name) of the
    trusted AD domain
-   The `full_name_format` option now accepts a new parameter that
    expands to the NetBIOS name of the domain
-   The new `krb5_use_kdcinfo` option allows the administrator to
    disable the Kerberos locator plugin and rely on information read
    from the krb5.conf file completely.
-   A new option `ldap_disable_range_retrieval` was added. Switching
    this option to True skips large Active Directory groups that might
    otherwise take a long time to download and process.
-   A new option `refresh_expired_interval` was added. This option
    allows to configure a background task that would automatically
    refresh entries that are nearing their expiration time. In this
    release, only refreshing netgroups is implemented.
-   Setting the SELinux context on the IPA server now also works for
    users coming from a trusted Active Directory domain
-   Many internal interfaces were refactored, making the code more
    readable and maintainable in the long term. This refactoring
    includes the subdomains code, the sysdb interface as a whole,
    internal error code reporting, SELinux login context processing and
    processing of nested LDAP groups.

Packaging changes {#Packagingchanges}
-----------------

-   The shared components of the SSSD are now built as a shared library
    to reduce amount of duplicated code being linked into multiple SSSD
    binaries and lower the disk usage of SSSD installation.
-   The check that ensured that SSSD is running with the same ldb
    version it was built against was made optional, defaulting to false.
    You can enable the strict check again by selecting
    --enable-ldb-version-check during configure
-   The SSSD python ConfigAPI was moved to its own noarch subpackage to
    make the SSSD packaging more compliant with the Fedora packaging
    guidelines
-   The libsss\_nss\_idmap library and its Python bindings are packaged
    in separate subpackages
-   The upstream RPM specfile now packages each provider separately. The
    SSSD deamon and the responders are now included in the sssd-common
    package, while the sssd package has become a "meta package" that
    Requires all the existing providers for backwards compatibility.
-   The libsss\_sudo and libsss\_autofs libraries are now part of the
    sssd-common package

Tickets fixed {#Ticketsfixed}
-------------

<div>

[\#1199](/sssd/ticket/1199 "[RFE] Prune idle connections from responders"){.closed}
:   \[RFE\] Prune idle connections from responders

[\#1693](/sssd/ticket/1693 "sudoHost mismatch response is incorrect sometimes"){.closed}
:   sudoHost mismatch response is incorrect sometimes

[\#1806](/sssd/ticket/1806 "sssd_be goes to 99% CPU and causes significant login delays when client is ..."){.closed}
:   sssd\_be goes to 99% CPU and causes significant login delays when
    client is under load

[\#1815](/sssd/ticket/1815 ""touch" krb5.conf file after installing new domain-realm mappings"){.closed}
:   "touch" krb5.conf file after installing new domain-realm mappings

[\#1847](/sssd/ticket/1847 "if there is no blank line at the end of /etc/sssd/sssd.conf, sssd wont ..."){.closed}
:   if there is no blank line at the end of /etc/sssd/sssd.conf, sssd
    wont start and you get an error in /var/log/messages about "sssd:
    Cannot load configuration database".

[\#1849](/sssd/ticket/1849 "improper use of negative value"){.closed}
:   improper use of negative value

[\#1863](/sssd/ticket/1863 "Dereference after a NULL check in krb5_child.c"){.closed}
:   Dereference after a NULL check in krb5\_child.c

[\#1873](/sssd/ticket/1873 "password migration is not working using sssd"){.closed}
:   password migration is not working using sssd

[\#1886](/sssd/ticket/1886 "If previous SRV query failed, the next try might not be retried in some ..."){.closed}
:   If previous SRV query failed, the next try might not be retried in
    some cases

[\#1894](/sssd/ticket/1894 "sssd_be crashes while processing ASQ dereference request"){.closed}
:   sssd\_be crashes while processing ASQ dereference request

[\#1931](/sssd/ticket/1931 "cannot login to the 1st domain when 2 domains are configured in sssd"){.closed}
:   cannot login to the 1st domain when 2 domains are configured in sssd

[\#1936](/sssd/ticket/1936 "GSSAPI working only on first login"){.closed}
:   GSSAPI working only on first login

[\#1947](/sssd/ticket/1947 "[abrt] sssd-1.10.0-4.fc19.beta1: get_server_status: Process ..."){.closed}
:   \[abrt\] sssd-1.10.0-4.fc19.beta1: get\_server\_status: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)

[\#1949](/sssd/ticket/1949 "SSH host keys are not removed from cache when host is deleted in IPA"){.closed}
:   SSH host keys are not removed from cache when host is deleted in IPA

[\#1953](/sssd/ticket/1953 "System error while trying to auth as an expired user"){.closed}
:   System error while trying to auth as an expired user

[\#1959](/sssd/ticket/1959 "Enhance sssd init script so that it would source a configuration"){.closed}
:   Enhance sssd init script so that it would source a configuration

[\#1969](/sssd/ticket/1969 "dead code in SRV resolution"){.closed}
:   dead code in SRV resolution

[\#1973](/sssd/ticket/1973 "Improve global catalog DNS SRV lookups"){.closed}
:   Improve global catalog DNS SRV lookups

[\#1980](/sssd/ticket/1980 "SSSD service randomly dies"){.closed}
:   SSSD service randomly dies

[\#1986](/sssd/ticket/1986 "SYSV init script should use @sbindir@"){.closed}
:   SYSV init script should use @sbindir@

[\#1989](/sssd/ticket/1989 "Fix core dump in the PAC responder"){.closed}
:   Fix core dump in the PAC responder

[\#1995](/sssd/ticket/1995 "The PAC responder is contacted even for local IPA users."){.closed}
:   The PAC responder is contacted even for local IPA users.

</div>

\`

<div>

[\#364](/sssd/ticket/364 "[RFE] Recognize trusted domains in AD provider"){.closed}
:   \[RFE\] Recognize trusted domains in AD provider

[\#453](/sssd/ticket/453 "Replace pam status codes with sssd specific codes"){.closed}
:   Replace pam status codes with sssd specific codes

[\#812](/sssd/ticket/812 "Support libnl 3.x"){.closed}
:   Support libnl 3.x

[\#902](/sssd/ticket/902 "[RFE] Allow setting krb5_renew_interval with a delimiter"){.closed}
:   \[RFE\] Allow setting krb5\_renew\_interval with a delimiter

[\#1032](/sssd/ticket/1032 "[RFE] sssd should support DNS sites"){.closed}
:   \[RFE\] sssd should support DNS sites

[\#1033](/sssd/ticket/1033 "[RFE] implement a script/tool joining to the Active Directory domain"){.closed}
:   \[RFE\] implement a script/tool joining to the Active Directory
    domain

[\#1287](/sssd/ticket/1287 "compilation warnings with -O2"){.closed}
:   compilation warnings with -O2

[\#1327](/sssd/ticket/1327 "When multiple values are assigned, sss_debuglevel should display a usage ..."){.closed}
:   When multiple values are assigned, sss\_debuglevel should display a
    usage message

[\#1371](/sssd/ticket/1371 "Missing resolv.conf should be non-fatal"){.closed}
:   Missing resolv.conf should be non-fatal

[\#1376](/sssd/ticket/1376 "[RFE] Add support for suppressing group members"){.closed}
:   \[RFE\] Add support for suppressing group members

[\#1405](/sssd/ticket/1405 "[RFE] Kerberos canonicalization should be skipped on password-changes in ..."){.closed}
:   \[RFE\] Kerberos canonicalization should be skipped on
    password-changes in AD provider

[\#1414](/sssd/ticket/1414 "[RFE] Improve syslog message when configuration cannot be loaded"){.closed}
:   \[RFE\] Improve syslog message when configuration cannot be loaded

[\#1468](/sssd/ticket/1468 "[RFE] AD: Should be able to log in as long or short domains"){.closed}
:   \[RFE\] AD: Should be able to log in as long or short domains

[\#1476](/sssd/ticket/1476 "SSSD has a much longer TTL when updating a DNS record than IPA client ..."){.closed}
:   SSSD has a much longer TTL when updating a DNS record than IPA
    client install placed in the beginning

[\#1481](/sssd/ticket/1481 "Move sss_cache to the main subpackage"){.closed}
:   Move sss\_cache to the main subpackage

[\#1484](/sssd/ticket/1484 "failover should protect against empty host names"){.closed}
:   failover should protect against empty host names

[\#1495](/sssd/ticket/1495 "include talloc log in our debug facility"){.closed}
:   include talloc log in our debug facility

[\#1504](/sssd/ticket/1504 "[RFE] AD dyndns updates"){.closed}
:   \[RFE\] AD dyndns updates

[\#1510](/sssd/ticket/1510 "Split providers into their own subpackages"){.closed}
:   Split providers into their own subpackages

[\#1557](/sssd/ticket/1557 "[RFE] Use the Global Catalog in SSSD for the AD provider"){.closed}
:   \[RFE\] Use the Global Catalog in SSSD for the AD provider

[\#1558](/sssd/ticket/1558 "[RFE] Use MS-PAC to retrieve user's group list"){.closed}
:   \[RFE\] Use MS-PAC to retrieve user's group list

[\#1559](/sssd/ticket/1559 "[RFE] Use the getpwnam()/getgrnam() interface as a gateway to resolve SID ..."){.closed}
:   \[RFE\] Use the getpwnam()/getgrnam() interface as a gateway to
    resolve SID to Names

[\#1566](/sssd/ticket/1566 "drop the libldb version requirement"){.closed}
:   drop the libldb version requirement

[\#1575](/sssd/ticket/1575 "Change responder contexts hierarchy"){.closed}
:   Change responder contexts hierarchy

[\#1586](/sssd/ticket/1586 "Make authtoken opaque objects"){.closed}
:   Make authtoken opaque objects

[\#1603](/sssd/ticket/1603 "[RFE] Send user principal together with the PAC to the pac responder"){.closed}
:   \[RFE\] Send user principal together with the PAC to the pac
    responder

[\#1609](/sssd/ticket/1609 "[RFE] Subdomain homedir template should be configurable/use flatname by ..."){.closed}
:   \[RFE\] Subdomain homedir template should be configurable/use
    flatname by default

[\#1625](/sssd/ticket/1625 "Confusing error messages for invalid sssd.conf"){.closed}
:   Confusing error messages for invalid sssd.conf

[\#1643](/sssd/ticket/1643 "Refactor sysdb interface"){.closed}
:   Refactor sysdb interface

[\#1648](/sssd/ticket/1648 "Fully qualified account names form should be able to use flatname in the ..."){.closed}
:   Fully qualified account names form should be able to use flatname in
    the fq format

[\#1660](/sssd/ticket/1660 "LDAP_CONTROL_X_DEREF: sssd should fallback if server returns ..."){.closed}
:   LDAP\_CONTROL\_X\_DEREF: sssd should fallback if server returns
    LDAP\_UNAVAILABLE\_CRITICAL\_EXTENSION error

[\#1712](/sssd/ticket/1712 "sudoNotBefore/sudoNotAfter not supported by sssd sudoers plugin"){.closed}
:   sudoNotBefore/sudoNotAfter not supported by sssd sudoers plugin

[\#1713](/sssd/ticket/1713 "[RFE] Add a task to the SSSD to periodically refresh cached entries"){.closed}
:   \[RFE\] Add a task to the SSSD to periodically refresh cached
    entries

[\#1733](/sssd/ticket/1733 "[RFE] support autoconfiguring SUDO with ipa provider and compat tree"){.closed}
:   \[RFE\] support autoconfiguring SUDO with ipa provider and compat
    tree

[\#1738](/sssd/ticket/1738 "Decrease the krb5_auth_timeout default value of 15"){.closed}
:   Decrease the krb5\_auth\_timeout default value of 15

[\#1741](/sssd/ticket/1741 "sss_cache doesn't support subdomains"){.closed}
:   sss\_cache doesn't support subdomains

[\#1743](/sssd/ticket/1743 "selinux: move all logic to responder, provider should only update db"){.closed}
:   selinux: move all logic to responder, provider should only update db

[\#1744](/sssd/ticket/1744 "selinux: reuse IPA_HBAC_REFRESH or provide an alternative"){.closed}
:   selinux: reuse IPA\_HBAC\_REFRESH or provide an alternative

[\#1745](/sssd/ticket/1745 "Unnecessary output is seen when invalid option is passed to sss_cache"){.closed}
:   Unnecessary output is seen when invalid option is passed to
    sss\_cache

[\#1746](/sssd/ticket/1746 "sss_* tools with use_fully_qualified_names should require fqdn"){.closed}
:   sss\_\* tools with use\_fully\_qualified\_names should require fqdn

[\#1747](/sssd/ticket/1747 "Refactor subdomain interfaces"){.closed}
:   Refactor subdomain interfaces

[\#1756](/sssd/ticket/1756 "append new line to error string from poptStrerror()"){.closed}
:   append new line to error string from poptStrerror()

[\#1763](/sssd/ticket/1763 "check the return values of sysdb_transaction_commit in sysdb tests"){.closed}
:   check the return values of sysdb\_transaction\_commit in sysdb tests

[\#1765](/sssd/ticket/1765 "remove the alt_db_path parameter of sysdb_init"){.closed}
:   remove the alt\_db\_path parameter of sysdb\_init

[\#1766](/sssd/ticket/1766 "use an explanatory macro for checking if a domain is a subdomain"){.closed}
:   use an explanatory macro for checking if a domain is a subdomain

[\#1767](/sssd/ticket/1767 "unify sss_mc_set_recycled"){.closed}
:   unify sss\_mc\_set\_recycled

[\#1771](/sssd/ticket/1771 "Negative cache messages are displayed at too low of a DEBUG level"){.closed}
:   Negative cache messages are displayed at too low of a DEBUG level

[\#1772](/sssd/ticket/1772 "Rename or alias the SAFEALIGN macros"){.closed}
:   Rename or alias the SAFEALIGN macros

[\#1774](/sssd/ticket/1774 "move processing of password expiration back to PAM provider only"){.closed}
:   move processing of password expiration back to PAM provider only

[\#1784](/sssd/ticket/1784 "rewrite nested group processing to follow the tevent_req coding style"){.closed}
:   rewrite nested group processing to follow the tevent\_req coding
    style

[\#1785](/sssd/ticket/1785 "NSCD warning is irritating"){.closed}
:   NSCD warning is irritating

[\#1786](/sssd/ticket/1786 "Use new interface from ding-libs ini interface"){.closed}
:   Use new interface from ding-libs ini interface

[\#1789](/sssd/ticket/1789 "ldap_access_order improvements (man page fix)"){.closed}
:   ldap\_access\_order improvements (man page fix)

[\#1790](/sssd/ticket/1790 "Possible null derefence in ipa_subdomains.c"){.closed}
:   Possible null derefence in ipa\_subdomains.c

[\#1794](/sssd/ticket/1794 "reuse open_cloexec elsewhere in the code"){.closed}
:   reuse open\_cloexec elsewhere in the code

[\#1797](/sssd/ticket/1797 "Use hardened flags for building RPMs"){.closed}
:   Use hardened flags for building RPMs

[\#1802](/sssd/ticket/1802 "[abrt] sssd-1.9.3-1.fc18: talloc_abort: Process /usr/libexec/sssd/sssd_be ..."){.closed}
:   \[abrt\] sssd-1.9.3-1.fc18: talloc\_abort: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 6 (SIGABRT)

[\#1803](/sssd/ticket/1803 "SSSD returns System Error if the ccachedir is not writable"){.closed}
:   SSSD returns System Error if the ccachedir is not writable

[\#1804](/sssd/ticket/1804 "Filter out inappropriate multicast and subnet broadcast addresses from IPA ..."){.closed}
:   Filter out inappropriate multicast and subnet broadcast addresses
    from IPA dynamic DNS update

[\#1805](/sssd/ticket/1805 "[RFE] Add a new override_homedir expansion for the "original value""){.closed}
:   \[RFE\] Add a new override\_homedir expansion for the "original
    value"

[\#1809](/sssd/ticket/1809 "Document that SSSD domains should only be named using ASCII characters"){.closed}
:   Document that SSSD domains should only be named using ASCII
    characters

[\#1810](/sssd/ticket/1810 "Uninitialized scalar variable in responder_get_domain"){.closed}
:   Uninitialized scalar variable in responder\_get\_domain

[\#1811](/sssd/ticket/1811 "Unchecked return value in tests"){.closed}
:   Unchecked return value in tests

[\#1812](/sssd/ticket/1812 "[RFE] make the get_next_domain() function a little more readable"){.closed}
:   \[RFE\] make the get\_next\_domain() function a little more readable

[\#1813](/sssd/ticket/1813 "make the ldb check configurable"){.closed}
:   make the ldb check configurable

[\#1816](/sssd/ticket/1816 "Non-fatal errors looking up trusted domains with IPA back end"){.closed}
:   Non-fatal errors looking up trusted domains with IPA back end

[\#1819](/sssd/ticket/1819 "Refresh doxygen template files"){.closed}
:   Refresh doxygen template files

[\#1820](/sssd/ticket/1820 "sysdb unit tests uses system memberof"){.closed}
:   sysdb unit tests uses system memberof

[\#1823](/sssd/ticket/1823 "getgrnam / getgrgid for large user groups is too slow due to range ..."){.closed}
:   getgrnam / getgrgid for large user groups is too slow due to range
    retrieval functionality

[\#1825](/sssd/ticket/1825 "Invalid assignment to enum"){.closed}
:   Invalid assignment to enum

[\#1830](/sssd/ticket/1830 "make the authtok structure really opaque"){.closed}
:   make the authtok structure really opaque

[\#1831](/sssd/ticket/1831 "use the -v flag with nsupdate to force TCP transmission for better ..."){.closed}
:   use the -v flag with nsupdate to force TCP transmission for better
    security

[\#1832](/sssd/ticket/1832 "[RFE] Provide a new option to update the reverse DNS zone in IPA domain"){.closed}
:   \[RFE\] Provide a new option to update the reverse DNS zone in IPA
    domain

[\#1833](/sssd/ticket/1833 "segmentation fault in cmocka unit tests with raised optization level"){.closed}
:   segmentation fault in cmocka unit tests with raised optization level

[\#1834](/sssd/ticket/1834 "Support for libini 1.0"){.closed}
:   Support for libini 1.0

[\#1838](/sssd/ticket/1838 "nss and pam clients broken in master"){.closed}
:   nss and pam clients broken in master

[\#1839](/sssd/ticket/1839 "Incorrect *.py[co] files placement"){.closed}
:   Incorrect \*.py\[co\] files placement

[\#1840](/sssd/ticket/1840 "Add --with-test-dir=/dev/shm to DISTCHECK_CONFIGURE_FLAGS"){.closed}
:   Add --with-test-dir=/dev/shm to DISTCHECK\_CONFIGURE\_FLAGS

[\#1842](/sssd/ticket/1842 "Allow usage of enterprise principals"){.closed}
:   Allow usage of enterprise principals

[\#1843](/sssd/ticket/1843 "Add exit value section to sss_ssh_* man page pages"){.closed}
:   Add exit value section to sss\_ssh\_\* man page pages

[\#1844](/sssd/ticket/1844 "add a call to calculated the range for a given domain SID to libsss_idmap"){.closed}
:   add a call to calculated the range for a given domain SID to
    libsss\_idmap

[\#1845](/sssd/ticket/1845 "move libsss_sudo and libsss_autofs back into the main sssd package"){.closed}
:   move libsss\_sudo and libsss\_autofs back into the main sssd package

[\#1848](/sssd/ticket/1848 "unused parameter in ipa_selinux handler"){.closed}
:   unused parameter in ipa\_selinux handler

[\#1860](/sssd/ticket/1860 "pidfile() may leak memory on error"){.closed}
:   pidfile() may leak memory on error

[\#1861](/sssd/ticket/1861 "potential out-of-bounds-write in sss_idmap_sid_to_dom_sid"){.closed}
:   potential out-of-bounds-write in sss\_idmap\_sid\_to\_dom\_sid

[\#1862](/sssd/ticket/1862 "negative return in files.c"){.closed}
:   negative return in files.c

[\#1864](/sssd/ticket/1864 "Bad comparisons in checks found by new Coverity instance"){.closed}
:   Bad comparisons in checks found by new Coverity instance

[\#1865](/sssd/ticket/1865 "Logically dead code in tools_util.c"){.closed}
:   Logically dead code in tools\_util.c

[\#1867](/sssd/ticket/1867 "document that AD provider is always case insensitive"){.closed}
:   document that AD provider is always case insensitive

[\#1870](/sssd/ticket/1870 "wrong failure handler in sdap_get_map"){.closed}
:   wrong failure handler in sdap\_get\_map

[\#1877](/sssd/ticket/1877 "ding-libs.dhash: uninitialized pointer read"){.closed}
:   ding-libs.dhash: uninitialized pointer read

[\#1883](/sssd/ticket/1883 "Add a new option to disable the Kerberos locator plugin completely"){.closed}
:   Add a new option to disable the Kerberos locator plugin completely

[\#1888](/sssd/ticket/1888 "freeipa 3.2 trusted ad user not listed in external group"){.closed}
:   freeipa 3.2 trusted ad user not listed in external group

[\#1889](/sssd/ticket/1889 "coverity: dead code in sudo client"){.closed}
:   coverity: dead code in sudo client

[\#1890](/sssd/ticket/1890 "SSSD doesn't display warning for last grace login."){.closed}
:   SSSD doesn't display warning for last grace login.

[\#1891](/sssd/ticket/1891 "unite periodic refresh API"){.closed}
:   unite periodic refresh API

[\#1892](/sssd/ticket/1892 "In IPA AD trust setup, the sssd logs throws 'sysdb_search_user_by_name ..."){.closed}
:   In IPA AD trust setup, the sssd logs throws
    'sysdb\_search\_user\_by\_name failed' error when AD user tries to
    login via ipa client.

[\#1897](/sssd/ticket/1897 "Autenticity of ipa server can't be established"){.closed}
:   Autenticity of ipa server can't be established

[\#1900](/sssd/ticket/1900 "Uninitialized scalar variable in idmap.c"){.closed}
:   Uninitialized scalar variable in idmap.c

[\#1901](/sssd/ticket/1901 "confdb: possible double free in new ini module"){.closed}
:   confdb: possible double free in new ini module

[\#1905](/sssd/ticket/1905 "pysss_nss_idmap improvements"){.closed}
:   pysss\_nss\_idmap improvements

[\#1909](/sssd/ticket/1909 "Clarify the AD site discovery in sssd-ad man page"){.closed}
:   Clarify the AD site discovery in sssd-ad man page

[\#1910](/sssd/ticket/1910 "Clarify that AD DNS updates are performed using GSS-TSIG"){.closed}
:   Clarify that AD DNS updates are performed using GSS-TSIG

[\#1912](/sssd/ticket/1912 "SUDO is not working for users from trusted AD domain"){.closed}
:   SUDO is not working for users from trusted AD domain

[\#1913](/sssd/ticket/1913 "SSSD crashes during nsupdate if the client hostname can't be resolved"){.closed}
:   SSSD crashes during nsupdate if the client hostname can't be
    resolved

[\#1914](/sssd/ticket/1914 "pysss_nss_idmap:  Support also Unicode strings and return them by default"){.closed}
:   pysss\_nss\_idmap: Support also Unicode strings and return them by
    default

[\#1915](/sssd/ticket/1915 "Turn on dyndns updates by default in the AD provider"){.closed}
:   Turn on dyndns updates by default in the AD provider

[\#1921](/sssd/ticket/1921 "Login failure: Enterprise Principal enabled by default for AD Provider"){.closed}
:   Login failure: Enterprise Principal enabled by default for AD
    Provider

[\#1922](/sssd/ticket/1922 "sssd_be crashes when looking up users in the LDAP provider with ID mapping"){.closed}
:   sssd\_be crashes when looking up users in the LDAP provider with ID
    mapping

[\#1924](/sssd/ticket/1924 "MAN: Make it clear which address is used to update DNS records"){.closed}
:   MAN: Make it clear which address is used to update DNS records

[\#1927](/sssd/ticket/1927 "Provide a script to create a SRPM without having to run configure"){.closed}
:   Provide a script to create a SRPM without having to run configure

[\#1928](/sssd/ticket/1928 "Libtool fails to find dependent libraries"){.closed}
:   Libtool fails to find dependent libraries

[\#1929](/sssd/ticket/1929 "Junk character in sssd_domain.log for domain string when sssd tries to go ..."){.closed}
:   Junk character in sssd\_domain.log for domain string when sssd tries
    to go online from offline mode

[\#1930](/sssd/ticket/1930 "Crash with negative values in ldap_idmap_range_size"){.closed}
:   Crash with negative values in ldap\_idmap\_range\_size

[\#1934](/sssd/ticket/1934 "sssd crashes if junk is present in sssd.conf"){.closed}
:   sssd crashes if junk is present in sssd.conf

[\#1950](/sssd/ticket/1950 "segfault while processing ASQ request"){.closed}
:   segfault while processing ASQ request

[\#1951](/sssd/ticket/1951 "NetBIOS domain name should be read at startup"){.closed}
:   NetBIOS domain name should be read at startup

[\#1971](/sssd/ticket/1971 "Dereference before NULL check in nscd.c"){.closed}
:   Dereference before NULL check in nscd.c

[\#1972](/sssd/ticket/1972 "Dereference after a NULL check in tests/common_dom.c"){.closed}
:   Dereference after a NULL check in tests/common\_dom.c

[\#1976](/sssd/ticket/1976 "Copy-n-paste error in AD provider"){.closed}
:   Copy-n-paste error in AD provider

[\#2362](/sssd/ticket/2362 "RHEL6.5 sssd_be crash when debug_level 3 or higher"){.closed}
:   RHEL6.5 sssd\_be crash when debug\_level 3 or higher

</div>

\`

Detailed Changelog {#DetailedChangelog}
------------------

Abhishek Singh (4):

-   filename in comment is corrected
-   cmocka unittest for find\_uid added
-   cmocka unittest for io added
-   Fix segmentation fault in test\_io.

Ariel Barria (4):

-   Improve syslog message when configuration cannot be loaded
-   Allow setting krb5\_renew\_interval with a delimiter
-   Confusing error messages for invalid sssd.conf
-   Removing BUILD.txt content

Jakub Hrozek (144):

-   Bump version to 1.10dev
-   Require ar in configure.ac
-   TESTS: Fix a couple of debug-level setters
-   SYSDB: Remove unused macros
-   LDAP: Remove double break
-   Indentation fix
-   Bump the version and reset release back to 0
-   tests: add a unit test for sysdb\_netgroup\_base\_dn
-   tests: unit test for test\_sysdb\_search\_users
-   tests: adda a unit test for test\_sysdb\_search\_groups
-   tests: test sysdb\_initgroups
-   tests: add unit test for sysdb\_get\_new\_id
-   tests: unit test for sysdb\_remove\_attrs
-   TOOLS: set domain in check\_group\_names
-   Fix code style
-   Don't use srcdir with tests
-   krb5: include backwards compatible declaration of krb5\_trace\_info
-   LDAP: Check for authtok validity
-   Filter out multicast addresses from IPA DNS updates
-   Lower the DEBUG level if an entry cannot be deleted from memcache
-   Fix the krb5 password expiration warning
-   Remove enumerate=true from man sssd-ldap
-   Do not process success case in an else
-   Revert "Add debug message to autofs client"
-   Don't treat 0 as default for pam\_pwd\_expiration warning
-   Remove unused functions
-   Use the correct memory context in be\_req\_create
-   Check the return value of sysdb\_search\_services
-   Detect the presence of libcmocka during configure
-   Add utility functions for tests that use sysdb or tevent.
-   Move sss\_cmd\_execute from client to responder code.
-   CMocka based test for the NSS responder
-   Retry the correct service on krb5 child timeout
-   Remove duplicate remake from bashrc\_sssd
-   Provide a be\_get\_account\_info\_send function
-   Add unit tests for simple access test by groups
-   Do not compile main() in DP if UNIT\_TESTING is defined
-   Resolve GIDs in the simple access provider
-   Return error code from ipa\_subdom\_store
-   Move signal.m4 from src/util to external
-   Document what does access\_provider=ad do
-   Include config.h to build io.c on RHEL5
-   selinux: Remove unused parameter
-   Updating the translations for the 1.10 alpha release
-   Updating the version for the 1.10 beta1 release
-   krb5 child: Use the correct type when processing OTP
-   pidfile(): Do not leak fd on error
-   Fix potential out-of-bounds write in sss\_idmap\_sid\_to\_dom\_sid
-   Return errno, not -1 on failure in files.c
-   Check for correct variable name
-   Init failover with be\_res options
-   Centralize resolv\_init, remove resolv context list
-   dyndns: Fix initializing sdap\_id\_ctx
-   Check for the correct variables
-   Allocate PAM DP request data on responder context
-   LDAP: Always fail if a map can't be found
-   Put the override\_homedir into an included xml file
-   Allow using flatname for subdomain home dir template
-   Fix simple access group control in case-insensitive domains
-   Make leak checks usable in tests that do not utilize check
-   tests: Fix the order of key/values
-   LDAP: do not invalidate pointer with realloc while processing ghost
    users
-   Convert the simple access check to new error codes
-   tests: Link the simple access tests with -ldl
-   Do not keep growing event context
-   Document the naming convention for SSSD domains
-   Document that the AD provider is case-insensitive
-   selinux: if no domain matches, make the debug message louder
-   Only try to relink ghost users if we're not enumerating
-   Display the last grace warning, too
-   Refactor dynamic DNS updates
-   Convert IPA-specific options to be back-end agnostic
-   dyndns: new option dyndns\_refresh\_interval
-   resolver: Return PTR record as string
-   dyndns: New option dyndns\_update\_ptr
-   dyndns: new option dyndns\_force\_tcp
-   dyndns: new option dyndns\_auth
-   Split out the common code from timed DNS updates
-   Active Directory dynamic DNS updates
-   AD: Always initialize ID mapping
-   Only check UPN if enterprise principals are not used
-   Updating the translations for the 1.10 beta1 release
-   Update the version for the 1.10 beta2 release
-   Actually use the index parameter in
    resolv\_get\_sockaddr\_address\_index
-   Fix a typo in sssd-ad man page
-   tests: Do not set cwd twice
-   Enable the AD dynamic DNS updates by default
-   man: Clarify that AD dyndns updates are secured using GSS-TSIG
-   LDAP: Always initialize idmap object
-   Re-add a useful DEBUG message
-   man: Clarify the AD site discovery documentation
-   man: Note that IPA updates are secured with GSS-TSIG
-   Remove unneeded parameter of setup\_child and namespace it
-   Fix dyndns timer initialization
-   IPA: Check for ENOMEM
-   Remove unneeded comment
-   FO: Fix setting status of duplicates
-   AD dyndns: extract the host name from URI
-   Add utility functions for formatting fully-qualified names
-   Check the validity of FQname format prior to using it
-   Allow flat name in the FQname format
-   Remove branching to improve readability
-   tests: Link fqnames\_tests with libsss\_test\_common.la
-   Do not obfuscate calls with booleans
-   LDAP: sdap\_id\_ctx might contain several connections
-   LDAP: Refactor account info handler into a tevent request
-   LDAP: Pass in a connection to ID functions
-   LDAP: new SDAP domain structure
-   LDAP: return sdap search return code to ID
-   Move domain\_to\_basedn outside IPA subtree
-   New utility function sss\_get\_domain\_name
-   LDAP: split a function to create search bases
-   LDAP: store FQDNs for trusted users and groups
-   Split generating primary GID for ID mapped users into a separate
    function
-   LDAP: Do not store separate GID for subdomain users
-   AD: Add additional service to support Global Catalog lookups
-   AD ID lookups - choose GC or LDAP as appropriate
-   AD: Store trusted AD domains as subdomains
-   rpm: Fold libsss\_sudo and libsss\_autofs back into the main SSSD
    package
-   dyndns: Fix NULL check
-   man: document the need to set ldap\_access\_order
-   A new option krb5\_use\_kdcinfo
-   Fix allocation check in the AD provider
-   rpm: Use hardened flags for RPM build
-   rpm: Split providers into separate subpackages
-   Update transifex URL to transifex.com
-   Updating translations for the 1.10 beta2 release
-   Bumping the version for the 1.10 final release
-   Use the correct talloc context when creating AD subdomains
-   AD: Fix segfault in DEBUG message
-   AD: Remove ad\_options-&gt;auth options reference
-   rpm: couple of small fixes
-   Fix allocation check
-   Fix dp\_copy\_options
-   FO: Check the return value of send\_fn
-   LDAP: Retry SID search based on result of LDAP search, not the
    return code
-   IPA: Do not download or store the member attribute of host groups
-   AD: kinit with the local DC even when talking to a GC
-   KRB5: guess UPN for subdomain users
-   AD: Write out domain-realm mappings
-   Fix compilation warning
-   Update the translations for the 1.10.0 release
-   Update the version for the 1.10.0 release
-   Updating the version for the 1.10.1 release

James Hogarth (1):

-   Make TTL configurable for dynamic dns updates

Jan Cholasta (8):

-   LDAP: If deref search fails, try again without deref
-   Add exit status section to sss\_ssh\_\* man pages
-   UTIL: Add function sss\_names\_init\_from\_args
-   SSH: Fix parsing of names from client requests
-   SSH: Use separate field for domain name in client requests
-   SSH: Do not skip domains with use\_fully\_qualified\_names in host
    key requests
-   SSH: When host is removed from LDAP, remove it from the cache as
    well
-   SSH: Update known\_hosts file after unsuccessful requests as well.

Jan Engelhardt (1):

-   sysdb: try dealing with binary-content attributes

John Hodrien (1):

-   Correct sss\_ssh\_knowhostsproxy typo in man pages

Kamil Dudka (1):

-   sssd-1.8.0: work around a bug in cov-build from Coverity

Lukas Slebodnik (37):

-   Improved readability of get\_next\_domain()
-   Fixed typo in debug message.
-   Removing unused parameter type from
    sudosrv\_get\_sudorules\_query\_cache()
-   Reuse sss\_open\_cloexec at other places in code.
-   More generalized function open\_debug\_file\_ex()
-   Removing unused header file providers.h
-   Fix sss\_client breakage.
-   Removing unused declaration of functions and variable.
-   Making the ldb check configurable
-   Fixing duplicate const
-   Reusing create\_pam\_data() on the other places.
-   Making the authtok structure really opaque.
-   LDAP: Fix value initialization warnings
-   Incorrect \*.py\[co\] files placement
-   Fix krbcc dir creation issue with MIT krb5 1.11
-   Default TEST\_DIR to cwd, not empty string if not set explicitly
-   SUDO: IPA provider
-   Fixes compilation without selinux.
-   Fix broken build with selinux.
-   Fix segfault in AD Subdomains Module
-   Fixing critical format string issues.
-   Adding script to create a SRPM
-   Removing unused functions.
-   Adding option to disable retrieving large AD groups.
-   Making order in tests.
-   Remove empty directories after tests run.
-   Prevent segfault while processing ASQ request
-   Fix compilation with disabled link\_all\_deplibs.
-   Use deep copy for dns\_domain and discovery\_domain
-   Fix dereference after a NULL check in tests.
-   Change order of libraries in linking process.
-   Fix wrong detection of krb5 ccname
-   Every time return directory for krb5 cache collection.
-   Do not switch to credentials everytime.
-   Add missing argument to DEBUG message
-   Handle too many results from getnetgr.
-   Do not call sss\_cmd\_done in function check\_cache.

Michal Zidek (22):

-   sss\_debuglevel: Multiple arguments are treated as error.
-   Include talloc log in our debug facility
-   failover: Protect against empty host names
-   sss\_cache: Call DEBUG\_INIT sooner
-   tools: Respect use\_fully\_qualified\_names
-   Possible null derefence in ipa\_subdomains.c.
-   Unchecked return value in files.c
-   Use the same dbg level for all ncache hits.
-   Remove the alt\_db\_path parameter of sysdb\_init
-   File descriptor leak in nss responder.
-   Debug message in sss\_mc\_create\_file.
-   Move SELinux processing to provider.
-   Reuse cached SELinux mappings.
-   Make the SELinux refresh time configurable.
-   tests: Print warning if LDB\_MODULES\_PATH is not set
-   Check for waitpid failure at wrong place.
-   Wrong condition after waitpid.
-   sss\_cache: support for subdomains
-   sss\_cache: Remove annoying messages
-   Inform about function duplication.
-   libsss\_idmap: function to calculate range
-   Rename SAFEALIGN macros.

Milan Cejnar (1):

-   tools: append new line to string from poptStrerror()

Nathaniel
[McCallum?](https://docs.pagure.org/sssd-test2/McCallum.html){.missing
.wiki} (1):

-   Add support for krb5 1.11's responder callback.

Ondrej Kos (25):

-   MAN: quotation fix
-   Display more information on DB version mismatch
-   SYSDB: split sysdb\_add\_user
-   TESTS: Fix coverity issues 13126, 13127
-   TESTS: include error message on fail
-   Fix uninitialized time\_t var in responder
-   krb5\_child: fix value type and initialization
-   Fix initialization of multiple variables
-   Fix coverity issue 13136
-   Decrease krb5\_auth\_timeout default
-   Update README file
-   LDAP: Fix value initialization
-   Provide libnl3 support
-   DB: Switch to new libini\_config API
-   CONFDB: prevent double free
-   IDMAP: Fix variable initialization
-   Fix segfault in DYNDNS
-   DB: Fix segfault when configuration file cannot be parsed
-   Move nscd.c from tools to util
-   Check NSCD configuration file
-   Fail with misconfigured id-mapping ranges
-   MAN: state default dyndns interface
-   DB: Don't add invalid ranges
-   Don't test for NULL in nscd config check
-   KRB: Handle preauthentication error correctly

Paul B. Henson (1):

-   Add ignore\_group\_members option.

Pavel Březina (63):

-   sudo: do not hardcode protocol version
-   fix -O3 variable may be uninitialized warnings
-   sudo: print message if old protocol is used
-   sudo manpage: clarify that sudoHost may contain wildcards and not
    regular expression
-   use talloc\_zfree when freeing rhostent in resolver
-   set ret to EOK after for loop in sdap\_sudo\_purge\_sudoers
-   Fix LDAP authentication - invalid password length
-   set struct bet\_info-&gt;bet\_type
-   krb: recreate ccache if it was deleted
-   dp: check whether hostid backend is configured before filing be
    request
-   get\_next\_domain() test dom-&gt;parent-&gt;next for NULL
-   subdomains: replace invalid characters with underscore in krb5
    mapping file name
-   if selinux is disabled, ignore that selogin dir is missing
-   sdap\_fill\_memberships: continue if a member is not foud in sysdb
-   Add debug message to autofs client
-   autofs: fix invalid header 'number of entries' in packet
-   build: require libcmocka on fedora 18+
-   fix segfault in nss responder unit test
-   krb5-utils-tests: remove invalid condition
-   correct order in error\_to\_str table
-   do not leak memory on failure in \*\_process\_init()
-   change responder contexts hierarchy
-   coding style fix
-   refactor nested group processing: add new code
-   refactor nested group processing: replace old code
-   resolv: add resolv\_get\_domain request to resolv utils
-   resolv: add resolv\_discover\_srv request to resolv utils
-   DNS sites support - SRV lookup plugin interface
-   DNS sites support - SRV DNS lookup plugin
-   fail over - add function to insert multiple servers to the list
-   DNS sites support - replace SRV lookup code with a plugin call
-   DNS sites support - use SRV DNS lookup plugin in all providers
-   DNS sites support - add IPA SRV plugin
-   sudo client: remove dead code
-   add fo\_discover\_servers request
-   IPA SRV plugin: use fo\_discover\_servers request
-   IPA SRV plugin: improve debugging
-   sdap: add sdap\_connect\_host request
-   add sss\_ldap\_encode\_ndr\_uint32
-   DNS sites support - add AD SRV plugin
-   dns srv plugin: compare domain names case insensitive
-   AD SRV plugin: check if site name is empty
-   fo\_discover\_servers\_send: don't crash when backup\_domain is NULL
-   sudo responder: search rules for subdomains in parent domain subtree
-   back end: periodic task API
-   back end: periodical refresh of expired records API
-   back end: add refresh expired records periodic task
-   providers: refresh expired netgroups
-   be\_ptask: send and recv shadow a global declaration
-   be\_refresh: send and recv shadow a global declaration
-   failover: set state-&gt;out when meta server remains in
    SRV\_RESOLVE\_ERROR
-   subdomains: touch krb5.conf when creating new domain-realm mappings
-   nested groups: allocate more space if deref returns more members
-   handle ERR\_ACCOUNT\_EXPIRED properly
-   nested groups: do not return ENOMEM if num\_groups is 0
-   nested groups: do not expect any particular number of groups
-   failover: do not return invalid pointer when server is already
    present
-   failover: return error when SRV lookup returned only duplicates
-   collapse\_srv\_lookup may free the server, make it clear from the
    API
-   failover: if expanded server is marked as neutral, invoke srv
    collapse
-   init script: source /etc/sysconfig/sssd
-   fix dead code in fail\_over\_srv.c
-   sudo responder: use different callback for oob refresh

Simo Sorce (132):

-   Add helpers to set common mc record fields
-   Save errno before it might be modified.
-   Revert "Avoid accessing half-deallocated memory when using
    talloc\_zfree macro."
-   Avoid duplicating macros
-   Avoid const warnings when deallocating memory
-   Fix tevent\_req style for krb5\_auth
-   Fix ipa\_subdomain\_id names and tevent\_req style
-   Fix tevent\_req style for get\_netgroup in ipa\_id
-   Streamline ipa\_account\_info handler
-   Use an entry type mask macro to filter entry types
-   Fix comment on wrong line
-   Remove redundant definition.
-   Fix tevent\_req style for sdap\_async\_sudo.
-   Remove unhelpful vtable from sss\_cache
-   Remove dead netgroup functions
-   Revert "Add a default section to a switch-statement"
-   Add sysdb\_search\_service() helper function
-   Use sysdb\_search\_service() for all svc queries
-   Fix sdap reinit.
-   Code can only check for cached passwords
-   Add function to safely wipe memory.
-   Add authtok utility functions.
-   Change pam data auth tokens.
-   Use new sysdb\_search\_service() in sss\_cache
-   The Big sysdb/domain split-up!
-   Refactor sysdb initialization
-   Refactor single domain initialization
-   Remove the sysdb\_ctx\_get\_domain() function.
-   Make sysdb\_user\_dn() require a domain explictly.
-   Make sysdb\_group\_dn() require a domain explictly.
-   Make sysdb\_netgroup\_dn() require a domain explictly.
-   Make sysdb\_netgroup\_base\_dn() require a domain.
-   Make sysdb\_domain\_dn() require a domain.
-   Make sysdb\_custom\_dn() require a domain.
-   Make sysdb\_custom\_subtree\_dn() require a domain.
-   Move range objects into their own top-level tree.
-   Upgrade DB and move ranges into top level object
-   Pass domain to sysdb\_get&lt;pw/gr&gt;nam() functions
-   Pass domain to sysdb\_get&lt;pwu/grg&gt;&lt;id() functions
-   Pass domain to sysdb\_enum&lt;pw/gr&gt;ebt() functions
-   Add domain option to sysdb\_get/netgr/attrs() fns
-   Add domain argument to sysdb\_initgroups()
-   Add domain argument to sysdb\_get\_user\_attr()
-   Add domain to sysdb\_search\_user\_by\_name()
-   Add domain to sysdb\_search\_user\_by\_uid()
-   Add domain to sysdb\_search\_group\_by\_name()
-   Add domain to sysdb\_search\_group\_by\_gid()
-   Add domain arg to sysdb\_search\_netgroup\_by\_name()
-   Add domain argument to sysdb\_set\_user\_attr()
-   Add domain argument to sysdb\_set\_group\_attr()
-   Add domain argument to sysdb\_set\_netgroup\_attr()
-   Add domain argument to sysdb\_get\_new\_id()
-   Add domain argument to sysdb\_add\_basic\_user()
-   Add domain argument to sysdb\_add\_user()
-   Add domain arguments to sysdb\_add\_group functions.
-   Add domain arguments to sysdb\_add\_inetgroup fns.
-   Add domain argument to sysdb\_store\_user()
-   Add domain argument to sysdb\_store\_group()
-   Add domain arg to sysdb group member functions
-   Add domain argument to sysdb\_cache\_password()
-   Add domain argument to sysdb\_cache\_auth()
-   Add domain argument to sysdb\_store\_custom()
-   Add domain argument to sysdb\_search\_custom()
-   Add domain to sysdb\_delete\_custom
-   Add domain arg to sysdb\_search\_users()
-   Add domain argument to sysdb\_delete\_user()
-   Add domain argument to sysdb\_search\_groups()
-   Add domain argument to sysdb\_delete\_group()
-   Add domain arg to sysdb\_search/delete\_netgroup()
-   Add domain argument to sysdb\_has/set\_enumerated()
-   Add domain argument to sysdb\_remove\_attrs()
-   Add domain argument to sysdb\_idmap\_ funcitons
-   Add domain arguemnt to sysdb\_get\_real\_name()
-   Add domain argument to sysdb autofs functions
-   Add domain argument to sysdb selinux functions
-   Add domain arguments to sysdb services functions
-   Add domain arguments to sysdb ssh functions
-   Add domain arguments to sysdb sudo functions
-   Add domain to some subdomain functions
-   Pass the domain to upgrade functions
-   Move mpg flag to the domain where it belongs
-   Kill sysdb-&gt;domain
-   Stop creating fake sysdb contexts
-   Tidy up BASE dn macros
-   Remove outdated code.
-   Move ldap provider access functions
-   Remove sysdb as a be context structure member
-   Remove sysdb as a be request structure member
-   Remove sysdb argument from ipa\_host\_info\_send()
-   Remove unused structure
-   Remove sysdb argument from hbac\_user\_attrs\_to\_rule()
-   Remove sysdb arg from hbac\_service\_attrs\_to\_rule()
-   Remove sysdb arg from hbac\_\*host\_attrs\_to\_rule()
-   Remove sysdb arg from ipa\_hbac\_service\_info\_send()
-   Remove sysdb arg from \[ipa\_\]hbac\_sysdb\_save()
-   Remove sysdb argument from hbac\_get\_cached\_rules()
-   Remove hbac\_ctx\_sysdb()
-   Remove hbac\_ctx\_be()
-   Remove hbac\_ctx\_ev()
-   Remove hbac\_ctx\_sdap\_id\_\[ctx|op\]()
-   Move hbac\_ctx\_is\_offline()
-   Do not pass NULL to ipa\_subdomain\_retrieve()
-   Split simple\_access\_check function out
-   Pass domain not be\_req to access check functions
-   Remove domain from be\_req structure
-   Introduce be\_req\_terminate() helper
-   Add be\_req\_create() helper
-   Add be\_req\_get\_be\_ctx() helper.
-   Add be\_req\_get\_data() helper funciton.
-   Make struct be\_req opaque
-   Add realm info to sss\_domain\_info
-   Avoid sysdb\_subdom in sysdb\_get\_subdomains()
-   Update main domain info in place
-   Refactor sysdb\_master\_domain\_add\_info()
-   Add sysdb\_subdomain\_store() function
-   Remove sysdb\_subdom completely
-   Add function get\_next\_domain()
-   Add ability to disable domains
-   Change the way domains are linked.
-   Parent and subdomains use the same sysdb
-   Introduce IS\_SUBDOMAIN() macro
-   krb5\_child style fix
-   Refactor krb5 child
-   Add SSSD specific error codes and definitions
-   Use SSSD specific errors for offline auth
-   Return ERR\_INTERNAL instead of EIO
-   Cleanup error message handling for krb5 child
-   Improve IS\_SSSD\_ERROR() macro
-   Use common error facility instead of sdap\_result
-   Convert sdap\_access to new error codes
-   ldap: Fallback option for rfc2307 schema
-   Further restrict become\_user drop of privileges.

Stef Walter (1):

-   Add a domain config attribute for realmd

Stephen Gallagher (13):

-   LDAP: Better debug logging when saving groups
-   Correct format security for talloc\_named of auth tokens
-   Fix minor grammar error in log
-   NSS: Add original homedir to home directory template options
-   BUILD: Build shared components as an internal shared library
-   BUILD: Add contributed macros and aliases to simplify building
-   BUILD: Include build aliases in the tarball
-   BUILD: Fix cmocka detection
-   BUILD: Fix up whitespace in Makefile.am
-   BUILD: Always run distcheck and RPM tests in /dev/shm
-   Remove old hash support from example spec
-   Add 'description' attribute to SSSDConfig API
-   Configure SYSV init scripts properly

Sumit Bose (54):

-   Add a default section to a switch-statement
-   Fix and rename get\_my\_domain\_data()
-   Refactoring: remove duplicated code in nss responder
-   Allow usage of enterprise principals
-   Make IPA SELinux provider aware of subdomain users
-   Add override\_homedir.xml to po4a.cfg
-   Remove unused TALLOC\_CTX from responder\_get\_domain()
-   responder\_get\_domain: do not return disabled domains
-   responder\_get\_domain(): remove timeout calculation
-   LDAP: always store SID if available
-   Add secid filter to responder-dp protocol
-   Add two new request types to the data-provider interface
-   Add idmap context to nss context
-   Add responder\_get\_domain\_by\_id()
-   sysdb: add sysdb\_search\_object\_by\_sid()
-   Add sss\_ncache\_set\_sid() and sss\_ncache\_check\_sid()
-   Remove unused attribute list
-   Use struct to hold different types of request parameters
-   Add SID related lookups to IPA subdomains
-   Add SID related calls to the NSS responder
-   Add client library for SID related lookups
-   Add python interface to libsss\_nss\_idmap
-   AD: read flat name and SID of the AD domain
-   Add missing \\n to debug string
-   Fix missing initialization in Python bindings for libsss\_nss\_idmap
-   Add support for tuples and unicode pysss\_nss\_idmap.so
-   Always update cached upn if enterprise principals are used
-   Fix return code for AD subdomain request
-   pysss\_nss\_idmap: do not treat strings as sequences
-   IPA: Always initialize ID mapping
-   Handle SID strings in sdap\_attrs\_get\_sid\_str() as well
-   IPA: read user and group SID
-   Add SID related requests to the LDAP provider
-   Set canonicalize flag if enterprise principals are used
-   Lookup domains at startup
-   Add be request queue
-   Use queue for get\_subdomains
-   Read SIDs of groups with sysdb\_initgroups() as well
-   Enhance PAC responder for AD users
-   Intermittent fix for get\_user\_and\_group\_users\_done
-   Always send the PAC to the PAC responder
-   Implicitly activate the PAC responder for AD provider
-   Fix some doxygen warnings
-   Use principal from the ticket to find validation entry
-   Set default realm for enterprise principals
-   PAC: do not expect that sysdb\_search\_object\_by\_sid() return
    ENOENT
-   PAC: do not delete originalDN or cached password if present
-   KRB5: use the right authtok type for renewals
-   Fix typo in pack\_authtok()
-   Revert "Always send the PAC to the PAC responder"
-   krb5: do not send pac for IPA users from the local domain
-   krb5: do not use enterprise principals for renewals
-   Revert "Implicitly activate the PAC responder for AD provider"
-   Use forest for GC SRV lookups

Thorsten Scherf (1):

-   Updated Doxygen configuration to 1.8.1

Yuri Chornoivan (3):

-   Fix typos in man pages
-   Fix minor typos
-   Fix minor typos

