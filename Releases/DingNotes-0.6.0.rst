Highlights
----------

libini\_config
~~~~~~~~~~~~~~

-  libini now supports validators that check for well-formed INI files.
   Please see the Doxygen documentation for more details on using the
   new functions. The new functions include:

   -  ini\_rules\_read\_from\_file
   -  ini\_rules\_check
   -  ini\_rules\_destroy
   -  ini\_errobj\_\*

Note for distribution packagers
-------------------------------

-  API and ABI is backward compatible with last release (0.5.0)

Detailed Changelog
------------------

Dmitri Pal (1):

-  ini: Add INI\_PARSE\_IGNORE\_NON\_KVP flag

Lukas Slebodnik (6):

-  INI: Enable string format check for ini\_errobj\_add\_msg
-  INI: Extend validator unit test for corner cases
-  INI: Reduce count of argumets for ini\_rules\_check
-  INI: Prepare for schema validation
-  Bump version-info
-  Update versions before 0.6.0 release

Michal Židek (6):

-  ini\_parse: Add missing TRACE\_FLOW\_EXIT
-  Add unit test for INI\_PARSE\_IGNORE\_NON\_KVP
-  ini: Add infrastructure for validators
-  ini: Add internal validator ini\_allowed\_options
-  tests: Tests for rules/validators infrastructure
-  ini: Add internal validator allowed\_sections

Robbie Harwood (3):

-  Document ini\_config\_augment alphabetical file processing
-  Fix comment in ini\_augment\_ut.c
-  Ensure ding-linbs metapackage depends on libbasicobjects
