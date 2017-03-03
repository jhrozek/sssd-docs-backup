Highlights
----------

-  Support ServiceGroups for FreeIPA v2 HBAC rules
-  Fix long-standing issue with auth\_provider = proxy
-  Better logging for TLS issues in LDAP

Detailed Release Notes
----------------------

David O'Brien (1):

-  Copy-edit and format review sssd.conf

Jakub Hrozek (1):

-  SSSDConfigAPI fixes

Petter Reinholdtsen (1):

-  Remove bash-isms from configure macros

Piotr Drąg (1):

-  Update pl translation

Stephen Gallagher (9):

-  Add a better error message for TLS failures
-  Add enumerate details to the manpage and examples
-  Make data provider id\_callback public
-  Fix error reporting for be\_pam\_handler
-  Proxy provider PAM handling in child process
-  Display name of PAM action in pam\_print\_data()
-  Fix queuing bug in proxy provider
-  Support password changes in chpass\_provider = proxy
-  Release SSSD version 1.2.0

Sumit Bose (9):

-  Reset run\_online\_cb flag even if there are no callbacks
-  Fix check if LDAP id provider is already initialized
-  Defer sbus\_dispatch() for 30ms during reconnect
-  Copy pam data from DBus message
-  Remove signal event if child was terminated by a signal
-  Do not modify IPA\_DOMAIN when setting Kerberos realm
-  Move parse\_args() to util
-  Check ipaEnabledFlag
-  Use new schema for HBAC service checks

Yuri Chornoivan (1):

-  Update uk translation
