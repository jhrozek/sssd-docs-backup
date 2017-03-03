Highlights
----------

-  Fix for older openldap libraries that can fail setting the "no
   canonicalization" option
-  pam\_sss will now return authinfo\_unavail when the SSSD daemon is
   shut down, instead of PAM\_SYSTEM\_ERR
-  Fixes a regression in LDAP failover handling
-  Adds support for using Glib to provide unicode support instead of
   libunistring

   -  SSSD must be built with the configure flag
      ``--with-unicode-lib=glib2``

-  All user/group/netgroup names passed to NSS/PAM are now validated to
   be valid UTF-8 strings

Detailed Changelog
------------------

Jakub Hrozek (1):

-  LDAP provider: Error while setting the nocanon option should not be
   fatal

Jan Zeleny (2):

-  Fixed an error in macro for merging double linked lists
-  Fixed incorrect return code in PAM client

Krzysztof Klimonda (1):

-  Fix FTBFS related to -Werror=format-security

Simo Sorce (1):

-  Use neutral name for functions used by both pam and nss

Stephen Gallagher (10):

-  Bumping version to 1.5.16
-  RESPONDER: Ensure that all input strings are valid UTF-8
-  Add -fno-strict-aliasing
-  LDAP: Try next failover server on any error
-  Allow using Glib for UTF8 support
-  Ignore NULL-terminator when checking UTF8-validity
-  DEBUG: fix bad backport containing new DEBUG representation
-  Ignore NULL-terminator when checking UTF8-validity for netgroups
-  Translation update
-  Adding new translation files
