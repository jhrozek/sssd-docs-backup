Highlights {#Highlights}
----------

-   Added support for netgroups to the LDAP provider
-   Performance improvements made to group processing of RFC2307 LDAP
    servers
-   Fixed nested group issues with RFC2307bis LDAP servers without a
    memberOf plugin
-   Build-system improvements to support Gentoo
-   Split out several libraries into the ding-libs tarball. Please find
    the most recent version of ding-libs on our [[​]{.icon}Releases
    page](https://docs.pagure.org/sssd-test2/Releases.html#DING-LIBSReleases){.ext-link}.
    You have to build and install ding-libs before bulding sssd.
-   Manpage reviewed and updated

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (30):

-   Fix wrong return value in HBAC time rules evaluation
-   Package systemd unit file
-   Move crypto functions into its own subdir
-   Add safe copy/move macros for uint16\_t
-   Password obfuscation utility functions
-   Fix pysss linking
-   Python bindings for obfuscation
-   sss\_obfuscate tool
-   Deobfuscate password in back ends
-   Fix assorted minor bugs in sss\_ tools
-   Fix parameter order when initializing decryption
-   Revert "Make ldap bind asynchronous"
-   Define objectclass with a constant
-   Use a different min\_id for local domain
-   Add parameter to skip cleanup in sysdb test
-   Fix sysdb\_group\_dn\_name
-   Fix sysdb\_attrs\_to\_list
-   Request the correct attribute name
-   Add KDC to the list of LDAP options
-   Report Kerberos error code from ldap\_child\_get\_tgt\_sync
-   Make ldap\_child report kerberos return code to parent
-   Initialize kerberos service for GSSAPI
-   Check for GSSAPI before attempting to kinit
-   Add sysdb\_attrs\_get\_ulong utility function
-   sysdb interface for adding incomplete groups
-   Save dummy groups to cache during initgroups
-   sysdb interface for adding fake users
-   Save dummy member users during RFC2307 getgr{nam,gid}
-   Use unsigned long for conversion to id\_t
-   set in\_transaction explicitly to false

Jan Zeleny (14):

-   Initialized return value in dp\_copy\_options()
-   Fixed potential comparison of undefined variable
-   Fixed printing of undefined value in sdap\_async\_accounts.c
-   Fixed uninialized value in proxy\_id provider
-   Cleaned some dead assignments
-   Reviewed sssd-ldap man page
-   Fixed small issue in memory context hierarchy
-   Dead assignments cleanup in providers code
-   Dead assignments cleanup in NSS responder
-   Dead assignments cleanup in memberof module
-   Dead assignments cleanup in various places in SSSD
-   Disable events on ldap fd when offline.
-   Man pages should mention supported providers
-   Move all references to ldap\_&lt;entity&gt;\_search\_base to
    "advanced" section

Martin Nagy (1):

-   Make ldap bind asynchronous

Maxim (6):

-   Fix building sssd
-   Fix configure check for ldb
-   Add gentoo distrubutions
-   Add custom pam module dir
-   Add gentoo-specific init dir
-   Remove useless /etc/dbus-1/system.d directory from installation

Ralf Haferkamp (2):

-   Shortcut for save\_group() to accept sysdb DNs as member attributes
-   Return all group members from getgr(nam|gid)

Simo Sorce (2):

-   Check if control is supported before using it.
-   Add option to limit nested groups

Stephen Gallagher (36):

-   Fix chpass operations with LDAP provider
-   Remove common directory
-   Rewrite toplevel Makefile
-   Build SSSD RPMs with external libraries
-   Remove src/Makefile.am and src/configure.ac
-   Don't build SSSDConfig API when configured with
    --without-python-bindings
-   Treat a zero-length password as a failure
-   Properly handle errors from a password change operation
-   Handle multiple simultaneous enumeration requests
-   Remove generated manpages when performing "make clean"
-   Request all group attributes during initgroups processing
-   Fix missing variable substitution in DEBUG message
-   Initgroups on a non-cached user should go to the data provider
-   Fix assorted specfile issues
-   Initialize debug\_level to zero in crypto tests
-   Return offline instead of error
-   Add common hash table setup
-   Add utility function sss\_strnlen()
-   Store entry\_cache\_timeout in sss\_domain\_info object
-   Require explicit setting of callback context for check\_cache
-   Netgroups sysdb API
-   netgroup tests
-   Rename group.c and passwd.c for clarity
-   Add support for netgroups to NSS sss\_client
-   Add negative cache features for netgroups
-   Split out some helper functions for the NSS responder
-   Add netgroup support to the NSS responder
-   Rename upgrade\_config.py and build it properly
-   Assorted specfile changes
-   Make sdap\_save\_users\_send handle zero users gracefully
-   Handle nested groups in RFC2307bis
-   Modify sysdb\_\[add|remove\]\_group\_member to accept users and
    groups
-   Add proper nested initgroup support for RFC2307bis servers
-   Updating translation files for release
-   Fix 'make distcheck' for XML documentation
-   Updating version for SSSD 1.4.0 release

Sumit Bose (21):

-   Store rootdse supported features in sdap\_handler
-   Handle host objects like other objects
-   Save all data to sysdb in one transaction
-   Use new MIT krb5 API for better password expiration warnings
-   Suppress some 'may be used uninitialized' warnings
-   Suppress some 'unchecked return value' warnings
-   Use POPT\_TABLEEND to close option table
-   Add a missing include file
-   Rename index to idx
-   Distribute XML sources instead of man-pages
-   Remove unused defines
-   Raise the required version of libdhash
-   Add missing tevent\_req\_done()
-   Return NSS\_STATUS\_RETURN instead of NSS\_STATUS\_NOTFOUND
-   Add handling of nested netgroups to nss client
-   Do not fail if netgroup exists just update the attributes
-   Add sysdb\_netgroup\_base\_dn()
-   Also return member groups to the client
-   Add infrastructure to LDAP provider for netgroup support
-   Implement netgroup support for LDAP provider
-   Avoid a global variable in netgroup client.

