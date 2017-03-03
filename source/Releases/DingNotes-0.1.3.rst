Highlights
----------

-  Fixes a serious bug in libdhash with very large (> 1024 slots)
   initial size
-  Minor bugfixes

Detailed Changelog
------------------

Dmitri Pal (2):

-  Initializing variables in test
-  Freeing memory used for source dir

John Dennis (1):

-  Resolves: bug #735464 Fix the loop limit used to initialize the table
   di

Stephen Gallagher (6):

-  Fix license text for several files that should be LGPLv3+
-  Fix incorrect allocation check
-  Eliminate memory leak on error
-  Bump version for 0.1.3 release
-  Update spec file for newer library versions
-  Update version numbers for ding-libs 0.1.3 release

Sumit Bose (2):

-  Fix typo which makes make prerelease-srpm fail
-  Ensure error\_string() never returns NULL
