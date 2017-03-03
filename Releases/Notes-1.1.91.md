Highlights {#Highlights}
----------

-   Better support for FreeIPA v2
-   Allow use of DNS SRV records for failover
-   Support dynamic DNS updates with FreeIPA v2
-   Add deferred kinit feature for offline users
    -   When `krb5_store_password_if_offline` is set to true, the user
        will automatically kinit when the SSSD comes online (e.g.
        connecting to VPN)
-   Add retries option to pam\_sss.so
-   Better warnings for nearly-expired passwords

Detailed Release Notes {#DetailedReleaseNotes}
----------------------

Release notes may be inaccurate due to the branching that occurred in
this release

Cheng-Chia Tseng (4):

-   Adding empty zh\_TW translation files
-   Updating zh\_TW translation
-   Update zh\_TW translation

Dmitri Pal (7):

-   Documentation for collection interface
-   Do not generate man pages for COLLECION for now.
-   Fixing verbosity and formatting of the INI unit test.
-   Adding interface description using doxygen.
-   Convert collection to use sized values.
-   Fixing type conversion in INI interface.
-   Adding interface documentation

Cheng-Chia Tseng (4):

-   Adding empty zh\_TW translation files
-   Updating zh\_TW translation
-   Update zh\_TW translation

Dmitri Pal (7):

-   Documentation for collection interface
-   Do not generate man pages for COLLECION for now.
-   Fixing verbosity and formatting of the INI unit test.
-   Adding interface description using doxygen.
-   Convert collection to use sized values.
-   Fixing type conversion in INI interface.
-   Adding interface documentation

Dmitry Drozdov (1):

-   Adding Russion Translation

Eugene Indenbom (1):

-   Add krb5\_kpasswd to IPA provider

George
[McCollister?](https://docs.pagure.org/sssd-test2/McCollister.html){.missing
.wiki} (2):

-   Fixed alignment problems in nss client/server
-   Fixed buffer alignment in exchange\_credentials().

Guido Grazioli (1):

-   Updating IT translation

Héctor Daniel Cabrera (4):

-   Updating ES translation
-   Updating ES translation for 1.1.0
-   Update ES translation
-   Updating ES translation for 1.1.0

Jakub Hrozek (31):

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
-   Fixes for path\_utils
-   Unit tests for path\_utils
-   Generate doxygen documentation for path\_utils
-   Allow running with read only root
-   Regression test against RHBZ [\#576856]{.missing .ticket}
-   Add userdel\_cmd param
-   Make sss\_userdel check for logged in users
-   Move SELinux related functions into its own module
-   SELinux login management
-   Treat server names as case-insensitive in failover code
-   Do not mark a request as failed twice
-   Sort SRV replies according to RFC 2782
-   Remove freed server\_common entities from list
-   Support SRV servers in failover
-   Try all servers during Kerberos auth
-   Fix uninitialized variable
-   Add a README file
-   Use all available servers in LDAP provider
-   Improve the offline authentication message
-   Fix memory hierarchy in the ipa timerules
-   Use service discovery in backends

Piotr Drąg (3):

-   Updating PL translation for 1.1
-   Updating PL translation
-   Updating PL translation for 1.1.0

Ralf Haferkamp (6):

-   Fixed check for expired passwords
-   Fixed authentication check for CHAUTHTOK\_PRELIM
-   Warn user about an expired password
-   Prompt for old password even when running as root
-   use logfiles for debug messages
-   Improvements for LDAP Password Policy support

Rui Gouveia (4):

-   Updating PT translation for 1.1.0
-   Updating PT translation
-   Updating PT translation for 1.1.0
-   Update PT translation

Simo Sorce (5):

-   Fix memberof calculation when deleting groups
-   Fix invalid read cause by premature free of tmpctx
-   Fix multiple errors with destructors.
-   Better handle sdap\_handle memory from callers.
-   Avoid freeing sdap\_handle too early

Stephen Gallagher (38):

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
-   Properly handle dbus send attempts on a closed connection
-   Use correct python macros in sssd.spec
-   Clean up changelog for sssd.spec
-   Build and package libini\_config docs
-   Fix a series of memory leaks in the SBUS
-   Fix error message for ldap\_start\_tls
-   Add missing ldap\_tls\_cacertdir option to SSSDConfig API
-   Add translated help text for ldap\_tls\_cacertdir
-   Update version in master branch to 1.1.90
-   Ensure the SSSDConfig creates sssd.conf with the correct mode
-   Fix path\_utils\_ut segfault
-   Allow arbitrary-length PAM messages
-   Fix typo in ldap\_id\_use\_start\_tls option description
-   Add regression test for
    [[​]{.icon}https://fedorahosted.org/sssd/ticket/441](https://fedorahosted.org/sssd/ticket/441){.ext-link}
-   Do not revert options to defaults in SSSDConfig.get\_domain()
-   Protect against check-and-open race conditions
-   Support docdir and abs\_builddir
-   Update translations for SSSD 1.2 branch
-   Remove unused configure macro
-   Give information about ldap\_schema in the sample config
-   Make ID provider init functions clearer
-   Remove the NSS\_LIBS and KRB5\_LIBS variables from sssd.spec
-   Add dns\_resolver\_timeout option
-   Fix segfault in GSSAPI reconnect code
-   Properly set up SIGCHLD handlers
-   Make krb5\_kpasswd available for any krb5 provider
-   Clean up kdcinfo and kpasswdinfo files when exiting
-   Add callback when the ID provider switches from offline to online
-   Add dynamic DNS updates to FreeIPA
-   Update version to 1.1.91

Sumit Bose (30):

-   Add simple access provider
-   Add better checks on PAM socket
-   Add expandable sequences to krb5\_ccachedir
-   Write the IP address of the KDC to the kdcinfo file
-   Add krb5\_kpasswd option
-   Fixes for client communication
-   Lower debug level of unexpected LDAP result codes
-   Fix kinit after password change
-   Set LDAP\_OPT\_RESTART for ldap\_sasl\_interactive\_bind\_s()
-   Fix warnings from -Wmissing-field-initializers
-   Fix LDAP search paths for IPA HBAC
-   Add a test for domain\_to\_basedn()
-   Revert "Add better checks on PAM socket"
-   Use SO\_PEERCRED on the PAM socket
-   Set LDAP\_OPT\_RESTART for all LDAP connections
-   Fix a potential memory violation
-   Make Kerberos authentication a tevent\_req
-   New version of IPA auth and password migration
-   Make the handling of fd events opaque
-   Unset authentication tokens if password change fails
-   Display a message if a password reset by root fails
-   Fix wrong return value
-   Fix a wrong return value in IPA HBAC
-   Split pam\_data utilities into a separate file
-   Handle Krb5 password expiration warning
-   Create kdcinfo and kpasswdinfo file at startup
-   Compare the full service name
-   Add support for delayed kinit if offline
-   Add retry option to pam\_sss
-   Add more warnings about nearly expired passwords

Yuri Chornoivan (1):

-   Add UK translation

eindenbom (1):

-   Avoid accessing half-deallocated memory when using talloc\_zfree
    macro.

Dmitry Drozdov (1):

-   Adding Russion Translation

Eugene Indenbom (1):

-   Add krb5\_kpasswd to IPA provider

George
[McCollister?](https://docs.pagure.org/sssd-test2/McCollister.html){.missing
.wiki} (2):

-   Fixed alignment problems in nss client/server
-   Fixed buffer alignment in exchange\_credentials().

Guido Grazioli (1):

-   Updating IT translation

Héctor Daniel Cabrera (4):

-   Updating ES translation
-   Updating ES translation for 1.1.0
-   Update ES translation
-   Updating ES translation for 1.1.0

Jakub Hrozek (31):

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
-   Fixes for path\_utils
-   Unit tests for path\_utils
-   Generate doxygen documentation for path\_utils
-   Allow running with read only root
-   Regression test against RHBZ [\#576856]{.missing .ticket}
-   Add userdel\_cmd param
-   Make sss\_userdel check for logged in users
-   Move SELinux related functions into its own module
-   SELinux login management
-   Treat server names as case-insensitive in failover code
-   Do not mark a request as failed twice
-   Sort SRV replies according to RFC 2782
-   Remove freed server\_common entities from list
-   Support SRV servers in failover
-   Try all servers during Kerberos auth
-   Fix uninitialized variable
-   Add a README file
-   Use all available servers in LDAP provider
-   Improve the offline authentication message
-   Fix memory hierarchy in the ipa timerules
-   Use service discovery in backends

Piotr Drąg (3):

-   Updating PL translation for 1.1
-   Updating PL translation
-   Updating PL translation for 1.1.0

Ralf Haferkamp (6):

-   Fixed check for expired passwords
-   Fixed authentication check for CHAUTHTOK\_PRELIM
-   Warn user about an expired password
-   Prompt for old password even when running as root
-   use logfiles for debug messages
-   Improvements for LDAP Password Policy support

Rui Gouveia (4):

-   Updating PT translation for 1.1.0
-   Updating PT translation
-   Updating PT translation for 1.1.0
-   Update PT translation

Simo Sorce (5):

-   Fix memberof calculation when deleting groups
-   Fix invalid read cause by premature free of tmpctx
-   Fix multiple errors with destructors.
-   Better handle sdap\_handle memory from callers.
-   Avoid freeing sdap\_handle too early

Stephen Gallagher (38):

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
-   Properly handle dbus send attempts on a closed connection
-   Use correct python macros in sssd.spec
-   Clean up changelog for sssd.spec
-   Build and package libini\_config docs
-   Fix a series of memory leaks in the SBUS
-   Fix error message for ldap\_start\_tls
-   Add missing ldap\_tls\_cacertdir option to SSSDConfig API
-   Add translated help text for ldap\_tls\_cacertdir
-   Update version in master branch to 1.1.90
-   Ensure the SSSDConfig creates sssd.conf with the correct mode
-   Fix path\_utils\_ut segfault
-   Allow arbitrary-length PAM messages
-   Fix typo in ldap\_id\_use\_start\_tls option description
-   Add regression test for
    [[​]{.icon}https://fedorahosted.org/sssd/ticket/441](https://fedorahosted.org/sssd/ticket/441){.ext-link}
-   Do not revert options to defaults in SSSDConfig.get\_domain()
-   Protect against check-and-open race conditions
-   Support docdir and abs\_builddir
-   Update translations for SSSD 1.2 branch
-   Remove unused configure macro
-   Give information about ldap\_schema in the sample config
-   Make ID provider init functions clearer
-   Remove the NSS\_LIBS and KRB5\_LIBS variables from sssd.spec
-   Add dns\_resolver\_timeout option
-   Fix segfault in GSSAPI reconnect code
-   Properly set up SIGCHLD handlers
-   Make krb5\_kpasswd available for any krb5 provider
-   Clean up kdcinfo and kpasswdinfo files when exiting
-   Add callback when the ID provider switches from offline to online
-   Add dynamic DNS updates to FreeIPA
-   Update version to 1.1.91

Sumit Bose (30):

-   Add simple access provider
-   Add better checks on PAM socket
-   Add expandable sequences to krb5\_ccachedir
-   Write the IP address of the KDC to the kdcinfo file
-   Add krb5\_kpasswd option
-   Fixes for client communication
-   Lower debug level of unexpected LDAP result codes
-   Fix kinit after password change
-   Set LDAP\_OPT\_RESTART for ldap\_sasl\_interactive\_bind\_s()
-   Fix warnings from -Wmissing-field-initializers
-   Fix LDAP search paths for IPA HBAC
-   Add a test for domain\_to\_basedn()
-   Revert "Add better checks on PAM socket"
-   Use SO\_PEERCRED on the PAM socket
-   Set LDAP\_OPT\_RESTART for all LDAP connections
-   Fix a potential memory violation
-   Make Kerberos authentication a tevent\_req
-   New version of IPA auth and password migration
-   Make the handling of fd events opaque
-   Unset authentication tokens if password change fails
-   Display a message if a password reset by root fails
-   Fix wrong return value
-   Fix a wrong return value in IPA HBAC
-   Split pam\_data utilities into a separate file
-   Handle Krb5 password expiration warning
-   Create kdcinfo and kpasswdinfo file at startup
-   Compare the full service name
-   Add support for delayed kinit if offline
-   Add retry option to pam\_sss
-   Add more warnings about nearly expired passwords

Yuri Chornoivan (1):

-   Add UK translation

eindenbom (1):

-   Avoid accessing half-deallocated memory when using talloc\_zfree
    macro.

