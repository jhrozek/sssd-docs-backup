Highlights {#Highlights}
----------

-   This release focuses primarily on bug fixes, especially for use
    cases where SSSD is acting as an Active Directory client
-   The simple access provider supports specifying users and groups
    using their NetBIOS domain name (such as `DOMAIN\username`)
-   Support for enumerating users and groups from trusted AD domains was
    added to the AD provider
-   The Active Directory site discovery was made more robust for
    configurations which use multiple trusted domains
-   Several bugs in the LDAP provider that affected setups which mapped
    Windows SIDs to POSIX IDs were fixed
-   The SSSD is now able to use One Time Password (OTP) authentication
    configured on an IPA server. Please note that this functionality is
    not present in the released FreeIPA versions yet

Documentation Changes {#DocumentationChanges}
---------------------

-   The `krb5_use_fast` option changes its default from `never` to `try`
    in the IPA provider. The config option value did not change in the
    other providers.

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#2142](/sssd/ticket/2142 "AD Enumeration reads data from LDAP while regular lookups connect to GC"){.closed}
:   AD Enumeration reads data from LDAP while regular lookups connect to
    GC

[\#2152](/sssd/ticket/2152 "Implement heuristics to detect if POSIX attributes have been replicated to ..."){.closed}
:   Implement heuristics to detect if POSIX attributes have been
    replicated to the Global Catalog or not

[\#2160](/sssd/ticket/2160 "sssd_be crashes when ad_access_filter uses FOREST keyword."){.closed}
:   sssd\_be crashes when ad\_access\_filter uses FOREST keyword.

[\#2164](/sssd/ticket/2164 ""System Error" when invalid ad_access_filter is used"){.closed}
:   "System Error" when invalid ad\_access\_filter is used

[\#2169](/sssd/ticket/2169 "RHEL7 sssd not setting IPA AD trusted user homedir"){.closed}
:   RHEL7 sssd not setting IPA AD trusted user homedir

[\#2172](/sssd/ticket/2172 "Enabling ldap_id_mapping doesn't exclude uidNumber in filter"){.closed}
:   Enabling ldap\_id\_mapping doesn't exclude uidNumber in filter

[\#2186](/sssd/ticket/2186 "FAST does not work in SSSD 1.11.2 in Fedora 20"){.closed}
:   FAST does not work in SSSD 1.11.2 in Fedora 20

[\#2189](/sssd/ticket/2189 "Access denied for users from gc domain when using format DOMAIN\user"){.closed}
:   Access denied for users from gc domain when using format
    DOMAIN\\user

[\#2190](/sssd/ticket/2190 "Group membership lookup issue"){.closed}
:   Group membership lookup issue

[\#2191](/sssd/ticket/2191 "Group lookup does not return member with multiple names after user lookup"){.closed}
:   Group lookup does not return member with multiple names after user
    lookup

[\#2196](/sssd/ticket/2196 "sssd ad trusted sub domain do not inherit fallbacks and overrides settings"){.closed}
:   sssd ad trusted sub domain do not inherit fallbacks and overrides
    settings

[\#2199](/sssd/ticket/2199 "sssd_be crashes when ldap_search_base cannot be parsed."){.closed}
:   sssd\_be crashes when ldap\_search\_base cannot be parsed.

[\#2200](/sssd/ticket/2200 "sssd_be aborts a request if it doesn't match any configured idmap domain"){.closed}
:   sssd\_be aborts a request if it doesn't match any configured idmap
    domain

[\#2202](/sssd/ticket/2202 "sssd_be should hint about increasing the krb5_auth_timeout if krb5 auth ..."){.closed}
:   sssd\_be should hint about increasing the krb5\_auth\_timeout if
    krb5 auth times out

[\#2208](/sssd/ticket/2208 "Warn with a user-friendly error message when permissions on sssd.conf are ..."){.closed}
:   Warn with a user-friendly error message when permissions on
    sssd.conf are incorrect

[\#2213](/sssd/ticket/2213 "sudo rules time filter is nondeterministic"){.closed}
:   sudo rules time filter is nondeterministic

[\#2215](/sssd/ticket/2215 "Man page states default_shell option supersedes other shell options but in ..."){.closed}
:   Man page states default\_shell option supersedes other shell options
    but in fact override\_shell does.

[\#2237](/sssd/ticket/2237 "SSSD needs to enable FAST by default"){.closed}
:   SSSD needs to enable FAST by default

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Alexander Bokovoy (1):

-   FAST: when parsing krb5\_child response, make sure to not miss OTP
    message if it was last one

Benjamin Franzke (1):

-   dlopen-tests: Check the result of asprintf

Jakub Hrozek (27):

-   Updating the version for the 1.11.4 release
-   LDAP: Fix typo and use the right attribute map
-   LDAP: Add a new error code for malformed access control filter
-   tests: Remove tests that check creating public directories
-   UTIL: Inherit parent domain's default\_shell
-   NSS: Use plain user name when expanding homedir
-   AD: Don't fail the request if ad\_account\_can\_shortcut fails
-   MAN: Fix a typo
-   LDAP: Fix error check
-   LDAP: Don't abort request if no id mapping domain matches
-   AD: Don't mark domain as enumerated twice
-   AD: Store info on whether a subdomain is set to enumerate
-   LDAP: Pass a private context to enumeration ptask instead of
    hardcoded connection
-   LDAP: Add enum request with custom connection
-   AD: Enumerate users from GC, other entities from LDAP
-   LDAP: Don't clobber original\_member during enumeration
-   DB: Add sss\_ldb\_el\_to\_string\_list
-   AD: Establish cross-domain memberships after enumeration finishes
-   MAN: clarify which shell option takes precedence
-   LDAP: Detect the presence of POSIX attributes
-   AD: Only download domains that are set to enumerate
-   AD: Remove dead code
-   LDAP: Handle errors from sdap\_id\_op properly in enum code
-   SSS\_CACHE: Reset the initgroups attribute when resetting users
-   IPA: Default to krb5\_use\_fast=try
-   MAN: Clarify the new krb5\_use\_fast IPA default
-   Updating translations for the 1.11.4 release

Lukas Slebodnik (7):

-   AD: Return right error code from netlogon\_get\_flat\_name
-   LDAP: Don't fail if subdomain cannot be found by sid
-   LDAP: update id mapping detection for ldap provider
-   sdap\_idamp: Fall back to another method if sid is wrong
-   krb5: fix warning may be used uninitialized
-   LDAP: store group if subdomain cannot be found by sid
-   LDAP: require attribute groupType for AD groups

Pavel Březina (2):

-   sudo: memset tm when converting time attributes
-   IPA: default krb5\_fast\_principal to host/\$client@\$realm

Pavel Reichl (10):

-   responder: Set forest attribute in AD domains
-   simple access: match objects using flat name
-   simple access: refresh master domain info
-   NSS: add support for subdomain\_homedir
-   krb5: hint to increase krb5\_auth\_timeout
-   MONITOR: Incorrect permissions on sssd.conf
-   Revert "NSS: add support for subdomain\_homedir"
-   AD: support for subdomain\_homedir
-   MAN: update of subdomain\_homedir usage
-   utils: handling NULL params in sss\_parse\_name

Sumit Bose (2):

-   IPA: fix for recent AD group membership changes
-   AD SRV: use right domain name for CLDAP ping

