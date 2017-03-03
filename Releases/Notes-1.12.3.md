Highlights {#Highlights}
----------

-   This is mostly a bug fixing release with only minor enhancements
    visible to the end user
-   Contains many fixes and enhancements related to the ID views
    functionality of FreeIPA servers
    -   SSSD now allows the IPA client to move from one ID view to
        another after SSSD restart
    -   It is possible to apply ID views to IPA domains as well.
        Previous SSSD versions only allowed views to be applied to AD
        trusted domains
    -   Overriding SSH public keys is supported in this release
-   This release contains several fixes and enhancements related to
    users and groups from trusted AD domains
    -   When a trusted AD domain is disabled on the server side, access
        is denied for users logging in from these domains
    -   External group memberships (i.e. memberships in IPA groups) are
        now resolved correctly for trusted AD users
    -   The localauth plugin configuration is written into the pubconf
        directory which should be included from krb5.conf on IPA
        clients. As a result, the localauth plugin should be configured
        automatically on IPA clients.
-   Password change when One-Time-Passwords are used was fixed
-   The tokenGroups support was disabled by default in the LDAP
    provider. The tokenGroups support is still enabled by default in the
    AD provider
-   Simple access provider skips user or group names that can't be
    resolved if only allow rules are configured

Packaging Changes {#PackagingChanges}
-----------------

-   Support for running SSSD as a non-privileged user was added. SSSD's
    directories must be owned by this user, hence SSSD needs to be
    configured properly at build time, using the new configure option
    `--with-sssd-user`. Additionally, the non-privileged user must also
    be selected in sssd.conf using the `user` configuration option.

Documentation Changes {#DocumentationChanges}
---------------------

-   A new configuration option `krb5_confd_path` was added. This option
    specifies the directory where SSSD places Kerberos configuration
    snippets.
-   The default value of `ldap_user_uuid` was changed to be `objectSID`
    for the AD back end and unset for all other back ends.
-   The option `ldap_use_tokengroups` changed its default value to True
    for AD and IPA providers only.
-   The `allowed_shells` option newly accepts the wildcard (`*`) value,
    allowing any shell

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1195](/sssd/ticket/1195 "4 functions with reference leaks within sssd (src/python/pyhbac.c)"){.closed}
:   4 functions with reference leaks within sssd (src/python/pyhbac.c)

[\#1939](/sssd/ticket/1939 "Create unit test for be_ptask"){.closed}
:   Create unit test for be\_ptask

[\#2102](/sssd/ticket/2102 "disable midpoint refresh for netgroups if ptask refresh is enabled"){.closed}
:   disable midpoint refresh for netgroups if ptask refresh is enabled

[\#2219](/sssd/ticket/2219 "Shell fallback mechanism in SSSD"){.closed}
:   Shell fallback mechanism in SSSD

[\#2370](/sssd/ticket/2370 "sssd should run under unprivileged user"){.closed}
:   sssd should run under unprivileged user

[\#2372](/sssd/ticket/2372 "SELinux: Audit changes to the SELinux label files"){.closed}
:   SELinux: Audit changes to the SELinux label files

[\#2404](/sssd/ticket/2404 "Remove password from the PAM stack if OTP is used"){.closed}
:   Remove password from the PAM stack if OTP is used

[\#2430](/sssd/ticket/2430 "sssd segfaults repeatedly with error 4 in memberof.so"){.closed}
:   sssd segfaults repeatedly with error 4 in memberof.so

[\#2439](/sssd/ticket/2439 "Return a different errno from client when sssd is not running."){.closed}
:   Return a different errno from client when sssd is not running.

[\#2445](/sssd/ticket/2445 "Race condition while invalidating memory cache in client code"){.closed}
:   Race condition while invalidating memory cache in client code

[\#2451](/sssd/ticket/2451 "sssd-ldap man page changes, add 'access_provider = ldap' as a requirement ..."){.closed}
:   sssd-ldap man page changes, add 'access\_provider = ldap' as a
    requirement 'ldap\_access\_order = for lockout'

[\#2454](/sssd/ticket/2454 "[RFE] Views: apply user SSH public key override"){.closed}
:   \[RFE\] Views: apply user SSH public key override

[\#2456](/sssd/ticket/2456 "Error message not helpful if extdom lookup fails"){.closed}
:   Error message not helpful if extdom lookup fails

[\#2460](/sssd/ticket/2460 "service lookups returned in lowercase with case_sensitive=preserving"){.closed}
:   service lookups returned in lowercase with
    case\_sensitive=preserving

[\#2461](/sssd/ticket/2461 "Proxy Provider: Fails to lookup case sensitive users and groups with ..."){.closed}
:   Proxy Provider: Fails to lookup case sensitive users and groups with
    case\_sensitive=preserving

[\#2462](/sssd/ticket/2462 "Manpage description of case_sensitive=preserving is incomplete"){.closed}
:   Manpage description of case\_sensitive=preserving is incomplete

[\#2464](/sssd/ticket/2464 "Use ldap_extra_attrs when requesting attributes from extdom plugin"){.closed}
:   Use ldap\_extra\_attrs when requesting attributes from extdom plugin

[\#2467](/sssd/ticket/2467 "Set the right permissions in Makefile.am when installing from source"){.closed}
:   Set the right permissions in Makefile.am when installing from source

[\#2468](/sssd/ticket/2468 "Don't set the umask in the utility function that creates sockets"){.closed}
:   Don't set the umask in the utility function that creates sockets

[\#2470](/sssd/ticket/2470 "refactor create_pipe_fd()"){.closed}
:   refactor create\_pipe\_fd()

[\#2473](/sssd/ticket/2473 "RFE: Add a configuration option to specify where a snippet with ..."){.closed}
:   RFE: Add a configuration option to specify where a snippet with
    sssd\_krb5\_localauth\_plugin.so is generated

[\#2475](/sssd/ticket/2475 "Wrong results returned with enumeration"){.closed}
:   Wrong results returned with enumeration

[\#2477](/sssd/ticket/2477 "SSSD doesn't tell that it can't start because of no longer existent ID ..."){.closed}
:   SSSD doesn't tell that it can't start because of no longer existent
    ID range

[\#2481](/sssd/ticket/2481 "ID Views implementation does not support IPA user&group overrides"){.closed}
:   ID Views implementation does not support IPA user&group overrides

[\#2484](/sssd/ticket/2484 "Password change over ssh doesn't work with OTP and FreeIPA"){.closed}
:   Password change over ssh doesn't work with OTP and FreeIPA

[\#2487](/sssd/ticket/2487 "sssd does not work with custom value of option re_expression"){.closed}
:   sssd does not work with custom value of option re\_expression

[\#2490](/sssd/ticket/2490 "dereferencing failure against openldap server"){.closed}
:   dereferencing failure against openldap server

[\#2492](/sssd/ticket/2492 "Group membership gets lost in IPA server mode"){.closed}
:   Group membership gets lost in IPA server mode

[\#2498](/sssd/ticket/2498 ""debug_timestamps = false" and "debug_microseconds = true" do not work ..."){.closed}
:   "debug\_timestamps = false" and "debug\_microseconds = true" do not
    work after enabling journald with sssd.

[\#2501](/sssd/ticket/2501 "pam_sss domains option: Untrusted users from the same domain are allowed ..."){.closed}
:   pam\_sss domains option: Untrusted users from the same domain are
    allowed to auth.

[\#2503](/sssd/ticket/2503 "Use the MEMORY ccache to pass around keytab contents"){.closed}
:   Use the MEMORY ccache to pass around keytab contents

[\#2506](/sssd/ticket/2506 "Check unlink return values to silence Coverity warnings"){.closed}
:   Check unlink return values to silence Coverity warnings

[\#2510](/sssd/ticket/2510 "The Kerberos provider is not properly views-aware"){.closed}
:   The Kerberos provider is not properly views-aware

[\#2512](/sssd/ticket/2512 "selinuxusermap rule does not apply to trusted AD users"){.closed}
:   selinuxusermap rule does not apply to trusted AD users

[\#2514](/sssd/ticket/2514 "gid is overridden by uid in default trust view"){.closed}
:   gid is overridden by uid in default trust view

[\#2516](/sssd/ticket/2516 "pam_sss domains option: User auth should fail when domains=<emtpy value>"){.closed}
:   pam\_sss domains option: User auth should fail when
    domains=&lt;emtpy value&gt;

[\#2518](/sssd/ticket/2518 "SSSD master doesn't build on RHEL-6"){.closed}
:   SSSD master doesn't build on RHEL-6

[\#2519](/sssd/ticket/2519 "SSSD should not fail authentication when only allow rules are used"){.closed}
:   SSSD should not fail authentication when only allow rules are used

[\#2520](/sssd/ticket/2520 "Crash in function get_object_from_cache"){.closed}
:   Crash in function get\_object\_from\_cache

[\#2521](/sssd/ticket/2521 "be_ptask unit test fails sometimes"){.closed}
:   be\_ptask unit test fails sometimes

[\#2524](/sssd/ticket/2524 "getent fails for posix group with AD users after login"){.closed}
:   getent fails for posix group with AD users after login

[\#2526](/sssd/ticket/2526 "User is unable to authenticate if the option krb5_fast_principal is NULL"){.closed}
:   User is unable to authenticate if the option krb5\_fast\_principal
    is NULL

[\#2529](/sssd/ticket/2529 "IPA: incomplete group memberships for AD users on IPA clients"){.closed}
:   IPA: incomplete group memberships for AD users on IPA clients

[\#2530](/sssd/ticket/2530 "MAN: Document that only usernames are checked for pam_trusted_uids"){.closed}
:   MAN: Document that only usernames are checked for pam\_trusted\_uids

[\#2535](/sssd/ticket/2535 "Access is not rejected for disabled domain"){.closed}
:   Access is not rejected for disabled domain

[\#2537](/sssd/ticket/2537 "sssd-libwbclient conflicts with Samba's and causes crash in wbinfo"){.closed}
:   sssd-libwbclient conflicts with Samba's and causes crash in wbinfo

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Carlos A. Munoz (1):

-   Add zanata.xml file for integration with Zanata command line client

Dan Lavu (3):

-   MAN PAGE: modified sssd-ldap.5.xml for sssd ticket
    [\#2451](https://fedorahosted.org/sssd/ticket/2451 "defect: sssd-ldap man page changes, add 'access_provider = ldap' as a requirement ... (closed: fixed)"){.closed
    .ticket}
-   MAN: page edit for ldap\_use\_tokengroups
-   MAN: Clarify ad\_gpo\_map\* options

Denis Kutin (1):

-   NSS: Possibility to use any shells in 'allowed\_shells'

Jakub Hrozek (68):

-   Updating the version for the 1.12.3 development
-   SSSD: Add the options to specify a UID and GID to run as
-   SSSD: Chown the log files
-   UTIL: Use a custom PID\_PATH and DB\_PATH when unit testing server.c
-   TESTS: Unit tests can use confdb without using sysdb
-   TESTS: Unit tests for server\_setup
-   RPM: Package the libsss\_semanage.so library
-   IPA: Handle NULL members in process\_members()
-   UTIL: Add a function to convert id\_t from a number or a name
-   BUILD: Add a config option for sssd user, own private directories as
    the user
-   RPM: Change file ownership to sssd.sssd
-   SSSD: Load a user to run a service as from configuration
-   SBUS: Chown the sbus socket if needed
-   SBUS: Allow connections from other UIDs
-   BE: Own the sbus socket as the SSSD user
-   NSS: Run as a user specified by monitor
-   TEST: Unit test for create\_pipe\_fd
-   AUTOFS: Run the autofs responder as the SSSD user
-   PAC: Run the pac responder as the SSSD user
-   SUDO: Run the sudo responder as the SSSD user
-   SSH: Run the ssh responder as the SSSD user
-   GPO: Terminate request on error
-   TESTS: Add tests for the views-related option maps
-   IPA: Don't fail the request when BE doesn't find the object
-   IPA: Rename user\_dom into obj\_dom
-   BUILD: Install ldap\_child and as setuid if running under
    non-privileged user
-   LDAP: Move sss\_krb5\_verify\_keytab\_ex to ldap\_child
-   LDAP: read the correct data type from ldap\_child's input buffer
-   LDAP: Drop privileges after kinit in ldap\_child
-   UTIL: Remove code duplication of struct io
-   UTIL: Remove more code duplication setting up child processes
-   IPA: Move setting the SELinux context to a child process
-   BE: Make struct bet\_queue\_item private to sssd\_be
-   BUILD: Install krb5\_child as suid if running under non-privileged
    user
-   KRB5: Drop privileges in the child, not the back end
-   KRB5: Move ccache-related functions to krb5\_ccache.c
-   KRB5: Move checking for illegal RE to krb5\_utils.c
-   KRB5: Move all ccache operations to krb5\_child.c
-   KRB5: Do not switch\_creds() if already the specified user
-   BUILD: Use separate chown to make changing ownership to the sssd
    user non-fatal
-   BUILD: Make chown of files to sssd user non-fatal
-   BUILD: Touch files in DESTDIR
-   BE: Become a regular user after initialization
-   BE: Fix a debug message
-   IPA: Handle IPA groups returned from extop plugin
-   Hint about removing sysdb if initializing ID map fails
-   PAM: Make pam\_forwarder\_parse\_data static
-   SBUS: Initialize DBusError before using it
-   PAM: Check for trusted domain before sending the request to BE
-   PAM: Move is\_uid\_trusted from pam\_ctx to preq
-   TESTS: Basic child tests
-   Add extra\_args to exec\_child()
-   KRB5: Create the fast ccache in a child process
-   LDAP: Remove useless include
-   sss\_atomic\_write\_s() return value is signed
-   KRB5: Relax DEBUG message
-   TESTS: Build test\_child even without cmocka
-   Rename test-child to dummy-child
-   CI: Suppress memory errors from poptGetNextOpt
-   tests: Free popt\_context
-   IFP: Return group names with the right case
-   KRB5: Check FAST kinit errors using get\_tgt\_times()
-   Skip CHAUTHTOK\_PRELIM when using OTPs
-   PAM: Domain names are case-insensitive
-   PAM: Missing argument to domains= should fail auth
-   MAN: Misspelled username in pam\_trusted\_users is not fatal
-   RESPONDER: Log failures to resolve user names in
    csv\_string\_to\_uid\_array
-   Updating translations for the 1.12.3 release

Lukas Slebodnik (28):

-   BUILD: Fix automake warning
-   test\_server: Fix waiting for background process
-   SPEC: Print testsuite log for failed test
-   SBUS: Fix error handling after closing container
-   BUILD: Fix linking cwrap tests with -Wl,--as-needed
-   test\_sysdb\_views: Use unique directory for cache
-   IPA: Store right username to selinux child context
-   PAM: Remove authtok from PAM stack with OTP
-   NSS: Fix warning enumerated type mixed with another type
-   Revert "LDAP: Change defaults for ldap\_user/group\_objectsid"
-   AD: Change level of debug message
-   CI: Build sssd on debian with samba support
-   LDAP: Disable token groups by default
-   sss\_client: Extract destroying of mmap cache to function
-   sss\_client: Fix race condition in memory cache
-   krb5: Check return value of krb5\_principal\_get\_realm
-   krb5: Check return value of sss\_krb5\_princ\_realm
-   AD: Set dp\_error if gc was not used
-   TOOLS: sss\_debuglevel should worh with ifp responder
-   CI: Update valgrind suppresion database for libselinux
-   IPA: Do not append domain name to fq name
-   sss\_client: Work around glibc bug
-   MAKE: Fix linking of test\_child\_common
-   UTIL: Fix dependencies of internal sss libraries
-   BUILD: Install libsss\_crypt after its dependencies
-   MONITOR: Disable inlining of function load\_configuration
-   krb5\_child: Initialize REALM earlier
-   IPA: properly handle groups from different domains

Michal Zidek (21):

-   util: Move semanage related functions to src/util
-   sss\_semanage: Add mlsrange parameter to set\_seuser
-   IPA: Use set\_seuser instead of writing selinux login file
-   MONITOR: Allow confdb to be accessed by nonroot user
-   SYSDB: Allow calling chown on the sysdb file from monitor
-   responder\_common: Create fd for pipe in helper
-   responders: Do not initialize pipe fd if already present
-   PAM: Create pipe file descriptors before privileges are dropped
-   PAM: Run pam responder as nonroot
-   nss: preserve service name in getsrv call
-   MONITOR: Fix warning may be used uninitialized
-   selinux\_child: Do not ignore return values.
-   proxy: Do not try to store same alias twice
-   PROXY: Preserve service name in proxy provider
-   MAN: Update case\_sensitive=Preserving in man pages.
-   Man: debug\_timestamps and debug\_microseconds
-   test: Wrong parameter type in sss\_parse\_name\_check
-   util: Special-case PCRE\_ERROR\_NOMATCH in sss\_parse\_name
-   util: sss\_get\_domain\_name regex mismatch not fatal
-   confdb: Make confdb\_set\_string accept const char pointer
-   AD: Never store case\_sensitive as "true" to confdb

Nikolai Kondrashov (1):

-   CI: Remove Clang analyzer

Pavel Březina (8):

-   IPA: use ipaUserGroup object class for groups
-   be\_ptask: create a private header file
-   be\_ptask: handle OFFLINE\_DISABLE mode before task execution
-   be\_ptask: add next\_execution time to struct be\_ptask
-   be\_ptask: do not store sync ctx to \_task
-   tests: be\_ptask
-   be\_ptask: let backoff affect only period
-   be\_ptask: use gettimeofday() instead of time()

Pavel Reichl (20):

-   TESTS: Add -std=gnu99 to cwrap tests CFLAGS
-   Fix debug messages - trailing '.'
-   pyhbac,pysss: fix reference leaks
-   RESPONDERS: refactor create\_pipe\_fd()
-   RESPONDERS: Don't hard-code umask value in utility function
-   RESPONDERS: Set default value for umask
-   CONFDB: Detect&fix misconf opt refresh\_expired\_interval
-   NSS: disable midpoint refresh for netgroups
-   SYSDB: sysdb\_idmap\_get\_mappings returns ENOENT
-   Fix: always check return value of unlink()
-   BUILD: restrict perms. when installing from source
-   SYSDB: sysdb\_get\_bool() return ENOENT & unit tests
-   simple access provider: non-existing object
-   simple-access-provider: break matching allowed users
-   LDAP: retain external members
-   TESTS: sysdb\_delete\_by\_sid() test return value
-   NSS: nss\_cmd\_getbysid\_search return ENOENT
-   SYSDB: sysdb\_search\_object\_by\_sid returns ENOENT
-   CONFDB: Typo in debug message
-   TESTS: typo in 'assert message'

Stephen Gallagher (1):

-   monitor: Service restart fixes

Sumit Bose (48):

-   ipa: fix issues with older servers not supporting views
-   ipa: improve error reporting for extdom LDAP exop
-   ipa\_subdomains\_handler\_master\_done: initialize reply\_count
-   nss: group enumeration fix
-   sdap\_print\_server: use getpeername() to get server address
-   IFP: Fix typo in debug message
-   memberof: check for empty arrays to avoid segfaults
-   Add add\_strings\_lists() utility function
-   IPA: inherit ldap\_user\_extra\_attrs to AD subdomains
-   Add parse\_attr\_list\_ex() helper function
-   nss: parse user\_attributes option
-   nss: return user\_attributes in origbyname request
-   sysdb\_get\_user\_attr\_with\_views: add mandatory override
    attributes
-   sysdb\_add\_overrides\_to\_object: add new parameter and multi-value
    support
-   Views: apply user SSH public key override
-   Add test for sysdb\_add\_overrides\_to\_object()
-   Add ssh pubkey to origbyname request
-   Revert "LDAP: Remove unused option ldap\_user\_uuid"
-   Revert "LDAP: Remove unused option ldap\_group\_uuid"
-   Fix uuid defaults
-   sysdb: add sysdb\_search\_object\_by\_uuid()
-   ipa: add split\_ipa\_anchor()
-   LDAP: add support for lookups by UUID
-   LDAP: always store UUID if available
-   ipa: add get\_be\_acct\_req\_for\_uuid()
-   IPA: make get\_object\_from\_cache() public
-   IPA: check overrrides for IPA users as well
-   Enable views for all domains
-   Fix KRB5\_CONF\_PATH
-   AD/IPA: add krb5\_confd\_path configuration option
-   sysdb: add sysdb\_delete\_view\_tree()
-   sysdb: add sysdb\_invalidate\_overrides()
-   views: allow view name change at startup
-   krb5: make krb5 provider view aware
-   IPA: only update view data if it really changed
-   krb5: do not fail if checking the old ccache failed
-   test: avoid leaks in leak tests
-   krb5: add copy\_ccache\_into\_memory()
-   krb5: add copy\_keytab\_into\_memory()
-   ldap\_child: copy keytab into memory to drop privileges earlier
-   krb5\_child: become user earlier
-   krb5: add wrapper for krb5\_kt\_have\_content()
-   krb5: handle KRB5KRB\_ERR\_GENERIC as unspecific error
-   IPA: verify group memberships of trusted domain users
-   IPA: do not try to add override gid twice
-   IPA: handle GID overrides for MPG domains on clients
-   libwbclient: initialize some return values
-   Add test for sysdb\_store\_override

