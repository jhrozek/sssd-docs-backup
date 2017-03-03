Highlights {#Highlights}
----------

-   This release contains bugfixes since the 0.99.0 release.

Detailed Changelog {#DetailedChangelog}
------------------

David O'Brien (1):

-   Copy-edit sssd-ipa man page

Dmitri Pal (5):

-   COMMON Improvements to the trace macro
-   COLLECTION Create reference to the top level collection
-   COLLECTION: Cleaning FIXME comments
-   INI: Cleaning FIXME comments.
-   INI Correcting build warnings.

Fabian Affolter (1):

-   Add German translation

Göran Uddeborg (2):

-   Add Swedish translation for sss\_client
-   Add Swedish translation for SSSD server

Jakub Hrozek (13):

-   Warn visibly about permission problems with the config file
-   Better error message when there is no local domain configured
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

Martin Nagy (3):

-   Fix egg-info file generation in the spec file
-   Add some debugging statements to fail\_over and resolver
-   Correctly restart server status after the timeout

Simo Sorce (17):

-   Fix tabs
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

Stephen Gallagher (28):

-   Remove ELAPI from build and tarball
-   Stop configuring ELAPI
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
-   Updating to version 0.99.1

Sumit Bose (13):

-   Do not include libsss\_ipa.la in rpm package
-   Immediately return a krb5 change password request when offline
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

beckerde (1):

-   Add Spanish translation

ruigo (1):

-   Add Portuguese translation

