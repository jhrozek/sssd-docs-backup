Highlights
----------

-  This release adds several new enhancements and fixes many bugs
-  Notable new enhancements:

   -  The background refresh tasks now supports refreshing users and
      groups as well. Please see the description of the
      ``refresh_expired_interval`` parameter in the ``sssd.conf`` man
      page.
   -  A new option ``subdomain_inherit`` was added. Options included in
      the ``subdomain_inherit`` option also apply for trusted domains,
      if supported. This release supports inheriting
      ``ignore_group_members``, ``ldap_purge_cache_timeout``,
      ``ldap_use_tokengroups`` and ``ldap_user_principal``.
   -  When an expired account attempts to log in, a configurable error
      message can be displayed with sufficient ``pam_verbosity``
      setting. Please see the description of the
      ``pam_account_expired_message`` option for more information.
   -  OpenLDAP ppolicy can be honored even when an alternate login
      method (such as SSH key) is used. Please see the description of
      the new ``ppolicy`` value of the ``ldap_access_order`` option.
   -  A new option ``krb5_map_user`` was added. This option allows the
      admin to map UNIX usernames to Kerberos principals. The option
      would be mostly useful for setups that wish to continue using UNIX
      file-based identities together with SSSD Kerberos authentication

-  The important bug fixes include:

   -  Several AD-specific bugs that resulted in the incorrect set of
      groups being displayed after the initgroups operation were fixed
   -  Many fixes related to the IPA ID views feature are included.
      Setups using the ID views feature should update the SSSD instance
      on both IPA servers and clients.
   -  The AD provider now handles binary GUIDs correctly. This bug was
      manifested with an error message saying
      ``ldb_modify failed: Invalid attribute syntax``.
   -  The AD provider no longer downloads full group objects during
      initgroups request if POSIX attributes are used. This fix may
      speed up the login times significantly.
   -  A bug that prevented the ``ignore_group_members`` parameter to be
      used with the AD provider was fixed
   -  The fail over code now reads and honors TTL value for SRV queries
      as well. Previously, SRV queries used a hardcoded timeout
   -  The SELinux context set up during login with an IPA provider is
      only called if the context had changed. This fixes a performance
      regression with the IPA provider.
   -  Race condition between setting the timeout in the back ends and
      reading it in the front end during initgroup operation was fixed.
      This bug affected applications that perform the ``initgroups(3)``
      operation in multiple processes simultaneously.
   -  Setups that only want to use the domain SSSD is connected to, but
      not the autodiscovered trusted domains by setting
      ``subdomains_provider=none`` now work correctly as long as the
      domain SID is set manually in the config file
   -  In case only allow rules are used, the simple access provider is
      now able to skip unresolvable groups.
   -  The GPO access control code now handles situations where user and
      computer objects were in different domains. Previously, an attempt
      to log in as user from a different domain than computer always
      resulted in login failure.

Packaging Changes
-----------------

-  The cmocka unit tests now require cmocka version 1.0 or later
-  The ``libsss_krb5_common.so`` library had been moved to the
   sssd-common subpackage to avoid ordering issues between
   libsss\_krb5\_common and libsss\_ldap\_common
-  The ``proxy_child`` helper binary was marked as setuid in order for
   the proxy provider to work without root privileges.

Documentation Changes
---------------------

-  A new option ``subdomain_inherit`` was added. See the highlights
   section for more details.
-  A new option ``krb5_map_user`` was added. See the highlights section
   for more details.
-  The ``ldap_access_order`` option accepts new value ``ppolicy``.
-  Account expiration message can be customized using a new option
   ``pam_account_expired_message``

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1884 </sssd/ticket/1884>`__
    [RFE] Read and use the TTL value when resolving a SRV query
`#2050 </sssd/ticket/2050>`__
    ssh login reject is abrupt
`#2083 </sssd/ticket/2083>`__
    Document the best practices for AD access control
`#2167 </sssd/ticket/2167>`__
    [RFE] Allow SSSD to issue shadow expiration warning even if
    alternate authentication method is used
`#2346 </sssd/ticket/2346>`__
    [RFE] Implement background refresh for users and groups
`#2444 </sssd/ticket/2444>`__
    extop request marks dp\_req as failed when an entry is not found
`#2507 </sssd/ticket/2507>`__
    Cyclic dependencies between sssd-ldap and krb5-common
`#2509 </sssd/ticket/2509>`__
    RFE: Handle setups with id\_provider=proxy and auth\_provider=krb5
    better
`#2513 </sssd/ticket/2513>`__
    Add a hint on using DEBUG levels to the troubleshooting page
`#2528 </sssd/ticket/2528>`__
    Document that that libkrb5 and sssd use different expansion
    templates for principals
`#2534 </sssd/ticket/2534>`__
    [RFE] Lock out ssh keys when account naturally expires
`#2570 </sssd/ticket/2570>`__
    Document how to handle setups that only wish to include certain
    groups
`#2587 </sssd/ticket/2587>`__
    With empty ipaselinuxusermapdefault security context on client is
    staff\_u
`#2588 </sssd/ticket/2588>`__
    Properly handle AD's binary objectGUID
`#2591 </sssd/ticket/2591>`__
    sssd nss bug update vs create cache
`#2592 </sssd/ticket/2592>`__
    ccname\_file\_dummy is not unlinked on error
`#2598 </sssd/ticket/2598>`__
    sssd\_nss segfaults if initgroups request is by UPN and doesn't find
    anything
`#2601 </sssd/ticket/2601>`__
    SSSD downloads too much information when fetching information about
    groups
`#2604 </sssd/ticket/2604>`__
    sssd\_be segfault on IPA(when auth with AD trusted domain) client at
    src/providers/ipa/ipa\_s2n\_exop.c:1605
`#2606 </sssd/ticket/2606>`__
    GPO access control looks for computer object in user's domain only
`#2608 </sssd/ticket/2608>`__
    sssd crashes intermittently
`#2611 </sssd/ticket/2611>`__
    sssd\_be dumping core if enumeration times out
`#2612 </sssd/ticket/2612>`__
    ldap\_access\_order=ppolicy: Explicitly mention in manpage that
    unsupported time specification will lead to sssd denying access
`#2613 </sssd/ticket/2613>`__
    sysdb sudo search doesn't escape special characters
`#2614 </sssd/ticket/2614>`__
    id lookup resolves "Domain Local" group and errors appear in domain
    log
`#2624 </sssd/ticket/2624>`__
    Only set the selinux context if the context differs from the local
    one
`#2629 </sssd/ticket/2629>`__
    sssd\_be segfault id\_provider = ad src/providers/ad/ad\_gpo.c:843
`#2630 </sssd/ticket/2630>`__
    Overrides with --login work in second attempt
`#2631 </sssd/ticket/2631>`__
    idoverridegroup for ipa group with --group-name does not work
`#2632 </sssd/ticket/2632>`__
    Overridde with --login fails trusted adusers group membership
    resolution
`#2633 </sssd/ticket/2633>`__
    Group resolution is inconsistent with group overrides
`#2634 </sssd/ticket/2634>`__
    sssd nss responder gets wrong number of secondary groups
`#2635 </sssd/ticket/2635>`__
    ID mapping does not wotk with disabled subdomains
`#2642 </sssd/ticket/2642>`__
    Override for IPA users with login does not list user all groups
`#2643 </sssd/ticket/2643>`__
    autofs provider fails when default\_domain\_suffix and
    use\_fully\_qualified\_names set
`#2644 </sssd/ticket/2644>`__
    ignore\_group\_members doesn't work for subdomains
`#2646 </sssd/ticket/2646>`__
    Disapeared groups with ad providers and enabled
    ignore\_group\_members
`#2647 </sssd/ticket/2647>`__
    external users do not resolve with "default\_domain\_suffix" set in
    IPA server sssd.conf
`#2649 </sssd/ticket/2649>`__
    /usr/libexec/sssd/selinux\_child crashes and gets avc denial when
    ssh
`#2650 </sssd/ticket/2650>`__
    Unable to resolve group memberships for AD users when using
    sssd-1.12.2-58.el7\_1.6.x86\_64 client in combination with
    ipa-server-3.0.0-42.el6.x86\_64 with AD Trust
`#2654 </sssd/ticket/2654>`__
    sssd\_be crashed if initialisation of proxy\_child failed
`#2655 </sssd/ticket/2655>`__
    proxy provider does not work in non-root mode
`#2659 </sssd/ticket/2659>`__
    IPA enumeration provider crashes
`#2663 </sssd/ticket/2663>`__
    id lookup for non-root domain users doesn't return all groups on
    first attempt

.. raw:: html

   </div>

Detailed changelog
------------------

Adam Tkac (1):

-  Option filter\_users had no effect for retrieving sudo rules

Aron Parsons (2):

-  IPA: fix segfault in ipa\_s2n\_exop
-  autofs: fix 'Cannot allocate memory' with FQDNs

Daniel Hjorth (1):

-  LDAP: unlink ccname\_file\_dummy if there is an error

Jakub Hrozek (34):

-  Updating the version for the 1.12.5 release
-  resolv: Use the same default timeout for SRV queries as previously
-  FO: Use SRV TTL in fail over code
-  selinux: Delete existing user mapping on empty default
-  NSS: Handle ENOENT when doing initgroups by UPN
-  selinux: Handle setup with empty default and no configured rules
-  tests: convert all unit tests to cmocka 1.0 or later
-  RPM:
   `BuildRequire? <https://docs.pagure.org/sssd-test2/BuildRequire.html>`__!
   libcmocka >= 1.0
-  build: Only run cmocka tests if cmocka 1.0 or newer is available
-  Resolv: re-read SRV query every time if its TTL is 0
-  IPA: Use custom error codes when validating HBAC rules
-  IPA: Drop useless sysdb parameter
-  IPA: Only treat malformed HBAC rules as fatal if deny rules are
   enabled
-  IPA: Deprecate the ipa\_hbac\_treat\_deny\_as option
-  selinux: Disconnect before closing the handle
-  selinux: Begin and end the transaction on the same nesting level
-  selinux: Only call semanage if the context actually changes
-  tests: Use cmocka-1.0+ API in test\_sysdb\_utils
-  sysdb: Add cache\_expire to the default
   sysdb\_search\_object\_by\_str\_attr set
-  SELINUX: Avoid disconnecting disconnected handle
-  LDAP: return after tevent\_req\_error
-  MAN: refresh\_expired\_interval also supports users and groups
-  tests: ncache\_hit must be an int to test UPNs
-  tests: Add a getpwnam-by-UPN test
-  Add unit tests for initgroups
-  Download complete groups if ignore\_group\_members is set with
   tokengroups
-  DP: Set extra\_value to NULL for enum requests
-  Skip enumeration requests in IPA and AD providers as well
-  confdb: Add new option subdomain\_inherit
-  DP: Add a function to inherit DP options, if set
-  SDAP: Add sdap\_copy\_map\_entry
-  UTIL: Inherit ignore\_group\_members
-  subdomains: Inherit cleanup period and tokengroup settings from
   parent domain
-  Updating translations for the 1.12.5 release

Lukas Slebodnik (19):

-  Log reason in debug message why ldb\_modify failed
-  ipa\_selinux: Fix warning may be used uninitialized
-  memberof: Do not create request with 0 attribute values
-  CLIENT: Clear errno with enabled sss-default-nss-plugin
-  GPO: Check return value of ad\_gpo\_store\_policy\_settings
-  SDAP: Do not set gid 0 twice
-  SDAP: Extract filtering AD group to function
-  SDAP: Filter ad groups in initgroups
-  GPO: Do not ignore missing attrs for GPOs
-  sss\_nss\_idmap-tests: Use different prepared buffers for big endian
-  SDAP: Fix id mapping with disabled subdomains
-  SPEC: Fix cyclic dependencies between sssd-{krb5,}-common
-  negcache: Soften condition for expired entries
-  test\_nss\_srv: Use right function for storing time\_t
-  nss: Do not ignore default vaue of SYSDB\_INITGR\_EXPIRE
-  SDAP: Set initgroups expire attribute at the end
-  SDAP: Remove unnecessary argument from sdap\_save\_user
-  PROXY: proxy\_child should work in non-root mode
-  PROXY: Do not register signal with SA\_SIGINFO

Michal Zidek (2):

-  DEBUG: Add missing strings for error messages
-  test: Check ERR\_LAST

Pavel Březina (8):

-  be\_refresh: refresh all domains in backend
-  sdap\_handle\_acct\_req\_send: remove be\_req
-  be\_refresh: refactor netgroups refresh
-  be\_refresh: add sdap\_refresh\_init
-  be\_refresh: support users
-  be\_refresh: support groups
-  enumeration: fix talloc context
-  sudo: sanitize filter values

Pavel Reichl (18):

-  PAM: do not reject abruptly
-  PAM: new option pam\_account\_expired\_message
-  PAM: warn all services about account expiration
-  PAM: check return value of confdb\_get\_string
-  SDAP: refactor pwexpire policy
-  SDAP: enable change phase of pw expire policy check
-  UTIL: convert
   `GeneralizedTime? <https://docs.pagure.org/sssd-test2/GeneralizedTime.html>`__!
   to unix time
-  SDAP: Lock out ssh keys when account naturally expires
-  SDAP: fix minor neglect in is\_account\_locked()
-  ldap\_child: fix coverity warning
-  MAN: libkrb5 and SSSD use different expansions
-  IPA: set EINVAL if dn can't be linearized
-  LDAP: remove unused code
-  LDAP: fix a typo in debug message
-  MAN: Update ppolicy description
-  simple-access-provider: make user grp res more robust
-  LDAP: warn about lockout option being deprecated
-  krb5: new option krb5\_map\_user

Stephen Gallagher (3):

-  AD: Clean up ad\_access\_gpo
-  AD: Always get domain-specific ID connection
-  AD GPO: Always look up GPOs from machine domain

Sumit Bose (25):

-  ldap\_child: initialized ccname\_file\_dummy
-  PAM: use the logon\_name as the key for the PAM initgr cache
-  pam\_initgr\_check\_timeout: add debug output
-  ipa: do not treat missing sub-domain users as error
-  ipa: make sure extdom expo data is available
-  LDAP/AD: do not resolve group members during tokenGroups request
-  IPA idviews: check if view name is set
-  IPA: make sure output variable is set
-  GPO: error out instead of leaving array element uninitialized
-  sdap: properly handle binary objectGuid attribute
-  IPA: do not try to save override data for the default view
-  IPA: use sysdb\_attrs\_add\_string\_safe to add group member
-  IPA: check ghosts in groups found by uuid as well
-  IPA: allow initgroups by SID for AD users
-  IPA: do initgroups if extdom exop supports it
-  IPA: update initgr expire timestamp conditionally
-  IPA: enhance ipa\_initgr\_get\_overrides\_send()
-  IPA: search for overrides during initgroups in sever mode
-  IPA: do not add domain name unconditionally
-  NSS: check for overrides before calling backend
-  IPA: allow initgroups by UUID for FreeIPA users
-  SDAP: use DN to update entry
-  IPA: do not fail if view name lookup failed on older versions
-  libwbclient-sssd: update interface to version 0.12
-  ldap: use proper sysdb name in groups\_by\_user\_done()
