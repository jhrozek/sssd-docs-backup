Highlights
----------

-  Fixes for several crash bugs
-  LDAP group lookups will no longer abort if there is a zero-length
   member attribute
-  Add automatic fallback to 'cn' if the 'gecos' attribute does not
   exist

Detailed Changelog
------------------

Jakub Hrozek (5):

-  Fix typo in sdap\_nested\_group\_process\_step
-  Mark transaction as done when cancelled
-  Do not attempt to resolve nameless servers
-  Remove detection of duplicates from SRV result processing
-  Use safe alignment macros for in-tree SRV record parsing

Stephen Gallagher (5):

-  Update version to 1.5.5
-  Always complete the transaction in
   sdap\_process\_group\_members\_2307
-  RFC2307: Ignore zero-length member names in group lookups
-  Fall back to cn if gecos is not available
-  Updating translation files

Sumit Bose (3):

-  Read only rootDSE data if rootDSE is available
-  Initialise srv\_opts even if rootDSE is missing
-  Initialise rootdse to NULL if not available
