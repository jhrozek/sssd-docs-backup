<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Tickets Fixed](#TicketsFixed)
    3.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   Add support for the Kerberos DIR cache for storing multiple TGTs
    automatically
-   Major performance enhancement when storing large groups in the cache
-   Major performance enhancement when performing initgroups() against
    Active Directory
-   SSSDConfig data file default locations can now be set during
    configure for easier packaging

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#974](/sssd/ticket/974 "[RFE] Support DIR: credential caches for multiple TGT support"){.closed}
:   \[RFE\] Support DIR: credential caches for multiple TGT support

[\#984](/sssd/ticket/984 "RFE: sssd should support Netscape LDAP password expiration controls"){.closed}
:   RFE: sssd should support Netscape LDAP password expiration controls

[\#1213](/sssd/ticket/1213 "Warn to syslog when dereference requests fail"){.closed}
:   Warn to syslog when dereference requests fail

[\#1240](/sssd/ticket/1240 "sudo: contact data provider only once"){.closed}
:   sudo: contact data provider only once

[\#1255](/sssd/ticket/1255 "RFE: change the way we deal with fake users"){.closed}
:   RFE: change the way we deal with fake users

[\#1256](/sssd/ticket/1256 "Document the expectations about ghost users showing in the lookups"){.closed}
:   Document the expectations about ghost users showing in the lookups

[\#1330](/sssd/ticket/1330 "Potential NULL dereference in sss_krb5_read_etypes_for_keytab"){.closed}
:   Potential NULL dereference in sss\_krb5\_read\_etypes\_for\_keytab

[\#1336](/sssd/ticket/1336 "Please only use named parameters in translatable strings"){.closed}
:   Please only use named parameters in translatable strings

[\#1337](/sssd/ticket/1337 "Minor typos in SSSD messages and man pages"){.closed}
:   Minor typos in SSSD messages and man pages

[\#1346](/sssd/ticket/1346 "in-memory cache causes nss to segfault if it cannot be initialized ..."){.closed}
:   in-memory cache causes nss to segfault if it cannot be initialized
    properly

[\#1367](/sssd/ticket/1367 "Optimize AD memberOf lookups with LDAP_MATCHING_RULE_IN_CHAIN"){.closed}
:   Optimize AD memberOf lookups with LDAP\_MATCHING\_RULE\_IN\_CHAIN

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Ariel Barria (3):

-   Potential NULL dereference in proxy provider
-   Warn to syslog when dereference requests fail
-   Clarify how comments work in sssd.conf

Jakub Hrozek (20):

-   NSS: keep a pointer to body after body is reallocated
-   Use sized\_string correctly in FQDN domains
-   Use the sysdb attribute name, not LDAP attribute name
-   LDAP nested groups: Do not process callback with \_post deep in the
    nested structure
-   Send 16bit protocol numbers from the sss\_client
-   Revert the client packet length, too, after reverting the packet
    protocol
-   Fix the default sssd.conf path
-   Fix the 0.11 sysdb upgrade
-   sss\_names\_init: Report correct error code if allocation failed
-   Two small krb5\_child fixes
-   Provide more debugging in krb5\_child and ldap\_child
-   Allow redefining the KRB5\_CHILD path
-   Split parse\_krb5\_child\_response so it can be reused
-   Add a krb5\_child test tool
-   Residual util functions
-   Handle trailing slash in the ccname template
-   Add a credential cache back end structure
-   Add support for storing credential caches in the DIR: back end
-   Use Kerberos context in KRB5\_DEBUG
-   Make krb5\_ccname\_template and krb5\_ccachedir configurable

Jan Cholasta (3):

-   SSH: Update sss\_ssh\_knownhostsproxy manual page
-   SSH: Supress error message output in sss\_ssh\_knownhostsproxy
-   SSH: Don't abort connection in sss\_ssh\_knownhostsproxy when DNS
    records are missing

Jan Zeleny (20):

-   Fixed two minor memory leaks
-   Fixed issue in SELinux user maps
-   Ghost members - add the ghost attribute to sysdb
-   Ghost members - support in LDAP provider
-   Ghost members - support in proxy provider
-   Ghost members - modifications in sysdb
-   Ghost members - modifications in memberof plugin
-   Ghost members - sysdb upgrade routine
-   Ghost members - NSS responder changes
-   Ghost members - removed sdap\_check\_aliases()
-   Ghost members - modified sss\_groupshow
-   Ghost members - various small changes
-   Add support for filtering atributes
-   Utilize attribute exclusion in LDAP initgroups
-   Fixed setting of debug level in test suite
-   IPA subdomains - ask for information about master domain
-   Allow fast memcache timeout to be configurable
-   Fix an issue in ghost users
-   Provide "service filter" for SELinux context
-   Fixed debug message in sdap\_save\_group()

Joshua Roys (1):

-   Simple implementation of Netscape password warning expiration
    control

Nick Guay (1):

-   added DEBUG messages to krb5\_child and ldap\_child

Stef Walter (1):

-   Make re\_expression and full\_name\_format per domain options

Stephen Gallagher (27):

-   Bumping version ton 1.8.92 for beta 2 development
-   RPM: Allow running 'make rpms' on RHEL 5 machines
-   NSS: Expire in-memory netgroup cache before the nowait timeout
-   Always use positional arguments in translatable strings
-   KRB5: Avoid NULL-dereference with empty keytab
-   Update translation sources
-   NSS: Fix segfault when mmap cache cannot be initialized
-   NSS: Restore original protocol for getservbyport
-   SSSDConfig: Make SSSDConfig a package
-   SSSDConfig: Make default config and schema file locations
    configurable
-   PAM: Better pam\_reply message
-   SYSDB: Reduce noise level of debug messages in lookups
-   LDAP: Remove redundant check
-   LDAP: Fix incorrect switch statement in sdap\_get\_initgr\_done()
-   LDAP: Add helper function to get list of a user's groups from sysdb
-   LDAP: Make sdap\_initgr\_common\_store() non-static
-   LDAP: Add ldap\_\*\_use\_matching\_rule\_in\_chain options
-   LDAP: Add support for AD chain matching extension in group lookups
-   LDAP: Add support for AD chain matching extension in initgroups
-   LDAP: Auto-detect support for the ldap match rule
-   LDAP: Fix missing variable in debug message
-   SSS\_CLIENT: Fix uninitialized value error
-   Fix compilation on older little-endian systems
-   KRB5: Update DEBUG macros for create\_ccache\_dir and
    find\_ccdir\_parent\_data
-   KRB5: Auto-detect DIR cache support in configure
-   KRB5: Avoid shadowing dirname
-   Updating translations for 1.9.0 beta 2 release

Sumit Bose (4):

-   Rename struct dom\_sid to struct sss\_dom\_sid
-   Fix libsss\_hbac library version
-   sss\_idmap: add support for samba struct dom\_sid
-   sss\_idmap: fix typo which prevents sub auth larger then 2^31^

Yuri Chornoivan (1):

-   Fix typos in message and man pages.

