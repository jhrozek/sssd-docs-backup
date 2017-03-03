Highlights {#Highlights}
----------

-   SSSD's cache performance was improved. SSSD now stores operational
    attributes of cache entries to a separate database with asynchronous
    writes mode, which results in substantially faster cache update
    times in most cases. Note that the performance of the initial cache
    write with an empty cache does not improve, only subsequent updates.
-   SSSD is able to merge configuration file snippets from an include
    directory. This functionality requires the latest libini release
    1.3.0.
-   The GPO evaluator is able to skip malformed INI files. This feature
    is also only available with libini release 1.3.0 or newer.
-   A new command line tool, called `sssctl` was added. This tool allows
    the administrator to observe the status of SSSD. In this version,
    the tool is able to:
    -   list SSSD domains and subdomains, including their online and
        offline status
    -   print information about objects stored in the cache
    -   backup or remove the local databases
    -   help truncate SSSD logs
-   SSSD is able to validate configuration files against a built-in
    schema. To retain backwards-compatibility with configuration files
    that would otherwise not validate, the validator only warns about
    errors in the config file in this version.
-   An ID-mapping plugin for the winbind deamon was added. With this
    plugin, it's possible for winbind to use the same ID-mapping scheme
    as SSSD uses, producing consistent ID values
-   A new "secrets" responder was added. This responder allows an
    application to communicate with SSSD over a UNIX socket using the
    [[​]{.icon}Custodia
    API](https://github.com/simo5/custodia/blob/master/API.md){.ext-link}.
    SSSD then stores the secrets either in its local database or proxies
    them to a remote Custodia server.

Packaging Changes {#PackagingChanges}
-----------------

-   SSSD stores ephemeral attributes in a new ldb database called
    `timestamps_$domain.ldb` stored in the same directory as the regular
    caches.
-   The winbind ID-mapping plugin is packages in its own subpackage
    called `winbind-idmap`
-   The SSSD configuration snippets are being read from a newly-owned
    directory `/etc/sssd/conf.d`.
-   SSSD ships a file with rules for the configuration validator. In
    Fedora, this file is located at `/var/lib/sss/cfg_rules.ini`

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#385](/sssd/ticket/385 "[RFE] Provide a Method to Display SSSD Status Information"){.closed}
:   \[RFE\] Provide a Method to Display SSSD Status Information

[\#1662](/sssd/ticket/1662 "[RFE] Provide a force reload utility"){.closed}
:   \[RFE\] Provide a force reload utility

[\#1800](/sssd/ticket/1800 "[RFE] create a generic sssdctl utility"){.closed}
:   \[RFE\] create a generic sssdctl utility

[\#1937](/sssd/ticket/1937 "[RFE] Improve LDAP error logging"){.closed}
:   \[RFE\] Improve LDAP error logging

[\#2028](/sssd/ticket/2028 "sssd does not detail which line in configuration is invalid"){.closed}
:   sssd does not detail which line in configuration is invalid

[\#2166](/sssd/ticket/2166 "[RFE] SSSD cache database reporting"){.closed}
:   \[RFE\] SSSD cache database reporting

[\#2247](/sssd/ticket/2247 "[RFE] SSSD should be able to merge configuration from multiple files"){.closed}
:   \[RFE\] SSSD should be able to merge configuration from multiple
    files

[\#2466](/sssd/ticket/2466 "[RFE] Method for setting custom shells without Unix Attributes in AD ..."){.closed}
:   \[RFE\] Method for setting custom shells without Unix Attributes in
    AD account

[\#2602](/sssd/ticket/2602 "Optimize cache writes to sysdb"){.closed}
:   Optimize cache writes to sysdb

[\#2671](/sssd/ticket/2671 "RFE: sss_cache: Add an option to rm the database files"){.closed}
:   RFE: sss\_cache: Add an option to rm the database files

[\#2735](/sssd/ticket/2735 "Document best practices from security standpoint for OpenScap team"){.closed}
:   Document best practices from security standpoint for OpenScap team

[\#2751](/sssd/ticket/2751 "SSSD can't process GPO from Active Directory when it contains lines with ..."){.closed}
:   SSSD can't process GPO from Active Directory when it contains lines
    with no equal sign

[\#2913](/sssd/ticket/2913 "Add a Secrets as a Service component"){.closed}
:   Add a Secrets as a Service component

[\#2918](/sssd/ticket/2918 "Make cli_ctx more generic"){.closed}
:   Make cli\_ctx more generic

[\#2921](/sssd/ticket/2921 "Replace the monitor ping with an in-process heartbeat"){.closed}
:   Replace the monitor ping with an in-process heartbeat

[\#2957](/sssd/ticket/2957 "Extend interface between DP and IFP"){.closed}
:   Extend interface between DP and IFP

[\#3070](/sssd/ticket/3070 "Add infrastructure for socket-activated responders"){.closed}
:   Add infrastructure for socket-activated responders

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Christian Heimes (1):

-   Secrets: m4 macros for jansson and http-parser

Jakub Hrozek (19):

-   Updating the version for the 1.14 beta release
-   SYSDB: Move sysdb initialization into a new module sysdb\_init.c
-   UTIL: Add error codes for sysdb too old or too new
-   SYSDB: Refactor database connection
-   SYSDB: Add a second, timestamp-only ldb cache
-   SYSDB: Open a timestamps cache for caching domains
-   SYSDB: Wrap sysdb\_store\_group in a transaction and split it into
    smaller functions
-   SYSDB: Search the timestamp caches in addition to the sysdb cache
-   SYSDB: If modifyTimestamp is the same, only update the TS cache
-   SYSDB: Check if group attributes differ before saving a group
-   SYSDB: Refactor sysdb\_store\_user
-   SYSDB: Only update user attributes if needed
-   TESTS: Add a unit test for timestamps caches
-   TESTS: Add an integration test for the timestamps cache
-   LDAP: Shortcut looking up for group members sooner
-   Contrib: Add a gdbinit file
-   BUILD: Fall back to non-strict http parser, if strict is not
    available
-   MAN: Include idmap\_sss.8.xml in the manpage sources
-   Updating the translations for the 1.14 beta release

Lukas Slebodnik (6):

-   Prepare ini schema with rules for validation
-   UTIL: Fix debug message in sssd\_async\_connect\_done
-   UTIL: Revent connection handling in sssd\_async\_connect\_send
-   Downcast to errno\_t after tevent\_req\_is\_error
-   BUILD: Fix detection of systemd
-   BUILD: Detect libsystemd-daemon or libsystemd

Michal Židek (3):

-   GPO: ignore non-KVP lines if possible
-   confdb: Make it possible to use config snippets
-   confdb: Check for config file errors on sssd startup

Pavel Březina (25):

-   IFP: Add domain nodes
-   IFP: new header file that contains interface definitions
-   sss\_sifp: make it compatible with latest version of the infopipe
-   sss\_sifp: return context even on IO error
-   sss\_sifp: bump version to 1:0:1
-   sss\_tools: add command description
-   sss\_tools: add help commands to usage message
-   sss\_tools: unify description of --debug
-   sss\_tools: tell whether an option was provided
-   sss\_tools: add commands delimiter
-   sss\_tools: pad help message properly
-   sss\_tools: return errno\_t instead of system code
-   sss\_tools: add test if sssd is running
-   sss\_tools: create confdb if not exist
-   sss\_override: return EXIT\_SUCCESS even when no overrides are found
-   sss\_override: return EXIT\_FAILURE if file does not exist during
    import
-   ERRORS: Add errors to indicated whether SSSD is running or not
-   SBUS ERRORS: Add unknown domain
-   SBUS: Fix typo in comment
-   SBUS: Add string helper macros
-   DP: Add function to get be\_ctx directly from dp\_client
-   DP: Add
    org.freedesktop.sssd.[DataProvider?](https://docs.pagure.org/sssd-test2/DataProvider.html){.missing
    .wiki}.Backend
-   DP: Add
    org.freedesktop.sssd.[DataProvider?](https://docs.pagure.org/sssd-test2/DataProvider.html){.missing
    .wiki}.Failover
-   IFP: Provide domain and failover status
-   sssctl: new tool

Simo Sorce (14):

-   Util: Add watchdog helper
-   Server: Enable Watchdog in all daemons
-   Monitor: Remove ping infrastructure
-   Responders: Make the client context more generic
-   Responders: Add support for socket activation
-   ConfDB: Add helper function to get "subsections"
-   Secrets: Add autoconf macros to build with secrets
-   Secrets: Add initial responder code for secrets service
-   Add initial providers infrastructure.
-   Secrets: Add encryption at rest
-   Secrets: Add Proxy backend
-   Local secrets provider Content-Type handling
-   Secrets: Add local container entries support
-   Monitor: Add mode to generate confdb only

Sumit Bose (1):

-   Add winbind idmap plugin

