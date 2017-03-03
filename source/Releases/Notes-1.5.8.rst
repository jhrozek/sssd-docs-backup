Highlights
----------

-  Support for the LDAP paging control
-  Support for multiple DNS servers for name resolution
-  Fixes for several group membership bugs
-  Fixes for rare crash bugs

Detailed Changelog
------------------

Jakub Hrozek (2):

-  Set c-ares to retry nameservers
-  Only save members for successfully saved groups

Simo Sorce (1):

-  clients: use poll instead of select

Stephen Gallagher (5):

-  Make "password" the default for ldap\_default\_authtok\_type
-  simple provider: Don't treat primary GID lookup failures as fatal
-  Enable paging support for LDAP
-  IPA Provider: don't fail if user is not a member of any groups
-  Add more detail to ldap\_uri manpage entry

Sumit Bose (2):

-  Return pam data to the renewal item if renewal fails
-  Sanitize username during initgroups call
