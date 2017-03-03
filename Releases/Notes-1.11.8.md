Highlights {#Highlights}
----------

-   This release focuses on backporting bug fixes from the 1.12 and 1.13
    releases. At the moment, the SSSD upstream does not plan on
    releasing 1.11.9, barring security issues or regressions in this
    release. We recommend that all users of 1.11 upgrade to 1.12 or
    1.13.
-   Several bugs related to using `id_provider=ldap` together with ID
    mapping enabled were fixed
-   Fixed a potential use-after-free error in the nested groups
    resolution code
-   The service restart code in the main "sssd" process was improved
-   The PAC responder can be built with MIT Kerberos versions 1.13 and
    1.14
-   A potential segfault in the memberof ldb plugin was fixed
-   The LDAP child no longer leaves a stray temporary file behind in
    case acquiring the credentials fails
-   The sudo responder works correctly even for users or groups whose
    name contains an LDAP special character such as `)`
-   The `autofs` responder now works even with setups that enable the
    `default_domain_suffix` option
-   A memory leak in the NSS responder when a non-existing netgroup was
    requested is fixed in this release
-   The SSSD no longer leaks a file descriptor if service discovery
    times out when discovering an LDAP server
-   The sudo responder fixed the logic to sort entries with the
    sudoOrder attribute to match the sudo's native LDAP code

Documentation Changes {#DocumentationChanges}
---------------------

-   The `ldap_use_tokengroups` option defaults to `false` in the generic
    LDAP provider. Previously, both the AD and LDAP provider (with
    `ldap_schema` set to `ad`) attempted to use the `tokenGroups`,
    resulting in numerous bugs.

Tickets Fixed {#TicketsFixed}
-------------

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2412](https://fedorahosted.org/sssd/ticket/2412){.ext-link} -
    Error processing universal groups with cross-domain membership in
    SSSD server mode
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2471](https://fedorahosted.org/sssd/ticket/2471){.ext-link} -
    RHEL6.6 sssd (1.11) fails if IPA permissions and roles have the same
    name
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2484](https://fedorahosted.org/sssd/ticket/2484){.ext-link} -
    Password change over ssh doesn't work with OTP and FreeIPA
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2448](https://fedorahosted.org/sssd/ticket/2448){.ext-link} -
    MAN: If ldap\_group\_base is set, tokengroups might not be able to
    convert all GIDs to names
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2445](https://fedorahosted.org/sssd/ticket/2445){.ext-link} -
    Race condition while invalidating memory cache in client code
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2492](https://fedorahosted.org/sssd/ticket/2492){.ext-link} -
    Group membership gets lost in IPA server mode
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2573](https://fedorahosted.org/sssd/ticket/2573){.ext-link} -
    Use after free in proxy provider.
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2611](https://fedorahosted.org/sssd/ticket/2611){.ext-link} -
    sssd\_be dumping core if enumeration times out
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2525](https://fedorahosted.org/sssd/ticket/2525){.ext-link} -
    Monitor SIGKILL timer issue and service restart failure
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2572](https://fedorahosted.org/sssd/ticket/2572){.ext-link} -
    \[abrt\] sssd-common: talloc\_abort(): sssd killed by SIGABRT
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2430](https://fedorahosted.org/sssd/ticket/2430){.ext-link} -
    sssd segfaults repeatedly with error 4 in memberof.so
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1096](https://fedorahosted.org/sssd/ticket/1096){.ext-link} -
    Clock skew in krb5 auth should result in offline operation, not
    failure
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2592](https://fedorahosted.org/sssd/ticket/2592){.ext-link} -
    ccname\_file\_dummy is not unlinked on error
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2613](https://fedorahosted.org/sssd/ticket/2613){.ext-link} -
    sysdb sudo search doesn't escape special characters
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2625](https://fedorahosted.org/sssd/ticket/2625){.ext-link} -
    Sudo responder does not respect filter\_users and filter\_groups
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2643](https://fedorahosted.org/sssd/ticket/2643){.ext-link} -
    autofs provider fails when default\_domain\_suffix and
    use\_fully\_qualified\_names set
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2634](https://fedorahosted.org/sssd/ticket/2634){.ext-link} -
    sssd nss responder gets wrong number of secondary groups
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2644](https://fedorahosted.org/sssd/ticket/2644){.ext-link} -
    ignore\_group\_members doesn't work for subdomains
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2659](https://fedorahosted.org/sssd/ticket/2659){.ext-link} -
    IPA enumeration provider crashes
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2663](https://fedorahosted.org/sssd/ticket/2663){.ext-link} -
    id lookup for non-root domain users doesn't return all groups on
    first attempt
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2681](https://fedorahosted.org/sssd/ticket/2681){.ext-link} -
    SSSD cache is not updated after user is deleted from ldap server
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2744](https://fedorahosted.org/sssd/ticket/2744){.ext-link} -
    cleanup\_groups should sanitize dn of groups
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2800](https://fedorahosted.org/sssd/ticket/2800){.ext-link} -
    Relax POSIX check
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2803](https://fedorahosted.org/sssd/ticket/2803){.ext-link} -
    Memory leak / possible DoS with krb auth.
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2792](https://fedorahosted.org/sssd/ticket/2792){.ext-link} -
    SSSD is not closing sockets properly
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2888](https://fedorahosted.org/sssd/ticket/2888){.ext-link} -
    SRV lookups with id\_provider=proxy and auth\_provider=krb5
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2865](https://fedorahosted.org/sssd/ticket/2865){.ext-link} -
    sssd\_nss memory usage keeps growing on sssd-1.12.4-47.el6.x86\_64
    (RHEL6.7) when trying to retrieve non-existing netgroups
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2682](https://fedorahosted.org/sssd/ticket/2682){.ext-link} -
    sudoOrder not honored as expected

Detailed Changelog {#DetailedChangelog}
------------------

Adam Tkac (1):

-   Option filter\_users had no effect for retrieving sudo rules

Aron Parsons (1):

-   autofs: fix 'Cannot allocate memory' with FQDNs

Dan Lavu (1):

-   MAN: page edit for ldap\_use\_tokengroups

Daniel Hjorth (1):

-   LDAP: unlink ccname\_file\_dummy if there is an error

Jakub Hrozek (8):

-   Updating the version for the 1.11.8 development
-   IPA: Use GC for group lookups in server mode
-   LDAP: Do not clobber return value when multiple controls are
    returned
-   PAC: krb5\_pac\_verify failures should not be fatal
-   LDAP: return after tevent\_req\_error
-   KRB5: Go offline in case of clock skew
-   Download complete groups if ignore\_group\_members is set with
    tokengroups
-   DP: Set extra\_value to NULL for enum requests

Jan Engelhardt (1):

-   build: call AC\_BUILD\_AUX\_DIR before anything else

Lukas Slebodnik (16):

-   Revert "LDAP: Change defaults for ldap\_user/group\_objectsid"
-   LDAP: Disable token groups by default
-   sss\_client: Extract destroying of mmap cache to function
-   sss\_client: Fix race condition in memory cache
-   PROXY: Fix use after free
-   pysss\_nss\_idmap: Use wrapper for older python
-   MONITOR: Fix double free
-   TEST: Test empty results from functions sysdb\_search\_\*
-   SDAP: Do not set gid 0 twice
-   nss: Do not ignore default vaue of SYSDB\_INITGR\_EXPIRE
-   SDAP: Set initgroups expire attribute at the end
-   SDAP: Remove user from cache for missing user in LDAP
-   LDAP: Sanitize group dn before using in filter
-   LDAP: Fix leak of file descriptors
-   BUILD: Accept krb5 1.14 for building the PAC plugin
-   BUILD: Fix linking issues on debian

Michal Zidek (1):

-   LDAP: Change defaults for ldap\_user/group\_objectsid

Nalin Dahyabhai (1):

-   Accept krb5 1.13 for building the PAC plugin

Nikolai Kondrashov (1):

-   build: Don't install ad and ipa man pages unnecessarily

Pavel Březina (4):

-   IPA: use ipaUserGroup object class for groups
-   enumeration: fix talloc context
-   sudo: sanitize filter values
-   sudo: use "higher value wins" when ordering rules

Pavel Reichl (14):

-   LDAP: retain external members
-   SDAP: return after tevent\_req\_error
-   sudo: return after tevent\_req\_error
-   monitor: use-after-free bugfix
-   monitor: monitor\_kill\_service - refactor
-   monitor: memory-leak bug
-   SYSDB: sysdb\_search\_entry fix memory leak
-   SYSDB: sysdb\_search\_custom fix memory leak
-   TESTS: sysdb\_search\_return\_ENOENT - check mem leaks
-   SDAP: Relax POSIX check
-   NSS: sysdb\_getnetgr check return value first
-   NSS: sysdb\_getnetgr refactor
-   NSS: fix memory leak in sysdb\_getnetgr
-   NSS: Fix memory leak netgroup

Petr Cech (1):

-   KRB5: Adding DNS SRV lookup for krb5 provider

Simo Sorce (1):

-   Signals: Remove unused functions

Stephen Gallagher (2):

-   monitor: Service restart fixes
-   UTIL: Do not change SSSD domains in get\_domains\_head

Sumit Bose (2):

-   memberof: check for empty arrays to avoid segfaults
-   ldap: use proper sysdb name in groups\_by\_user\_done()

Thomas Oulevey (1):

-   Fix memory leak in sssdpac\_verify()

