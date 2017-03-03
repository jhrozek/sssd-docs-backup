Highlights {#Highlights}
----------

-   The Active Directory provider now includes support for Site-based
    discovery. This feature allows the Active Directory clients to find
    the most suitable Domain Controller to connect to.
-   Support for dynamic DNS updates in the Active Directory provider.
    This feature enables the clients to automatically update or refresh
    their DNS records stored in the AD server.
-   A new library, called `libsss_nss_idmap` was introduced. This
    library allows the user to convert Windows Security Identifiers
    (SIDs) to names and vice versa. The library also includes Python
    bindings.
-   Setting the SELinux context on the IPA server now also works for
    users coming from a trusted Active Directory domain
-   Fixed a serious performance issue when enumerating large number of
    users
-   The `subdomain_homedir` configuration option gained a new template
    expansion `%F` that expands to the flat name (NetBIOS name) of the
    trusted AD domain

Packaging Changes {#PackagingChanges}
-----------------

-   The SSSD python ConfigAPI was moved to its own noarch subpackage to
    make the SSSD packaging more compliant with the Fedora packaging
    guidelines
-   The `libsss_nss_idmap` library and its Python bindings are packaged
    in separate subpackages

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1625](/sssd/ticket/1625 "Confusing error messages for invalid sssd.conf"){.closed}
:   Confusing error messages for invalid sssd.conf

[\#1741](/sssd/ticket/1741 "sss_cache doesn't support subdomains"){.closed}
:   sss\_cache doesn't support subdomains

[\#1767](/sssd/ticket/1767 "unify sss_mc_set_recycled"){.closed}
:   unify sss\_mc\_set\_recycled

[\#1774](/sssd/ticket/1774 "move processing of password expiration back to PAM provider only"){.closed}
:   move processing of password expiration back to PAM provider only

[\#1784](/sssd/ticket/1784 "rewrite nested group processing to follow the tevent_req coding style"){.closed}
:   rewrite nested group processing to follow the tevent\_req coding
    style

[\#1786](/sssd/ticket/1786 "Use new interface from ding-libs ini interface"){.closed}
:   Use new interface from ding-libs ini interface

[\#1830](/sssd/ticket/1830 "make the authtok structure really opaque"){.closed}
:   make the authtok structure really opaque

[\#1839](/sssd/ticket/1839 "Incorrect *.py[co] files placement"){.closed}
:   Incorrect \*.py\[co\] files placement

[\#1844](/sssd/ticket/1844 "add a call to calculated the range for a given domain SID to libsss_idmap"){.closed}
:   add a call to calculated the range for a given domain SID to
    libsss\_idmap

[\#1848](/sssd/ticket/1848 "unused parameter in ipa_selinux handler"){.closed}
:   unused parameter in ipa\_selinux handler

[\#1860](/sssd/ticket/1860 "pidfile() may leak memory on error"){.closed}
:   pidfile() may leak memory on error

[\#1861](/sssd/ticket/1861 "potential out-of-bounds-write in sss_idmap_sid_to_dom_sid"){.closed}
:   potential out-of-bounds-write in sss\_idmap\_sid\_to\_dom\_sid

[\#1862](/sssd/ticket/1862 "negative return in files.c"){.closed}
:   negative return in files.c

[\#1864](/sssd/ticket/1864 "Bad comparisons in checks found by new Coverity instance"){.closed}
:   Bad comparisons in checks found by new Coverity instance

[\#1865](/sssd/ticket/1865 "Logically dead code in tools_util.c"){.closed}
:   Logically dead code in tools\_util.c

[\#1867](/sssd/ticket/1867 "document that AD provider is always case insensitive"){.closed}
:   document that AD provider is always case insensitive

[\#1877](/sssd/ticket/1877 "ding-libs.dhash: uninitialized pointer read"){.closed}
:   ding-libs.dhash: uninitialized pointer read

[\#1888](/sssd/ticket/1888 "freeipa 3.2 trusted ad user not listed in external group"){.closed}
:   freeipa 3.2 trusted ad user not listed in external group

[\#1889](/sssd/ticket/1889 "coverity: dead code in sudo client"){.closed}
:   coverity: dead code in sudo client

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Abhishek Singh (3):

-   cmocka unittest for find\_uid added
-   cmocka unittest for io added
-   Fix segmentation fault in test\_io.

Ariel Barria (2):

-   Allow setting krb5\_renew\_interval with a delimiter
-   Confusing error messages for invalid sssd.conf

Jakub Hrozek (38):

-   Updating the version for the 1.10 beta1 release
-   krb5 child: Use the correct type when processing OTP
-   pidfile(): Do not leak fd on error
-   Fix potential out-of-bounds write in sss\_idmap\_sid\_to\_dom\_sid
-   Return errno, not -1 on failure in files.c
-   Check for correct variable name
-   Init failover with be\_res options
-   Centralize resolv\_init, remove resolv context list
-   dyndns: Fix initializing sdap\_id\_ctx
-   Check for the correct variables
-   Allocate PAM DP request data on responder context
-   LDAP: Always fail if a map can't be found
-   Put the override\_homedir into an included xml file
-   Allow using flatname for subdomain home dir template
-   Fix simple access group control in case-insensitive domains
-   Make leak checks usable in tests that do not utilize check
-   tests: Fix the order of key/values
-   LDAP: do not invalidate pointer with realloc while processing ghost
    users
-   Convert the simple access check to new error codes
-   tests: Link the simple access tests with -ldl
-   Do not keep growing event context
-   Document the naming convention for SSSD domains
-   Document that the AD provider is case-insensitive
-   selinux: if no domain matches, make the debug message louder
-   Only try to relink ghost users if we're not enumerating
-   Display the last grace warning, too
-   Refactor dynamic DNS updates
-   Convert IPA-specific options to be back-end agnostic
-   dyndns: new option dyndns\_refresh\_interval
-   resolver: Return PTR record as string
-   dyndns: New option dyndns\_update\_ptr
-   dyndns: new option dyndns\_force\_tcp
-   dyndns: new option dyndns\_auth
-   Split out the common code from timed DNS updates
-   Active Directory dynamic DNS updates
-   AD: Always initialize ID mapping
-   Only check UPN if enterprise principals are not used
-   Updating the translations for the 1.10 beta1 release

Jan Cholasta (1):

-   Add exit status section to sss\_ssh\_\* man pages

Lukas Slebodnik (5):

-   LDAP: Fix value initialization warnings
-   Incorrect \*.py\[co\] files placement
-   Fix krbcc dir creation issue with MIT krb5 1.11
-   Default TEST\_DIR to cwd, not empty string if not set explicitly
-   SUDO: IPA provider

Michal Zidek (6):

-   Check for waitpid failure at wrong place.
-   Wrong condition after waitpid.
-   sss\_cache: support for subdomains
-   sss\_cache: Remove annoying messages
-   Inform about function duplication.
-   libsss\_idmap: function to calculate range

Ondrej Kos (3):

-   DB: Switch to new libini\_config API
-   CONFDB: prevent double free
-   IDMAP: Fix variable initialization

Pavel Březina (18):

-   resolv: add resolv\_get\_domain request to resolv utils
-   resolv: add resolv\_discover\_srv request to resolv utils
-   DNS sites support - SRV lookup plugin interface
-   DNS sites support - SRV DNS lookup plugin
-   fail over - add function to insert multiple servers to the list
-   DNS sites support - replace SRV lookup code with a plugin call
-   DNS sites support - use SRV DNS lookup plugin in all providers
-   DNS sites support - add IPA SRV plugin
-   sudo client: remove dead code
-   add fo\_discover\_servers request
-   IPA SRV plugin: use fo\_discover\_servers request
-   IPA SRV plugin: improve debugging
-   sdap: add sdap\_connect\_host request
-   add sss\_ldap\_encode\_ndr\_uint32
-   DNS sites support - add AD SRV plugin
-   dns srv plugin: compare domain names case insensitive
-   AD SRV plugin: check if site name is empty
-   fo\_discover\_servers\_send: don't crash when backup\_domain is NULL

Simo Sorce (1):

-   Further restrict become\_user drop of privileges.

Sumit Bose (21):

-   Fix and rename get\_my\_domain\_data()
-   Refactoring: remove duplicated code in nss responder
-   Allow usage of enterprise principals
-   Make IPA SELinux provider aware of subdomain users
-   Add override\_homedir.xml to po4a.cfg
-   Remove unused TALLOC\_CTX from responder\_get\_domain()
-   responder\_get\_domain: do not return disabled domains
-   responder\_get\_domain(): remove timeout calculation
-   LDAP: always store SID if available
-   Add secid filter to responder-dp protocol
-   Add two new request types to the data-provider interface
-   Add idmap context to nss context
-   Add responder\_get\_domain\_by\_id()
-   sysdb: add sysdb\_search\_object\_by\_sid()
-   Add sss\_ncache\_set\_sid() and sss\_ncache\_check\_sid()
-   Remove unused attribute list
-   Use struct to hold different types of request parameters
-   Add SID related lookups to IPA subdomains
-   Add SID related calls to the NSS responder
-   Add client library for SID related lookups
-   Add python interface to libsss\_nss\_idmap

Yuri Chornoivan (1):

-   Fix typos in man pages

