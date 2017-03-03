<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Tickets Fixed](#TicketsFixed)
    3.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   Add native support for autofs to the IPA provider
-   Support for ID-mapping when connecting to Active Directory
-   Support for handling very large (&gt; 1500 users) groups in Active
    Directory
-   Support for sub-domains (will be used for dealing with trust
    relationships)
-   Add a new fast in-memory cache to speed up lookups of cached data on
    repeated requests

Tickets Fixed {#TicketsFixed}
-------------

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

Ariel Barria (1):

-   Bad check for id\_provider=local and access\_provider=permit

Jakub Hrozek (105):

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

Jan Cholasta (22):

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

Jan Engelhardt (1):

-   build: resolve link failure

Jan Zeleny (34):

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

Marco Pizzoli (1):

-   Two manual pages fixes

Pavel Březina (16):

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

Simo Sorce (11):

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

Stef Walter (6):

-   Fix erronous reference to the 'allow' access\_provider
-   execv, excvp and exec\_child never return EOK
-   If canon'ing principals, write ccache with updated default principal
-   Remove erroneous failure message in find\_principal\_in\_keytab
-   Limit krb5\_get\_init\_creds\_keytab() to etypes in keytab
-   Clearer documentation for use\_fully\_qualified\_names

Stephen Gallagher (96):

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

Sumit Bose (13):

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

Yuri Chornoivan (2):

-   fix typos in manual
-   Fix typo: retreiving-&gt;retrieving

