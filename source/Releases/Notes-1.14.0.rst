Highlights
----------

This section includes all changes since the last stable release, even
those included in the Alpha and Beta releases.

Smart Card related enhancements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  The IPA provider allows looking up users from trusted Active
   Directory domains by certificates that are included in the IPA
   ID-views. Please note that this functionality requires a recent IPA
   server.
-  The AD provider is now able to look up users from Active Directory
   domains by certificate. This change enables logins for Active
   Directory users with the help of a smart card.
-  The sss\_override tool is now able to add certificates as local
   overrides in the SSSD cache. Please note that the certificate
   overrides are stored in the local cache, so removing the cache also
   removes all the certificates!
-  Invalid certificates are skipped instead of aborting the whole
   operation when logging in with a smart card using SSH.
-  This version allows several OCSP-related options such as the OCSP
   responder to be configured during smart card authentication
-  SSSD is now able to determine the name of the user who logs in from
   the inserted smart card without having to type in the username.
   Please note that this functionality must be enabled with the
   ``allow_missing_name`` pam\_sss option.

Enhancements for easier administration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  The sss\_cache command line tool is now able to invalidate SUDO rules
   with its new ``-r/-R`` switches. Please note that the sudo rules are
   not refreshed with the ``sss_cache`` tool immediately. Refer to the
   sssd-sudo man page for the existing refresh timeouts.
-  SSSD is able to merge configuration file snippets from an include
   directory. This functionality requires the latest libini release
   1.3.0.
-  The GPO evaluator is able to skip malformed INI files. This feature
   is also only available with libini release 1.3.0 or newer.
-  SSSD is able to validate configuration files against a built-in
   schema. To retain backwards-compatibility with configuration files
   that would otherwise not validate, the validator only warns about
   errors in the config file in this version.
-  A new command line tool, called ``sssctl`` was added. This tool
   allows the administrator to observe the status of SSSD. In this
   version, the tool is able to:

   -  list SSSD domains and subdomains, including their online and
      offline status
   -  print information about objects stored in the cache
   -  backup or remove the local databases
   -  check the validity of the configuration file
   -  help truncate SSSD logs

Two-factor authentication improvements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  With a recent IPA server (4.4.x), it is now possible to authenticate
   either with OTP or with password. When a user has OTP authentication
   enabled and hits enter during the password prompt, the authentication
   will proceed with single factor only. The authentication method is
   stored in the ticket and depending on configuration of Kerberized
   services, the user will be able to only access selected service
   unless he authenticates with the second factor as well.

Performance improvements
^^^^^^^^^^^^^^^^^^^^^^^^

-  Several systemtap probes were added across the SSSD codebase as well
   as example systemtap scripts that use these probes. The scripts allow
   the administrator to observe the performance of some operations such
   as saving a group or the 'id' command with systemtap.
-  SSSD's cache performance was improved. SSSD now stores operational
   attributes of cache entries to a separate database with asynchronous
   writes mode, which results in substantially faster cache update times
   in most cases. Note that the performance of the initial cache write
   with an empty cache does not improve, only subsequent updates.

Miscellanous improvements
^^^^^^^^^^^^^^^^^^^^^^^^^

-  A new option ``local_negative_timeout`` was added. This option allows
   the admin to specify the time during which lookups for users that are
   not handled by SSSD but are present on the system (typically in
   ``/etc/passwd`` and ``/etc/group``) and prevents repeated lookups of
   local users on the remote server during initgroups operation.
-  The AD provider as well as the IPA provider part that handles AD
   users is able to use the PAC blob attached to the Kerberos ticket to
   resolve group memberships for a user if available. If the PAC blob is
   not available, other methods such as tokenGroups are used instead.
-  An ID-mapping plugin for the winbind deamon was added. With this
   plugin, it's possible for winbind to use the same ID-mapping scheme
   as SSSD uses, producing consistent ID values

Developer-facing features
^^^^^^^^^^^^^^^^^^^^^^^^^

-  A new "secrets" responder was added. This responder allows an
   application to communicate with SSSD over a UNIX socket using the
   `​Custodia
   API <https://github.com/simo5/custodia/blob/master/API.md>`__. SSSD
   then stores the secrets either in its local database or proxies them
   to a remote Custodia server.

Internal changes
^^^^^^^^^^^^^^^^

-  All user and group names are now stored fully qualified in the SSSD
   cache. This change decouples the format for storing the users from
   the format used for output. As a consequence, it is now possible to
   configure short user names even for users from trusted domains.
-  Several internal interfaces were refactored, providing cleaner code
   and better memory hierarchy. This change will allow the code to be
   easier to maintain and extend and get rid of sssd\_be crashes on
   service restarts while active requests are running.
-  The libipa\_hbac library was decorated with debug statements,
   allowing the administrator to see individual parts of the HBAC rules
   as well as the request passed to the evaluator

Packaging Changes
-----------------

-  The ``libsss_sudo.so`` and ``libsss_autofs.so`` libraries were moved
   to individual subpackage. This change allows the sudo and autofs
   libraries to be installed in containers when the SSSD deamon is
   running on the host or in another container.
-  The
   `PolicyKit? <https://docs.pagure.org/sssd-test2/PolicyKit.html>`__
   rules used by the p11 child during smartcard authentication were
   moved into their own subpackage to prevent conflict in ownership with
   the polkit package
-  The upstream RPMs no longer run as an unprivileged user, because
   there are several known issues related to running SSSD completely
   unprivileged. It it still possible to switch to a non-privileged user
   in the sssd.conf file.
-  If no configuration file exists on SSSD startup, the SSSD is now able
   to read a default sssd.conf on first start. Downstreams are
   encouraged to ship a default sssd.conf to allow SSSD to be enabled by
   default.
-  SSSD stores ephemeral attributes in a new ldb database called
   ``timestamps_$domain.ldb`` stored in the same directory as the
   regular caches.
-  The winbind ID-mapping plugin is packages in its own subpackage
   called ``winbind-idmap``
-  The SSSD configuration snippets are being read from a newly-owned
   directory ``/etc/sssd/conf.d``.
-  SSSD ships a file with rules for the configuration validator. In
   Fedora, this file is located at ``/var/lib/sss/cfg_rules.ini``

Documentation Changes
---------------------

-  The default attribute mappings for autofs provider with
   ``ldap_schema`` set to ``rfc2307`` were changed. The ``rfc2307``
   schema now uses the ``nis*`` attribute maps. This is especially
   important for users who store their automounter maps on an Active
   Directory server, which typically lacks the RFC2307bis extensions.
-  It is possible to configure SSSD debugging with the ``debug`` option
   which is an alias to the existing ``debug_level`` option.
-  A new ``local_negative_timeout`` option was added to configure the
   time during which lookups for users that exist on the system but are
   not handled by SSSD are negatively cached.
-  The PAC responder allows the time during which data read from the PAC
   bloc is considered valid with a new ``pac_lifetime`` option.
-  Several PAM services were added to the default list of Group Policy
   mappings. These include adding the ``unity`` login manager to the
   ``ad_gpo_map_interactive`` list and the ``polkit-1`` service to the
   ad\_gpo\_map\_allow list.
-  The p11 responder allows configuring the default OCSP responder with
   its new option ``ocsp_default_responder`` and the certificate
   expected to sign the OCSP response with the new
   ``ocsp_default_responder_signing_cert`` option.
-  The ``pam_sss.so`` PAM module has a new option ``allow_missing_name``
   that allows looking up the user (typically with the help of a
   certificate on a smartcard) during login.
-  The ``sss_override`` tool gained a new option ``-x/--certificate``
   that can be used to specify a local (as in the local cache)
   certificate for a particular user.
-  The ``sss_cache`` tool gained new options ``-r/-R`` that allow the
   administrator to invalidate the sudo rules in the cache.

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1656 </sssd/ticket/1656>`__
    Name-space add\_string and make it clear it can also remove string
`#2081 </sssd/ticket/2081>`__
    [RFE] sss\_cache: invalidate sudo rules
`#2151 </sssd/ticket/2151>`__
    [RFE] Integrate SSSD with containers
`#2158 </sssd/ticket/2158>`__
    PAC responder needs much time to process large group lists
`#2317 </sssd/ticket/2317>`__
    make the negcache timeout part of nc\_ctx
`#2369 </sssd/ticket/2369>`__
    check correct usage of talloc\_realloc
`#2424 </sssd/ticket/2424>`__
    review the use of umask() in sssd code
`#2683 </sssd/ticket/2683>`__
    man sssd.conf should clarify details about subdomain\_inherit
    option.
`#2703 </sssd/ticket/2703>`__
    Need better libhbac debuging added to sssd
`#2715 </sssd/ticket/2715>`__
    Make it possible to lookup user via UPN / Kerberos principal via IFP
`#2816 </sssd/ticket/2816>`__
    CI: whitespace\_test FAILED without any output
`#2848 </sssd/ticket/2848>`__
    cache\_req: add SID lookups
`#2855 </sssd/ticket/2855>`__
    Move libsss\_sudo.so outside sssd-common
`#2866 </sssd/ticket/2866>`__
    Cannot authenticate AD trust users after disconnecting network
`#2869 </sssd/ticket/2869>`__
    cache\_req tests don't use leak\_check\_push/leak\_check\_pop in
    fixtures
`#2870 </sssd/ticket/2870>`__
    AD GPO fails if the machine account belongs to a domain controller
`#2897 </sssd/ticket/2897>`__
    Smart Cards: Certificate in the ID View
`#2903 </sssd/ticket/2903>`__
    Review and update wiki pages for 1.14 Alpha
`#2924 </sssd/ticket/2924>`__
    Incorrect mapping for locked vs expired accounts with the krb
    provider
`#2928 </sssd/ticket/2928>`__
    NSS responder should negatively cache local users for a longer time
`#2941 </sssd/ticket/2941>`__
    Screen locks and smart card is removed - must show a message to
    insert the correct smartcard
`#2968 </sssd/ticket/2968>`__
    Abstract async connect functions from sss\_ldap
`#2973 </sssd/ticket/2973>`__
    Common responder code closes socket to early on client shutdown
`#2977 </sssd/ticket/2977>`__
    ssh with Smartcards - skip invalid certificates
`#2999 </sssd/ticket/2999>`__
    RFE - alias log\_level to debug\_level
`#3005 </sssd/ticket/3005>`__
    [Patch] Vague error message: [sss\_ldap\_init\_sys\_connect\_done]
    (0x0020): ldap\_install\_tls failed: Connect error
`#3010 </sssd/ticket/3010>`__
    SSSD doesn't fail over to next GC if authentication fails

.. raw:: html

   </div>

.. raw:: html

   <div>

`#385 </sssd/ticket/385>`__
    [RFE] Provide a Method to Display SSSD Status Information
`#1662 </sssd/ticket/1662>`__
    [RFE] Provide a force reload utility
`#1800 </sssd/ticket/1800>`__
    [RFE] create a generic sssdctl utility
`#1937 </sssd/ticket/1937>`__
    [RFE] Improve LDAP error logging
`#2028 </sssd/ticket/2028>`__
    sssd does not detail which line in configuration is invalid
`#2166 </sssd/ticket/2166>`__
    [RFE] SSSD cache database reporting
`#2247 </sssd/ticket/2247>`__
    [RFE] SSSD should be able to merge configuration from multiple files
`#2466 </sssd/ticket/2466>`__
    [RFE] Method for setting custom shells without Unix Attributes in AD
    account
`#2602 </sssd/ticket/2602>`__
    Optimize cache writes to sysdb
`#2671 </sssd/ticket/2671>`__
    RFE: sss\_cache: Add an option to rm the database files
`#2735 </sssd/ticket/2735>`__
    Document best practices from security standpoint for OpenScap team
`#2751 </sssd/ticket/2751>`__
    SSSD can't process GPO from Active Directory when it contains lines
    with no equal sign
`#2913 </sssd/ticket/2913>`__
    Add a Secrets as a Service component
`#2918 </sssd/ticket/2918>`__
    Make cli\_ctx more generic
`#2921 </sssd/ticket/2921>`__
    Replace the monitor ping with an in-process heartbeat
`#2957 </sssd/ticket/2957>`__
    Extend interface between DP and IFP
`#3070 </sssd/ticket/3070>`__
    Add infrastructure for socket-activated responders

.. raw:: html

   </div>

.. raw:: html

   <div>

`#2011 </sssd/ticket/2011>`__
    sysdb API is not consistent about the RDN of subdomain users
`#2269 </sssd/ticket/2269>`__
    [RFE] SSSD configuration file test tool (sssd\_check)
`#2449 </sssd/ticket/2449>`__
    Enable the sssd krb5 localauth plugin by default
`#2788 </sssd/ticket/2788>`__
    Allow fallback to default krb5\_kuserok() implementation for root
    user from localauth plugin
`#2838 </sssd/ticket/2838>`__
    full\_name\_format and default\_domain\_suffix breaks supplemental
    AD trust groups
`#2858 </sssd/ticket/2858>`__
    Please fix rfc2307 ldap schema implementation
`#2919 </sssd/ticket/2919>`__
    Improve sudo protocol
`#2929 </sssd/ticket/2929>`__
    NSS responder does not lowercase AD external group members
`#2966 </sssd/ticket/2966>`__
    Support authentication indicators from IPA
`#2988 </sssd/ticket/2988>`__
    [RFE] Make OTP/2FA authentication optional
`#3003 </sssd/ticket/3003>`__
    IPA key authentication logs false error message for root user.
`#3041 </sssd/ticket/3041>`__
    SSSD IPA provider should request client principal canonicalization
    by default
`#3055 </sssd/ticket/3055>`__
    The sssctl tool is missing a manpage
`#3059 </sssd/ticket/3059>`__
    The sssctl tool doesn't work with users from subdomains
`#3062 </sssd/ticket/3062>`__
    amend the sssd.conf manpage to mention include directories
`#3066 </sssd/ticket/3066>`__
    sssctl remove-cache should restart, not stop sssd
`#3071 </sssd/ticket/3071>`__
    Review and update SSSD's wiki pages for 1.14.0 release
`#3079 </sssd/ticket/3079>`__
    endianess issues in NSS tests and sysdb utils
`#3135 </sssd/ticket/3135>`__
    [RFE] Functionality to change the default OCSP responder
`#3190 </sssd/ticket/3190>`__
    sssd debug logging prints "No matching domain found for [$id]"
    everytime nss\_cmd\_getpwuid\_search is called

.. raw:: html

   </div>

Detailed changelog
------------------

Alexander Bokovoy (1):

-  SPEC: Move polkit rules into sssd-polkit-rules subpackage

Christian Heimes (1):

-  Secrets: m4 macros for jansson and http-parser

Dan Lavu (8):

-  sss\_override: Add restart requirements to man page
-  sss\_override: Add restart requirements to man page
-  MAN: Clarify that subdomain\_inherit only works for IPA and AD
-  URL in BUILD.txt is incorrect
-  Clarify that subdomains always use service discovery
-  Clarify that subdomains always use service discovery
-  PAM: Fix man for pam\_account\_{expired,locked}\_message
-  PAM: Fix man for pam\_account\_{expired,locked}\_message

David Disseldorp (2):

-  build: detect endianness at configure time
-  build: detect endianness at configure time

Fabiano Fidêncio (4):

-  sysdb: move add\_string() convenience to sysdb.c
-  sysdb: add sysdb\_{add,replace,delete}\_string()
-  sysdb: move add\_ulong() convenience to sysdb.c
-  sysdb: add sysdb\_{add,replace,delete}\_ulong()

Graham Leggett (1):

-  Add underlying diagnostic message for SSL errors.

Jakub Hrozek (189):

-  Updating the version to track 1.14 development
-  MAN: Clarify pam\_trusted\_users option description
-  MAN: proxy and krb5 are valid access control modules
-  contrib: Add a pre-push hook to warn about commits without
   Reviewed-By
-  AD: Provide common connection list construction functions
-  AD: Consolidate connection list construction on ad\_common.c
-  AD: Provide common connection list construction functions
-  AD: Consolidate connection list construction on ad\_common.c
-  tests: Fix compilation warning
-  tests: Fix compilation warning
-  FO: Don't free rc-allocated structure
-  tests: Reduce failover code duplication
-  FO: Use refcount to keep track of servers returned to callers
-  tools: Don't shadow 'exit'
-  tools: Don't shadow 'exit'
-  IFP: Skip non-POSIX groups properly
-  IFP: Skip non-POSIX groups properly
-  SSSD: Add a new option diag\_cmd
-  DP: Drop dp\_pam\_err\_to\_string
-  DP: Check callback messages for valid UTF-8
-  sbus: Check string arguments for valid UTF-8 strings
-  DP: Drop dp\_pam\_err\_to\_string
-  DP: Check callback messages for valid UTF-8
-  sbus: Check string arguments for valid UTF-8 strings
-  Updating translations for the 1.13.2 release
-  Upgrading the version for the 1.13.3 release
-  DP: Do not confuse static analysers with dead code
-  DP: Do not confuse static analysers with dead code
-  CONTRIB: Add a gdb pretty-printer for ldb and sysdb\_attrs
-  BUILD: Only install polkit rules if the directory is available
-  BUILD: Only install polkit rules if the directory is available
-  AD: Add autofs provider
-  KRB5: Handle preauth request timeout more gracefully
-  KRB5: Handle KRB5\_REALM\_UNKNOWN as ERR\_NETWORK\_IO
-  FO: Use tevent\_req\_defer\_callback() when notifying callers
-  IPA: Use search timeout, not enum timeout for searching overrides
-  IPA: Use search timeout, not enum timeout for searching overrides
-  AD: Add autofs provider
-  DP: Reduce code duplication in the callback handlers
-  DP: Reduce code duplication in Data Provider handlers
-  MAN: Clarify when should TGs be disabled for group nesting
   restriction
-  MAN: Clarify when should TGs be disabled for group nesting
   restriction
-  Update translations for the 1.13.3 release
-  Upgrading the version for the 1.13.4 release
-  DP: Print warning when the handler is not configured
-  tests: use
   unittest.\ `TestCase? <https://docs.pagure.org/sssd-test2/TestCase.html>`__.assertCountEqual
   if possible
-  Fix pep8 warnings in pyhbac-test.py
-  SDAP: Make it possible to silence errors from dereference
-  SDAP: Make it possible to silence errors from dereference
-  Add a new option ldap\_group\_external\_member
-  IPA: Add interface to call into IPA provider from LDAP provider
-  LDAP: Use the IPA provider interface to resolve external group
   members
-  Add a new option ldap\_group\_external\_member
-  IPA: Add interface to call into IPA provider from LDAP provider
-  LDAP: Use the IPA provider interface to resolve external group
   members
-  IPA: Use the common if-else coding style
-  tests: Extend test\_child\_common.c to include tests for the
   only\_extra\_args functionality
-  FO: Don't free rc-allocated structure
-  tests: Reduce failover code duplication
-  FO: Use refcount to keep track of servers returned to callers
-  FO: Use tevent\_req\_defer\_callback() when notifying callers
-  NSS: Move a DEBUG message so that it's less confusing
-  MAN: Move subdomain\_inherit to the correct man section
-  MAN: Move proxy\_fast\_alias to the correct man section
-  memberof: Don't allocate on a NULL context
-  memberof: Don't allocate on a NULL context
-  tests: Add a unit test for the external groups resolution
-  tests: Add a unit test for the external groups resolution
-  libipa\_hbac: Do not use C99
-  libipa\_hbac: Add more debug messages
-  libipa\_hbac: Fix typo in constant name
-  libipa\_hbac: Move the library to src/lib/ipa\_hbac
-  MAN: Remove duplicate description of the
   pam\_account\_locked\_message option
-  MAN: Remove duplicate description of the
   pam\_account\_locked\_message option
-  AD: Recognize Windows Server 2016
-  AD: Recognize Windows Server 2016
-  memberof: Fix a memory leak when removing ghost users
-  memberof: Don't allocate on NULL when deleting memberUids
-  tests: Check NULL context in sysdb-tests when removing group members
-  memberof: Fix a memory leak when removing ghost users
-  memberof: Don't allocate on NULL when deleting memberUids
-  tests: Check NULL context in sysdb-tests when removing group members
-  Updating translations for the 1.13.4 release
-  MAN: Drop the reference to IPAv2 in the man page
-  Make sdap\_process\_group\_send() static
-  MAN: Remove references to the obsolete
   `PubkeyAgent? <https://docs.pagure.org/sssd-test2/PubkeyAgent.html>`__
   ssh option
-  UTIL: Add ERR\_SBUS\_REQUEST\_HANDLED
-  IFP: Do not crash on invalid arguments to
   `GetUserAttr? <https://docs.pagure.org/sssd-test2/GetUserAttr.html>`__
-  UTIL: exit() the forked process if exec()-ing a child process fails
-  AD: Do not schedule the machine renewal task if adcli is not
   executable
-  AD: Do not leak file descriptors during machine password renewal
-  Do not leak fds in case of failures setting up a child process
-  LDAP: Try also the AD access control for IPA users
-  RESPONDER: Fix error check in cache\_req.c
-  UTIL: Add a PROBE macro into probes.h
-  BUILD: Add build infrastructure for systemtap scripts
-  SYSDB: Track transaction nesting in sysdb\_ctx
-  SYSDB: Add systemtap probes to track sysdb transactions
-  STAP: Add helper functions to for human-readable account request
   representation
-  LDAP: Decorate the hot paths in the LDAP provider with systemtap
   probes
-  CONTRIB: Add a systemtap script to analyze the performance of the
   'id' command
-  CONTRIB: Add a systemstap script to measure nested group code
   performance
-  BUILD: Enable systemtap during RPM build and CI
-  Updating the translations for the 1.14 alpha release
-  Updating the version for the 1.14 beta release
-  SYSDB: Move sysdb initialization into a new module sysdb\_init.c
-  UTIL: Add error codes for sysdb too old or too new
-  SYSDB: Refactor database connection
-  SYSDB: Add a second, timestamp-only ldb cache
-  SYSDB: Open a timestamps cache for caching domains
-  SYSDB: Wrap sysdb\_store\_group in a transaction and split it into
   smaller functions
-  SYSDB: Search the timestamp caches in addition to the sysdb cache
-  SYSDB: If modifyTimestamp is the same, only update the TS cache
-  SYSDB: Check if group attributes differ before saving a group
-  SYSDB: Refactor sysdb\_store\_user
-  SYSDB: Only update user attributes if needed
-  TESTS: Add a unit test for timestamps caches
-  TESTS: Add an integration test for the timestamps cache
-  LDAP: Shortcut looking up for group members sooner
-  Contrib: Add a gdbinit file
-  BUILD: Fall back to non-strict http parser, if strict is not
   available
-  MAN: Include idmap\_sss.8.xml in the manpage sources
-  Updating the translations for the 1.14 beta release
-  Updating the version for the next release
-  SSH: Do not print an error message if sss\_ssh\_authorizedkeys is
   asked for a local user
-  LDAP: Change the default rfc2307 autofs attribute mappings
-  TESTS: Add a test for sss\_parse\_internal\_fqname
-  TESTS: Add a test for sss\_create\_internal\_fqname
-  UTIL: Add a utility function to create a list of qualified names
-  UTIL: Add a utility function sss\_output\_name
-  BUILD: Temporarily disable unit and integration tests until we fix
   them to cope with qualified names in sysdb
-  SYSDB: add\_name\_and\_aliases\_for\_name\_override no longer needs
   to special case subdomain users
-  SDAP: Search functions don't need to construct per-domain names
-  TESTS: Fix sysdb tests to work with the new format
-  TESTS: Amend sysdb\_view tests for the FQDN schema
-  SIMPLE: Make the simple access provider work with qualified names
-  TESTS: Convert the simple access provider to cmocka
-  RESPONDER: Use fqnames for cache\_req lookups of users and groups
-  RESPONDER: Add a helper function sss\_resp\_create\_fqname
-  UTIL: expand\_homedir\_template manages usernames internally
-  TESTS: Fix the nested group tests to cope with FQDNs
-  NCACHE: Store FQDNs internaly, check for shortnames in files
-  NSS: Fix NSS responder to cope with fully-qualified usernames
-  PAM: Use qualified names internally in the PAM responder
-  SSH: Use a qualified name for user searches in the SSH responder
-  LDAP: Rename DP filter value from name to filter\_value
-  LDAP: Use shortname for LDAP queries
-  LDAP: save users with FQDN
-  LDAP: Convert RFC2307 member attribute values to FQDN-style
   ghostnames before acting on them
-  SYSDB: Add a utility function to return a list of qualified names
-  LDAP: make it clear that sdap\_add\_incomplete\_groups operates on
   sysdb names
-  LDAP: Use fqdns during nested RFC2307 initgroups
-  LDAP: Use FQDNs when saving incomplete groups
-  LDAP: Delete cache entry if not found by UPN
-  LDAP: The access control filter just needs the plain username
-  PROXY: Use fully qualified names internally
-  TOOLS: Make the local domain operate on FQDNs
-  SSS\_CACHE: Make internal functions static
-  SSS\_CACHE: Don't use sss\_get\_domain\_name, but create the internal
   fqname instead for users and groups
-  SSS\_SEED: Use FQDN for accessing sysdb
-  SSS\_OVERRIDE: Fixes for fully qualified names
-  KRB5: Rely on internal fqname when constructing UPNs
-  KRB5: Rely on sysdb names for the renewal task
-  KRB5: Use shortname when expanding the user template in Kerberos
   ccache
-  AD: No need to separately qualify subdomain users anymore
-  SYSDB: Construct internal fqnames, not NSS names in
   sysdb\_add\_group\_member\_overrides
-  IPA: Use internal fqname format instead of parsing NSS names
-  IPA: HBAC evaluator consumes shortnames
-  SELINUX: Parse the internal fqname before using it
-  RESPONDERS: Return the sysdb name from cache\_req
-  IPA: Save sudoUser qualified in the cache
-  LDAP: Qualify user and group names when saving the sudo users
-  IFP: Amend the
   `InfoPipe? <https://docs.pagure.org/sssd-test2/InfoPipe.html>`__
   responder for fqdns
-  TOOLS: sssctl: Work with trusted users
-  UTIL: Parse internal fqnames in find\_domain\_by\_object\_name
-  UTIL: Remove unused functions
-  TESTS: Convert the tests to use qualified names for ldb lookups
-  SYSDB: Remove useless parameter from sysdb\_init()
-  SYSDB: Allow passing a context to sysdb upgrade functions
-  SYSDB: Fix small issues during db upgrade
-  SYSDB: Remove the timestamps cache on update
-  MEMBEROF: Allow bypassing memberof during upgrade
-  SYSDB: Upgrade sysdb to use qualified names for users and groups,
   sudo rules and override objects
-  TOOLS: Some tools command might not need initialization to succeed
-  TOOLS: Add the upgrade-cache command
-  SUDO: Add more low-level tracing messages
-  LDAP: Lookup services by all protocols unless a protocol is specified
-  Updating the translations for the 1.14.0 release
-  Updating the version for the 1.14.0 release

Lukas Slebodnik (187):

-  CONTRIB: pre-push hook could work with python3
-  BUILD: Link just libsss\_crypto with crypto libraries
-  BUILD: Link crypto\_tests with existing library
-  BUILD: Remove unused variable TEST\_MOCK\_OBJ
-  BUILD: Link just libsss\_crypto with crypto libraries
-  BUILD: Link crypto\_tests with existing library
-  BUILD: Remove unused variable TEST\_MOCK\_OBJ
-  BUILD: Avoid symlinks with python modules
-  BUILD: Avoid symlinks with python modules
-  SSSDConfigTest: Try load saved config
-  SSSDConfigTest: Test real config without config\_file\_version
-  SSSDConfigTest: Try load saved config
-  SSSDConfigTest: Test real config without config\_file\_version
-  intg\_tests: Fix PEP8 warnings
-  intg\_tests: Fix PEP8 warnings
-  responder\_common\_tests: Removed unused libraries
-  BUILD: Remove unused variables
-  BUILD: Remove SSS\_CRYPTO\_LIBS from common libraries
-  BUILD: Accept krb5 1.14 for building the PAC plugin
-  BUILD: Accept krb5 1.14 for building the PAC plugin
-  BUILD: Fix detection of pthread with strict CFLAGS
-  BUILD: Fix detection of pthread with strict CFLAGS
-  sbus\_codegen\_tests: Suppress warning Wmaybe-uninitialized
-  BUILD: Fix cleanup without NLS
-  SDAP: Remove unused sdap\_id\_ctx from sdap\_id\_conn\_cache\_create
-  BUILD: Fix doc directory for sss\_simpleifp
-  BUILD: Fix doc directory for sss\_simpleifp
-  LDAP: Fix leak of file descriptors
-  LDAP: Fix leak of file descriptors
-  BUILD: Remove sudo doxygen file
-  CI: Workaroung for code coverage with old gcc
-  CI: Workaroung for code coverage with old gcc
-  FAIL\_OVER: Fix warning value computed is not used
-  cache\_req: Fix warning -Wshadow
-  SBUS: Fix warnings -Wshadow
-  TESTS: Fix warnings -Wshadow
-  cache\_req: Fix warning -Wshadow
-  SBUS: Fix warnings -Wshadow
-  TESTS: Fix warnings -Wshadow
-  INIT: Drop syslog.target from service file
-  INIT: Drop syslog.target from service file
-  sbus\_codegen\_tests: Suppress warning Wmaybe-uninitialized
-  AD: Remove unused memory context from ad\_user\_conn\_list
-  DP\_PTASK: Fix warning may be used uninitialized
-  DP\_PTASK: Fix warning may be used uninitialized
-  UTIL: Fix memory leak in switch\_creds
-  TESTS: Initialize leak check
-  TESTS: Check return value of check\_leaks\_pop
-  TESTS: Make check\_leaks static function
-  TESTS: Add warning for unused result of leak check functions
-  UTIL: Fix memory leak in switch\_creds
-  TESTS: Initialize leak check
-  TESTS: Check return value of check\_leaks\_pop
-  TESTS: Make check\_leaks static function
-  TESTS: Add warning for unused result of leak check functions
-  sss\_client: Fix underflow of active\_threads
-  sssd\_client: Do not use removed memory cache
-  test\_memory\_cache: Test removing mc without invalidation
-  Revert "intg: Invalidate memory cache before removing files"
-  sss\_client: Fix underflow of active\_threads
-  sssd\_client: Do not use removed memory cache
-  test\_memory\_cache: Test removing mc without invalidation
-  Revert "intg: Invalidate memory cache before removing files"
-  CONFIGURE: Bump AM\_GNU\_GETTEXT\_VERSION
-  CONFIGURE: Bump AM\_GNU\_GETTEXT\_VERSION
-  test\_sysdb\_subdomains: Do not use assignment in assertions
-  test\_sysdb\_subdomains: Do not use assignment in assertions
-  ldap\_local\_override\_test: Fix failure with python2.6
-  sbus\_codegen\_tests: Use portable definition of large constants
-  sbus\_codegen\_tests: Use portable definition of large constants
-  CI: Update suppression file for 32bit el6
-  DEBUG: Add missing new lines
-  DEBUG: Add missing new lines
-  AD: Log SID in debug message
-  SPEC: Change package ownership of %{pubconfpath}/krb5.include.d
-  SPEC: Change package ownership of %{pubconfpath}/krb5.include.d
-  SPEC: Move libsss\_sudo.so outside sssd-common
-  SPEC: Fix unowned directories
-  SPEC: Use systemd macros
-  pam-srv-tests: Reuse test directory for IO tests
-  FAILOVER: Improve reporting of errors
-  TOOLS: Fix warning Wsign-compare
-  pysss\_murmur: Fix warning Wsign-compare
-  pyhbac: Fix warning Wsign-compare
-  SPEC: Remove unnecessary clean-up of buildroot
-  SPEC: Fix packaging of libsss\_simpleifp
-  CONFIGURE: Replace obsoleted macro AC\_PROG\_LIBTOOL
-  CONFIGURE: Replace obsoleted macro AC\_PROG\_LIBTOOL
-  TESTS: Fix race condition in python test
-  TESTS: Fix race condition in python test
-  server-tests: Fix clean-up after successful test
-  PYTHON: sss\_obfuscate should work with python3
-  PYTHON: Fix pep8 errors in sss\_obfuscate
-  PYTHON: sss\_obfuscate should work with python3
-  PYTHON: Fix pep8 errors in sss\_obfuscate
-  intg: Change preference of openldap module path
-  SPEC: Move libsss\_autofs.so outside sssd-common
-  SPEC: Remove unnecessary requirements
-  UTIL: Backport error code ERR\_ACCOUNT\_LOCKED
-  sss\_idmap-tests: Fix segmentation fault
-  sss\_idmap-tests: Fix segmentation fault
-  krb5\_child: Warn if user cannot read krb5.conf
-  krb5\_child: Warn if user cannot read krb5.conf
-  Fix typos reported by lintian
-  Fix typos reported by lintian
-  UTIL: Use prefix for debug function
-  UTIL: Provide varargs version of debug\_fn
-  IPA: Use sss\_vdebug\_fn in hbac\_debug\_messages
-  IPA: log real hbac function
-  HBAC: Check format string in hbac log function
-  UTIL: Use sss\_vdebug\_fn for callbacks
-  UTIL: Use prefix for debug function
-  UTIL: Provide varargs version of debug\_fn
-  UTIL: Use sss\_vdebug\_fn for callbacks
-  Revert "DEBUG: Preventing chown\_debug\_file if journald on"
-  DEBUG: Ignore ENOENT for change owner of log files
-  Revert "DEBUG: Preventing chown\_debug\_file if journald on"
-  DEBUG: Ignore ENOENT for change owner of log files
-  TOOLS: Fix minor memory leak in sss\_colondb\_writeline
-  TOOLS: Fix minor memory leak in sss\_colondb\_writeline
-  CI: Use yum-deprecated instead of dnf
-  CI: Use yum-deprecated instead of dnf
-  FAIL\_OVER: Fix warning value computed is not used
-  BUILD: Remove unused include directories
-  BUILD: Simplify build of cwrap tests
-  UTIL: Fix indentation in dlinklist.h
-  UTIL: Fix warning misleading-indentation
-  UTIL: Fix indentation in dlinklist.h
-  UTIL: Fix warning misleading-indentation
-  CLIENT: Reduce code duplication
-  CLIENT: Retry request after EPIPE
-  CLIENT: Reduce code duplication
-  CLIENT: Retry request after EPIPE
-  libipa\_hbac: Ensure we always build with C90
-  UTIL: Do not call stderr with negative number
-  UTIL: Move debug part from util.h -> new debug.h
-  UTIL: Allow to append new line in sss\_vdebug\_fn
-  UTIL: Move debug part from util.h -> new debug.h
-  UTIL: Allow to append new line in sss\_vdebug\_fn
-  AUTOMAKE: Force usage of parallel test harness
-  CI: Use make check instead of make-check-wrap
-  AUTOMAKE: Force usage of parallel test harness
-  CI: Use make check instead of make-check-wrap
-  IPA: Remove unused parameter from ipa\_ext\_group\_member\_check
-  SDAP: Remove unused parameter talloc context
-  test\_ipa\_subdom\_server: Workaround for slow krb5 + SELinux
-  SPEC: Run extra unit tests with epel
-  GPO: Soften umask in gpo\_child
-  GPO\_CHILD: Create directories in gpo\_cache with right permissions
-  test\_ipa\_subdom\_server: Workaround for slow krb5 + SELinux
-  SPEC: Run extra unit tests with epel
-  GPO: Soften umask in gpo\_child
-  GPO\_CHILD: Create directories in gpo\_cache with right permissions
-  GPO: Process GPOS in offline mode if ldap search failed
-  GPO: Process GPOS in offline mode if ldap search failed
-  IPA: Check RDN in ipa\_add\_ad\_memberships\_get\_next
-  IPA: Check RDN in ipa\_add\_ad\_memberships\_get\_next
-  dp\_ptask: Fix memory leak in synchronous ptask
-  test\_be\_ptask: Check leaks in tests
-  dp\_ptask: Fix memory leak in synchronous ptask
-  test\_be\_ptask: Check leaks in tests
-  test\_ad\_common: Include missing header if building with NSS
-  SYSDB\_SUDO: Remove useless test
-  IPA\_SUDO: Prevent dereference of NULL pointer
-  intg: Use different uid range for add\_remove tests
-  LDAP: Print port in sdap\_print\_server
-  TOOLS: Fix warning maybe-uninitialized
-  pam-srv-tests: Increase cached\_auth\_timeout
-  CI: Exclude files in /tmp during coverage runs
-  pam-srv-tests: Fix warning unused-function
-  SPEC: Run sssd as privileged user
-  Prepare ini schema with rules for validation
-  UTIL: Fix debug message in sssd\_async\_connect\_done
-  UTIL: Revent connection handling in sssd\_async\_connect\_send
-  Downcast to errno\_t after tevent\_req\_is\_error
-  BUILD: Fix detection of systemd
-  BUILD: Detect libsystemd-daemon or libsystemd
-  Secrets: Fix format string
-  UTIL: Fix warning Wmissing-braces
-  Fix warning sign-compare
-  MAN: Update documentation of sss\_cache
-  IPA: Fix uninitialized pointer read (UNINIT)
-  DOC: Fix few typos in doxygen comments
-  MAN: Remove leading spaces from elements programlisting
-  test\_sysdb\_ts\_cache: Do not use wrong pointer for output argument
-  sysdb: Use ldb\_result as output in sysdb\_search\_ts\_{users,groups}
-  CONFIGURE: Inform about optional build dependencies

Mathieu Deaudelin-Lemay (1):

-  Changes to allow SSSD to be used for access control with a machine
   account belonging to a domain controller.

Michal Zidek (12):

-  Remove misleading comment
-  UTIL: Add function to parse internal fqname format
-  UTIL: Add function to create internal fqname
-  SYSDB: convert sysdb\_group\_membership\_mod to operate on qualified
   names
-  SYSDB: Search functions don't need to construct per-domain names
-  SDAP: Save user and group aliases qualified
-  SDAP: Store SID members during AD initgroups with a qualified name
-  TESTS: Fix the ldap\_id\_cleanup test for using qualified names in
   sysdb
-  TESTS: First pass on converting the sysdb tests to the fqname format
-  TESTS: Start converting the sysdb views tests to the fqname format
-  TESTS: Start fixing the NSS test for fully qualified names in sysdb
-  TESTS: Start fixing the PAM responder tests for fully qualified names
   in sysdb

Michal Židek (36):

-  SSSDConfig: Do not raise exception if config\_file\_version is
   missing
-  SSSDConfig: Do not raise exception if config\_file\_version is
   missing
-  spec: Missing initgroups mmap file
-  spec: Missing initgroups mmap file
-  util: Update get\_next\_domain's interface
-  tests: Add get\_next\_domain\_flags test
-  sysdb: Include disabled domains in link\_forest\_roots
-  sysdb: Use get\_next\_domain instead of dom->next
-  Refactor some conditions
-  util: Update get\_next\_domain's interface
-  tests: Add get\_next\_domain\_flags test
-  sysdb: Include disabled domains in link\_forest\_roots
-  sysdb: Use get\_next\_domain instead of dom->next
-  Refactor some conditions
-  util: Continue if setlocale fails
-  server\_setup: Log failed attempt to set locale
-  tests: Run intgcheck without libsemanage
-  tests: Regression test with wrong LC\_ALL
-  ldap\_local\_override\_test: Remove sss\_cache from teardown
-  MAN: sssd.conf should mention SSS\_NSS\_USE\_MEMCACHE
-  MAN: sssd.conf should mention SSS\_NSS\_USE\_MEMCACHE
-  NSS: do not skip cache check for netgoups
-  NSS: do not skip cache check for netgoups
-  util: Continue if setlocale fails
-  server\_setup: Log failed attempt to set locale
-  tests: Run intgcheck without libsemanage
-  tests: Regression test with wrong LC\_ALL
-  GPO: log specific ini parse error messages
-  GPO: log specific ini parse error messages
-  GPO: ignore non-KVP lines if possible
-  confdb: Make it possible to use config snippets
-  confdb: Check for config file errors on sssd startup
-  config: Fix filename matching regex
-  sss\_ini: Small refacoring of sss\_ini\_call\_validators
-  sssctl: Add config-check command
-  MAN: Config file merging

Nikolai Kondrashov (28):

-  CI: Exclude whitespace\_test from Valgrind checks
-  CI: Exclude whitespace\_test from Valgrind checks
-  TESTS: Make whitespace\_test pass without whitespace
-  man: Mention groups in filter\_groups description
-  man: Note filter\_groups are not affecting nesting
-  intg: Get base DN from LDAP connection object
-  intg: Add support for specifying all user attrs
-  intg: Split LDAP test fixtures for flexibility
-  intg: Reduce sssd.conf duplication in test\_ldap.py
-  intg: Fix RFC2307bis group member creation
-  intg: Get base DN from LDAP connection object
-  intg: Add support for specifying all user attrs
-  intg: Split LDAP test fixtures for flexibility
-  intg: Reduce sssd.conf duplication in test\_ldap.py
-  intg: Fix RFC2307bis group member creation
-  intg: Do not use non-existent pre-increment
-  intg: Do not use non-existent pre-increment
-  CI: Do not skip tests not checked with Valgrind
-  CI: Handle dashes in valgrind-condense
-  CI: Do not skip tests not checked with Valgrind
-  CI: Handle dashes in valgrind-condense
-  intg: Fix all PEP8 issues
-  intg: Fix all PEP8 issues
-  CI: Enforce coverage make check failures
-  CI: Enforce coverage make check failures
-  intg: Add more LDAP tests
-  intg: Add more LDAP tests
-  Fix packet size calculation in sss\_packet\_new

Pavel Březina (242):

-  sbus codegen tests: free ctx
-  sss tools: improve option handling
-  sss tools: improve option handling
-  sbus codegen tests: free ctx
-  cache\_req: provide extra flag for oob request
-  cache\_req: add support for UPN
-  cache\_req tests: reduce code duplication
-  cache\_req: remove raw\_name and do not touch orig\_name
-  cache\_req: provide extra flag for oob request
-  cache\_req: add support for UPN
-  cache\_req tests: reduce code duplication
-  cache\_req: remove raw\_name and do not touch orig\_name
-  intg: fix typos
-  sss\_override: fix comment describing format
-  sss\_override: explicitly set ret = EOK
-  sss\_override: steal msgs string to objs
-  sss\_override: fix comment describing format
-  sss\_override: explicitly set ret = EOK
-  sss\_override: steal msgs string to objs
-  nss: send original name and id with local views if possible
-  sudo: search with view even if user is found
-  sudo: send original name and id with local views if possible
-  nss: send original name and id with local views if possible
-  sudo: search with view even if user is found
-  sudo: send original name and id with local views if possible
-  sss\_tools: always show common and help options
-  sss\_override: fix exporting multiple domains
-  sss\_override: add user-find
-  sss\_override: add group-find
-  sss\_override: add user-show
-  sss\_override: add group-show
-  sss\_override: do not free ldb\_dn in get\_object\_dn()
-  sss\_override: use more generic help text
-  sss\_tools: do not allow unexpected free argument
-  sss\_tools: always show common and help options
-  sss\_override: fix exporting multiple domains
-  sss\_override: add user-find
-  sss\_override: add group-find
-  sss\_override: add user-show
-  sss\_override: add group-show
-  sss\_override: do not free ldb\_dn in get\_object\_dn()
-  sss\_override: use more generic help text
-  sss\_tools: do not allow unexpected free argument
-  BE: Add IFP to known clients
-  BE: Add IFP to known clients
-  AD: remove annoying debug message
-  AD: remove annoying debug message
-  man sssd-ad: fix typo
-  SYSDB: Add missing include to sysdb\_services.h
-  LDAP: Mark globals in ldap\_opts.h as extern
-  AD: Mark globals in ad\_opts.h as extern
-  IPA: Mark globals in ipa\_opts.h as extern
-  KRB5: Mark globals in krb5\_opts.h as extern
-  SYSDB: Add missing include to sysdb\_services.h
-  LDAP: Mark globals in ldap\_opts.h as extern
-  AD: Mark globals in ad\_opts.h as extern
-  IPA: Mark globals in ipa\_opts.h as extern
-  KRB5: Mark globals in krb5\_opts.h as extern
-  SUDO: convert periodical refreshes to be\_ptask
-  SUDO: move refreshes from sdap\_sudo.c to sdap\_sudo\_refresh.c
-  SUDO: move offline check to handler
-  SUDO: simplify error handling
-  SUDO: fix sdap\_id\_op logic
-  SUDO: fix tevent style
-  SUDO: fix sdap\_sudo\_smart\_refresh\_recv()
-  SUDO: sdap\_sudo\_load\_sudoers improve iterator
-  SUDO: set USN inside sdap\_sudo\_refresh request
-  SUDO: built host filter inside sdap\_sudo\_refresh request
-  SUDO: do not imitate full refresh if usn is unknown in smart refresh
-  SUDO: fix potential memory leak in sdap\_sudo\_init
-  SUDO: obtain host information when going online
-  SUDO: remove finalizer
-  SUDO: make sdap\_sudo\_handler static
-  SUDO: use size\_t instead of int in for cycles
-  SUDO: get srv\_opts after we are connected
-  SUDO: convert periodical refreshes to be\_ptask
-  SUDO: move refreshes from sdap\_sudo.c to sdap\_sudo\_refresh.c
-  SUDO: move offline check to handler
-  SUDO: simplify error handling
-  SUDO: fix sdap\_id\_op logic
-  SUDO: fix tevent style
-  SUDO: fix sdap\_sudo\_smart\_refresh\_recv()
-  SUDO: sdap\_sudo\_load\_sudoers improve iterator
-  SUDO: set USN inside sdap\_sudo\_refresh request
-  SUDO: built host filter inside sdap\_sudo\_refresh request
-  SUDO: do not imitate full refresh if usn is unknown in smart refresh
-  SUDO: fix potential memory leak in sdap\_sudo\_init
-  SUDO: obtain host information when going online
-  SUDO: remove finalizer
-  SUDO: make sdap\_sudo\_handler static
-  SUDO: use size\_t instead of int in for cycles
-  SUDO: get srv\_opts after we are connected
-  AD SRV: prefer site-local DCs in LDAP ping
-  AD SRV: prefer site-local DCs in LDAP ping
-  SDAP: handle ret properly in ldap\_get\_options()
-  SDAP: do not fail if refs are found but not processed
-  SDAP: do not fail if refs are found but not processed
-  SDAP: Add request that iterates over all search bases
-  SDAP: rename sdap\_get\_id\_specific\_filter
-  SDAP: support empty filters in sdap\_combine\_filters()
-  SUDO: use sdap\_search\_bases instead custom sb iterator
-  SUDO: make sudo sysdb interface more reusable
-  SUDO: move code shared between ldap and ipa to separate module
-  SUDO: allow to disable ptask
-  SUDO: fail on failed request that cannot be retry
-  IPA: add ipa\_get\_rdn and ipa\_check\_rdn
-  SDAP: use ipa\_get\_rdn() in nested groups
-  IPA SUDO: choose between IPA and LDAP schema
-  IPA SUDO: Add ipasudorule mapping
-  IPA SUDO: Add ipasudocmdgrp mapping
-  IPA SUDO: Add ipasudocmd mapping
-  IPA SUDO: Implement sudo handler
-  IPA SUDO: Implement full refresh
-  IPA SUDO: Implement rules refresh
-  IPA SUDO: Remember USN
-  SDAP: Add sdap\_or\_filters
-  IPA SUDO: Implement smart refresh
-  SUDO: sdap\_sudo\_set\_usn() do not steal usn
-  SUDO: remove full\_refresh\_in\_progress
-  SUDO: assume zero if usn is unknown
-  SUDO: allow disabling full refresh
-  SUDO: remember usn as number instead of string
-  SUDO: simplify usn filter
-  IPA SUDO: Add support for ipaSudoRunAsExt\* attributes
-  SDAP: Add request that iterates over all search bases
-  SDAP: rename sdap\_get\_id\_specific\_filter
-  SDAP: support empty filters in sdap\_combine\_filters()
-  SUDO: use sdap\_search\_bases instead custom sb iterator
-  SUDO: make sudo sysdb interface more reusable
-  SUDO: move code shared between ldap and ipa to separate module
-  SUDO: allow to disable ptask
-  SUDO: fail on failed request that cannot be retry
-  IPA: add ipa\_get\_rdn and ipa\_check\_rdn
-  SDAP: use ipa\_get\_rdn() in nested groups
-  IPA SUDO: choose between IPA and LDAP schema
-  IPA SUDO: Add ipasudorule mapping
-  IPA SUDO: Add ipasudocmdgrp mapping
-  IPA SUDO: Add ipasudocmd mapping
-  IPA SUDO: Implement sudo handler
-  IPA SUDO: Implement full refresh
-  IPA SUDO: Implement rules refresh
-  IPA SUDO: Remember USN
-  SDAP: Add sdap\_or\_filters
-  IPA SUDO: Implement smart refresh
-  SUDO: sdap\_sudo\_set\_usn() do not steal usn
-  SUDO: remove full\_refresh\_in\_progress
-  SUDO: assume zero if usn is unknown
-  SUDO: allow disabling full refresh
-  SUDO: remember usn as number instead of string
-  SUDO: simplify usn filter
-  IPA SUDO: Add support for ipaSudoRunAsExt\* attributes
-  sdap\_connect\_send: fail if uri or sockaddr is NULL
-  sdap\_connect\_send: fail if uri or sockaddr is NULL
-  MAKE: Do not compile generated header files
-  cache\_req: simplify cache\_req\_cache\_check()
-  cache\_req: do not lookup views if possible
-  cache\_req: simplify cache\_req\_cache\_check()
-  cache\_req: do not lookup views if possible
-  remove user certificate if not found on the server
-  remove user certificate if not found on the server
-  IPA SUDO: download externalUser attribute
-  IPA SUDO: download externalUser attribute
-  cache\_req: bring together search parameters
-  cache\_req: fix typo in debug message
-  cache\_req: break cache\_req\_input\_create into more functions
-  cache\_req: rename debug\_fqn to debugobj
-  cache\_req: improve debugging
-  cache\_req tests: remove unused users and groups
-  mock domain: reset ldb errors
-  cache\_req tests: use leak check in test fixtures
-  cache\_req tests: improve user and group creation
-  utils: return const char **from dup\_string\_list**
-  cache\_req: add SID lookups
-  cache\_req test: add lookup by sid
-  cache\_req: hide input and pass parameters in struct
-  cache\_req: rename cache\_req\_input to cache\_req
-  cache\_req: remove old comment
-  IPA SUDO: fix typo
-  IPA SUDO: support old ipasudocmd rdn
-  IPA SUDO: fix typo
-  IPA SUDO: support old ipasudocmd rdn
-  SUDO: be able to parse modifyTimestamp correctly
-  SUDO: be able to parse modifyTimestamp correctly
-  sudo: remove unused structure sudo\_dp\_request
-  sudo: use cache\_req for initgroups
-  sudo: do not use tevent when parsing query
-  sudo: convert get\_sudorules to tevent
-  Inform about (un)successful connection
-  Failover to next server if authentication fails
-  Remove braces from DEBUG statements
-  Rename dp\_ptask to be\_ptask
-  Rename dp\_refresh.h to be\_refresh.h
-  Rename dp\_refresh.c to be\_refresh.c
-  Rename dp\_dyndns.h to be\_dyndns.h
-  Rename dp\_dyndns.c to be\_dyndns.c
-  Rename dp\_backend.h to backend.h
-  SBUS: Add sbus\_conn\_register\_iface\_map
-  SBUS: Add data provider errors
-  SBUS: Print debug message when handler fails
-  ERRORS: Add ERR\_OFFLINE
-  ERRORS: Add ERR\_TERMINATED
-  ERRORS: Add ERR\_INVALID\_DATA\_TYPE
-  ERRORS: Add ERR\_MISSING\_DP\_TARGET
-  sdap\_search\_bases: allow map to be NULL
-  sdap\_search\_bases: allow returning only the first reply
-  sdap ops: add support for deref
-  DP: Introduce new interface for backend
-  DP: Add callback for backward compatibility
-  DP TESTS: Mock data\_provider
-  DP TESTS: Add unit tests for dp\_request\_table.c
-  DP: Switch to new interface
-  RESPONDER: New interface for client registration
-  DP: Move be\_req\_acct and remove discard\_const
-  IFP: Add domain nodes
-  IFP: new header file that contains interface definitions
-  sss\_sifp: make it compatible with latest version of the infopipe
-  sss\_sifp: return context even on IO error
-  sss\_sifp: bump version to 1:0:1
-  sss\_tools: add command description
-  sss\_tools: add help commands to usage message
-  sss\_tools: unify description of --debug
-  sss\_tools: tell whether an option was provided
-  sss\_tools: add commands delimiter
-  sss\_tools: pad help message properly
-  sss\_tools: return errno\_t instead of system code
-  sss\_tools: add test if sssd is running
-  sss\_tools: create confdb if not exist
-  sss\_override: return EXIT\_SUCCESS even when no overrides are found
-  sss\_override: return EXIT\_FAILURE if file does not exist during
   import
-  ERRORS: Add errors to indicated whether SSSD is running or not
-  SBUS ERRORS: Add unknown domain
-  SBUS: Fix typo in comment
-  SBUS: Add string helper macros
-  DP: Add function to get be\_ctx directly from dp\_client
-  DP: Add
   org.freedesktop.sssd.\ `DataProvider? <https://docs.pagure.org/sssd-test2/DataProvider.html>`__.Backend
-  DP: Add
   org.freedesktop.sssd.\ `DataProvider? <https://docs.pagure.org/sssd-test2/DataProvider.html>`__.Failover
-  IFP: Provide domain and failover status
-  sssctl: new tool
-  sssctl: restart SSSD when removing cache
-  sssctl: remove also ccache
-  sudo: solve problems with fully qualified names
-  sssctl: manual page

Pavel Reichl (61):

-  SDAP: Relax POSIX check
-  SDAP: Relax POSIX check
-  AD: fix minor memory leak
-  IPA: fix minor memory leak
-  SDAP: fix minor memory leak
-  PROXY: fix minor memory leak
-  sss\_override: amend man page - overrides do not stack
-  DYNDNS: use realm and server commands only as fallback
-  DYNDNS: improve nsupdate\_msg\_add\_fwd()
-  intg: fix assert messages in test\_memory\_cache
-  HBAC: remove misleading comment about deny rules
-  sudo: remove unused param. in ldap\_get\_sudo\_options
-  autofs: remove unused params in del\_autofs\_entries
-  LDAP: remove unused param. in sdap\_fallback\_local\_user
-  PAM: remove unused parameter cdb
-  sss\_override: Remove unused parameter tool\_ctx
-  SDAP: optional warning - sizelimit exceeded in POSIX check
-  SDAP: allow\_paging in sdap\_get\_generic\_ext\_send()
-  SDAP: change type of attrsonly in sdap\_get\_generic\_ext\_state
-  SDAP: pass params in sdap\_get\_and\_parse\_generic\_send
-  SDAP: optional warning - sizelimit exceeded in POSIX check
-  SDAP: allow\_paging in sdap\_get\_generic\_ext\_send()
-  SDAP: change type of attrsonly in sdap\_get\_generic\_ext\_state
-  SDAP: pass params in sdap\_get\_and\_parse\_generic\_send
-  sss\_override: Removed overrides might be in memcache
-  sss\_override: amend man page - overrides do not stack
-  sss\_override: Removed overrides might be in memcache
-  sudo: remove unused param name in sdap\_sudo\_get\_usn()
-  pam-srv-tests: split pam\_test\_setup() so it can be reused
-  pam-srv-tests: Add UT for cached 'online' auth.
-  pam-srv-tests: split pam\_test\_setup() so it can be reused
-  pam-srv-tests: Add UT for cached 'online' auth.
-  intg: Add test for user and group local overrides
-  intg: Add test for user and group local overrides
-  sysdb-tests: Fix warning - incompatible pointer type
-  sysdb-tests: Fix warning - incompatible pointer type
-  sudo: remove unused param name in sdap\_sudo\_get\_usn()
-  sudo: remove unused param. in ldap\_get\_sudo\_options
-  IDMAP: Fix computing max id for slice range
-  IDMAP: New structure for domain range params
-  IDMAP: Add support for automatic adding of ranges
-  IDMAP: Fix computing max id for slice range
-  IDMAP: New structure for domain range params
-  IDMAP: Add support for automatic adding of ranges
-  IDMAP: Fix minor memory leak
-  IDMAP: Fix minor memory leak
-  IDMAP: Man change for ldap\_idmap\_range\_size option
-  IDMAP: Man change for ldap\_idmap\_range\_size option
-  NSS: Fix memory leak netgroup
-  NSS: Fix memory leak netgroup
-  SDAP: Add error code to debug message
-  IDMAP: Add test to validate off by one bug
-  IDMAP: Add test to validate off by one bug
-  SDAP: Add return code ERR\_ACCOUNT\_LOCKED
-  PAM: Pass account lockout status and display message
-  SDAP: Add return code ERR\_ACCOUNT\_LOCKED
-  PAM: Pass account lockout status and display message
-  IDMAP: Add minor performance improvements
-  IDMAP: Make parameter names more descriptive
-  DP TESTS: Add unit tests for dp\_request.c
-  DP TESTS: Add unit tests for dp\_builtin.c

Petr Cech (73):

-  TESTS: Fixing of uninitialized pointer.
-  HBAC: Better libhbac debugging
-  REFACTOR: umask(0177) --> umask(SSS\_DFL\_UMASK)
-  REFACTOR: DFL\_RSP\_UMASK constant in responder code
-  REFACTOR: umask(077) --> umask(SSS\_DFL\_X\_UMASK)
-  REFACTOR: SCKT\_RSP\_UMASK constant in responder code
-  P11\_CHILD\_NSS: More restrictive permissions
-  UTILS: More restrictive permissions in domain\_info
-  UTIL-TESTS: More restrictive permissions
-  TESTS: More restrictive permissions in debug\_tests
-  TESTS: Restrictive permissions in check\_and\_open
-  DEBUG: Preventing chown\_debug\_file if journald on
-  DEBUG: Preventing chown\_debug\_file if journald on
-  KRB5\_CHILD: More restrictive umask
-  UTIL: More restrictive umask on sss\_unique\_file()
-  TOOLS: DFL\_UMASK --> SSS\_DFL\_UMASK
-  TEST: Add test\_user\_by\_recent\_filter\_valid
-  TEST: Refactor of test\_responder\_cache\_req.c
-  TEST: Refactor of test\_responder\_cache\_req.c
-  TEST: Add common function are\_values\_in\_array()
-  TEST: Add test\_users\_by\_recent\_filter\_valid
-  TEST: Add test\_group\_by\_recent\_filter\_valid
-  TEST: Refactor of test\_responder\_cache\_req.c
-  TEST: Add test\_groups\_by\_recent\_filter\_valid
-  TEST: Add test\_user\_by\_recent\_filter\_valid
-  TEST: Refactor of test\_responder\_cache\_req.c
-  TEST: Refactor of test\_responder\_cache\_req.c
-  TEST: Add common function are\_values\_in\_array()
-  TEST: Add test\_users\_by\_recent\_filter\_valid
-  TEST: Add test\_group\_by\_recent\_filter\_valid
-  TEST: Refactor of test\_responder\_cache\_req.c
-  TEST: Add test\_groups\_by\_recent\_filter\_valid
-  IPA\_PROVIDER: Explicit no handle of services
-  IPA\_PROVIDER: Explicit no handle of services
-  KRB5\_CHILD: Debug logs for PAC timeout
-  KRB5\_CHILD: Debug logs for PAC timeout
-  KRB5: Adding DNS SRV lookup for krb5 provider
-  KRB5: Adding DNS SRV lookup for krb5 provider
-  TOOLS: Fix memory leak after getline() failed
-  TOOLS: Add comments on functions in colondb
-  TEST\_TOOLS\_COLONDB: Add tests for sss\_colondb\_\*
-  TOOLS: Fix memory leak after getline() failed
-  TOOLS: Add comments on functions in colondb
-  TEST\_TOOLS\_COLONDB: Add tests for sss\_colondb\_\*
-  REFACTOR: umask(077) --> umask(SSS\_DFL\_X\_UMASK)
-  REFACTOR: umask(0177) --> umask(SSS\_DFL\_UMASK)
-  TESTS: global\_talloc\_context push/pop remove
-  NEGCACHE: Fixing typo in test\_sss\_ncache\_gid()
-  NEGCACHE: Removing of condition for ttl = -1
-  SYSDB: Add new funtions into sysdb\_sudo
-  TESTS: Test of sysdb\_search\_sudo\_rules
-  SSS\_CACHE: Refactor
-  TOOL: Invalidation of sudo rules at sss\_cache
-  AUTOFS: Removing of redudant debug message
-  TEST: Removing duplication of mock\_rctx
-  NEGCACHE: Adding timeout to struct sss\_nc\_ctx
-  NEGCACHE: Removing timeout from sss\_ncache\_check\_\*
-  NEGCACHE: Adding getter for timeout
-  RESPONDER: Removing neg\_timeout from pam responder
-  RESPONDER: Removing neg\_timeout from pac\_ctx
-  RESPONDER: Removing neg\_timeout from sudo resp.
-  RESPONDER: Removing neg\_timeout from ifp repsonder
-  RESPONDER: Removing neg\_timeout from nss responder
-  RESPONDERS: Negcache in resp\_ctx preparing
-  RESPONDER: Removing ncache from nss\_ctx
-  RESPONDER: Removing ncache from ifp\_ctx
-  RESPONDER: Removing ncache from pac\_ctx
-  RESPONDER: Removing ncache from pam\_ctx
-  RESPONDER: Removing ncache from sudo\_ctx
-  RESPONDER: Removing of redudant function
-  AD\_PROVIDER: Fix constant char \*
-  RESPONDERS: Negative caching of local users
-  TEST: New tests for negative caching of locals

Robert Antoni Buj Gelonch (1):

-  Add Catalan translation to LINGUAS

Simo Sorce (20):

-  Krb5/PAM: Fix account lockout error handling
-  Util: Improve code to get connection credentials
-  Util: Move socket setup in a common utility file
-  Util: Set socket options and flags separately
-  Util Sockets: Tidy up connect() handling
-  Responders: Fix client destructor
-  Util: Add watchdog helper
-  Server: Enable Watchdog in all daemons
-  Monitor: Remove ping infrastructure
-  Responders: Make the client context more generic
-  Responders: Add support for socket activation
-  ConfDB: Add helper function to get "subsections"
-  Secrets: Add autoconf macros to build with secrets
-  Secrets: Add initial responder code for secrets service
-  Add initial providers infrastructure.
-  Secrets: Add encryption at rest
-  Secrets: Add Proxy backend
-  Local secrets provider Content-Type handling
-  Secrets: Add local container entries support
-  Monitor: Add mode to generate confdb only

Stephen Gallagher (15):

-  LDAP: Inform about small range size
-  LDAP: Inform about small range size
-  Monitor: Show service pings at debug level 8
-  Monitor: Show service pings at debug level 8
-  GPO: Add Cockpit to the Remote Interactive defaults
-  GPO: Add other display managers to interactive logon
-  GPO: Add Cockpit to the Remote Interactive defaults
-  GPO: Add other display managers to interactive logon
-  Netlink: Ignore RTM\_NEWADDR signals from link-local
-  GPO: Add "unity" to ad\_gpo\_map\_interactive
-  UTIL: Add secure copy function
-  Internal: Rename CONFDB\_DEFAULT\_CONFIG\_FILE
-  CONFIG: Use default config when none provided
-  GPO: Add "polkit-1" to ad\_gpo\_map\_allow
-  DEBUG: Add ``debug`` alias for debug\_level

Sumit Bose (117):

-  PAM: only allow missing user name for certificate authentication
-  PAM: only allow missing user name for certificate authentication
-  fix ldb\_search usage
-  fix upn cache\_req for sub-domain users
-  nss: fix UPN lookups for sub-domain users
-  fix ldb\_search usage
-  fix upn cache\_req for sub-domain users
-  nss: fix UPN lookups for sub-domain users
-  DP: successful authentication sets explicitly PAM\_SUCCESSS
-  NSS: fix a use-after-free issue
-  pam-srv-tests: Change service name
-  cache\_req: check all domains for lookups by certificate
-  cache\_req: check all domains for lookups by certificate
-  IPA: fix override with the same name
-  IPA: fix override with the same name
-  p11: allow p11\_child to run completely unprivileged
-  p11: allow p11\_child to run completely unprivileged
-  p11: check if cert is valid before selecting it
-  p11: check if cert is valid before selecting it
-  p11: enable ocsp checks
-  p11: enable ocsp checks
-  ldap: skip sdap\_save\_grpmem() if ignore\_group\_members is set
-  initgr: only search for primary group if it is not already cached
-  ldap: skip sdap\_save\_grpmem() if ignore\_group\_members is set
-  initgr: only search for primary group if it is not already cached
-  LDAP: check early for missing SID in mapping check
-  LDAP: check early for missing SID in mapping check
-  nfs idmap: fix infinite loop
-  nfs idmap: fix infinite loop
-  ipa\_s2n\_save\_objects(): use configured user and group timeout
-  Use right domain for user lookups
-  sdap\_save\_grpmem: determine domain by SID if possible
-  Use right domain for user lookups
-  sdap\_save\_grpmem: determine domain by SID if possible
-  ipa\_s2n\_save\_objects(): use configured user and group timeout
-  ldap: remove originalMeberOf if there is no memberOf
-  ldap: remove originalMeberOf if there is no memberOf
-  UTIL: allow to skip default options for child processes
-  DP\_TASK: add be\_ptask\_get\_timeout()
-  AD: add task to renew the machine account password if needed
-  FO: add fo\_get\_active\_server()
-  FO: add be\_fo\_get\_active\_server\_name()
-  AD: try to use current server in the renewal task
-  UTIL: allow to skip default options for child processes
-  DP\_TASK: add be\_ptask\_get\_timeout()
-  AD: add task to renew the machine account password if needed
-  FO: add fo\_get\_active\_server()
-  FO: add be\_fo\_get\_active\_server\_name()
-  AD: try to use current server in the renewal task
-  p11: add gnome-screensaver to list of allowed services
-  p11: add gnome-screensaver to list of allowed services
-  Just return NULL if tevent\_req\_create() fails
-  subdomains: inherit ldap\_krb5\_keytab
-  IPA: lookup idview name even if there is no master domain record
-  IPA: invalidate override data if original view is missing
-  IPA: lookup idview name even if there is no master domain record
-  IPA: invalidate override data if original view is missing
-  sdap: improve filtering of multiple results in GC lookups
-  sdap: improve filtering of multiple results in GC lookups
-  pam\_sss: reorder pam\_message array
-  pam\_sss: reorder pam\_message array
-  SDAP: make some AD specific calls public
-  LDAP: refactor sdap\_ad\_tokengroups\_initgr\_mapping\_done()
-  util: make concatenate\_string\_array() reusable
-  AD: process PAC during initgroups request
-  IPA: rename ipa\_s2n\_get\_fqlist\* to ipa\_s2n\_get\_list\*
-  IPA: ipa\_s2n\_get\_list\_send() allow other list types
-  IPA: resolve PAC for trusted users on IPA clients
-  PAC: only save PAC blob into the cache
-  sss\_override: do not generate DN, search object
-  tools: read additional data of the master domain
-  sss\_override: only add domain if name is not fully qualified
-  intg: local override for user with mixed case name
-  sss\_override: do not generate DN, search object
-  tools: read additional data of the master domain
-  sss\_override: only add domain if name is not fully qualified
-  intg: local override for user with mixed case name
-  krb5\_auth\_store\_creds: silence spurious debug message
-  build: move ndr\_krb5pac check to the other Samba checks
-  IPA: terminate properly if view name lookup fails
-  IPA: use forest name when looking up the Global Catalog
-  libwbclient: wbcSidsToUnixIds() don't fail on errors
-  AD: use krb5\_keytab for subdomain initialization
-  p11: add missing man page entry and config API
-  p11: add no\_verification option
-  p11: add OCSP default responder options
-  PAM: add pam\_sss option allow\_missing\_name
-  p11: add PKCS11\_LOGIN\_TOKEN\_NAME environment variable
-  sysdb: add sysdb\_attrs\_add\_base64\_blob()
-  sysdb: add searches by certificate with overrides
-  cache\_req: use overide aware call for lookup by certificate
-  ipa: add support for certificate overrides
-  nss: include certificates in full result list
-  ipa: save cert as blob in the cache
-  AD: read user certificate if available
-  nss: return user certificate base64 encoded
-  sss\_override: add certificate support
-  IPA: allow lookups by cert in sub-domains on the client
-  NSS: add SSS\_NSS\_GETNAMEBYCERT request
-  nss-idmap: add sss\_nss\_getnamebycert()
-  ssh: skip invalid certificates
-  Add winbind idmap plugin
-  localauth: remove enable\_only sssd from config snippet
-  localauth: make plugin non-authoritative on failures
-  utils: add sss\_write\_krb5\_snippet\_common()
-  IPA/AD: globally set krb5 canonicalization flag
-  NSS: Fix domain for UPN based lookups
-  TESTS; orig\_name does not need to be expanded to sysdb format
-  LDAP: fix typo
-  IPA: expand name in ipa\_add\_ad\_memberships\_get\_next()
-  IPA: add missing user name to homedir\_ctx
-  IPA: make get\_object\_from\_cache() aware of UPN searches
-  SYSDB: qualify\_attr: create new attribute only once
-  fix some 'might be used uninitialized' warnings
-  PAM/KRB5: optional otp and password prompting
-  SSH-CERT: always initialize cert\_verify\_opts
-  cert\_to\_ssh\_key: properly add leading 0 to bignums
