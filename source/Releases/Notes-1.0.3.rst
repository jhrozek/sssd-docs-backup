Highlights
----------

-  Fixes link error on platforms that do not do implicit linking
-  Fixes double-free segfault in PAM
-  Fixes double-free error in async resolver
-  Fixes support for TCP-based DNS lookups in async resolver
-  Fixes memory alignment issues on ARM processors
-  Manpage fixes

Detailed Changelog
------------------

George McCollister (1):

-  Pointers to non 32 bit aligned data were being cast to uint32\_t \*

Jakub Hrozek (2):

-  document debug\_timestamps
-  Deleting nonexistent users or groups is not a noop

Stephen Gallagher (7):

-  Fix timeout memory heirarchy
-  Use version.m4 for setting the SSSD version
-  Add 'prerelease-srpms' target to Makefile
-  Add 'prerelease-rpms' target to Makefile
-  Add missing link for Kerberos
-  Fix async resolver integration with tevent
-  Update version to 1.0.3

Sumit Bose (1):

-  Fix a double free bug
