.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Tickets Fixed <#TicketsFixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

-  Add a new AD provider to improve integration with Active Directory
   2008 R2 or later servers
-  SUDO integration was completely rewritten. The new implementation
   works with multiple domains and uses an improved refresh mechanism to
   download only the necessary rules
-  The IPA authentication provider now supports subdomains
-  Fixed regression for setups that were setting default\_tkt\_enctypes
   manually by reverting a previous workaround.

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1239 </sssd/ticket/1239>`__
    [RFE] sudo: send username and uid while requesting default options
`#1299 </sssd/ticket/1299>`__
    Per domain formats for qualified user names
`#1352 </sssd/ticket/1352>`__
    [RFE] Add the subdomain functionality to IPA auth provider
`#1377 </sssd/ticket/1377>`__
    [RFE] Add AD provider
`#1382 </sssd/ticket/1382>`__
    pac responder interface needs checks
`#1385 </sssd/ticket/1385>`__
    heimdal: compile time diference
`#1398 </sssd/ticket/1398>`__
    Dependency issue while "yum update libsss\_sudo"
`#1403 </sssd/ticket/1403>`__
    Combine keytab options for AD provider
`#1404 </sssd/ticket/1404>`__
    AD provider should default to case-insensitive operation
`#1407 </sssd/ticket/1407>`__
    Revert sssd patch for limiting enctypes to keytab
`#1409 </sssd/ticket/1409>`__
    Resource leak in sssdpac\_import\_authdata
`#1410 </sssd/ticket/1410>`__
    Dead code in ipa\_subdomains\_handler\_done()
`#1412 </sssd/ticket/1412>`__
    Starting SSSD with a domain using the LOCAL provider segfaults the
    responders

.. raw:: html

   </div>

Detailed Changelog
------------------

George McCollister (1):

-  libcrypto fully implemented

Jakub Hrozek (3):

-  Print based on pointer contents not address
-  Cast uid\_t to unsigned long long in DEBUG messages
-  Update translations for 1.9.0 beta 4 release

Pavel Březina (53):

-  sudo api: remove EOK
-  sudo responder: remove code duplication in commands
-  sudo responder: get rid of dctx where possible
-  sudo sysdb: make sysdb\_get\_sudo\_user\_info more configurable
-  sudo api: send uid, username and domainname
-  sudo responder: change protocol version to 1
-  libsss\_sudo: bump version to 2:0:1
-  sudo responder: discard in-memory cache
-  sudo ldap provider: move async routines to sdap\_async\_sudo.c
-  sudo ldap provider: give sdap\_sudo\_refresh\_send() search and purge
   filters
-  confdb: add entry\_cache\_sudo\_timeout option
-  sudo ldap provider: add sysdb ctx in sdap\_sudo\_refresh\_state
-  sudo ldap provider: add domain info in sdap\_sudo\_refresh\_state
-  sudo ldap provider: add expiration time to each rule
-  sysdb: add getter/setter for last sudo full refresh time
-  sudo ldap provider: provide API for full refresh
-  sudo ldap provider: add support for on demand full refresh
-  sudo ldap provider: provide API for refresh of specific rules
-  sudo ldap provider: add support for on demand refresh of specific
   rules
-  sudo backend - support only on demand full refresh
-  sudo backend - add support for on demand refresh of specific rules
-  sudo provider: add ldap\_sudo\_full\_refresh\_interval
-  sudo provider: remove old timer
-  sudo ldap provider: add new timer API
-  sysdb: remove sudo\_set/get\_refreshed
-  sudo ldap provider: support periodical full refresh
-  ldap provider: add sudo usn value
-  sudo ldap provider: find highest USN
-  sudo ldap provider: add sdap\_sudo\_set\_usn()
-  sudo ldap provider: remember highest usn after full refresh
-  sudo ldap provider: add smart refresh API
-  sudo ldap provider: when sysdb filter is NULL remove downloaded rules
-  sudo provider: add ldap\_sudo\_smart\_refresh\_interval
-  sudo ldap provider: add periodical smart refresh API
-  sudo ldap provider: support periodical smart refresh
-  sudo responder: new request enum type
-  sudo sysdb: add expiration time to the filter
-  sudo responder: allow fetching only expired rules in
   sudosrv\_get\_sudorules\_query\_cache()
-  sudo responder: update dp interface
-  sudo responder: refresh expired rules
-  sudo ldap provider: return number of downloaded rules in
   sdap\_sudo\_refresh\_recv()
-  sudo ldap provider: notify responder when an expired rule has been
   deleted
-  sudo responder: schedule OOB full refresh when expired rule is
   deleted
-  sudo: clean up
-  sudo ldap provider: modify highest USN in
   sdap\_sudo\_rules\_refresh\_done()
-  sdap\_sudo.c: move \_recv after \_done
-  sudo ldap provider: pass sudo\_ctx instead of id\_ctx
-  sudo: add host info options
-  sudo ldap provider: load host filter configuration on init
-  sudo ldap provider: mark sdap\_sudo\_setup\_periodical\_refresh() as
   static
-  sudo ldap provider: do per-host updates
-  sudo ldap provider: support autoconfiguration of IP addresses
-  sudo: manpage updated

Rambaldi (2):

-  heimdal: fix compile error in krb5-child-test
-  heimdal: use sss\_krb5\_princ\_realm to access realm

Simo Sorce (1):

-  Fix segfault when sudo is not configured.

Stef Walter (2):

-  Fix crash when interface doesn't have an address
-  Revert commit
   `4c157ecedd52602f75574605ef48d0c48e9bfbe8 <https://fedorahosted.org/sssd/changeset/4c157ecedd52602f75574605ef48d0c48e9bfbe8/>`__

Stephen Gallagher (33):

-  Bumping version to 1.9.0 beta 4
-  TESTS: Print messages when LDAP options do not match
-  DEBUG: Log to syslog if we are unable to open a debug fd
-  KRB5: Initialize the credential cache type properly
-  IPA: Don't hang onto memory longer than necessary
-  LDAP: Print extended failure message for SASL bind
-  MAN: Unify "SEE ALSO" sections
-  KRB5: Some logging enhancements for krb5\_child
-  KRB5\_LOCATOR: Print the filename that couldn't be opened
-  KRB5: Drop memctx parameter of krb5\_try\_kdcip
-  KRB5: Create a common init routine for krb5\_child options
-  LDAP: Rename user and group maps for AD
-  AD: Add AD identity provider
-  AD: Add AD auth and chpass providers
-  AD: Add AD access-control provider
-  AD: Add AD provider to the spec file
-  AD: use krb5\_keytab for validation and GSSAPI
-  AD: Add manpages and SSSDConfig entries
-  CONFDB: Add the ability to set a boolean value in the confdb
-  AD: Force case-insensitive operation in AD provider
-  Fix use-after-free
-  Fix uninitialized variable
-  Fix potential NULL-dereference
-  Fix potential NULL-dereference
-  Fix incorrect return value in tests
-  Fix potential NULL-dereference
-  Fix uninitialized value return
-  Fix uninitialized memcpy error
-  Avoid NULL-dereference in error-handling
-  Add missing return value check
-  Check for errors from krb5\_unparse\_name
-  Fix incorrect error-check
-  Fix segfault when using local provider

Sumit Bose (5):

-  Fix SSSDConfigTest for separate build directories
-  Set file descriptor limits in pac responder
-  Remove resource leak in sssdpac\_import\_authdata
-  Remove dead code in ipa\_subdomains\_handler\_done()
-  pac responder: limit access by checking UIDs
