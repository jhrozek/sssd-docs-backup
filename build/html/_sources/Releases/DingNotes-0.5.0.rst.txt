Highlights
----------

libini\_config
~~~~~~~~~~~~~~

-  This release adds an API to create, modify and save INI files
-  Merging configuration snippets installed in different locations is
   supported

libcollection
~~~~~~~~~~~~~

-  New functions: ``col_get_dup_item``, ``col_delete_item_with_cb``,
   ``col_remove_item_with_cb``

Note for distribution packagers
-------------------------------

-  New public header file ``ini_configmod.h``
-  API and ABI is backward compatible with last release (0.4.0)

Detailed Changelog
------------------

Dmitri Pal (22):

-  Print info when array is empty
-  Declaring new internal access check function
-  Refactored access control check
-  New function to merge snippets
-  Test file for unit test
-  [INI] Make the merge function build
-  Function to return one of the dups
-  Allow to modify item name
-  Expose delete with callback function
-  Comment creation helper
-  Comment can be NULL
-  Move definition to common header
-  Fix wrapping error
-  New interface to modify configuration
-  Build new interface
-  Generate doxy doc for INI modification API
-  Cleaning doxygen comments
-  Change order of the headers
-  New interface to save configuration in a file
-  Implementation of the interface to save configuration
-  Unit test for the save interface
-  Build new tests for the save interface

Lukas Slebodnik (10):

-  SPEC: Use correct soname for packages lib{collection,ini\_config}
-  SPEC: Do not include compiled files into package libdhash-devel
-  ini\_config\_ut: enable verbose mode with env variable
-  collection: Add new function col\_remove\_item\_with\_cb
-  INI: Fix memory leak with INI\_VA\_CLEAN
-  COLLECTION: Return the last duplicate for big index
-  INI: Fix adding string with INI\_VA\_MODADD\_E and big index
-  INI: Add check based test ini\_configmod\_ut\_check
-  Bump version-info
-  Update versions before 0.5.0 release
