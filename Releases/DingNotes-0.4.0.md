Highlights {#Highlights}
----------

### libini\_config

-   Ability to convert input INI file from UTF 16/32 to UTF8 during
    parsing
-   Support C style comments in INI file parsing
-   Ability to read configuration data from a memory buffer
-   Fixed processing of multi-valued strings
-   Fixed parsing of line with multiple tokens

Note for distribution packagers {#Notefordistributionpackagers}
-------------------------------

-   This release bumps the soname of subpackages (libcollection,
    libini\_config)
-   A new version script was added (for more detailed information please
    see
    [\#2193](https://fedorahosted.org/sssd/ticket/2193 "task: Use version script file for libraries from ding-libs (closed: fixed)"){.closed
    .ticket})

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#2106](/sssd/ticket/2106 "[RFE] Add ability to convert input ini file from UTF 16/32 to UTF8 during ..."){.closed}
:   \[RFE\] Add ability to convert input ini file from UTF 16/32 to UTF8
    during parsing

[\#2107](/sssd/ticket/2107 "Description of the parse flags use is missing in header file"){.closed}
:   Description of the parse flags use is missing in header file

[\#2108](/sssd/ticket/2108 "[RFE] Support C/C++ style comments in INI file parsing"){.closed}
:   \[RFE\] Support C/C++ style comments in INI file parsing

[\#2110](/sssd/ticket/2110 "Processing miltivalue strings does not return last token"){.closed}
:   Processing miltivalue strings does not return last token

[\#2119](/sssd/ticket/2119 "Double parsing failes for a complex file"){.closed}
:   Double parsing failes for a complex file

[\#2192](/sssd/ticket/2192 "refactor the UTF-8 conversion function"){.closed}
:   refactor the UTF-8 conversion function

[\#2193](/sssd/ticket/2193 "Use version script file for libraries from ding-libs"){.closed}
:   Use version script file for libraries from ding-libs

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Dmitri Pal (20):

-   Trim trailing spaces
-   Adding missing argument to docs
-   Fix for ini\_get\_string\_config\_array
-   Do not check validity of comments
-   Extend error set and add parsing error
-   Process c-style comments
-   Test files for unit test
-   Unit test for c-style comments
-   Expose buffer context as void
-   Extend internal file handle
-   Convert files to UTF
-   Updated unit test for UTF8 conversion
-   Fix typo in trace message
-   Fix processing of the white space at the end of the line
-   Unit test for space trimming in multiline values
-   Adding more unit tests
-   Refactor conversion function
-   New entry to read data from mem
-   Prevent tight loop
-   Unit test for the new interface

Jakub Hrozek (2):

-   libiniconfig\_devel must require libref\_array-devel and
    libbasicobjects-devel
-   rpm: Include the right filename of libini\_config

Jan Engelhardt (1):

-   build: add missing Requires to pkgconfig file

Lukas Slebodnik (19):

-   Fix warning format string is not a string literal.
-   Fix linking of tests on debian
-   DHASH: Remove dead code.
-   AUTOTOOLS: fix warning: macro xyz not found in library
-   DOC: Fix problems in documentation comments.
-   SPEC: path-utils unit test requires libcheck
-   INI: run also negative\_test
-   Collection: Fix typo in function declarations
-   INI: Use static modifier for non public functions
-   Use static modifier for unit test functions
-   INI: Fix warning missing-prototypes for some functions.
-   INI: Include missing header file with declarations
-   REFARRAY: Move declaration of ref\_array\_debug to public header
    file
-   DHASH: Use ifdef for testing DEBUG macro
-   Enable extra compiler warning flags
-   Add version symbol files
-   AUTOMAKE: Do not treat warnings as errors
-   Bump version-info
-   Bump versions for 0.4.0 release

Ondrej Kos (8):

-   COLLECTION: Fix comparision
-   DHASH: Check before dereferencing
-   PATH\_UTILS: check against character representation of NULL
-   INI: Remove dead code
-   DHASH: Don't use backward jumps
-   DHASH: minor fixes
-   INI: Bump version-info
-   DOXY: Don't generate timestamp

Peter Robinson (1):

-   Fix build with automake 1.14

