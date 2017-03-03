Highlights
----------

-  This release mostly focuses on bug fixes, especially in the AD
   provider
-  The AD provider is able to resolve group memberships for groups with
   Global and Universal scope
-  The initgroups (get groups for user) operation for users from trusted
   AD domains was made more reliable by reading the required tokenGroups
   attribute from LDAP instead of Global Catalog
-  A new option ``ad_enable_gc`` was added to the AD provider. This
   option allows the administrator to force SSSD to talk to LDAP port
   only and never try the Global Catalog
-  The AD provider is now able to leverage the tokenGroups attribute
   even when POSIX attributes are used, providing better performance
   during logins.
-  A memory leak in the NSS responder that affected long-lived clients
   that requested netgroup data was fixed

Documentation Changes
---------------------

-  A new option ``ldap_group_type`` was added to LDAP, IPA and AD
   providers
-  A new option ``ad_enable_gc`` was added to the AD provider

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1568 </sssd/ticket/1568>`__
    [RFE] AD Provider should use tokenGroups with non-ID-mapping
`#2077 </sssd/ticket/2077>`__
    [RFE] If originalDN is not available during LDAP auth, the SSSD
    should look it up
`#2132 </sssd/ticket/2132>`__
    Improve detection of the right domain when processing group with
    members from several domains
`#2133 </sssd/ticket/2133>`__
    sss\_idmap: add API to free objects allocated by the library
`#2137 </sssd/ticket/2137>`__
    SSSD fails to fetch netgroup information with setnetgrent failed
    error
`#2138 </sssd/ticket/2138>`__
    Valgrind sssd "Syscall param socketcall.sendto(msg) points to
    uninitialised byte(s)"
`#2145 </sssd/ticket/2145>`__
    Push patch to bump version-info of libsss\_idmap
`#2146 </sssd/ticket/2146>`__
    sssd can't retrieve auto.master when using the
    "default\_domain\_suffix" option in
`#2147 </sssd/ticket/2147>`__
    sssd\_be crashes on manually adding a cleartext password to
    ldap\_default\_authtok
`#2148 </sssd/ticket/2148>`__
    Individual group search returned multiple results in GC lookups
`#2154 </sssd/ticket/2154>`__
    Incorrect mention of access\_filter in sssd-ad manpage
`#2156 </sssd/ticket/2156>`__
    Non descriptive error message when sssd.conf is missing completely
`#2157 </sssd/ticket/2157>`__
    sssd\_be segfaults if empty grop is resolved using
    ad\_matching\_rule
`#2161 </sssd/ticket/2161>`__
    tokenGroups do not work reliable with Global Catalog
`#2165 </sssd/ticket/2165>`__
    Update Gentoo init script
`#2168 </sssd/ticket/2168>`__
    If SSSD starts offline, subdomains list is never read.
`#2170 </sssd/ticket/2170>`__
    sssd\_nss grows memory footprint when netgroups are requested
`#2173 </sssd/ticket/2173>`__
    sssd\_be crashes occasionally
`#2178 </sssd/ticket/2178>`__
    AD groups with domain-local scope should be filtered out for trusted
    domains

.. raw:: html

   </div>

Detailed Changelog
------------------

Aron Parsons (1):

-  do not use default\_domain\_suffix with autofs

Jakub Hrozek (14):

-  Updating the version for the 1.11.3 release
-  Initialize sid\_str to NULL to avoid freeing random data
-  LDAP: Split out a request to search for a user w/o saving
-  LDAP: Search for original DN during auth if it's missing
-  AD: Fix a typo in the man page
-  LDAP: Initialize user count for AD matching rule
-  SUBDOMAINS: Reuse cached results if DP is offline
-  AD: Refresh subdomain data structures on startup
-  IPA: Refresh subdomain data structures on startup
-  IPA: Call ipa\_ad\_subdom\_refresh when server mode is initialized
-  AD: Add a utility function to create list of connections
-  AD: Add a new option to turn off GC lookups
-  AD: Enable fallback to LDAP of trusted domain
-  Updating translations for the 1.11.3 release

Jan Engelhardt (1):

-  build: fix ordering of linker flags

Lukas Slebodnik (7):

-  NSS: Set packet length for initgroups
-  LDAP: Prevent from using uninitialized sdap\_options
-  SYSDB: Skip malformed netgroup attribute.
-  SYSDB: Sanitize filter before sysdb\_search\_groups
-  SYSDB: Sanitize filter before removing ghost attrs
-  NSS: Fix memory leak in sss\_setnetgrent
-  AUTOTOOLS: krb5 1.12 is also supported krb5 libs

Markos Chandras (2):

-  sysv/gentoo: Use xdm if possible
-  sysv/gentoo: Send debug output to a file instead of stderr

Pavel Březina (11):

-  idmap: add API to free allocated SIDs
-  free idmapped SIDs correctly
-  free idmapped dom SIDs correctly
-  free idmapped smb SIDs correctly
-  free idmapped binary SIDs correctly
-  pac: fix double free
-  pac: fix potential memory leaks
-  failover: check dns\_domain if primary servers lookup failed
-  ad: refactor tokengroups initgroups
-  ad: use tokengroups even when id mapping is disabled
-  Bump sss\_idmap version to 3:0:3

Pavel Reichl (3):

-  monitor: Specific error message for missing sssd.conf
-  SSSD: Improved domain detection
-  SSSD: Unit test - sss\_ldap\_dn\_in\_search\_bases

Sumit Bose (10):

-  AD: use LDAP for group lookups
-  sss\_cache: initialize names member of sss\_domain\_info
-  sss\_cache: fix case-sensitivity issue
-  Add sysdb\_attrs\_add\_lc\_name\_alias
-  Use sysdb\_attrs\_add\_lc\_name\_alias to add case-insensitive alias
-  Use lower-case name for case-insensitive searches
-  Add new option ldap\_group\_type
-  Add sysdb\_attrs\_get\_int32\_t
-  AD: filter domain local groups for trusted/sub domains
-  AD: cross-domain membership fix
