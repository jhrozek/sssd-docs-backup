Highlights {#Highlights}
----------

-   The GPO access control was further enhanced to allow the access
    control decisions while offline and map the Windows logon rights
    onto Linux PAM services
-   The SSSD now ships a plugin for the rpc.idmapd daemon. Please refer
    to the
    [[​]{.icon}sss\_rpcidmapd(5)](https://jhrozek.fedorapeople.org/sssd/1.12.1/man/sss_rpcidmapd.5.html){.ext-link}
    man page for more details on the plugin.
-   A MIT Kerberos localauth plugin was added to SSSD. This plugin helps
    translating principals to user names in IPA-AD trust scenarios,
    allowing the krb5.conf configuration to be less complex.
-   A libwbclient plugin implementation is now part of the SSSD. The
    main purpose is to map Active Directory users and groups identified
    by their SID to POSIX users and groups for the file-server use-case.
-   Active Directory users ca nnow use their User Logon Name to log in
-   The sss\_cache tool was enhanced to allow invalidating the SSH host
    keys.
-   Groups without full POSIX information can now be used to enroll
    group membership (fixes
    [[​]{.icon}CVE-2014-0249](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0249){.ext-link})
-   Detection of transition from offline to online state was improved,
    resulting in fewer timeouts when SSSD is offline.
-   The Active Directory provider now correctly detects Windows Server
    2012 R2. Previous versions would fall back to the slower non-AD path
    with 2012 R2.
-   Several other bugs related to deployments where SSSD is acting as an
    AD client were fixed. Please refer to the detailed changelog for
    more information.

Packaging Changes {#PackagingChanges}
-----------------

-   The upstream spec file dropped support for RHEL-5
-   The libwbclient plugin implementation is packaged in its own
    subpackage
-   GPO files are stored in a new subdirectory, by default
    `/var/lib/sss/gpo_cache`

Documentation Changes {#DocumentationChanges}
---------------------

-   The case\_sensitive option was changed to be a tri-state and accepts
    a new value "preserving". When this option is used, the sssd would
    match case-insensitive, but return the original case.
-   A new option override\_space was added. When this option is set, a
    space character in user or group names is replaced by the character
    specified in this option
-   The NFS plugin has a new man page
    [[​]{.icon}sss\_rpcidmapd(5)](https://jhrozek.fedorapeople.org/sssd/1.12.1/man/sss_rpcidmapd.5.html){.ext-link}
-   A small random value is now added to the offline\_timeout parameter
    value to avoid flooding servers with periodical online checks
-   Several new GPO-related options were added. Please refer to the
    [[​]{.icon}sssd-ad](https://jhrozek.fedorapeople.org/sssd/1.12.1/man/sssd-ad.5.html){.ext-link}
    man page for more details. The options are prefixed with `ad_gpo_*`

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1560](/sssd/ticket/1560 "Enable OpenSSH-LPK support by default"){.closed}
:   Enable OpenSSH-LPK support by default

[\#1588](/sssd/ticket/1588 "[RFE] Allow SSSD to be used with smbd shares"){.closed}
:   \[RFE\] Allow SSSD to be used with smbd shares

[\#1749](/sssd/ticket/1749 "[RFE] Allow email-address in ldap_user_principal"){.closed}
:   \[RFE\] Allow email-address in ldap\_user\_principal

[\#1835](/sssd/ticket/1835 "[RFE] Implement localauth plugin for MIT krb5 1.12"){.closed}
:   \[RFE\] Implement localauth plugin for MIT krb5 1.12

[\#1974](/sssd/ticket/1974 "Remove the references to RHEL5 from upstream spec file"){.closed}
:   Remove the references to RHEL5 from upstream spec file

[\#2281](/sssd/ticket/2281 "[GSS 7.0] if access_provider is not set sssd fails with no good error"){.closed}
:   \[GSS 7.0\] if access\_provider is not set sssd fails with no good
    error

[\#2344](/sssd/ticket/2344 "a bug in codegen causes diffs in generated code when switching branches"){.closed}
:   a bug in codegen causes diffs in generated code when switching
    branches

[\#2357](/sssd/ticket/2357 "Failover SRV discovery not honouring priority/weight"){.closed}
:   Failover SRV discovery not honouring priority/weight

[\#2358](/sssd/ticket/2358 "[PATCH] sss_cache flush ssh host keys."){.closed}
:   \[PATCH\] sss\_cache flush ssh host keys.

[\#2359](/sssd/ticket/2359 ""local" auth_provider is not documented in sssd.conf"){.closed}
:   "local" auth\_provider is not documented in sssd.conf

[\#2367](/sssd/ticket/2367 "RFE: SSSD should preserve case for user uid field."){.closed}
:   RFE: SSSD should preserve case for user uid field.

[\#2382](/sssd/ticket/2382 "Push patches to bump the version info of sss_sifp"){.closed}
:   Push patches to bump the version info of sss\_sifp

[\#2403](/sssd/ticket/2403 ""Mapping ID [4294967295] to SID failed" messages clutter the sssd domain ..."){.closed}
:   "Mapping ID \[4294967295\] to SID failed" messages clutter the sssd
    domain log

[\#2423](/sssd/ticket/2423 "Man sssd-ldap shows parameter ldap_purge_cache_timeout with "Default: ..."){.closed}
:   Man sssd-ldap shows parameter ldap\_purge\_cache\_timeout with
    "Default: 10800 (12 hours)"

[\#2431](/sssd/ticket/2431 "offline gpo processing yields incorrect results if "tattooing" occurs"){.closed}
:   offline gpo processing yields incorrect results if "tattooing"
    occurs

[\#2523](/sssd/ticket/2523 "PAC: krb5_pac_verify failures should not be fatal (backport fix from ..."){.closed}
:   PAC: krb5\_pac\_verify failures should not be fatal (backport fix
    from upstream)

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Ian Lee (1):

-   Add user lookup and session dependencies to systemd service file.

Jakub Hrozek (45):

-   Updating the version for the 1.12.1 development
-   MAN: local auth\_provider is not documented in sssd.conf
-   MAN: Document that each provider type uses its own set of options
-   No point in searching for gid if we already know the group should be
    filtered
-   Only check GID if ID-mapping
-   AD: Check return value of ad\_gpo\_evaluate\_dacl
-   AD: Increment som\_index when advancing to the next GPO
-   LDAP: Print referrals for debugging purposes
-   LDAP: Dump LDAP server IP address with a high DEBUG level
-   LDAP: Avoid undefined ret value
-   UTIL: remove get\_username\_from\_uid
-   PAC: krb5\_pac\_verify failures should not be fatal
-   IFP: Fix lookups with fully-qualified names
-   RPM: Restart service in %posttrans, not %post
-   TESTS: Check if option maps have the right number of members
-   NSS: Ignore default\_domain for netgroups
-   Only replace space with the specified substitution
-   Make the space override responder-agnostic
-   PAM: Use the override\_space option
-   IFP: Use the override\_space option
-   SUDO: Use the override\_space option
-   TESTS: Add unit tests for the replace-space functionality
-   BE: Handle SIGUSR2
-   IPA: handle searches by SID in apply\_subdomain\_homedir
-   SYSDB: Clarify sss\_ldb\_modify\_permissive returns ldb error code
-   Revert "IPA: new attribute map for non-posix groups"
-   Revert "IPA: process non-posix nested groups"
-   Revert "IPA: try to resolve nested groups as poxix group"
-   LDAP: Do not shortcut on ret != EOK during password expiry check
-   LDAP: Split out linking primary group members into a separate
    function
-   LDAP: Don't add a user member twice when adding a primary group
-   LDAP: Use tmp\_ctx in ldap\_child for temporary data
-   LDAP: Use randomized ccname for storing credentials
-   LDAP: Add Windows Server 2012 R2 functional level
-   LDAP: Fall back to functional level of Windows Server 2003
-   LDAP: Enable tokenGroups with Windows Server 2003
-   TESTS: Add unit tests for the GPO interface
-   LDAP: Set umask before calling mkstemp
-   LDAP: Ignore returned referrals if referral support is disabled
-   LDAP: Don't reuse a single tevent callback for multiple requests
-   LDAP: Skip dereferenced entries that we are not permitted to read
-   TESTS: Add a unit test for dereference parsing
-   MAN: Add sss\_rpcidmapd.5.xml to the list of translatable man pages
-   LDAP: Check return value
-   Updating translations for the 1.12.1 release

Jan Cholasta (1):

-   SDAP: Set default value of ldap\_user\_ssh\_public\_key to
    "sshPublicKey"

Lukas Slebodnik (31):

-   sss\_client: thread safe initialisation of sss\_cli\_mc\_ctx
-   sss\_client: Fix memory leak in nss\_mc\_{group,passwd}
-   LDAP: Remove unused option ldap\_netgroup\_uuid
-   LDAP: Remove unused option ldap\_group\_uuid
-   LDAP: Remove unused option ldap\_user\_uuid
-   test\_utils: Use common header file for libsss\_util tests.
-   UTIL: Add functions for replacing whitespaces.
-   NSS: Replace spaces with specified string in names.
-   SDAP: Deref needn't be treated as critical
-   Revert "SDAP: Deref needn't be treated as critical"
-   dyndns\_test: Use right socket length of for IPv4 address.
-   responder-get-domains-tests: fix checking of leaks
-   test\_dyndns: Use different talloc context in wrapped functions.
-   TESTS: leak\_check functions shouldn't be called with NULL context
-   dyndns: Fix talloc hierarchy of "struct sss\_iface\_addr"
-   test\_dyndns: sss\_iface\_addr\_list\_get can return more values
-   SDAP: free subrequest in sdap\_dyndns\_update\_addrs\_done
-   SDAP: Immediately finish request for empty array
-   SDAP: Use different talloc\_context for array of names
-   SDAP: Update groups for user just once.
-   SDAP: Fix using of uninitialized variable
-   strtonum-tests: Add unit test for strtouint16.
-   responder\_socket\_access-tests: Fix condition in loop
-   MAN: Fix a conversion of seconds to hours
-   AD: Ignore all errors if gpo is in permissive mode.
-   AUTOCONF: Update detection of libnfsidmap
-   SPEC: Use netlink library version 3 for rhel7
-   SPEC: Drop old OS conditions from spec file.
-   refcount-tests: Do not force to run test in CK\_FORK mode
-   NSS: Use right domain for group members with fq names
-   pysss: test return value of realloc.

Michal Zidek (10):

-   Add function confdb\_set\_string.
-   case\_sensitivity = preserving
-   MAN: case\_sensitivity man page update
-   Remove unused function confdb\_set\_bool
-   ptask: Allow adding random\_offset to scheduled execution time
-   ptask: Add backoff feature to the ptask api.
-   Exit offline mode only if server is available.
-   MAN: offline\_timeout
-   be\_get\_account\_info change level of debug message
-   IFP: Suppress 'git diff' noise

Michal Šrubař (1):

-   LDAP SUDO: sudo provider doesn't fetch 'EntryUSN'

Nalin Dahyabhai (2):

-   sss\_client: Fix "struct sss\_cli\_mc\_ctx" reinitialize-on-errors
-   Accept krb5 1.13 for building the PAC plugin

Nikolai Kondrashov (10):

-   build: Remove substitution of \*\_OBJ variables
-   build: Mention required libini\_config version
-   build: Distinguish libini\_config version checks
-   build: Distinguish libnl version checks
-   build: Reverse order of libini\_config checks
-   build: Move libini\_config 1.1.0 check to libini\_config.m4
-   build: Don't install ad and ipa man pages unnecessarily
-   Add basic support for CI test execution
-   CI: Add libnfsidmap-dev Debian dependency
-   CI: Consider libcmocka-devel always present

Noam Meltzer (5):

-   NEW CLIENT: plugin for NFSv4 rpc.idmapd
-   NFSv4 client: (private) headers from libnfsidmap
-   NFSv4 client: add to build system
-   NFSv4 client: add to RPM spec
-   NFSv4 client: man page

Pavel Březina (15):

-   resolv tests: remove ununused variable from for cyclus
-   resolv tests: add test for multiple servers with zero weights
-   resolv: fix server sort by weight
-   sudo: fetch sudoRunAs attribute
-   sss\_sifp test: fix object path array test
-   sss\_sifp: set output parameters if attribute is NULL
-   ad\_handle\_acct\_info\_step: fix typo
-   ad: comment ENOENT when id mapping is disabled
-   ad: update membership after SIDs are resolved
-   sudo: use dbus array for rules refresh
-   sudo: replace asterisk with escape sequence in host filter
-   failover: set port status to not working if previous srv lookup
    failed
-   ad initgroups: continue if resolved SID is still missing
-   sudo: work with correct D-Bus iterator
-   sss\_sifp: bump version to 0:1:0

Pavel Reichl (25):

-   SYSDB: augmented logging when adding new group
-   LDAP: tokengroups do not work with id\_provider=ldap
-   SDAP: Continue resolving SID even if some fail
-   UTIL: rename find\_subdomain\_by\_sid
-   UTIL: rename find\_subdomain\_by\_name
-   UTIL: rename find\_subdomain\_by\_object\_name
-   SDAP: remove duplicated code
-   SDAP: reduce code duplicity-rfc2307bis nested groups
-   SDAP: fix use after free in async\_initgroups
-   SDAP: split sdap\_access\_filter\_get\_access\_done
-   SDAP: refactor sdap\_access\_filter\_send
-   SDAP: nitpicks in sdap\_access\_filter\_get\_access\_done
-   SDAP: refactor sdap\_access\_filter\_done
-   SDAP: don't log error on access denied
-   IPA: new attribute map for non-posix groups
-   IPA: process non-posix nested groups
-   IPA: try to resolve nested groups as poxix group
-   SDAP: refactor AC offline checks
-   SDAP: new option - DN to ppolicy on LDAP
-   SDAP: account lockout to restrict access via ssh key
-   MAN: options 'lockout' and 'ldap\_pwdlockout\_dn'
-   SYSDB: SSS\_LDB\_SEARCH - macro around ldb\_search
-   IPA: process non-posix nested groups
-   AD: process non-posix nested groups w/o tokenGroups
-   AD: process non-posix nested groups using tokenGroups

Sumit Bose (17):

-   KRB5: add missing debug-to-stderr option to krb5\_child
-   AD: add missing debug-to-stderr option to gpo\_child
-   libwbclient: SSSD implementation
-   sss\_log: fix handling of variable argument lists
-   sysdb\_get\_real\_name: allow UPN as input
-   LDAP: If extra\_value is 'U' do a UPN search
-   PAM: extract checks from parsing routines
-   PAM: remove ldb\_result member from pam\_auth\_req context
-   NSS: check\_cache() add extra option
-   PAM, NSS: allow UPN login names
-   Replace space: add some checks
-   Add conditional build for MIT Kerberos localauth plugin
-   Implement MIT Kerberos localauth plugin
-   Doxygen: replace &lt;pre&gt; with markdown table
-   libwbclient: make build optional
-   dlopen test: only test libwbclient when it is build
-   libwbclient: avoid collision with Samba version

William B (1):

-   SSS\_CACHE: Allow sss\_cache tool to flush SSH hosts cache

Yassir Elley (9):

-   AD-GPO: Store policy settings in local files
-   AD-GPO: add sysdb\_gpo support for caching gpo version
-   AD-GPO: only download policy files if gpo version changes
-   AD-GPO: add ad\_gpo\_cache\_timeout option
-   AD-GPO: sysdb\_gpo changes for offline gpo support
-   AD-GPO: ad\_gpo changes for offline gpo support
-   AD-GPO: config changes for gpo\_map\_\* options
-   AD-GPO: processing changes for gpo\_map\_\* options
-   AD-GPO: delete stale GPOs

