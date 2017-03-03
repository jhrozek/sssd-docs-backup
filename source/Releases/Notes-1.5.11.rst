Highlights
----------

-  Fix a serious regression that prevented SSSD from working with
   ``ldaps://`` URIs
-  IPA Provider: Fix a bug with dynamic DNS that resulted in the wrong
   IPv6 address being saved to the AAAA record.

Detailed Changelog
------------------

Jakub Hrozek (2):

-  ipa\_dyndns: Use sockaddr\_storage for storing IP addresses
-  Fix unchecked return values of pam\_add\_response

Matthew Ife (1):

-  Replace system() function with fork and execl call.

Stephen Gallagher (1):

-  Bumping version to 1.5.11

Sumit Bose (1):

-  Call ldap\_install\_tls() on ldaps connections
