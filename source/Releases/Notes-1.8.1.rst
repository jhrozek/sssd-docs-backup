Highlights
----------

-  Resolve issue where we could enter an infinite loop trying to connect
   to an auth server
-  Fix serious issue with complex (3+ levels) nested groups
-  Fix netgroup support for case-insensitivity and aliases
-  Fix serious issue with lookup bundling resulting in requests never
   completing
-  IPA provider will now check the value of nsAccountLock during
   pam\_acct\_mgmt in addition to pam\_authenticate
-  Fix several regressions in the proxy provider

Detailed Changelog
------------------

Jakub Hrozek (12):

-  Use proper errno code
-  Only do one cycle when resolving a server
-  krb5\_child: set debugging sooner
-  Search netgroups by alias, too
-  Detect cycle in the fail over on subsequent resolve requests only
-  Autofs: operate on contents of double-pointer, not address
-  Only free returned values on success
-  Save original name into the in-memory cache
-  Handle errors from lookup\_netgr\_step gracefully
-  Fix nested groups processing
-  Fix netgroup error handling
-  Handle empty elements in proxy netgroups:

Jan Cholasta (1):

-  Include missing source files to the list of source files which
   contain translatable strings

Jan Zeleny (5):

-  Fix the script path
-  Fixed uninitialized pointer in SSH known host proxy
-  Fixed uninitialized pointer in SSH authorized keys client
-  Add umask before mkstemp() call in SSH responder
-  Fixed resource leak in ssh client code

Pavel Březina (6):

-  Hide --debug option in sss\_debuglevel
-  Two memory leaks in sss\_sudo\_get\_values
-  Missing debug message if sdap\_sudo\_refresh\_set\_timer fails
-  Use of unininitialized value in sudosrv\_cache\_set\_entry and
   sudosrv\_cache\_lookup\_internal
-  Use of unininitialized value in sss\_sudo\_parse\_response
-  Potential NULL-dereference in sudosrv\_cmd\_get\_sudorules

Simo Sorce (1):

-  Use the correct hash table for pending requests

Stephen Gallagher (20):

-  Bump version to 1.8.1
-  Fix typo in autofs option description
-  Include the debug\_level upgrade tool in the tarball
-  Include new manpages in translations
-  Updating translations for SSSD 1.8.1
-  Fix typo in script name
-  Handle cases where UID is -1
-  IPA: Set the DNS discovery domain to match ipa\_domain
-  IPA: Fix segfault with srchost functionality enabled
-  DP: Reorganize memory hierarchy of requests
-  Prune python provides correctly
-  Make RPM spec more explicit
-  Build experimental features by default in RPMs
-  Properly terminate GIT\_CHECKOUT
-  LDAP: Make sdap\_access\_send/recv public
-  IPA: Check nsAccountLock during PAM\_ACCT\_MGMT
-  PROXY: Create fake user entries for group lookups
-  SSH: Fix missing semicolon
-  IPA: Initialize hbac\_ctx to NULL
-  i18n: Remove empty translations

Yuri Chornoivan (1):

-  fix typos in manual
