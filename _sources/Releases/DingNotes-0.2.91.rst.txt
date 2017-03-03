Highlights
----------

-  extensive changes in libini\_config (merging config section, better
   handling of metadata)
-  coverity and other bugfixes

Detailed Changelog
------------------

Dmitri Pal (71):

-  New wrapper macros for function entry and exit
-  Introducing basic objects
-  Fixing the cleaup code
-  Refining comment object
-  Introducing Value object
-  Allow destroying collection with a callback
-  Added a convenience function
-  More config files for testing
-  Extend the comment interface
-  Add error codes for the new parser
-  Fixes to the value object
-  The beginning of the new INI interface
-  New INI parser
-  Starting to consolidate the new interface in one place
-  Introducing configuration file object
-  Adding ref\_array copy method
-  Refactoring comment object
-  Fixing trace macros
-  Enhancements to value object
-  Refactoring error reporting
-  Minor tracing cleanup
-  Fix copy collection
-  Improvements to the value object
-  New copy and folding functionality
-  Allow merging values
-  Collision flag validation
-  Preparing to merge sections
-  Adding missing file to the package
-  Fix crashes with file object
-  Correcting paths to test files
-  Additional tests
-  Coverity issues 10071 & 10072
-  Coverity issue 10034
-  File descritpor leak
-  Leaking memory on failure
-  Initializing variables in test
-  Initialize simple buffer
-  Free newly created value in case of error
-  Freeing memory used for source dir
-  Adding missing const
-  Coverity issue 10042
-  Coverity issue 10075
-  Fixing dereferencing NULL
-  Fixing coverity issues 10078 & 10079
-  New error codes and messages
-  New merge flags
-  Add new vars to parse structure
-  Add save\_error function
-  Change parse\_error to use save\_error
-  Preparing for merging sections
-  Enhance value processing
-  Use section line number
-  Refactor section processing
-  Return error in DETECT mode
-  New test files for section merge
-  Test DETECT mode and use new file
-  Test for all section merge modes
-  Fix indentention in the switch statement
-  Separate close and destroy
-  Function to reopen file
-  Metadata collection is gone
-  Check access function
-  Function to check for changes
-  Tests for access and changes
-  Rename error print function
-  Initialize variables in loops
-  Exposing functions
-  Do not debug padding
-  Add missing assertion macro
-  Add missing cleanup in unit test
-  Use right macro

Jakub Hrozek (1):

-  INI: Silence compilation warnings

Jan Zeleny (1):

-  Update version numbers for ding-libs-0.2.91 release

John Dennis (1):

-  Resolves: bug #735464 Fix the loop limit used to initialize the table
   directory, was based on count, now limited to segment\_count.

Stephen Gallagher (10):

-  Bumping development version number
-  Updating dhash version to 0.4.2
-  Fix license text for several files that should be LGPLv3+
-  path\_utils: handle off-by-one error in path\_concat()
-  path\_utils: Handle "/" in path\_concat
-  path\_utils: path\_concat should return empty string on ENOBUFS
-  Bump version for 0.1.3 release
-  Update version numbers for ding-libs 0.1.3 release
-  Fix issue when running make distcheck
-  Properly handle file permissions for ini\_parse\_ut startup\_test()

Sumit Bose (10):

-  Fix typo in spec file
-  Fix overflow in ini\_parse unit test
-  Remove unneeded --disable-rpath configure option
-  Fix version handling of the libraries
-  dhash: add stddef.h to dhash.h
-  dhash: Fix memory leak in example
-  dhash: Allow hash\_enter() to update entries
-  Fix a typo in dhash.h
-  Fix typo which makes make prerelease-srpm fail
-  Ensure error\_string() never returns NULL
