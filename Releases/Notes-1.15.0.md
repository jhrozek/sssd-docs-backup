Highlights {#Highlights}
----------

-   SSSD now allows the responders to be activated by the systemd
    service manager and exit when idle. This means the `services` line
    in sssd.conf is optional and the responders can be started
    on-demand, simplifying the sssd configuration. Please note that this
    change is backwards-compatible and the responders listed explicitly
    in sssd.conf's services line are managed by sssd in the same manner
    as in previous releases. Please refer to `man sssd.conf(5)` for more
    information
-   The sudo provider is no longer disabled for configurations that do
    not explicitly include the `sudo` responder in the `services` list.
    In order to disable the sudo-related back end code that executes the
    periodic LDAP queries, set the `sudo_provider` to `none` explicitly
-   The watchdog signal handler no longer uses signal-unsafe functions.
    This bug was causing a deadlock in case the watchdog was about to
    kill a stuck process
-   A bug that prevented TLS to be set up correctly on systems where
    libldap links with GnuTLS was fixed
-   The functionality to alter SSSD configuration through the D-Bus
    interface provided by the IFP responder was removed. This
    functionality was not used to the best of our knowledge, had no
    tests and prevented the
    [InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
    .wiki} responder from running as a non-privileged user.
-   A bug that prevented statically-linked applications from using
    libnss\_sss was fixed by removing dependency on `-lpthreads` from
    the `libnss_sss` library (please see
    [[​]{.icon}https://sourceware.org/bugzilla/show\_bug.cgi?id=20500](https://sourceware.org/bugzilla/show_bug.cgi?id=20500){.ext-link}
    for an example on why linking with `-lpthread` from an NSS modules
    is problematic)
-   Previously, SSSD did not ignore GPOs that were missing the
    gPCFunctionalityVersion attribute and failed the whole GPO
    processing. Starting with this version, the GPOs without the
    gPCFunctionalityVersion are skipped.

Packaging Changes {#PackagingChanges}
-----------------

-   The Augeas development libraries are no longer required since the
    configuration manipulation interface was dropped from the
    [InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
    .wiki} responder
-   The `libsss_config.so` internal library was removed as well due to
    removal of the
    [InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
    .wiki} config management
-   In order to manage socket-activated or bus activated responders,
    each responder is now represented by a systemd service file (e.g.
    `sssd-nss.service`). All responders except
    [InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
    .wiki}, which is bus-activated, are also managed by a socket unit
    file (e.g. `sssd-nss.socket`)

Documentation Changes {#DocumentationChanges}
---------------------

-   The sssd-secrets responder gained a new option `max_payload_size`
    that allows the administrator to limit the maximum size of a secret
-   A new option `responder_idle_timeout` was added to support idle
    termination of socket-activated responders
-   The `sssd-ad` and `sssd-ipa` man pages now summarize differences
    between the generic Kerberos/LDAP back end and the specialized
    IPA/AD back ends

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#697](/sssd/ticket/697 "Use command line arguments instead env vars for krb5_child"){.closed}
:   Use command line arguments instead env vars for krb5\_child

[\#2201](/sssd/ticket/2201 "Man pages do not specify that sssd dyndns_refresh_interval < 60 is pulled ..."){.closed}
:   Man pages do not specify that sssd dyndns\_refresh\_interval &lt; 60
    is pulled to 60 seconds

[\#2243](/sssd/ticket/2243 "[RFE] Socket-activate responders"){.closed}
:   \[RFE\] Socket-activate responders

[\#2517](/sssd/ticket/2517 "krb5_child: Remove getenv() ran as root"){.closed}
:   krb5\_child: Remove getenv() ran as root

[\#3060](/sssd/ticket/3060 "better debugging of timestamp cache modifications"){.closed}
:   better debugging of timestamp cache modifications

[\#3129](/sssd/ticket/3129 "[RFE] socket-activate the IFP responder"){.closed}
:   \[RFE\] socket-activate the IFP responder

[\#3151](/sssd/ticket/3151 "cache_req: complete the needs of NSS responders"){.closed}
:   cache\_req: complete the needs of NSS responders

[\#3156](/sssd/ticket/3156 "nss_sss might leak memory when calling thread goes away"){.closed}
:   nss\_sss might leak memory when calling thread goes away

[\#3214](/sssd/ticket/3214 "Update man pages for any AD provider config options that differ from ..."){.closed}
:   Update man pages for any AD provider config options that differ from
    ldap/krb5 providers defaults

[\#3215](/sssd/ticket/3215 "Review and update SSSD's wiki pages for 1.15 Alpha release"){.closed}
:   Review and update SSSD's wiki pages for 1.15 Alpha release

[\#3235](/sssd/ticket/3235 "SSSCTL should not be case sensitive when searching for usernames or groups ..."){.closed}
:   SSSCTL should not be case sensitive when searching for usernames or
    groups in a case-insensitive domain

[\#3245](/sssd/ticket/3245 "[RFE] Shutdown timeout for {socket,bus}-activated responders"){.closed}
:   \[RFE\] Shutdown timeout for {socket,bus}-activated responders

[\#3275](/sssd/ticket/3275 "Unchecked return value of  sss_cmd_empty_packet(pctx->creq->out);"){.closed}
:   Unchecked return value of
    sss\_cmd\_empty\_packet(pctx-&gt;creq-&gt;out);

[\#3283](/sssd/ticket/3283 "getsidbyid can fail in some cases due to cache_req refactoring"){.closed}
:   getsidbyid can fail in some cases due to cache\_req refactoring

[\#3284](/sssd/ticket/3284 "getsidbyname does not work properly with case insensitive domains"){.closed}
:   getsidbyname does not work properly with case insensitive domains

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Amith Kumar (1):

-   MAN: Updation of sssd-ad man page for case when
    dyndns\_refresh\_interval &lt; 60 seconds

Carl Henrik Lunde (1):

-   Prevent use after free in fd\_input\_available

David Michael (1):

-   BUILD: Find a host-prefixed krb5-config when cross-compiling

Fabiano Fidêncio (34):

-   SECRETS: Fix secrets rule in the allowed sections
-   SECRETS: Add allowed\_sec\_users\_options
-   SECRETS: Delete all secrets stored during "max\_secrets" test
-   SECRETS: Add configurable payload size limit of a secret
-   BUILD: Drop libsss\_config
-   IFP: Remove
    "[ChangeDebugTemporarily?](https://docs.pagure.org/sssd-test2/ChangeDebugTemporarily.html){.missing
    .wiki}" method
-   AUTOFS: Check return of sss\_cmd\_empty\_packet()
-   SUDO: Drop logic to disable the backend in case the provider is not
    set
-   MONITOR: Expose the monitor's services type
-   MONITOR: Pass the service type to the
    [RegisterService?](https://docs.pagure.org/sssd-test2/RegisterService.html){.missing
    .wiki} method
-   UTIL: Introduce --socket-activated cmdline option for responders
-   UTIL: Introduce --dbus-activated cmd option for responders
-   RESPONDER: Make responders' common code ready for socket activation
-   AUTOFS: Make AutoFS responder socket-activatable
-   NSS: Make NSS responder socket-activatable
-   PAC: Make PAC responder socket-activatable
-   PAM: Make PAM responder socket-activatable
-   SSH: Make SSH responder socket-activatable
-   SUDO: Make Sudo responder socket-activatable
-   IFP: Make IFP responder dbus-activatable
-   MONITOR: Split up check\_services()
-   MONITOR: Deal with no services set up
-   MONITOR: Deal with socket-activated responders
-   MAN: Mention that the services' list is optional
-   MAN: "user" doesn't work with socket-activated services
-   MONITOR: Don't expose monitor\_common\_send\_id()
-   SBUS: Add a time\_t pointer to the sbus\_connection
-   SBUS: Add destructor data to sbus\_connection
-   RESPONDER: Make clear {reset\_,}idle\_timer() are related to client
-   RESPONDER: Don't expose client\_idle\_handler()
-   RESPONDER: Shutdown {dbus,socket}-activated responders in case
    they're idle
-   RESPONDER: Change how client timeout is calculated
-   SERVER: Set the process group during server\_setup()
-   WATCHDOG: Avoid non async-signal-safe from the signal\_handler

Howard Guo (1):

-   sss\_client: Defer thread cancellation until completion of nss/pam
    operations

Jakub Hrozek (16):

-   Updating the version for the 1.14.3 development
-   Updating the version to track sssd-1-15 development
-   SYSDB: Split sysdb\_try\_to\_find\_expected\_dn() into smaller
    functions
-   SYSDB: Augment sysdb\_try\_to\_find\_expected\_dn to match search
    base as well
-   MONITOR: Do not set up watchdog for monitor
-   MONITOR: Remove deprecated pong sbus method
-   MONITOR: Remove unused shutDown sbus method
-   Qualify ghost user attribute in case ldap\_group\_nesting\_level is
    set to 0
-   tests: Add a test for group resolution with
    ldap\_group\_nesting\_level=0
-   BUILD: Fix a typo in inotify.m4
-   SSH: Use default\_domain\_suffix for users' authorized keys
-   SYSDB: Suppress sysdb\_delete\_ts\_entry failed: 0
-   STAP: Only print transaction statistics if the script caught some
    transactions
-   test\_sssctl: Add an integration test for sssctl netgroup-show
-   KRB5: Advise the user to inspect the krb5\_child.log if the child
    fails with a System Error
-   IFP: Fix
    [GetUserAttr?](https://docs.pagure.org/sssd-test2/GetUserAttr.html){.missing
    .wiki}

Justin Stephenson (2):

-   MAN: Document different defaults for AD provider
-   MAN: Document different defaults for IPA provider

Lukas Slebodnik (45):

-   crypto: Port libcrypto code to openssl-1.1
-   BUILD: Fix build without samba
-   libcrypto: Check right value of CRYPTO\_memcmp
-   crypto-tests: Add unit test for sss\_encrypt + sss\_decrypt
-   crypto-tests: Rename encrypt decrypt test case
-   BUILD: Accept krb5 1.15 for building the PAC plugin
-   dlopen-test: Use portable macro for location of .libs
-   dlopen-test: Add missing libraries to the check list
-   dlopen-test: Move libraries to the right "sections"
-   dlopen-test: Add check for untested libraries
-   BUILD: Fix linking with librt
-   KRB5: Remove spurious warning in logs
-   TESTS: Check new line at end of file
-   UTIL: Fix implicit declaration of function 'htobe32'
-   SYSDB: Remove unused prototype from header file
-   sssctl: Fix missing declaration
-   UTIL: Fix compilation of sss\_utf8 with libunistring
-   CONFDB: Supress clang false passitive warnings
-   SIFP: Fix warning format-security
-   RESPONDER: Remove dead assignment to the variable ret
-   Fix compilation with python3.6
-   intg: Generate tmp dir with lowercase
-   LDAP: Fix debug messages after errors in \*\_get\_send
-   LDAP: Removed unused attr\_type from users\_get\_send
-   LDAP: Remove unused parameter attr\_type from groups\_get\_send
-   DP: Remove unused constants BE\_ATTR\_\*
-   DP: Remove unused attr\_type from struct dp\_id\_data
-   LDAP: Remove attrs\_type related TODO comments
-   sssd\_ldb.py: Remove a leftover debug message
-   intg: Fix python2,3 urllib
-   intg: Avoid using xrange in tests
-   intg: Avoid using iteritems for dictionary
-   intg: Use bytes with hash function
-   intg: Fix creating of slapd configuration
-   intg: Use bytes for value of attributes in ldif
-   intg: Use bytes as input in ctypes
-   intg: Return strings from ctypes wrappers
-   intg: Convert output of executed commands to strings
-   intg: Return list for enumeration functions
-   SYSDB: Update filter for get object by id
-   sysdb-tests: Add test for sysdb\_search\_object\_by\_id
-   sysdb: Search also aliases in sysdb\_search\_object\_by\_name
-   sysdb-tests: Add test for sysdb\_search\_object\_by\_name
-   MONITOR: Fix warning with undefined macro HAVE\_SYSTEMD
-   UTIL: Unset O\_NONBLOCK for ldap connection

Michal Židek (7):

-   sssctl: Flags for command initialization
-   ipa: Nested netgroups do not work
-   common: Fix domain case sensitivity init
-   sssctl: Search by alias
-   sssctl: Case insensitive filters
-   tests: sssctl user/group-show basic tests
-   MAN: sssctl debug level

Mike Ely (1):

-   ad\_access\_filter search for nested groups

Pavel Březina (40):

-   cache\_req: move from switch to plugins; add logic
-   cache\_req: move from switch to plugins, add plugins
-   cache\_req: switch to new code
-   cache\_req: delete old code
-   sudo: do not store usn if no rules are found
-   nss: move nss\_ctx-&gt;global\_names to rctx
-   ifp: remove unused fields from state
-   setent\_notify: remove unused private context
-   sss\_crypto.h: include required headers
-   sss\_output\_name: do not require fq name
-   cache\_req: fix initgroups by name
-   cache\_req: skip first search on bypass cache
-   cache\_req: encapsulate output data into structure
-   cache\_req: add ability to gather result from all domains
-   cache\_req: add ability to filter domains by enumeration
-   cache\_req: add user enumeration
-   cache\_req: add group enumeration
-   cache\_req: add support for service by name
-   cache\_req: add support for service by port
-   cache\_req: add support for services enumeration
-   cache\_req: add support for netgroups
-   cache\_req: allow shallow copy of result
-   cache\_req: allow to return well known object as result
-   cache\_req: return well known objects in object by sid
-   cache\_req: make sure that we always fetch default attrs
-   cache\_req: allow upn search with attrs
-   cache\_req: add object by name
-   cache\_req: add object by id
-   cache\_req: make plug-ins definition const
-   cache\_req: improve debugging
-   cache\_req: fix plugin function description
-   cache\_req: allow to search subdomains without fqn
-   cache\_req: do not set ncache if dp request fails
-   responders: unify usage of sss\_cmd\_send\_empty and \_error
-   responders: remove checks that are handled inside cache\_req
-   responders: do not try to contact DP with LOCAL provider
-   utils: add sss\_ptr\_hash module
-   nss: rewrite nss responder so it uses cache\_req
-   nss: make nss responder tests work with new code
-   nss: remove the old code

Petr Cech (2):

-   SYSDB: Adding message to inform which cache is used
-   SYSDB: Adding message about reason why cache changed

Petr Čech (5):

-   SYSDB: Adding lowercase sudoUser form
-   TESTS: Extending sysdb sudo store tests
-   RESPONDER: Adding of return value checking
-   UTIL: Removing of never read value
-   SYSDB: Fixing of sudorule without a sudoUser

Sorah Fukumori (1):

-   BUILD: Fix installation without samba

Sumit Bose (11):

-   sysdb: add parent\_dom to sysdb\_get\_direct\_parents()
-   sdap: make some nested group related calls public
-   LDAP/AD: resolve domain local groups for remote users
-   PAM: add a test for filter\_responses()
-   PAM: add pam\_response\_filter option
-   IPA/AD: check auth ctx before using it
-   krb5: Use command line arguments instead env vars for krb5\_child
-   krb5: fix two memory leaks
-   krb5: add tests for common functions
-   sss\_ptr\_hash\_delete\_all: use unsigned long int
-   libwbclient-sssd: wbcLookupSid() allow NULL arguments

Victor Tapia (1):

-   MONITOR: Create pidfile after responders started

