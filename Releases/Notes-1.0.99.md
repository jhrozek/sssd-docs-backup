Highlights {#Highlights}
----------

-   Support for IPv6
    -   IPv6 operation is not yet supported for chpass operations on
        Kerberos, due to a libkrb5 bug.
-   Support for LDAP referrals
    -   This is only supported on platforms running openldap
        libraries &gt;= 2.4.13
-   Offline failed login counter
-   Fix for the long-standing cache cleanup performance issues
    -   Running with 'enumerate=false' (the default) will now be much
        faster
-   libini\_config, libcollection, libdhash, libref\_array and
    libpath\_utils are now built as shared libraries for general
    consumption
-   Users get feedback from PAM if they authenticated offline
-   Native local backend now has a utility to show nested memberships
    (`sss_groupshow`)

Detailed Changelog {#DetailedChangelog}
------------------

David O'Brien (2):

-   Copy-edit sssd-ipa man page
-   Copy-edit, mainly fixing typos and English

Dmitri Pal (8):

-   COMMON Improvements to the trace macro
-   COLLECTION Create reference to the top level collection
-   COLLECTION: Cleaning FIXME comments
-   INI: Cleaning FIXME comments.
-   INI Correcting build warnings.
-   INI: Added method to get string list with empty values
-   REFARRAY: New referenced array object
-   COLLECTION: Fixing queue collection and unit tests.

Domingo Becker (1):

-   Updating ES translation

Fabian Affolter (1):

-   Add German translation

George
[McCollister?](https://docs.pagure.org/sssd-test2/McCollister.html){.missing
.wiki} (2):

-   Pointers to non 32 bit aligned data were being cast to uint32\_t \*
-   Added option to use libcrypto instead of NSS.

Göran Uddeborg (5):

-   Add Swedish translation for sss\_client
-   Add Swedish translation for SSSD server
-   Update SV translation
-   Update SV translation
-   Update SV translation

Jakub Hrozek (32):

-   Setup ldap child logging from IPA backend
-   Check the services started against a list of known services
-   Handle spaces in config parser
-   Fail on nonexistent input file
-   Do not start with provider=files
-   Reduce code duplication between LDAP child and Kerberos child
-   Change ares usage to be c-ares 1.7.0 compatible
-   Import ares 1.7.0 helpers
-   Don't build the SRV and TXT parsing code except for tests
-   Document the failover feature in manpages
-   Consolidate code for splitting strings by separator
-   sss\_groupshow - a utility to print properties of a local group
-   document debug\_timestamps
-   Deleting nonexistent users or groups is not a noop
-   Add missing include
-   Few misc minor man page bugs
-   Fix other memory alignment issues
-   sss\_groupshow improvements
-   gitignore additions
-   sss\_groupshow: separate member lists by comma
-   Synchronize IPA and LDAP options
-   Add test for number of options in IPA and LDAP backends
-   Supress warnings with -O2
-   Use macros to hide memcpy calls
-   Remove Kerberos options from confdb.h
-   Restrict family lookups
-   Do not schedule enumeration after a cleanup
-   Do not check entries during cleanup task
-   Store lastLogin attribute when authenticating online
-   Better cleanup task handling
-   Remove a check that was left behind
-   Fix check for values of expiration limits

Marina Latini (1):

-   Update IT translation

Martin Nagy (10):

-   Fix egg-info file generation in the spec file
-   Add some debugging statements to fail\_over and resolver
-   Correctly restart server status after the timeout
-   Don't consider one address with different port numbers as the same
-   fail over: Change the first server pick logic
-   Re-create c-ares channels if /etc/resolv.conf is modified
-   Make periodic checks for DNS timeouts
-   Don't recursively call ares\_process\_fd() from fd\_event()
-   Make sure callbacks never retry when ares channel is destroyed
-   Don't pass a variable as format to talloc\_asprintf()

Piotr Drąg (3):

-   Update SV translation
-   Updating PL translation
-   Update PL translation

Sergei V. Kovylov (1):

-   sssd.spec for SLES

Sergey V. Kovylov (1):

-   Update suse sssd.spec

Simo Sorce (20):

-   Fix memberof plugin
-   Compute and save memberuid in cache as well
-   Use memberuid and not member in group enumerations
-   Use the custom password field in groups too.
-   Resolve nested groups also when rfc2307bis is used
-   Make strdn build functions more available
-   Fix nested group memberships
-   Allow nesting to fix
    [\#310](https://fedorahosted.org/sssd/ticket/310 "defect: sssd_be segfaults because of tevent_loop_once nesting (closed: fixed)"){.closed
    .ticket}
-   Fix bug
    [\#311](https://fedorahosted.org/sssd/ticket/311 "defect: Segfault shutting down SSSD (closed: fixed)"){.closed
    .ticket}, properly set callback attribute
-   Change dhash API to be talloc-friendly
-   dhash: Add private pointer for delete callback
-   Add comments to document latest changes
-   Add rebuild task to memberof plugin
-   Handle the special 02 upgrade case for 04-&gt;05
-   Fix for
    [\#316](https://fedorahosted.org/sssd/ticket/316 "defect: Native LDAP Backend - Group Memberships Not Returned (closed: fixed)"){.closed
    .ticket}
-   Fix for
    [\#322](https://fedorahosted.org/sssd/ticket/322 "defect: DB Upgrades from 0.5.0 does not work correctly (closed: fixed)"){.closed
    .ticket}, update from old database versions.
-   Fix upgrade bug
    [\#323](https://fedorahosted.org/sssd/ticket/323 "defect: Upgrades from old versions only succeed if there was a LOCAL provider ... (closed: fixed)"){.closed
    .ticket}
-   Fix ldap child memory hierarchy and other issues
-   Don't free timer events within the handler.
-   Fix
    [\#382](https://fedorahosted.org/sssd/ticket/382 "defect: sssd_be segfault (closed: fixed)"){.closed
    .ticket}, a segfault bug in the memberof plugin.

Stephen Gallagher (103):

-   Revert "Stop configuring ELAPI"
-   Revert "Remove ELAPI from build and tarball"
-   Make debug log timestamps human-readable
-   Raise debug log level for LDB\_DEBUG\_WARNING
-   Add allocation error check
-   Avoid returning uninitialized result.
-   Fix potential uninitialized value errors in nsssrv\_cmd.c
-   Fix potential uninitialized value error in responder\_dp.c
-   SSSDDomain.remove\_provider() requires only the provider type
-   Make SSSDDomain.remove\_provider() remove configured options
-   Run dhash tests
-   Add SSSDDomain.set\_name() function to SSSDConfig API
-   Reduce the verbosity of the SSSDConfigTest
-   Fix broken SSSDChangeConf.set() function
-   Fix SSSDConfig API bugs around \[de-\]activation of domains
-   Fix RPM spec for RHEL6
-   SSSDConfig API: fix deactivate\_domain()
-   SSSDConfig.get\_domain() should properly detect active state
-   Ensure that list\_active\_domains returns the real value
-   Properly deny id\_provider=files
-   Add missing options to sssd-ipa configuraion
-   Add missing SSSDConfig file for IPA for make install
-   Fix processing of Boolean values in SSSDConfig
-   Add 'permit' and 'deny' access providers to SSSDConfig API
-   Remove default for ldap\_use\_start\_tls in IPA providers
-   Run SSSDConfig tests during 'make check'
-   Fix stupid copy-paste error
-   Updating version to 0.99.1
-   Properly close STDERR when daemonizing
-   Fix tight loop in monitor
-   Don't set explicit default for "timeout" in domains
-   Fix warning in server.c
-   Raise DEBUG level of sdap\_get\_generic\_done()
-   Change default for enumeration to TRUE
-   Fix tight-loop in monitor part 2
-   Properly handle EINTR from poll()
-   Updating ES translation
-   Add DEBUG messages to getpwnam\_callback and getpwuid\_callback
-   Clarify access\_provider manpage entry
-   Do not blindly accept zero-length passwords
-   Fix broken password changes for local users
-   Release SSSD 1.0
-   Allow debug\_timestamps setting on a per-domain basis
-   Update translations for master
-   Releasing version 1.0.1
-   Remove local and kerberos providers from the access\_provider list
-   Explicitly set async DNS timeout
-   Update version to 1.0.2
-   Updating version to 1.1
-   Resetting VERSION to 1.0.99
-   Fix timeout memory heirarchy
-   License libdhash under the LGPL
-   Split off libdhash into a shared library
-   Use version.m4 for setting the SSSD version
-   Add 'prerelease-srpms' target to Makefile
-   Add 'prerelease-rpms' target to Makefile
-   Add missing link for Kerberos
-   Fix async resolver integration with tevent
-   Fix release script to use version.m4
-   Handle IPv6 addresses with the async resolver
-   Fix size error on 64-bit systems
-   Force offline operation with SIGUSR1
-   License libpath\_utils under LGPL
-   Split off libpath\_utils into a shared library
-   Package libpath\_utils and libpath\_utils-devel
-   Add license files for collection
-   Remove private header requirements from collection\_tools.h
-   Split off libcollection into a shared library
-   Package libcollection and libcollection-devel
-   Add license files for ini\_config
-   Fix array index error
-   Split off libini\_config into a shared library
-   Package libini\_config and libini\_config-devel
-   Add license files for refarray
-   Split refarray off into a shared library
-   Package libref\_array and libref\_array-devel
-   Enable debug\_timestamps by default
-   Internationalize the command-line help message
-   Remove unnecessary explicit defaults from SSSDConfig API
-   Add mandatory flag to SSSD config schema
-   Add a few additional extensions to .gitignore
-   Update translatable strings
-   Make collection\_queue.h and collection\_stack.h into public headers
-   Remove ELAPI from the SSSD repository
-   Add doxygen docs for ConfDB
-   Make attr\_type an integer
-   Make PAM responses more compatible with D-BUS spec
-   Eliminate separate build tree for sss\_client
-   Merge sss\_client and sss\_daemon translations together
-   Remove unneeded files from sss\_client
-   Rename server/ directory to src/
-   Build all manpages from a single location
-   License libpath\_utils under LGPL
-   Fix licensing issues in SSSD
-   Properly license libdhash
-   Fix licensing issues for sss\_client
-   Fix bad merge
-   Disable rpath support in the linker
-   Remove unnecessary "domain" parameter from DP registration
-   Remove unnecessary domain parameter from PAM requests
-   Include hour in 'make prerelease-rpms'
-   Revert "Change default for enumeration to TRUE"
-   Update translations for release

Sumit Bose (51):

-   Check LDAP structure before calling ldap\_unbind\_ext()
-   Add sysdb\_search\_custom request
-   Do not treat missing proc files as errors.
-   Add basic OS detection
-   Make packaging of \*.egg-info files more flexible
-   Try to renew Kerberos credentials
-   Add checks to test the memberuid handling
-   Add offline support for ipa\_access
-   Add dummy credentials to an empty ccache file
-   Always update sysdb to the latest version
-   Fix DEBUG message for sysdb\_init
-   Use sys.exit instead of exit
-   Add elapi\_ut.conf to the list of dist files
-   Check for minimal version of check
-   Build python modules in builddir
-   Use --with-ldb-lib-dir while running make distcheck
-   Cleanup db files after test run
-   disable password migration code
-   Handle chauthtok with PAM\_PRELIM\_CHECK separately
-   Do not overwrite valid TGTs when offline
-   Fix for
    [\#344](https://fedorahosted.org/sssd/ticket/344 "defect: SSSD Kerberos does not play nicely with kdestroy (closed: fixed)"){.closed
    .ticket}
-   Return an error for an unknown PAM request
-   Fix return value when offline and TGT is valid
-   Add sysdb request to authenticate against a cached password
-   Fix a double free bug
-   Update the url in the spec files
-   Rename PAM\_USER\_INFO to PAM\_SYSTEM\_INFO
-   Avoid 'PAM' at the beginning of define and enum names
-   Improve logging of pam\_sss
-   Check cache\_credentials in sysdb\_cache\_auth\_send()
-   Use ldap connection callbacks to get file descriptors
-   Add new option ldap\_referrals
-   Add offline failed login counter
-   Warn the user if authentication happens offline
-   Make resolve and failover test work with CK\_FORK=no
-   Make krb5 and open checks work if forking is disabled
-   Reactivate old fd handling conditionally
-   Document when LDAP referral chasing is available
-   Send a message to the user if the login is delayed
-   Fix handling of the global context in the leak detector
-   Make return values more specific during password change
-   Make change password errors more transparent
-   Add check for broken LDAP connection callbacks
-   Remove replace
-   Fix two typos
-   Send Kerberos environment after password change
-   Remove unneeded items from struct pam\_data
-   Add documentation for PAM response messages
-   Check and set permissions on SBUS sockets
-   Fix file permissions of config.ldb
-   Handle expired passwords like other PAM modules

beckerde (1):

-   Add Spanish translation

ruigo (1):

-   Add Portuguese translation

