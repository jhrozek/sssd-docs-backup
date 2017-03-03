Highlights {#Highlights}
----------

-   Documentation for libcollection and libini\_config
-   Support for logrotate
-   New "simple" access provider for easy restriction of users

Detailed Changelog {#DetailedChangelog}
------------------

Cheng-Chia Tseng (3):

-   Adding empty zh\_TW translation files
-   Updating zh\_TW translation
-   Update zh\_TW translation

Dmitri Pal (6):

-   Documentation for collection interface
-   Do not generate man pages for COLLECION for now.
-   Fixing verbosity and formatting of the INI unit test.
-   Adding interface description using doxygen.
-   Convert collection to use sized values.
-   Fixing type conversion in INI interface.

George
[McCollister?](https://docs.pagure.org/sssd-test2/McCollister.html){.missing
.wiki} (2):

-   Define \_GNU\_SOURCE in pam\_sss.c.
-   Fixed alignment problems in nss client/server

Héctor Daniel Cabrera (4):

-   Updating ES translation
-   Updating ES translation for 1.1.0
-   Update ES translation
-   Updating ES translation for 1.1.0

Jakub Hrozek (10):

-   groupshow: only show all parents in recursive mode
-   Do not run negative resolv test with no network
-   Reopen logs when SIGHUP is caught
-   Package example logrotate script
-   Make filter\_users and filter\_groups also per-domain
-   Flush NSCD cache after modifying local database
-   Remove unused M4 code
-   Fix segfault in the locator plugin
-   Fix config file error message
-   Add generic error message

Martin Nagy (2):

-   Make confdb\_init's confdb\_location parameter const
-   Add forgotten \\n in DEBUG statements

Piotr Drąg (4):

-   Updating PL translation
-   Updating PL translation for 1.1
-   Updating PL translation
-   Updating PL translation for 1.1.0

Ralf Haferkamp (5):

-   Fixed check for expired passwords
-   Fixed authentication check for CHAUTHTOK\_PRELIM
-   Warn user about an expired password
-   Prompt for old password even when running as root
-   use logfiles for debug messages

Rui Gouveia (5):

-   Updating PT translation
-   Updating PT translation for 1.1.0
-   Updating PT translation
-   Updating PT translation for 1.1.0
-   Update PT translation

Simo Sorce (6):

-   proxy: use correct \_recv function
-   Improve safe alignment buffer handling macros
-   Fix debug\_timestamps
-   Fix memberof calculation when deleting groups
-   Fix invalid read cause by premature free of tmpctx
-   Fix multiple errors with destructors.

Stephen Gallagher (23):

-   Fix release script to handle version numbers with multiple digits
-   Update version to 1.1.0
-   Run 'make check' during rpmbuild
-   Add --with-test-dir option to configure
-   Eliminate monitor reconfig
-   Package libcollection documentation into libcollection-devel
-   Add
    [BuildRequires?](https://docs.pagure.org/sssd-test2/BuildRequires.html){.missing
    .wiki} for doxygen
-   Update translatable strings for string freeze
-   Add ID translation for SSSD 1.1.0
-   Update POTFILES.in to include missing translatable strings
-   Fix build when check-devel is not installed
-   Update translations for string freeze
-   Updating translation files for string freeze.
-   Revert "Add better checks on PAM socket"
-   Properly handle dbus send attempts on a closed connection
-   Use correct python macros in sssd.spec
-   Clean up changelog for sssd.spec
-   Build and package libini\_config docs
-   Fix a series of memory leaks in the SBUS
-   Fix error message for ldap\_start\_tls
-   Add missing ldap\_tls\_cacertdir option to SSSDConfig API
-   Ensure the SSSDConfig creates sssd.conf with the correct mode
-   Updating strings for 1.1.0 release

Sumit Bose (7):

-   Add simple access provider
-   Add better checks on PAM socket
-   Add expandable sequences to krb5\_ccachedir
-   Write the IP address of the KDC to the kdcinfo file
-   Add krb5\_kpasswd option
-   Fixes for client communication
-   Lower debug level of unexpected LDAP result codes

Yuri Chornoivan (1):

-   Add UK translation

