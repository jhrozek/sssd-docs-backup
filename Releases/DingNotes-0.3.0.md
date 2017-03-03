Highlights {#Highlights}
----------

-   New ini\_config interface
-   Clang, coverity and other bugfixes

Detailed Changelog {#DetailedChangelog}
------------------

Dmitri Pal (36):

-   No need to copy file in configure any more
-   Adding couple functions to value object
-   Definition of the new INI interface
-   Add a search state to the config object
-   The implementation of the new interface
-   Start building the new interface
-   Added new tests for the multi value keys
-   Build docs for new interface
-   Fix two issues in Makefile.am
-   Fixing coverity issue 11089
-   Fix doxygen warnings for the interface
-   Clean doxygen configurations
-   Remove code that allows dup sections
-   Adding a trace statement
-   Merge and serialize comments
-   Merge comments from different values
-   Fix trace message
-   Ability to merge configurations
-   Improve parser
-   Update comments in the public interface
-   Update files used in the unit test
-   Update unit tests
-   Fixing coverity issue 13105
-   Make CLANG happy
-   Fix CLANG errors in unit test
-   Add INI\_GET\_LAST\_VALUE
-   Converting errors to enum
-   Use ENOMEM instead of errno
-   Fixing headers
-   Replacing sprintf with snprintf
-   Refactor interface a bit
-   Introducing parsing flags
-   More interface refactoring
-   Unit test for parsing flags.
-   Check is the stats we collected
-   Expose collected stat data

Günther Deschner (1):

-   ini\_comment.h needs to be installed as well for the new ini
    interface.

Jakub Hrozek (3):

-   Include AM\_PROG\_AR in configure.ac to get rid of warnings
-   Run autoreconf before configure in the specfile
-   Add a release script

Ondrej Kos (2):

-   Fixed libcollection dependency and header files inclusion
-   Bump version for 0.3.0 release

Stephen Gallagher (1):

-   Fix permission checking unit test

