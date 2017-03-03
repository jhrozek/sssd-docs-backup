<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Packaging Changes](#PackagingChanges)
    3.  [Documentation Changes](#DocumentationChanges)
    4.  [Tickets Fixed](#TicketsFixed)
    5.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   A new responder, called InfoPipe was added. This responder provides
    a public D-Bus interface accessible over the system bus. In this
    release, methods for retrieving user attributes and list of groups
    were added as well as objects representing SSSD domains and
    processes. The next 1.12.x releases will publish objects
    representing users and groups, too.
-   SSSD provides an ID-mapping plugin for cifs-utils so that Windows
    SIDs can be mapped onto POSIX IDs and/or names without requiring
    Winbind and using the same code as the SSSD uses for identity
    information.
-   First phase of Group Policy-based access control for the AD provider
    was added. At the moment, the gpo-ldap component that downloads the
    list of GPOs that apply for the specific client has been implemented
    as well as the gpo-smb component that retrieves the group policy
    files and determines the access control check results based on those
    files. Future improvements will focus on storing the GPO policies as
    local files and mapping the Windows logon rights onto Linux PAM
    services.
-   journald can now be used to store debug logs. The journald support
    is not enabled by default. In order to enable it, compile SSSD with
    --with-syslog=journald.
-   Added a new library called sss\_sifp that provides a simple
    synchronous API for communication with our new InfoPipe responder
    over the system bus.
-   SSSD now works fine on systems that use Python 3 as their default
    interpreter, however, having Python 2 installed is still required.
-   Several patches that improve portability of SSSD, especially with
    consideration of BSD systems have been included
-   It is now possible to re-use a single LDAP attribute for several
    attribute mappings in sssd.conf. This enhancement is useful for
    environments that need to use a single ID number for both UID and
    GID.

Packaging Changes {#PackagingChanges}
-----------------

-   The sssd\_sifp library and the InfoPipe responder are packaged in
    their own subpackages

Documentation Changes {#DocumentationChanges}
---------------------

-   A new option ldap\_use\_tokengroups was added. Setting this option
    to False disables the support for tokenGroups, which is useful for
    environments that wish to restrict the group nesting level. Doing so
    with tokenGroups enabled is nontrivial since the tokenGroups
    attribute flattens the group memberships.
-   A new option homedir\_substring makes it possible to substitute a
    templatized home directory attribute for a client-side defined value
-   The new InfoPipe responder has several configuration options. Refer
    to the sssd-ifp manual page for details.
-   A new option offline\_timeout was added. This option allows the
    administrator to configure how often should SSSD attempt to
    reconnect when in offline mode
-   The LDAP provider has a new option ldap\_user\_extra\_attrs that
    enables the administrator to extend the map of attributes downloaded
    when looking up a user. These custom attributes can then be
    retrieved with the new DBus API.
-   The automounter master map name can now be configured with a new
    option ldap\_autofs\_map\_master\_name.
-   A new option ad\_gpo\_access\_control is available to let the user
    configure the behaviour of the GPO access control feature.

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1096](/sssd/ticket/1096 "Clock skew in krb5 auth should result in offline operation, not failure"){.closed}
:   Clock skew in krb5 auth should result in offline operation, not
    failure

[\#1187](/sssd/ticket/1187 "Delete IPA specific attribute mappings from man page"){.closed}
:   Delete IPA specific attribute mappings from man page

[\#1366](/sssd/ticket/1366 "[RFE] Optimize RFC2307bis lookups when user and group search bases do not ..."){.closed}
:   \[RFE\] Optimize RFC2307bis lookups when user and group search bases
    do not overlap

[\#1451](/sssd/ticket/1451 "Update manpage with the minimal value expected for ldap_idmap_range_size"){.closed}
:   Update manpage with the minimal value expected for
    ldap\_idmap\_range\_size

[\#1534](/sssd/ticket/1534 "[RFE] Integrate SSSD with CIFS client"){.closed}
:   \[RFE\] Integrate SSSD with CIFS client

[\#1585](/sssd/ticket/1585 "[RFE] Add a check to pam_sss to ensure that ..."){.closed}
:   \[RFE\] Add a check to pam\_sss to ensure that
    authtok\_type=SSS\_AUTHTOK\_TYPE\_PASSWORD is \\0 terminated

[\#1718](/sssd/ticket/1718 "Offline mode timeout not documented"){.closed}
:   Offline mode timeout not documented

[\#1866](/sssd/ticket/1866 "SSSD changes primary creds on authentication"){.closed}
:   SSSD changes primary creds on authentication

[\#1885](/sssd/ticket/1885 "Use a shorter retry timeout for SRV queries in cases the query cannot be ..."){.closed}
:   Use a shorter retry timeout for SRV queries in cases the query
    cannot be resolved (negative timeout)

[\#1918](/sssd/ticket/1918 "Undocument and deprecate ipa_hbac_support_srchost"){.closed}
:   Undocument and deprecate ipa\_hbac\_support\_srchost

[\#1923](/sssd/ticket/1923 "Create tickets to track unit test enhancements"){.closed}
:   Create tickets to track unit test enhancements

[\#2022](/sssd/ticket/2022 "Review Fedora 20 system wide changes and file corresponging tickets if ..."){.closed}
:   Review Fedora 20 system wide changes and file corresponging tickets
    if they affect SSSD

[\#2024](/sssd/ticket/2024 "Create unit test for nested groups"){.closed}
:   Create unit test for nested groups

[\#2037](/sssd/ticket/2037 "nondescriptive error message when ccache directory has wrong permissions"){.closed}
:   nondescriptive error message when ccache directory has wrong
    permissions

[\#2040](/sssd/ticket/2040 "Enable ad_compat sasl option"){.closed}
:   Enable ad\_compat sasl option

[\#2061](/sssd/ticket/2061 "ccache mangament simplification"){.closed}
:   ccache mangament simplification

[\#2072](/sssd/ticket/2072 "[RFE] Provide an experimental DBus responder to retrieve custom attributes ..."){.closed}
:   \[RFE\] Provide an experimental DBus responder to retrieve custom
    attributes from SSSD cache

[\#2073](/sssd/ticket/2073 "[RFE] Extend the LDAP backend to retrieve extended set of attributes"){.closed}
:   \[RFE\] Extend the LDAP backend to retrieve extended set of
    attributes

[\#2084](/sssd/ticket/2084 "check for active sessions not troll proc for uids"){.closed}
:   check for active sessions not troll proc for uids

[\#2094](/sssd/ticket/2094 "find uid tests fail"){.closed}
:   find uid tests fail

[\#2097](/sssd/ticket/2097 "Build library libsss_test_common in test phase"){.closed}
:   Build library libsss\_test\_common in test phase

[\#2125](/sssd/ticket/2125 "cifsidmap support should be optional"){.closed}
:   cifsidmap support should be optional

[\#2162](/sssd/ticket/2162 "[RFE] warn to syslog if an unresponsive subprocess is terminated"){.closed}
:   \[RFE\] warn to syslog if an unresponsive subprocess is terminated

[\#2171](/sssd/ticket/2171 "Do not start multiple backends for the same domain"){.closed}
:   Do not start multiple backends for the same domain

[\#2179](/sssd/ticket/2179 "Sssd dyndns update fails for addresses from different networks"){.closed}
:   Sssd dyndns update fails for addresses from different networks

[\#2195](/sssd/ticket/2195 "[RFE] Send debug logs to journald by default"){.closed}
:   \[RFE\] Send debug logs to journald by default

[\#2198](/sssd/ticket/2198 "remove unused tmp_ctx in async_resolv.c"){.closed}
:   remove unused tmp\_ctx in async\_resolv.c

[\#2210](/sssd/ticket/2210 "convert ad_account_can_shortcut to returning boolean"){.closed}
:   convert ad\_account\_can\_shortcut to returning boolean

[\#2225](/sssd/ticket/2225 "PO files changed during build"){.closed}
:   PO files changed during build

[\#2227](/sssd/ticket/2227 "[RFE] Expose domain object over DBus"){.closed}
:   \[RFE\] Expose domain object over DBus

[\#2234](/sssd/ticket/2234 "autogenerate introspection"){.closed}
:   autogenerate introspection

[\#2254](/sssd/ticket/2254 "[RFE] Create a library to simplify usage of D-Bus responder"){.closed}
:   \[RFE\] Create a library to simplify usage of D-Bus responder

[\#2258](/sssd/ticket/2258 "[src/providers/krb5/krb5_common.c:418] -> ..."){.closed}
:   \[src/providers/krb5/krb5\_common.c:418\] -&gt;
    \[src/providers/krb5/krb5\_common.c:418\]: (style) Same expression
    on both sides of '||'.

[\#2288](/sssd/ticket/2288 "sssd is crashing after several quick invokes of automount -m"){.closed}
:   sssd is crashing after several quick invokes of automount -m

[\#2290](/sssd/ticket/2290 "The DBus responder should not spawn a client socket"){.closed}
:   The DBus responder should not spawn a client socket

[\#2291](/sssd/ticket/2291 "make distcheck fails"){.closed}
:   make distcheck fails

[\#2304](/sssd/ticket/2304 "refactor splitting the selinux priority list"){.closed}
:   refactor splitting the selinux priority list

[\#2313](/sssd/ticket/2313 "consider going offline on KRB5KRB_ERR_GENERIC error instead of System ..."){.closed}
:   consider going offline on KRB5KRB\_ERR\_GENERIC error instead of
    System Error

[\#2319](/sssd/ticket/2319 "provide a compatible definition of ck_assert_uint_eq"){.closed}
:   provide a compatible definition of ck\_assert\_uint\_eq

[\#2321](/sssd/ticket/2321 "daemon FAILS to start with config file set to mode 400"){.closed}
:   daemon FAILS to start with config file set to mode 400

[\#2331](/sssd/ticket/2331 "sssd should also filter out S-1-18"){.closed}
:   sssd should also filter out S-1-18

</div>

<div>

[\#1503](/sssd/ticket/1503 "Document the IPC between different SSSD processes"){.closed}
:   Document the IPC between different SSSD processes

[\#2182](/sssd/ticket/2182 "[RFE] Add the possibility to add custom attributes for the local provider"){.closed}
:   \[RFE\] Add the possibility to add custom attributes for the local
    provider

[\#2308](/sssd/ticket/2308 "document that simple access provider supports group nesting"){.closed}
:   document that simple access provider supports group nesting

</div>

<div>

[\#1359](/sssd/ticket/1359 "clang reports possible alignment issues"){.closed}
:   clang reports possible alignment issues

[\#2056](/sssd/ticket/2056 "Add a sysdb utility call sysdb_attrs_add_lower_case_string"){.closed}
:   Add a sysdb utility call sysdb\_attrs\_add\_lower\_case\_string

[\#2149](/sssd/ticket/2149 "Add a contrib script to prepare two SRPMs for covscan-diff"){.closed}
:   Add a contrib script to prepare two SRPMs for covscan-diff

[\#2184](/sssd/ticket/2184 "LDAP searches are not able to reuse one LDAP attribute for multiple sysdb ..."){.closed}
:   LDAP searches are not able to reuse one LDAP attribute for multiple
    sysdb attributes

[\#2185](/sssd/ticket/2185 "cleanup redundant #define statements"){.closed}
:   cleanup redundant \#define statements

[\#2194](/sssd/ticket/2194 "Use version script file for libraries from sssd"){.closed}
:   Use version script file for libraries from sssd

[\#2209](/sssd/ticket/2209 "Rename label in users_get_send/groups_get_send"){.closed}
:   Rename label in users\_get\_send/groups\_get\_send

[\#2341](/sssd/ticket/2341 "sssd-ldap handles redundant group members incorrectly"){.closed}
:   sssd-ldap handles redundant group members incorrectly

[\#2347](/sssd/ticket/2347 "sbus_codegen_tests leaves processes running"){.closed}
:   sbus\_codegen\_tests leaves processes running

[\#2348](/sssd/ticket/2348 "debugging on the foregound does not work"){.closed}
:   debugging on the foregound does not work

[\#2352](/sssd/ticket/2352 "The es and fr translations on Transifex are malformed"){.closed}
:   The es and fr translations on Transifex are malformed

[\#2356](/sssd/ticket/2356 "Use python2 in shebang for python scripts"){.closed}
:   Use python2 in shebang for python scripts

[\#2658](/sssd/ticket/2658 "memory leak in sysdb_search_custom"){.closed}
:   memory leak in sysdb\_search\_custom

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Alexander Bokovoy (3):

-   FAST: when parsing krb5\_child response, make sure to not miss OTP
    message if it was last one
-   ipa subdomains provider: make sure search by SID works for homedir
-   well known sids: Windows Server 2012 new asserted identity SIDs

Alexey Shabalin (1):

-   Use KRB5\_CFLAGS where appropriate

Aron Parsons (1):

-   do not use default\_domain\_suffix with autofs

Benjamin Franzke (4):

-   Add CIFS idmap plugin
-   dlopen-tests: Check the result of asprintf
-   BUILD: Use OPENLDAP\_CFLAGS instead of LDAP\_CFLAGS
-   BUILD: Link libsss\_krb5\_common.so to libkeyutils.so

Chris Leick (1):

-   German translation update

Cove Schneider (1):

-   Add ldap\_autofs\_map\_master\_name option

Jakub Hrozek (209):

-   Bump version to track 1.12 development
-   KRB5: Call umask before mkstemp in the krb5 child code
-   Add journald support
-   BE: Log domain name to journald if available
-   AD: async request to retrieve master domain info
-   LDAP: sdap\_id\_setup\_tasks accepts a custom enum request
-   AD: Download master domain info when enumerating
-   MAN: Fix provider man page subtitle
-   LDAP: Deprecate ldap\_{user,group}\_search\_filter
-   AD: Failure to get flat name is not fatal
-   Check return values of setenv and unsetenv
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
-   krb5: Fix unit tests
-   INI: Disable line-wrapping functionality
-   MAN: Fix refsect-id
-   KRB5: Return PAM\_ACCT\_EXPIRED when logging in as expired AD user
-   PROXY: Fix memory hierarchy when enumerating services
-   Include external headers with \#include &lt;foo.h&gt;
-   Remove unused constants
-   IPA: Do not enable IPA sites in server mode
-   Remove duplicate declaration
-   UTIL: Move sss\_parse\_name\_for\_domains declaration to util.h
-   Inherit ID limits of parent domains if set
-   SYSDB: Add sysdb\_delete\_by\_sid
-   LDAP: Delete entry by SID if not found
-   LDAP: Amend sdap\_access\_check to allow any connection
-   LDAP: Parse FQDN into name/domain for subdomain users
-   AD: Add a new option ad\_access\_filter
-   AD: Use the ad\_access\_filter if it's set
-   AD: Search GC by default during access control, fall back to LDAP
-   AD: Add extended access filter
-   TEST: Test getgrnam with emphasis on members
-   NSS: Print FQDN for groups with mixed domain membership
-   KRB5: Handle ERR\_CHPASS\_FAILED
-   NSS: Fix service enumeration
-   NSS: Use new safealign macros in NSS responder
-   MAN: Document that krb5 directories can only be created as private
-   LDAP: Check all search bases during nested group processing
-   NSS: Fix parenthesis
-   AD: Fix ad\_access\_filter parsing with empty filter
-   UTIL: Free log message when using journald
-   Initialize sid\_str to NULL to avoid freeing random data
-   Remove unused variable
-   PAC: Free config attribute when it's processed
-   Merge ipa\_selinux\_common.c and ipa\_selinux.c
-   SYSDB: Drop the sysdb\_ctx parameter from the autofs API
-   SYSDB: Drop the sysdb\_ctx parameter from SELinux functions
-   SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_idmap module
-   SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_sudo.c module
-   LDAP: Initialize user count for AD matching rule
-   LDAP: Split out a request to search for a user w/o saving
-   LDAP: Search for original DN during auth if it's missing
-   AD: Fix a typo in the man page
-   KRB5: Go offline in case of clock skew
-   MAN: Add a link explaining different LDAP scopes
-   MAN: Remove unused experimental file
-   NSS: Compare bool with false, not 0
-   Fix a trivial typo
-   LDAP: Fix a debug message
-   SUBDOMAINS: Reuse cached results if DP is offline
-   AD: Don't mark domain as enumerated twice
-   AD: Refresh subdomain data structures on startup
-   IPA: Refresh subdomain data structures on startup
-   IPA: Call ipa\_ad\_subdom\_refresh when server mode is initialized
-   AD: Add a utility function to create list of connections
-   AD: Add a new option to turn off GC lookups
-   AD: Enable fallback to LDAP of trusted domain
-   LDAP: Fix typo and use the right attribute map
-   LDAP: Add a new error code for malformed access control filter
-   tests: Remove tests that check creating public directories
-   UTIL: Inherit parent domain's default\_shell
-   NSS: Use plain user name when expanding homedir
-   AD: Don't fail the request if ad\_account\_can\_shortcut fails
-   MAN: Fix a typo
-   LDAP: Fix error check
-   LDAP: Don't abort request if no id mapping domain matches
-   AD: Store info on whether a subdomain is set to enumerate
-   LDAP: Pass a private context to enumeration ptask instead of
    hardcoded connection
-   LDAP: Add enum request with custom connection
-   AD: Enumerate users from GC, other entities from LDAP
-   LDAP: Don't clobber original\_member during enumeration
-   DB: Add sss\_ldb\_el\_to\_string\_list
-   AD: Establish cross-domain memberships after enumeration finishes
-   MAN: clarify which shell option takes precedence
-   NSS: Fix DEBUG formatting of cmdctx-&gt;id
-   SSS\_CACHE: Reset the initgroups attribute when resetting users
-   LDAP: Detect the presence of POSIX attributes
-   AD: Only download domains that are set to enumerate
-   AD: Remove dead code
-   LDAP: Handle errors from sdap\_id\_op properly in enum code
-   IPA: Default to krb5\_use\_fast=try
-   MAN: Clarify the new krb5\_use\_fast IPA default
-   DEBUG: Fix build without journald
-   NSS: Continue if there is no port
-   IPA: Don't call tevent\_req\_post outside \_send
-   IPA: Don't fail if apply\_subdomain\_homedir returns ENOENT
-   Fix DEBUG message formatting
-   OPTS: Allow using defaults for blobs
-   DP: Provide separate dp\_copy\_defaults function
-   MAN: Clarify the ldap\_access\_filter option further
-   MAN: Clarify that changing ID mapping options might require purging
    the cache
-   IPA: Do not save intermediate data to sysdb
-   AD: Only connect to GC for subdomain users
-   MAN: Clarify the GC support a bit
-   IPA: Use the correct domain when processing SELinux rules
-   IPA: Write SELinux usernames in the right case
-   KRB5: Do not attempt to get a TGT after a password change using OTP
-   AD: connect to forest root when downloading the list of subdomains
-   IPA: Fix SELinux mapping order memory hierarchy
-   IFP: Fix a typo in the Makefile
-   IFP: Re-add the
    [InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
    .wiki} server
-   IFP: Connect to the system bus
-   tests: Don't set the check fork mode explicitly
-   SBUS: Generate introspection from the interface meta structure
-   ConfigAPI: Add two missing AD options
-   Add a unit test for sss\_parse\_name\_for\_domains
-   Minor fixes for sss\_parse\_name\_for\_domains
-   SBUS: Create an sbus\_method\_meta instance for Introspection
-   RESPONDER: Fix a wrong DEBUG message
-   DP: Remove unused 'force' parameter from the subdomain handler
-   TESTS: Create a default sss\_names\_ctx in create\_dom\_test\_ctx
-   TESTS: Split a separate common\_mock\_resp\_dp module
-   RESPONDERS: Add a new request sss\_parse\_inp\_send
-   KRB5: Print a verbose error message on failure reading the keytab
-   LDAP: Fix off-by-one bug in sdap\_copy\_opts
-   LDAP: Make it possible to extend an attribute map
-   IFP: Close memstream handle in introspect destructor
-   LDAP: Check the LDAP handle before using it
-   SBUS: several trivial style fixes
-   SBUS: Fix error handling condition
-   SBUS: Add a convenience function sbus\_error\_new
-   SBUS: Split out dbus\_conn\_send
-   SBUS: Add SBUS\_CONN\_TYPE\_SYSBUS
-   SBUS: Add an async request to retrieve the caller ID
-   SBUS: Refactor sbus\_message\_handler to retrieve caller ID
-   IFP: Add utility functions
-   IFP: use a list of allowed\_uids for authentication
-   IFP: Initialize negative cache timeout
-   IFP: Add
    [GetUserAttrs?](https://docs.pagure.org/sssd-test2/GetUserAttrs.html){.missing
    .wiki} call
-   AD: Do not remove non-root domains when looking up root domain
-   IFP: Per-attribute ACL for users
-   SBUS: Allow registering paths with fallback
-   SYSDB: return SYSDB\_NAME from sysdb\_initgroups
-   IFP: Add a
    [GetGroupsList?](https://docs.pagure.org/sssd-test2/GetGroupsList.html){.missing
    .wiki} method
-   AD: Initialize user\_map\_cnt in server mode
-   IFP: Add utility functions to escape and unescape object paths
-   IFP: Add a unit test for ifp\_reply\_objpath
-   SBUS: Utility function sbus\_request\_return\_as\_variant
-   IFP: Allow Set, Get and
    [GetAll?](https://docs.pagure.org/sssd-test2/GetAll.html){.missing
    .wiki} from DBus.Properties
-   SBUS: Implement org.freedesktop.DBus.Properties.Get for primitive
    types
-   SBUS: Return / if an object path getter returns NULL
-   SBUS: Add several error constant definitions
-   SBUS: Add org.freedesktop.DBus.Properties.Get to Introspection
-   IFP: Support multiple interfaces on sysbus
-   SBUS: Add utility function sbus\_add\_variant\_to\_dict
-   SBUS: Consolidate VTABLE\_FUNC definitions in sssd\_dbus\_meta.h
-   SBUS: Implement
    org.freedesktop.DBus.Properties.[GetAll?](https://docs.pagure.org/sssd-test2/GetAll.html){.missing
    .wiki} for primitive types
-   SBUS: Add
    org.freedesktop.DBus.Properties.[GetAll?](https://docs.pagure.org/sssd-test2/GetAll.html){.missing
    .wiki} to Introspection
-   TESTS: check allocation result
-   TESTS: check dbus mock result
-   IFP: Add
    [ListDomains?](https://docs.pagure.org/sssd-test2/ListDomains.html){.missing
    .wiki} and
    [FindDomainByName?](https://docs.pagure.org/sssd-test2/FindDomainByName.html){.missing
    .wiki}
-   tests: Add test for confdb\_list\_all\_domain\_names
-   tests: Add test for get\_known\_services
-   BUILD: Disable dbus tests when running distcheck
-   MAN: Add sssd-ifp to the list of translatable manual pages
-   Updating the translations for the 1.12 beta1 release
-   Updating the version to 1.12beta2
-   TOOLS: Allow adding and modifying custom attributes with
    sss\_usermod
-   TESTS: fgetc returns int, not char
-   MAN: Fix a typo in the ldap\_id\_mapping page
-   LDAP: Fix DEBUG message
-   Updating the translations for the 1.12beta2 release
-   Updating the version for the 1.12.0 stabilization
-   LDAP: Fix retrieving a group with no members
-   TESTS: Add confdb domain base DN to sss\_test\_ctx
-   TESTS: Use the right confdb path
-   TESTS: Fix group search base
-   TESTS: Do not require replies from mocked sdap\_get\_generic\_recv
    to be talloc contexts
-   TESTS: Change how mock\_sysdb\_user() is implemented
-   TESTS: Add more tests for nested groups processing
-   TESTS: Do not rely on order of hash items
-   PROVIDERS: Add ldap\_common.h to opts.h of each provider
-   TESTS: Add a unit test for the sdap.c module
-   LDAP: Try all attributes when saving an entry
-   SDAP: Fix DEBUG message priorities in sdap\_parse\_entry
-   LDAP: Remove unused output parameter \_dn from sdap\_parse\_entry
-   SDAP: Remove unused function sdap\_get\_msg\_dn
-   SDAP: Free bervals on failure in sdap\_parse\_entry
-   BUILD: dbusintrospectdir is not used anymore
-   IFP: Fix DEBUG messages
-   IFP: Return a specific value on failure connecting to the system bus
-   IFP: Provide a SBUS method to reconnect to sysbus
-   MONITOR: Signal
    [InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
    .wiki} to reconnect on SIGUSR2
-   TOOLS: New helper tool sss\_signal
-   BUILD: Add the DBus service activation
-   SSSD: Send debug to stderr when running on foreground
-   TOOLS: Always debug to stderr
-   Updating translations for the 1.12.0 release
-   Updating the version for the 1.12.0 release

Jan Cholasta (1):

-   SSH: Allow newline at the end of public key values in LDAP

Jan Engelhardt (1):

-   build: fix ordering of linker flags

Lukas Slebodnik (167):

-   Add missing new line in DEBUG message
-   LDAP: Use primary cn to search netgroup
-   RESPONDER: Use right function prototype
-   Revert "mmap\_cache: Skip records which doesn't have same hash"
-   mmap\_cache: Use two chains for hash collision.
-   Include right header file
-   Include header file in implementation module.
-   krb5: fix warning may be used uninitialized
-   LDAP: Set default value for dyndns update to false
-   krb5: Remove warning dereference of a null pointer
-   krb5: Use right function to free data.
-   IPA: Remove unused memory context.
-   AD: Prefer GC port from SRV record
-   AD: fall back to LDAP if GC is not available.
-   tests: Use right format string for type size\_t
-   Makefile: Add missing libraries
-   Makefile: Remove unused variable TEST\_MOCK\_OBJ
-   LDAP: Return correct error code
-   NSS: Set packet length for initgroups
-   BUILD: Explicitly link libsss\_ad.so with sasl libs
-   BUILD: Change error message if missing cifsimap.h
-   LDAP: Prevent from using uninitialized sdap\_options
-   monitor: return right error code
-   SYSDB: Skip malformed netgroup attribute.
-   TESTS: Link libsss\_test\_common with tevent
-   TESTS: Remove test dir after successful tests
-   Remove unused parameter from sss\_selinux\_extract\_user
-   Remove unused parameter from get\_user\_dn
-   Remove unused parameter from sdap\_save\_user
-   Remove unused parameter from sdap\_get\_members\_with\_primary\_gid
-   Remove unused parameter from sdap\_store\_group\_with\_gid
-   Remove unused parameter from sdap\_add\_group\_member\_2307
-   Remove unused parameter from sdap\_process\_missing\_member\_2307
-   Remove unused parameter from sdap\_save\_netgroup
-   Remove unused parameter from krb5\_auth\_cache\_creds
-   Remove unused parameter from krb5\_auth\_store\_creds
-   Remove unused parameter from mod\_groups\_member
-   Remove unused parameter from usermod
-   Remove unused parameter from groupmod
-   Remove unused parameter from useradd
-   Remove unused parameter from groupadd
-   Remove unused parameter from invalidate\_entry
-   Remove unused parameter from search\_autofsmaps
-   Remove unused parameter from seed\_domain\_user\_info
-   Remove unused parameter from sudosrv\_get\_sudorules\_query\_cache
-   Remove unused parameter from delete\_user
-   Remove unused parameter from save\_user
-   Remove unused parameter from save\_netgroup
-   Remove unused memory context in proxy
-   Remove unused parameter from ipa\_save\_netgroup
-   Remove unused parameter from group\_show\_mpg
-   Remove unused parameter from group\_show\_trim\_memberof
-   AUTOMAKE: Don't build libsss\_test\_common every time
-   SYSDB: Sanitize filter before sysdb\_search\_groups
-   SYSDB: Sanitize filter before removing ghost attrs
-   NSS: Fix memory leak in sss\_setnetgrent
-   AUTOTOOLS: krb5 1.12 is also supported krb5 libs
-   TESTS: Fix build with older version of check framework
-   AD: Return right error code from netlogon\_get\_flat\_name
-   LDAP: Don't fail if subdomain cannot be found by sid
-   LDAP: update id mapping detection for ldap provider
-   sdap\_idamp: Fall back to another method if sid is wrong
-   TESTS: Fix authtok test for zero length string.
-   CLIENT: Remove unused macros
-   LDAP: store group if subdomain cannot be found by sid
-   LDAP: require attribute groupType for AD groups
-   AD: Remove unused memory contexts
-   memberof: Removed unused parameter from mbof\_fill\_vals\_array.
-   Makefile: Remove unused libraries
-   DOC: Fix names of arguments in doxygen comments
-   test\_dyndns: Test right variable after allocation.
-   IPA: explicitly link libsss\_ipa with selinux library
-   Translation: Move german translation to right directory
-   SPEC: Fix packaging rpms on OSes without systemd
-   DEBUG: Fix crash after fallback from journal log
-   Fix warning unused variable ap\_fallback
-   LDAP: Setup periodic task only once.
-   UTIL: Sanitize whitespaces.
-   KRB5: Fix condition for empty string
-   NSS: Fix warning access array with index then check
-   TEST: Fix warning invalid printf argument type
-   Remove unused structures.
-   TEST: Use unique directory for negcache test
-   PAM: Test return value of strdup
-   Makefile: Add missing library to the dp\_opt\_tests
-   AD: Continue if sssd failes to check extra members
-   TEST: Remove unused argument sysdb\_path
-   TEST: Use right domain name in negcache test
-   TEST: Do not clean up if test fail.
-   hbac-test: Use defined macros instead of strings
-   TESTS: Remove unused macros
-   KRB: Prevent dereference of a null pointer
-   UTIL: Hide implementation details about unicode libraries.
-   Use pattern \#elif defined(identifier)
-   BUILD: Enable additional compiler warnings
-   SYSV: Do not call functions success and fail itself
-   IPA: Use function sysdb\_attrs\_get\_el in safe way
-   AUTOFS: terminate array after the last entry
-   Makefile: Use alternative method to replace \*bindir
-   krb5\_child: Remove unused krb5\_context from set\_changepw\_options
-   Remove unused argument from resolv\_gethostbyname\_dns\_parse
-   Fix warning zero-length gnu\_printf format string
-   krb5\_child: Fix use after free in debug message
-   AUTOMAKE: Do not include generated files into tarball
-   BUILD: Link libsss\_ldap\_common.so to libsss\_idmap.so
-   BUILD: Move file find\_uid.c into libsss\_util.so
-   BUILD: Move file sss\_krb5.c into libsss\_krb5\_common.so
-   BUILD: Move duplicated files from providers to
    libsss\_ldap\_common.so
-   TEST: Add untested libraries into dlopen test
-   TEST: Some macros aren't defined in older version of check.
-   CRYPTO: Fix access to uninitialized data
-   SPEC: Remove duplicate sssd\_ifp.
-   TEST: Link ipa\_ldap\_opt test with openldap libs
-   UTIL: Use constant instead of value for stdin.
-   MONITOR: Fix start up with empty standard input
-   SPEC: Add libsss\_ad\_common.so to the package sssd-ad
-   TEST: Refactor test\_io
-   BUILD: Make samba4 libraries optional
-   SBUS: Fix warning declaration shadows a global declaration
-   PAM: Fix problem with missing declaration.
-   PAM: macro PAM\_DATA\_REPLACE isn't available in openpam.
-   CRYPTO: Use unprefixed version of function stpncpy
-   CONFIGURE: Remove duplicate detection of pam
-   Remove unused parameter from ifp\_user\_get\_attr\_handle\_reply
-   Remove unused parameter from ifp\_user\_get\_groups\_reply
-   resolv: Do not try to free addrinfo in case of error
-   AUTOCONF: Move detection of samba libraries to one file
-   SBUS: Define DBUS\_ERROR\_INIT for old version of dbus
-   SBUS: Include config.h for enabling function in stdio.h
-   UTIL: Fix order of header files.
-   LDAP: Don't use macro \_XOPEN\_SOURCE for extra features
-   UTIL: Include netinet/in.h for ip adress macros
-   TEST: Test empty results from functions sysdb\_search\_\*
-   sss\_autofs: Check return value of autofs make request
-   sss\_autofs: Do not try to free empty autofs context
-   Don't use macro \_XOPEN\_SOURCE for function strptime
-   TEST: Add libsss\_simpleifp.so to dlopen test
-   man: Substitute entity values for entity references
-   MAKE: Link libsss\_ldap.so with ldap libraries
-   UTIL: Add function sss\_parse\_name\_const
-   NSS: Refactor expand\_homedir\_template
-   NSS: Add option to expand homedir template format
-   TEST: Add test for expand homedir
-   PAM: Include header file security/pam\_appl.h
-   MAKE: Remove PAM libraries from libsss\_simple
-   CONFIGURE: Enhance detection of pam
-   PAM: Fix compilation of pam\_test\_client with openpam
-   PAM: Use fallback version of some pam macros
-   PAM: Define compatible macros for some functions.
-   PAM: add ignore\_authinfo\_unavail option
-   SDAP: Use portable constant as level in setsockopt
-   Unify usage of function gethostname
-   MAN: Add reference to manual page sssd-sudo
-   Use python2 in shebang for python scripts.
-   CONFIGURE: Prefer python2
-   SYSDB: Remove useless NULL test.
-   SYSDB: Modify declaration of sysdb\_search\_entry
-   TESTS: Fix format string in check macros
-   BUILD: ad\_gpo\_tests should be built only with samba
-   SPEC: Add gpo\_child to package sssd-ad
-   UTIL: Fix access out of bound in parse\_args
-   BUILD: Add version symbol files for public libraries.
-   sdap-tests: Fix off by one.
-   BUILD: Link sdap-tests with openldap libraries
-   PAM: Test right variable after calling sss\_atomic\_read\_s
-   CONTRIB: make\_srpm.sh can prepare SRPM with patches
-   CONTRIB: Fix creation of tar.gz with old version of git

Markos Chandras (2):

-   sysv/gentoo: Use xdm if possible
-   sysv/gentoo: Send debug output to a file instead of stderr

Michal Zidek (31):

-   Rename \_SSS\_MC\_SPECIAL
-   man sssd: Add note about SSS\_NSS\_USE\_MEMCACHE
-   nss: Wrong debug message.
-   util: Add functions to check if IP addresses is special
-   dyndns: Use check\_ipvX\_addr functions
-   sdap\_async\_sudo\_hostinfo.c: Use check\_ipvX\_addr
-   tests: Silence alignment warning in tests.
-   responder: Access packet header using SAFEALIGN macros.
-   confdb: Make offline timeout configurable
-   SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_search module
-   SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_services module
-   SYSDB: Drop the sysdb\_ctx parameter from the sysdb\_ssh module
-   SYSDB: Drop the sysdb\_ctx parameter - module sysdb\_ops (part 1)
-   SYSDB: Drop the sysdb\_ctx parameter - module sysdb\_ops (part 2)
-   SYSDB: Drop redundant sysdb\_ctx parameter from sysdb.c
-   sss\_client: Use SAFEALIGN\_SETMEM\_&lt;type&gt; macros where
    appropriate.
-   krb5: Alignment warning reported by clang
-   monitor: Stop using unnecessary helper pointer.
-   Missing parameter name in declaration.
-   Fix parameter name.
-   sss\_client: Use SAFEALIGN\_COPY\_&lt;type&gt; macros where
    appropriate.
-   responder: Use SAFEALIGN macro when checking pam data validity.
-   Properly align buffer when storing pointers.
-   responder: Use SAFEALIGN macros where appropriate.
-   Possible null dereference in SELinux code
-   Remove dead code from ipa\_get\_selinux\_recv
-   mmap: Get errno when unlink fails
-   ipa\_selinux: Put SELinux map order related variables into structure
-   Add type parameter to DISCARD\_ALIGN macro
-   Suppress safealign warnings with DISCARD\_ALIGN.
-   Use DISCARD\_ALIGN in VTABLE\_FUNC macro

Nathaniel
[McCallum?](https://docs.pagure.org/sssd-test2/McCallum.html){.missing
.wiki} (1):

-   Fix krb5 changepw when FAST-only preauth methods are used (like OTP)

Nikolai Kondrashov (23):

-   dyndns: Update PTR records separately
-   Add cscope inverted index files to .gitignore
-   Update debug levels in sss\_semanage\_error\_callback
-   Move DEBUG macro body to debug\_fn
-   Remove extra flushing from debug message output
-   Cleanup debug\_fn
-   Make DEBUG macro definition variadic
-   Make DEBUG macro invocations variadic
-   Fixup DEBUG macro invocations update
-   Update DEBUG\* invocations to use new levels
-   Update debug level in sysdb\_check\_upgrade\_02
-   Remove DEBUG macro support for old debug levels
-   Use HW instead of processor name as build arch
-   Use functions, not aliases in bashrc\_sssd
-   Handle unbound variables in bashrc\_sssd
-   Clarify CFLAGS handling in bashrc\_sssd
-   Remove --with-distro-version
-   build: Don't assume systemd implies journald
-   build: List test extensions
-   build: Switch to AM\_DISTCHECK\_CONFIGURE\_FLAGS
-   build: Switch back to DISTCHECK\_CONFIGURE\_FLAGS
-   build: Augment systemdconfdir at configure stage
-   build: Allow augmenting TESTS\_ENVIRONMENT

Ondrej Kos (2):

-   MAN: Remove IPA specific LDAP settings
-   IPA: Deprecate ipa\_hbac\_support\_srchost option

Pallavi Jha (5):

-   added null checks to authtok module
-   permament is corrected to permanent
-   cmocka unit test for authtok module added
-   Unit-test-for-negcache-module-added
-   cmocka-unit-test-for-functions-getpwuid\*-added

Pavel Březina (94):

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
-   sudo: allow specifying only one time restriction
-   sudo: improve time restrictions debug messages
-   nss: wait for initial subdomains request to finish
-   subdomains: first destroy ptask then remove sdom
-   dp: make subdomains refresh interval configurable
-   dp: store list of ongoing requests
-   utils: add ERR\_DOMAIN\_NOT\_FOUND error code
-   dp: set request domain
-   dp: add function to terminate request of specific domain
-   dp: free sdap domain if subdomain is removed
-   be\_ptask: add be\_ptask\_create\_sync()
-   dp: convert cleanup task to be\_ptask
-   ipa: destroy cleanup task when subdomain is removed
-   ad: destroy ptasks when subdomain is removed
-   sdap\_save\_user: try to determine domain by SID
-   sdap\_save\_group: try to determine domain by SID
-   free sid obtained from sss\_idmap\_unix\_to\_sid()
-   ad: shortcut if possible during get object by ID or SID
-   sdap: store base dn in sdap\_domain
-   sdap: add sdap\_domain\_get\_by\_dn()
-   ghosts: pick correct domain for every member
-   sdap\_fill\_memberships: pick correct domain for every member
-   nested groups: pick correct domain for cache lookups
-   idmap: add API to free allocated SIDs
-   free idmapped SIDs correctly
-   free idmapped dom SIDs correctly
-   free idmapped smb SIDs correctly
-   free idmapped binary SIDs correctly
-   pac: fix double free
-   pac: fix potential memory leaks
-   failover: check dns\_domain if primary servers lookup failed
-   ad: refactor tokengroups initgroups
-   ad: use tokengroups even when id mapping is disabled
-   Bump sss\_idmap version to 3:0:3
-   sudo: memset tm when converting time attributes
-   resolv\_gethostbyname\_dns\_parse(): remove tmp\_ctx
-   IPA: default krb5\_fast\_principal to host/\$client@\$realm
-   sdap: move non async functions from sdap\_async.c to sdap\_utils.c
-   sdap: move non async functions from sdap\_async\_connection.c to
    sdap\_utils.c
-   sdap: move sdap\_get\_id\_specific\_filter() to sdap\_utils.c
-   ldap: move options related content from ldap\_common.c to
    ldap\_options.c
-   ldap: move domain related content from ldap\_common.c to
    sdap\_domain.c
-   make make\_realm\_upper\_case() static
-   tests: add confdb\_path to sss\_test\_ctx
-   tests: mock SDAP
-   tests: mock sysdb users and groups
-   tests: prepare makefile for provider related unit tests
-   tests: new macro sss\_will\_return\_always
-   tests: nested groups unit test
-   tests: don't print debug message when test dir does not exist
-   ad\_account\_can\_shortcut(): return bool instead of errno
-   IFP: do not create client socket
-   sbus\_tests: fix missing invoker in initializer
-   sbus request: fix error initialization
-   SBUS: remove unused variables
-   sss\_config: the code
-   sss\_config: build
-   sss\_config: unit tests
-   sss\_config: build only when IFP is allowed
-   IFP: Add a utility function to reply with an object path
-   SBUS: Utility function sbus\_request\_return\_array\_as\_variant
-   SBUS: Return empty string if a string getter returns NULL
-   SBUS: Add utility function sbus\_add\_array\_as\_variant\_to\_dict
-   IFP: Implement domain getters
-   confdb: add confdb\_list\_all\_domain\_names()
-   utils: add get\_known\_services()
-   IFP: Implement SSSD components
-   sss\_sifp: introduce API
-   sss\_sifp: implement API
-   sss\_sifp: build
-   sss\_sifp: unit tests
-   sss\_sifp: add support for string dictionary
-   sss\_sifp: add shortcuts for common use cases
-   man: clarify refresh\_expired\_interval
-   sbus\_codegen\_tests: free memory context
-   nested groups: do not fail if we get one entry twice
-   sbus\_request: fix potential NULL dereference
-   sss\_sifp: pkg-config requires is a comma separated list
-   sss\_sifp: add prefix and exec\_prefix to pkg-config
-   IFP: touch config when changing debug level temporarily

Pavel Reichl (64):

-   Include ext headers with \#include &lt;foo.h&gt; - cont
-   monitor: Specific error message for missing sssd.conf
-   SSSD: Improved domain detection
-   SSSD: Unit test - sss\_ldap\_dn\_in\_search\_bases
-   monitor: use-after-free bugfix
-   monitor: monitor\_kill\_service - refactor
-   monitor: memory-leak bug
-   monitor: syslog when process killed by monitor
-   SYSDB: typos & debug macro constants
-   SYSDB: missing conversion of LDB error to errno
-   SYSDB: simplification of condition in if statement
-   responder: Set forest attribute in AD domains
-   simple access: match objects using flat name
-   simple access: refresh master domain info
-   NSS: add support for subdomain\_homedir
-   krb5: hint to increase krb5\_auth\_timeout
-   utils: handling NULL params in sss\_parse\_name
-   Revert "NSS: add support for subdomain\_homedir"
-   AD: support for subdomain\_homedir
-   MAN: update of subdomain\_homedir usage
-   CONFDB: fail if there are domains with same name
-   MONITOR: Incorrect permissions on sssd.conf
-   MAN: new general options section
-   MAN: Option name typo in sssd-krb5
-   refactor calls of sss\_parse\_name
-   KRB5: log message - wrong permissions on ccache dir
-   MAN: minimal value expected for ldap\_idmap\_range\_size
-   PAC: fix clang warning
-   failover: Shorter retry time for failed SRV
-   SDAP: augmented logging for group saving
-   KRB: do not check ccache directory for GID
-   KRB5: Go offline in case of generic error
-   Monitor: fix message wrong perm. mode on config file
-   util: Fix 'wrong mode' debug message
-   AD Provider: bug-fix uninitialized variable
-   AD Provider: bugfix use-after-free
-   TEST: Remove unused variable
-   TEST: fix warning in sbus\_codegen\_tests
-   TEST: unused variable
-   TEST: simple\_access & sysdb tests - cleanup
-   LDAP: fix - find primary group by gid
-   MAN: Detailed ldap\_group\_nesting\_level option
-   SDAP: Make nesting\_level = 0 to ignore nested groups
-   SDAP: Add option to disable use of Token-Groups
-   MAN: hint nested groups by simple access provider
-   IPA: Rename label in users\_get\_send/groups\_get\_send
-   SYSDB: utility call sysdb\_attrs\_add\_lower\_case\_string
-   TESTS: sss\_ssh - textual public key format
-   AD: cleanup redundant \#define statements
-   NSS: sysdb\_getnetgr check return value first
-   NSS: sysdb\_getnetgr refactor
-   NSS: fix memory leak in sysdb\_getnetgr
-   NSS: minor code style improvements
-   TESTS: sysdb\_search\_return\_ENOENT - check mem leaks
-   SYSDB: sysdb\_search\_entry fix memory leak
-   SYSDB: sysdb\_search\_custom fix memory leak
-   SYSDB: sss\_ldb\_search - wrapper around ldb\_search
-   TESTS: add tests for sss\_ldb\_search
-   SYSDB: sysdb\_getnetgr returns ENOENT
-   TESTS: sysdb\_getnetgr - return ENOENT
-   NSS: lookup\_netgr\_step don't access result on ENOENT
-   sudo: return after tevent\_req\_error
-   SDAP: return after tevent\_req\_error
-   LDAP: group\_split\_members returns incorrectly ENOMEM

Pete Fritchman (1):

-   PAM: add ignore\_unknown\_user option

Simo Sorce (9):

-   util: Use systemd-login to check user sessions
-   krb5: Be more lenient on failures for old ccache
-   util: Allways fall back to old find\_uid method
-   krb5: Remove ability to create public directories
-   Signals: Remove unused functions
-   Signals: Remove empty sig\_hup
-   Signals: Refactor termination of processes
-   util: Change file check fns to use a mode mask
-   confdb: Change file checks for config file

Stef Walter (19):

-   Update .gitignore for 'make check' built files
-   util: Fix const cast failures when building with -Werror
-   util: A safe printf for user provided format strings
-   NSS: Don't use printf(3) on user provided strings.
-   sbus: Add meta data structures and code generator
-   sbus: Add sbus\_vtable and update codegen to support it
-   nss: Stop using one DBus interface with totally different methods
-   sbus: Rework sbus to use interface metadata and vtables
-   sbus: Generate constants from interface definitions
-   sbus: Use constants to make dbus calls
-   providers: Fix types passed to dbus varargs functions
-   sbus: Add struct sbus\_request to represent a DBus invocation
-   sbus: Refactor how we export DBus interfaces
-   sbus: Make sbus\_new\_server() work for non-priveleged processes
-   sbus\_tests: Add some testing of dispatch and handler code
-   sbus: Add the sbus\_request\_parse\_or\_finish() method
-   sbus: Add type-safe DBus method handlers and finish functions
-   sbus\_codegen\_tests: Add test case type-safe handler args
-   SBUS: Start implementing property access

Stephen Gallagher (9):

-   SYSDB: Fix incorrect DEBUG message
-   MAN: Clarify debug level documentation
-   MAN: Reflow debug\_levels.xml
-   BUILD: Update bashrc macros
-   DEBUG: Allow debug\_fn to process [FILE]{.underline} and
    [LINE]{.underline}
-   DEBUG: Enable sending structured debug logs to journald
-   BUILD: Build with journald support by default on Fedora
-   BUILD: Simplify enabling journald on installed systems
-   AD Provider: Fix crash looking up forest on Samba 4

Sumit Bose (68):

-   Do not set HAVE\_SYSTEMD\_LOGIN if libsystemd-login is not available
-   sdap\_domain\_add: remove too strict consistency check
-   krb5: save canonical upn to sysdb
-   krb5: do not expand enterprise principals is offline
-   IPA: store forest name for forest member domains
-   ipa\_server\_mode: write capaths to krb5 include file
-   Do not return DP\_ERR\_FATAL in case of success
-   AD: properly intitialize GC from ad\_server option
-   LDAP: handle SID requests if noexist\_delete is set
-   Spec file changes for cifs-utils plugin
-   IPA server mode: properly initialize ext\_groups
-   idmap: add internal function to free a domain struct
-   idmap: fix a memory leak if a collision is detected
-   idmap: allow ranges with external mapping to overlap
-   sdap\_idmap: add sdap\_idmap\_get\_configured\_external\_range()
-   sdap\_idmap: properly handle ranges for external mappings
-   Add unconditional online callbacks
-   IPA: add callback to reset subdomain timeouts
-   sdap\_get\_generic\_ext\_send: check if we a re still connected
-   find\_subdomain\_by\_sid: skip domains with missing domain\_id
-   idmap: add sss\_idmap\_domain\_by\_name\_has\_algorithmic\_mapping()
-   sdap\_idmap\_domain\_has\_algorithmic\_mapping: add domain name
    argument
-   IPA: add trusted domains with missing idrange
-   ad\_subdom\_store: check ID mapping of the domain not of the parent
-   be\_spy\_create: free be\_req and not the long living data
-   Enhance/add unit tests for find\_subdomain\_by\_sid/name
-   Replace prog\_DEPENDENCIES with EXTRA\_prog\_DEPENDENCIES
-   Add sss\_packet\_get\_status()
-   sss\_names\_init: allow empty domain name
-   nss: save global name configuration to the nss context
-   Add sss\_tc\_fqname2()
-   Add utility to handle Well-Known SIDs
-   nss-srv-tests: check packet status
-   nss: check for Well-Known SIDs in SID based requests
-   Update CIFS plugin for Well-Known SID support
-   rfc2307bis\_nested\_groups\_send: reuse search base
-   AD: use LDAP for group lookups
-   sss\_cache: initialize names member of sss\_domain\_info
-   sss\_cache: fix case-sensitivity issue
-   Add sysdb\_attrs\_add\_lc\_name\_alias
-   Use sysdb\_attrs\_add\_lc\_name\_alias to add case-insensitive alias
-   Use lower-case name for case-insensitive searches
-   Add new option ldap\_group\_type
-   Add sysdb\_attrs\_get\_int32\_t
-   AD: filter domain local groups for trusted/sub domains
-   AD: cross-domain membership fix
-   IPA: fix for recent AD group membership changes
-   AD SRV: use right domain name for CLDAP ping
-   IDMAP: add sss\_idmap\_check\_collision(\_ex)
-   IPA: refactor idmap code and add test
-   IPA: check ranges for collisions before saving them
-   libsss\_idmap: bump version-info
-   config API: add missing subdomain target to AD provider test
-   SUDO: AD provider
-   config API: read only specific files from schemaplugindir
-   config API: prepend source dir search path for tests
-   ipa-server-mode: use lower-case user name for home dir
-   IPA: Use GC for AD initgroup requests
-   IPA/KRB5: handle KRB5\_PROG\_ETYPE\_NOSUPP during IPA password
    migration
-   krb5\_child: remove unused option lifetime\_str from
    k5c\_setup\_fast()
-   krb5-child: extract lifetime settings into set\_lifetime\_options()
-   krb5\_client: rename krb5\_set\_canonicalize() to
    set\_canonicalize\_option()
-   krb5-child: add revert\_changepw\_options()
-   Make LDAP extra attributes available to IPA and AD
-   contrib: add
    [BuildRequires?](https://docs.pagure.org/sssd-test2/BuildRequires.html){.missing
    .wiki} libsmbclient-devel to spec file
-   Fix return value of attr\_name\_val\_split() and attr\_op()
-   sysdb: make canonicalUserPrincipalName case-insensitive
-   sysdb: add sysdb\_search\_user\_by\_upn() with tests

Yassir Elley (9):

-   ad\_access\_filter man page typo
-   Implemented LDAP component of GPO-based access control
-   AD-GPO: Remove dependency on libsamba-security
-   AD-GPO: add libsmbclient to makefiles
-   AD-GPO: Fix some failure modes in ad\_gpo.c
-   TEST: Add ad\_gpo unit tests
-   AD-GPO: Add gpo-smb implementation in gpo\_child process
-   Use ldap\_url\_parse to extract hostname from ldap uri
-   AD-GPO: Add support for gpo permissive mode

