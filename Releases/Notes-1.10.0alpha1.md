Highlights {#Highlights}
----------

-   Includes a fix for
    [[​]{.icon}CVE-2013-0287](https://lists.fedorahosted.org/pipermail/sssd-devel/2013-March/014066.html){.ext-link}:
    A simple access provider flaw prevents intended ACL use when SSSD is
    configured as an Active Directory client
-   Many internal interfaces were refactored, making the code more
    readable and maintanable in the long term. This refactoring includes
    the subdomains code, the sysdb interface as a whole, internal error
    code reporting, SELinux login context processing and processing of
    nested LDAP groups.
-   A new option `ipa_dyndns_ttl` was added, allowing the client to set
    a custom TTL on IPA dynamic DNS updates
-   A new `ignore_group_members` option was added. This option can be
    used to suppress downloading group members on group lookups, making
    the group lookups much faster for environments that do not need to
    know the group members.
-   A new option `ldap_rfc2307_fallback_to_local_users` was added. If
    this option is set to true, SSSD is be able to resolve local group
    members of LDAP groups.
-   Added support for krb5 1.11's responder callback.
-   Support for libnl version 3 was added.
-   Fixed an indexing bug that prevented the contents of autofs maps
    from being returned to the automounter deamon in case the map
    contained a large number of entries
-   Fixed spurious password expiration warning that was printed on login
    with the Kerberos back end
-   Fixed a regression when saving binary attributes to the cache
-   Fixed a file descriptor leak when sss\_cache was executed

Packaging Changes {#PackagingChanges}
-----------------

-   The shared components of the SSSD are now built as a shared library
    to reduce amount of duplicated code being linked into multiple SSSD
    binaries and lower the disk usage of SSSD installation.
-   The check that ensured that SSSD is running with the same ldb
    version it was built against was made optional, defaulting to false.
    You can enable the strict check again by selecting
    `--enable-ldb-version-check` during configure

Tickets Fixed {#TicketsFixed}
-------------

<div>

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

[\#1405](/sssd/ticket/1405 "[RFE] Kerberos canonicalization should be skipped on password-changes in ..."){.closed}
:   \[RFE\] Kerberos canonicalization should be skipped on
    password-changes in AD provider

[\#1476](/sssd/ticket/1476 "SSSD has a much longer TTL when updating a DNS record than IPA client ..."){.closed}
:   SSSD has a much longer TTL when updating a DNS record than IPA
    client install placed in the beginning

[\#1481](/sssd/ticket/1481 "Move sss_cache to the main subpackage"){.closed}
:   Move sss\_cache to the main subpackage

[\#1484](/sssd/ticket/1484 "failover should protect against empty host names"){.closed}
:   failover should protect against empty host names

[\#1495](/sssd/ticket/1495 "include talloc log in our debug facility"){.closed}
:   include talloc log in our debug facility

[\#1575](/sssd/ticket/1575 "Change responder contexts hierarchy"){.closed}
:   Change responder contexts hierarchy

[\#1586](/sssd/ticket/1586 "Make authtoken opaque objects"){.closed}
:   Make authtoken opaque objects

[\#1712](/sssd/ticket/1712 "sudoNotBefore/sudoNotAfter not supported by sssd sudoers plugin"){.closed}
:   sudoNotBefore/sudoNotAfter not supported by sssd sudoers plugin

[\#1738](/sssd/ticket/1738 "Decrease the krb5_auth_timeout default value of 15"){.closed}
:   Decrease the krb5\_auth\_timeout default value of 15

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

[\#1771](/sssd/ticket/1771 "Negative cache messages are displayed at too low of a DEBUG level"){.closed}
:   Negative cache messages are displayed at too low of a DEBUG level

[\#1790](/sssd/ticket/1790 "Possible null derefence in ipa_subdomains.c"){.closed}
:   Possible null derefence in ipa\_subdomains.c

[\#1794](/sssd/ticket/1794 "reuse open_cloexec elsewhere in the code"){.closed}
:   reuse open\_cloexec elsewhere in the code

[\#1803](/sssd/ticket/1803 "SSSD returns System Error if the ccachedir is not writable"){.closed}
:   SSSD returns System Error if the ccachedir is not writable

[\#1804](/sssd/ticket/1804 "Filter out inappropriate multicast and subnet broadcast addresses from IPA ..."){.closed}
:   Filter out inappropriate multicast and subnet broadcast addresses
    from IPA dynamic DNS update

[\#1810](/sssd/ticket/1810 "Uninitialized scalar variable in responder_get_domain"){.closed}
:   Uninitialized scalar variable in responder\_get\_domain

[\#1811](/sssd/ticket/1811 "Unchecked return value in tests"){.closed}
:   Unchecked return value in tests

[\#1813](/sssd/ticket/1813 "make the ldb check configurable"){.closed}
:   make the ldb check configurable

[\#1819](/sssd/ticket/1819 "Refresh doxygen template files"){.closed}
:   Refresh doxygen template files

[\#1820](/sssd/ticket/1820 "sysdb unit tests uses system memberof"){.closed}
:   sysdb unit tests uses system memberof

[\#1833](/sssd/ticket/1833 "segmentation fault in cmocka unit tests with raised optization level"){.closed}
:   segmentation fault in cmocka unit tests with raised optization level

[\#1834](/sssd/ticket/1834 "Support for libini 1.0"){.closed}
:   Support for libini 1.0

[\#1838](/sssd/ticket/1838 "nss and pam clients broken in master"){.closed}
:   nss and pam clients broken in master

[\#1840](/sssd/ticket/1840 "Add --with-test-dir=/dev/shm to DISTCHECK_CONFIGURE_FLAGS"){.closed}
:   Add --with-test-dir=/dev/shm to DISTCHECK\_CONFIGURE\_FLAGS

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Abhishek Singh (1):

-   filename in comment is corrected

Ariel Barria (1):

-   Improve syslog message when configuration cannot be loaded

Jakub Hrozek (44):

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

James Hogarth (1):

-   Make TTL configurable for dynamic dns updates

Jan Cholasta (1):

-   LDAP: If deref search fails, try again without deref

Jan Engelhardt (1):

-   sysdb: try dealing with binary-content attributes

John Hodrien (1):

-   Correct sss\_ssh\_knowhostsproxy typo in man pages

Kamil Dudka (1):

-   sssd-1.8.0: work around a bug in cov-build from Coverity

Lukas Slebodnik (12):

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

Michal Zidek (15):

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

Milan Cejnar (1):

-   tools: append new line to string from poptStrerror()

Nathaniel
[McCallum?](https://docs.pagure.org/sssd-test2/McCallum.html){.missing
.wiki} (1):

-   Add support for krb5 1.11's responder callback.

Ondrej Kos (13):

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

Paul B. Henson (1):

-   Add ignore\_group\_members option.

Pavel Březina (25):

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

Simo Sorce (131):

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

Stephen Gallagher (10):

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

Sumit Bose (1):

-   Add a default section to a switch-statement

Thorsten Scherf (1):

-   Updated Doxygen configuration to 1.8.1

