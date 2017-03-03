Highlights
----------

-  A new option ad\_access\_filter was added. This option allows the
   administrator to easily configure LDAP search filter that the users
   logging in must match in order to be granted access
-  Group resolution now supports resolving group members from different
   trusted AD domains in a single forest
-  A bug that prevented a configuration file with trailing spaces to be
   loaded was fixed
-  SSSD no longer crashes if the LDAP connection is terminated while
   LDAP requests are still in progress
-  Several important bugs related to the Global Catalog support were
   fixed:

   -  SSSD now correctly falls back to LDAP lookups in case Global
      Catalog is not reachable
   -  If the AD servers were specified using the ad\_server option and
      not autodiscovered, server fail over did not work correctly with
      1.11.1

Feature removal
---------------

-  The Kerberos provider will no longer try to create public directories
   when evaluating the krb5\_ccachedir option. This is a necessary
   backwards-incompatible change, as SSSD has no way to know when a
   directory should be public and when it shouldn't without additional
   information. Moreover creating public directories is something the
   system administrator should perform, not the authentication daemon.
   The tmpfiles.d(5) facility can be used for that purpose by admins
   that need dynamic creation of public directories at system boot time.

Documentation Changes
---------------------

-  The decimal debug levels are now recommended instead of the advanced
   hexadecimal levels which are more suitable for developers

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1968 </sssd/ticket/1968>`__
    Memory grows if subdomain goes away in the AD provider
`#2030 </sssd/ticket/2030>`__
    getent response requires sssd restart after trust add
`#2064 </sssd/ticket/2064>`__
    ad: unable to resolve membership when user is from different domain
    than group
`#2071 </sssd/ticket/2071>`__
    Ccache directory creation leads to unexpected results
`#2082 </sssd/ticket/2082>`__
    [RFE] Add a new option ad\_access\_filter
`#2092 </sssd/ticket/2092>`__
    Group lookup is not returned immediately after service startup
`#2100 </sssd/ticket/2100>`__
    sudo responder does not support specifying just one of
    sudoNotBefore/sudoNotAfter
`#2101 </sssd/ticket/2101>`__
    Use idrange of forest root if there is none for a member domain and
    type is ipa-ad-trust-posix
`#2104 </sssd/ticket/2104>`__
    AD provider should fall back the LDAP if Global Catalog is not
    reachable
`#2105 </sssd/ticket/2105>`__
    Do not show 'Could not add new domain' error messages if
    ldap\_id\_mapping=false
`#2112 </sssd/ticket/2112>`__
    Coverity reported potential NULL dereference
`#2116 </sssd/ticket/2116>`__
    SID looksups are not handled if noexist\_delete flag is set
`#2121 </sssd/ticket/2121>`__
    ipa ad trusted user lookups failed with sssd\_be crash
`#2123 </sssd/ticket/2123>`__
    Creating system accounts on a IdM client takes up to 10 minutes when
    AD trust is configured in the IdM.
`#2124 </sssd/ticket/2124>`__
    sssd\_nss exited abnormally and generated core files.
`#2126 </sssd/ticket/2126>`__
    sssd\_be segfault when authenticating against active directory
`#2131 </sssd/ticket/2131>`__
    NSS responder doesn't qualify memberuid and ghost users of groups
    that contain members from different domains

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (23):

-  Updating the version for the 1.11.2 release
-  krb5: Fix unit tests
-  INI: Disable line-wrapping functionality
-  KRB5: Return PAM\_ACCT\_EXPIRED when logging in as expired AD user
-  PROXY: Fix memory hierarchy when enumerating services
-  Inherit ID limits of parent domains if set
-  SYSDB: Add sysdb\_delete\_by\_sid
-  LDAP: Delete entry by SID if not found
-  LDAP: Amend sdap\_access\_check to allow any connection
-  LDAP: Parse FQDN into name/domain for subdomain users
-  AD: Add a new option ad\_access\_filter
-  AD: Use the ad\_access\_filter if it's set
-  AD: Search GC by default during access control, fall back to LDAP
-  AD: Add extended access filter
-  TEST: Test getgrnam with emphasis on members
-  NSS: Print FQDN for groups with mixed domain membership
-  KRB5: Handle ERR\_CHPASS\_FAILED
-  NSS: Fix service enumeration
-  MAN: Document that krb5 directories can only be created as private
-  LDAP: Check all search bases during nested group processing
-  NSS: Fix parenthesis
-  AD: Fix ad\_access\_filter parsing with empty filter
-  Updating translation for the 1.11.2 release

Lukas Slebodnik (9):

-  LDAP: Set default value for dyndns update to false
-  krb5: Remove warning dereference of a null pointer
-  krb5: Use right function to free data.
-  AD: Prefer GC port from SRV record
-  AD: fall back to LDAP if GC is not available.
-  tests: Use right format string for type size\_t
-  Makefile: Add missing libraries
-  Makefile: Remove unused variable TEST\_MOCK\_OBJ
-  LDAP: Return correct error code

Pavel Březina (23):

-  sudo: allow specifying only one time restriction
-  sudo: improve time restrictions debug messages
-  nss: wait for initial subdomains request to finish
-  subdomains: first destroy ptask then remove sdom
-  dp: make subdomains refresh interval configurable
-  dp: store list of ongoing requests
-  utils: add ERR\_DOMAIN\_NOT\_FOUND error code
-  dp: set request domain
-  dp: add function to terminate request of specific domain
-  dp: free sdap domain if subdomain is removed
-  be\_ptask: add be\_ptask\_create\_sync()
-  dp: convert cleanup task to be\_ptask
-  ipa: destroy cleanup task when subdomain is removed
-  ad: destroy ptasks when subdomain is removed
-  sdap\_save\_user: try to determine domain by SID
-  sdap\_save\_group: try to determine domain by SID
-  free sid obtained from sss\_idmap\_unix\_to\_sid()
-  ad: shortcut if possible during get object by ID or SID
-  sdap: store base dn in sdap\_domain
-  sdap: add sdap\_domain\_get\_by\_dn()
-  ghosts: pick correct domain for every member
-  sdap\_fill\_memberships: pick correct domain for every member
-  nested groups: pick correct domain for cache lookups

Simo Sorce (1):

-  krb5: Remove ability to create public directories

Stephen Gallagher (4):

-  SYSDB: Fix incorrect DEBUG message
-  MAN: Clarify debug level documentation
-  MAN: Reflow debug\_levels.xml
-  BUILD: Update bashrc macros

Sumit Bose (17):

-  AD: properly intitialize GC from ad\_server option
-  LDAP: handle SID requests if noexist\_delete is set
-  IPA server mode: properly initialize ext\_groups
-  idmap: add internal function to free a domain struct
-  idmap: fix a memory leak if a collision is detected
-  idmap: allow ranges with external mapping to overlap
-  sdap\_idmap: add sdap\_idmap\_get\_configured\_external\_range()
-  sdap\_idmap: properly handle ranges for external mappings
-  Add unconditional online callbacks
-  IPA: add callback to reset subdomain timeouts
-  sdap\_get\_generic\_ext\_send: check if we a re still connected
-  find\_subdomain\_by\_sid: skip domains with missing domain\_id
-  idmap: add sss\_idmap\_domain\_by\_name\_has\_algorithmic\_mapping()
-  sdap\_idmap\_domain\_has\_algorithmic\_mapping: add domain name
   argument
-  IPA: add trusted domains with missing idrange
-  ad\_subdom\_store: check ID mapping of the domain not of the parent
-  be\_spy\_create: free be\_req and not the long living data
