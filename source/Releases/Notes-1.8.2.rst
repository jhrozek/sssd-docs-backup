.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Tickets fixed <#Ticketsfixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

-  Several fixes to case-insensitive domain functions
-  Fix for GSSAPI binds when the keytab contains unrelated principals
-  Fixed several segfaults
-  Workarounds added for LDAP servers with unreadable RootDSE
-  SSH knownhostproxy will no longer enter an infinite loop preventing
   login
-  The provided SYSV init script now starts SSSD earlier at startup and
   stops it later during shutdown
-  Assorted minor fixes for issues discovered by static analysis tools

Tickets fixed
-------------

.. raw:: html

   <div>

`#1237 </sssd/ticket/1237>`__
    only free if sure data has been allocated
`#1245 </sssd/ticket/1245>`__
    "Error looking up public keys" while ssh to replica using IP
    address.
`#1251 </sssd/ticket/1251>`__
    SSSD memory usage continuously growing
`#1253 </sssd/ticket/1253>`__
    Service lookup shows case sensitive names twice with
    case\_sensitive=false
`#1257 </sssd/ticket/1257>`__
    Unable to bind to IPA server when minssf set
`#1259 </sssd/ticket/1259>`__
    Initial service lookups having name with uppercase alphabets doesn't
    work.
`#1260 </sssd/ticket/1260>`__
    RFE: support case-insensitive service lookups by port including
    protocols
`#1268 </sssd/ticket/1268>`__
    sss\_ssh\_knownhostproxy infinite loop hangs SSH login
`#1269 </sssd/ticket/1269>`__
    sssd: Uses the wrong key for GSSAPI when there a multiple realms in
    a single keytab.
`#1270 </sssd/ticket/1270>`__
    sssd\_nss crashes on request when no back end is running
`#1272 </sssd/ticket/1272>`__
    Unable to lookup user, group, netgroup aliases with
    case\_sensitive=false.
`#1273 </sssd/ticket/1273>`__
    SSSD should start before NFS processes
`#1274 </sssd/ticket/1274>`__
    Wrong resolv\_status might cause crash when name resolution times
    out
`#1282 </sssd/ticket/1282>`__
    Wrong attribute counter causing crash during IPA service lookups
`#1283 </sssd/ticket/1283>`__
    accessing an undefined variable in list\_missing\_attrs might crash
    SSSD
`#1288 </sssd/ticket/1288>`__
    Invalid keytab path logged when using the default keytab
`#1293 </sssd/ticket/1293>`__
    Building manpages in a parallel build dir is broken
`#1304 </sssd/ticket/1304>`__
    autofs client: map name length used as key length

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (17):

-  Fix uninitialized variable
-  Free entry found in negative cache
-  Make the string\_equal() function public
-  Save alias of the primary name, too
-  NSS: Look for services with correct case when cache is updated
-  AUTOFS: fix copy-and-paste bug in the autofs client
-  LDAP services: Keep the protocol around
-  Silence Coverity warning in the autofs test tool
-  Return correct resolv\_status on resolver timeout
-  Add sss\_get\_cased\_name\_list utility function
-  LDAP services: Save lowercased protocol names in case-insensitive
   domains
-  Proxy services: Save lowercased protocol names and aliases in
   case-insensitive domains
-  Fix off-by-one error in principal selection
-  Catch cases where D-Bus connection is NULL
-  Fix regression in SSSDConfig.py
-  Use the correct options counter
-  netlink integration: ensure that interface name is NULL-terminated

Jan Cholasta (3):

-  SSH: Allow clients to explicitly specify host alias
-  SSH: Canonicalize host name and do reverse DNS lookup in
   sss\_ssh\_knownhostsproxy
-  SSH: Fix infinite loop in sss\_ssh\_knownhostsproxy

Stephen Gallagher (10):

-  Bumping version to 1.8.2
-  IPA: Allow service lookups
-  SYSDB: Save only lowercased aliases in case-insensitive domains
-  LDAP: Errors retrieving the RootDSE should not be fatal
-  Start SSSD earlier and stop it later
-  LDAP: Add better error logging when ldap\_result() fails
-  LDAP: Fix memory leaks in synchronous\_tls\_setup
-  Fix building manpages in parallel build dirs
-  Clean up log messages about keytab\_name
-  Updating translation files for 1.8.2 release

Sumit Bose (1):

-  Always initialize the returned data in sss\_krb5\_princ\_realm()
