Highlights
----------

-  New LDAP access provider allows for filtering user access by LDAP
   attribute
-  Reduced default timeout for detecting offline status with LDAP

   -  For ``enumerate=False``, reduced to five seconds
   -  For ``enumerate=True``, reduced to thirty seconds

-  GSSAPI ticket lifetime made configurable

   -  New default is 24 hours (or server maximum, whichever is lower)

-  Better offline->online transition support in Kerberos

Detailed Changelog
------------------

Petter Reinholdtsen (1):

-  Allow
   `Debian/Ubuntu? <https://docs.pagure.org/sssd-test2/Debian/Ubuntu.html>`__
   build to pass --install-layout=deb to setup.py

Piotr Drąg (1):

-  Update pl translation

Stephen Gallagher (6):

-  Add ldap\_access\_filter option
-  Don't report a fatal error for an HBAC denial
-  Add ldap\_access\_filter option
-  Remove unused ldap\_offline\_timeout option
-  Set ldap\_search\_timeout default to 5 seconds
-  Update version to 1.1.92

Sumit Bose (11):

-  Add ldap\_krb5\_ticket\_lifetime option
-  Revert "Create kdcinfo and kpasswdinfo file at startup"
-  Refactor data provider callbacks
-  Add offline callbacks
-  Refactor krb5\_finalize()
-  Add run\_callbacks flag
-  Add callback to remove krb5 info files when going offline
-  Krb5 locator plugin returns KRB5\_PLUGIN\_NO\_HANDLE
-  Refactor krb5 SIGTERM handler installation
-  Add krb5 SIGTERM handler to ipa auth provider
-  Add offline callback to disconnect global SDAP handle

Yuri Chornoivan (1):

-  Update uk translation
