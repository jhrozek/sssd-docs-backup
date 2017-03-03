Highlights {#Highlights}
----------

-   The Active Directory provider now includes support for retrieving
    identity information and authentication as users from trusted
    domains in the same forest. The SSSD looks up the information using
    the Global Catalog. Currently this feature is only supported when
    the SSSD is connected to the forest root.
-   The group memberships for Active Directory users are read from the
    PAC during login. If the PAC is not available (such as when group
    membership is requested for a user who has never logged in), the
    SSSD falls back to using tokenGroups.
-   The Active Directory provider is able to autodiscover the NetBIOS
    (flat) name of the domain it connects to. The NetBIOS name is
    discovered automatically on startup.
-   The full\_name\_format option now accepts a new parameter that
    expands to the NetBIOS name of the domain
-   The new krb5\_use\_kdcinfo option allows the administrator to
    disable the Kerberos locator plugin and rely on information read
    from the krb5.conf file completely.
-   A new option ldap\_disable\_range\_retrieval was added. Switching
    this option to True skips large Active Directory groups that might
    otherwise take a long time to download and process.
-   A new option refresh\_expired\_interval was added. This option
    allows to configure a background task that would automatically
    refresh entries that are nearing their expiration time. In this
    release, only refreshing netgroups is implemented.

Packaging Changes {#PackagingChanges}
-----------------

-   The Makefile has been amended so that it no longer uses overlinking
    which is disabled by default on some distributions (such as Debian
    and its derivatives)
-   The upstream RPM specfile now packages each provider separately. The
    SSSD deamon and the responders are now included in the sssd-common
    package, while the sssd package has become a "meta package" that
    Requires all the existing providers for backwards compatibility.
-   The libsss\_sudo and libsss\_autofs libraries are now part of the
    sssd-common package

Tickets Fixed {#TicketsFixed}
-------------

-   [\#1510](https://fedorahosted.org/sssd/ticket/1510 "task: Split providers into their own subpackages (closed: fixed)"){.closed
    .ticket} - Split providers into their own subpackages
-   [\#1797](https://fedorahosted.org/sssd/ticket/1797 "task: Use hardened flags for building RPMs (closed: fixed)"){.closed
    .ticket} - Use hardened flags for building RPMs
-   [\#1976](https://fedorahosted.org/sssd/ticket/1976 "defect: Copy-n-paste error in AD provider (closed: fixed)"){.closed
    .ticket} - Copy-n-paste error in AD provider
-   [\#1883](https://fedorahosted.org/sssd/ticket/1883 "defect: Add a new option to disable the Kerberos locator plugin completely (closed: fixed)"){.closed
    .ticket} - Add a new option to disable the Kerberos locator plugin
    completely
-   [\#1713](https://fedorahosted.org/sssd/ticket/1713 "enhancement: [RFE] Add a task to the SSSD to periodically refresh cached entries (closed: fixed)"){.closed
    .ticket} - \[RFE\] Add a task to the SSSD to periodically refresh
    cached entries
-   [\#1891](https://fedorahosted.org/sssd/ticket/1891 "task: unite periodic refresh API (closed: fixed)"){.closed
    .ticket} - unite periodic refresh API
-   [\#1789](https://fedorahosted.org/sssd/ticket/1789 "defect: ldap_access_order improvements (man page fix) (closed: fixed)"){.closed
    .ticket} - ldap\_access\_order improvements (man page fix)
-   [\#1972](https://fedorahosted.org/sssd/ticket/1972 "defect: Dereference after a NULL check in tests/common_dom.c (closed: fixed)"){.closed
    .ticket} - Dereference after a NULL check in tests/common\_dom.c
-   [\#1971](https://fedorahosted.org/sssd/ticket/1971 "defect: Dereference before NULL check in nscd.c (closed: fixed)"){.closed
    .ticket} - Dereference before NULL check in nscd.c
-   [\#1816](https://fedorahosted.org/sssd/ticket/1816 "defect: Non-fatal errors looking up trusted domains with IPA back end (closed: fixed)"){.closed
    .ticket} - Non-fatal errors looking up trusted domains with IPA back
    end
-   [\#1845](https://fedorahosted.org/sssd/ticket/1845 "defect: move libsss_sudo and libsss_autofs back into the main sssd package (closed: fixed)"){.closed
    .ticket} - move libsss\_sudo and libsss\_autofs back into the main
    sssd package
-   [\#364](https://fedorahosted.org/sssd/ticket/364 "enhancement: [RFE] Recognize trusted domains in AD provider (closed: fixed)"){.closed
    .ticket} - \[RFE\] Recognize trusted domains in AD provider
-   [\#1557](https://fedorahosted.org/sssd/ticket/1557 "enhancement: [RFE] Use the Global Catalog in SSSD for the AD provider (closed: fixed)"){.closed
    .ticket} - \[RFE\] Use the Global Catalog in SSSD for the AD
    provider
-   [\#1558](https://fedorahosted.org/sssd/ticket/1558 "enhancement: [RFE] Use MS-PAC to retrieve user's group list (closed: fixed)"){.closed
    .ticket} - \[RFE\] Use MS-PAC to retrieve user's group list
-   [\#1951](https://fedorahosted.org/sssd/ticket/1951 "defect: NetBIOS domain name should be read at startup (closed: fixed)"){.closed
    .ticket} - NetBIOS domain name should be read at startup
-   [\#1929](https://fedorahosted.org/sssd/ticket/1929 "defect: Junk character in sssd_domain.log for domain string when sssd tries to go ... (closed: fixed)"){.closed
    .ticket} - Junk character in sssd\_domain.log for domain string when
    sssd tries to go online from offline mode
-   [\#1928](https://fedorahosted.org/sssd/ticket/1928 "defect: Libtool fails to find dependent libraries (closed: fixed)"){.closed
    .ticket} - Libtool fails to find dependent libraries
-   [\#1950](https://fedorahosted.org/sssd/ticket/1950 "defect: segfault while processing ASQ request (closed: fixed)"){.closed
    .ticket} - segfault while processing ASQ request
-   [\#1924](https://fedorahosted.org/sssd/ticket/1924 "defect: MAN: Make it clear which address is used to update DNS records (closed: fixed)"){.closed
    .ticket} - MAN: Make it clear which address is used to update DNS
    records
-   [\#1648](https://fedorahosted.org/sssd/ticket/1648 "defect: Fully qualified account names form should be able to use flatname in the ... (closed: fixed)"){.closed
    .ticket} - Fully qualified account names form should be able to use
    flatname in the fq format
-   [\#1930](https://fedorahosted.org/sssd/ticket/1930 "defect: Crash with negative values in ldap_idmap_range_size (closed: fixed)"){.closed
    .ticket} - Crash with negative values in ldap\_idmap\_range\_size
-   [\#1823](https://fedorahosted.org/sssd/ticket/1823 "defect: getgrnam / getgrgid for large user groups is too slow due to range ... (closed: fixed)"){.closed
    .ticket} - getgrnam / getgrgid for large user groups is too slow due
    to range retrieval functionality
-   [\#1927](https://fedorahosted.org/sssd/ticket/1927 "task: Provide a script to create a SRPM without having to run configure (closed: fixed)"){.closed
    .ticket} - Provide a script to create a SRPM without having to run
    configure
-   [\#1785](https://fedorahosted.org/sssd/ticket/1785 "defect: NSCD warning is irritating (closed: fixed)"){.closed
    .ticket} - NSCD warning is irritating
-   [\#1934](https://fedorahosted.org/sssd/ticket/1934 "defect: sssd crashes if junk is present in sssd.conf (closed: fixed)"){.closed
    .ticket} - sssd crashes if junk is present in sssd.conf
-   [\#1772](https://fedorahosted.org/sssd/ticket/1772 "task: Rename or alias the SAFEALIGN macros (closed: fixed)"){.closed
    .ticket} - Rename or alias the SAFEALIGN macros
-   [\#1909](https://fedorahosted.org/sssd/ticket/1909 "defect: Clarify the AD site discovery in sssd-ad man page (closed: fixed)"){.closed
    .ticket} - Clarify the AD site discovery in sssd-ad man page
-   [\#1921](https://fedorahosted.org/sssd/ticket/1921 "defect: Login failure: Enterprise Principal enabled by default for AD Provider (closed: fixed)"){.closed
    .ticket} - Login failure: Enterprise Principal enabled by default
    for AD Provider
-   [\#1905](https://fedorahosted.org/sssd/ticket/1905 "defect: pysss_nss_idmap improvements (closed: fixed)"){.closed
    .ticket} - pysss\_nss\_idmap improvements
-   [\#1914](https://fedorahosted.org/sssd/ticket/1914 "defect: pysss_nss_idmap:  Support also Unicode strings and return them by default (closed: fixed)"){.closed
    .ticket} - pysss\_nss\_idmap: Support also Unicode strings and
    return them by default
-   [\#1922](https://fedorahosted.org/sssd/ticket/1922 "defect: sssd_be crashes when looking up users in the LDAP provider with ID mapping (closed: fixed)"){.closed
    .ticket} - sssd\_be crashes when looking up users in the LDAP
    provider with ID mapping
-   [\#1910](https://fedorahosted.org/sssd/ticket/1910 "defect: Clarify that AD DNS updates are performed using GSS-TSIG (closed: fixed)"){.closed
    .ticket} - Clarify that AD DNS updates are performed using GSS-TSIG
-   [\#1915](https://fedorahosted.org/sssd/ticket/1915 "defect: Turn on dyndns updates by default in the AD provider (closed: fixed)"){.closed
    .ticket} - Turn on dyndns updates by default in the AD provider
-   [\#1912](https://fedorahosted.org/sssd/ticket/1912 "defect: SUDO is not working for users from trusted AD domain (closed: fixed)"){.closed
    .ticket} - SUDO is not working for users from trusted AD domain
-   [\#1468](https://fedorahosted.org/sssd/ticket/1468 "enhancement: [RFE] AD: Should be able to log in as long or short domains (closed: fixed)"){.closed
    .ticket} - \[RFE\] AD: Should be able to log in as long or short
    domains

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (45):

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

Jan Cholasta (4):

-   UTIL: Add function sss\_names\_init\_from\_args
-   SSH: Fix parsing of names from client requests
-   SSH: Use separate field for domain name in client requests
-   SSH: Do not skip domains with use\_fully\_qualified\_names in host
    key requests

Lukas Slebodnik (13):

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

Michal Zidek (1):

-   Rename SAFEALIGN macros.

Ondrej Kos (8):

-   Fix segfault in DYNDNS
-   DB: Fix segfault when configuration file cannot be parsed
-   Move nscd.c from tools to util
-   Check NSCD configuration file
-   Fail with misconfigured id-mapping ranges
-   MAN: state default dyndns interface
-   DB: Don't add invalid ranges
-   Don't test for NULL in nscd config check

Pavel Březina (5):

-   sudo responder: search rules for subdomains in parent domain subtree
-   back end: periodic task API
-   back end: periodical refresh of expired records API
-   back end: add refresh expired records periodic task
-   providers: refresh expired netgroups

Stef Walter (1):

-   Add a domain config attribute for realmd

Stephen Gallagher (2):

-   Remove old hash support from example spec
-   Add 'description' attribute to SSSDConfig API

Sumit Bose (21):

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

Yuri Chornoivan (1):

-   Fix minor typos

