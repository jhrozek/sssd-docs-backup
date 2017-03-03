Highlights
----------

-  This pre-release does not bring any changes visible to the end-user.
   It is intended to be part of the development of FreeIPA 3.3 and its
   focus of supporting legacy (non-SSSD) clients in a setup where IPA
   server established a trust relationship with an Active Directory
   clients.
-  The handling of ID ranges in the provides has been changed to use a
   plugin interface where each provider can use a different plugin and
   have a different behaviour
-  The libsss\_idmap library has been enhanced in several ways such as
   handling "external mappings" or supporting base RIDs other than 0
-  The assumption that subdomain users always have a primary
   user-private-group (UPG) has been removed
-  If the SSSD is running on the IPA server, it is able to perform
   lookups for trusted users directly against the AD server using the AD
   provider lookups

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1938 </sssd/ticket/1938>`__
    [RFE] Add a new call to libsss\_idmap to add a new mapping where the
    first RID is not 0
`#1960 </sssd/ticket/1960>`__
    [RFE] Add range type for ID mapping in AD to libsss\_idmap
`#1961 </sssd/ticket/1961>`__
    [RFE] Add plugin to LDAP provider to find new ranges
`#1962 </sssd/ticket/1962>`__
    [RFE] Integrate AD provider lookup code into IPA subdomain user
    lookup
`#1979 </sssd/ticket/1979>`__
    [RFE] Add an optional unique range identifier
`#1993 </sssd/ticket/1993>`__
    [RFE] Add a new option to denote server mode

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (11):

-  Updating the version for the 1.10.1 release
-  Bump version to track 1.11 development
-  IPA: Add a server mode option
-  LDAP: Add utility function sdap\_copy\_map
-  AD: decouple ad\_id\_ctx initialization
-  AD: initialize failover with custom realm, domain and failover
   service
-  IPA: Initialize server mode ctx if server mode is on
-  AD: Move storing sdap\_domain for subdomain to generic LDAP code
-  IPA: Create and remove AD id\_ctx for subdomains discovered in server
   mode
-  IPA: Look up AD users directly if IPA server mode is on
-  Updating translations for the 1.11 beta1 release

Sumit Bose (18):

-  idmap: allow first RID to be set
-  idmap: add optional unique range id
-  idmap: add option to indicate external\_mapping
-  idmap: allow NULL domain sid for external mappings
-  idmap: add calls to check if ID mapping conforms to ranges
-  idmap: add sss\_idmap\_domain\_has\_algorithmic\_mapping
-  Add cmocka based tests for libsss\_idmap
-  Add now options ldap\_min\_id and ldap\_max\_id
-  SDAP IDMAP: Add configured domain to idmap context
-  Allow different methods to find new domains for idmapping
-  Add sdap\_idmap\_domain\_has\_algorithmic\_mapping()
-  Replace SDAP\_ID\_MAPPING checks with
   sdap\_idmap\_domain\_has\_algorithmic\_mapping
-  Add ipa\_idmap\_init()
-  Add support for new ipaRangeType attribute
-  Replace new\_subdomain() with find\_subdomain\_by\_name()
-  IPA: read ranges before subdomains
-  Save mpg state for subdomains
-  Read mpg state for subdomains from cache
