Highlights {#Highlights}
----------

-   Eliminated many potential bugs identified by Coverity's Integrity
    manager
-   Improvements and bugfixes to the negative cache and
    filter\_users/groups
-   Eliminated a serious tight-loop condition
-   Changed default min\_id value to 1 to avoid conflicts with many
    real-world deployments
-   Fix a bug with ldap\_access\_filter not being able to handle outer
    parentheses
-   Fix a bug in the SSSDConfig API that caused it to through unexpected
    exceptions if there were unknown entries in the configuration file
-   Properly handle the Kerberos credential cache when going offline
-   Remove the krb5\_changepw\_principal option (there are no kerberos
    implementations that use anything other than kadmin/changepw@REALM)

Detailed Release Notes {#DetailedReleaseNotes}
----------------------

Dmitri Pal (3):

-   Memory leak in case of empty value
-   Fixing NULL dereferencing in ini\_config
-   Addressing initialization issues.

Göran Uddeborg (2):

-   Updating sv translation
-   Update sv translation

Jakub Hrozek (15):

-   Man page fixes
-   Skip empty attributes with warning
-   Fix realm\_str dereference
-   Fix potential NULL dereference in sss\_groupshow
-   Fix potential NULL dereference in fail\_over.c
-   Fix Incorrect NULL check in get\_server\_common()
-   Add missing break to switch statement
-   Undocument the krb5\_changepw\_principal option
-   Remove the -g option from useradd
-   get\_uid\_from\_pid should use fstat rather than lstat
-   Fix invalid talloc\_move in groupshow
-   Fix potential resource leak in copy\_tree\_ctx()
-   Potential memory leak in \_nss\_sss\_\*\_r()
-   Check closedir call in find\_uid
-   Print correct return code

Stephen Gallagher (30):

-   Fix typo in Makefile
-   Fix broken build against older versions of OpenLDAP
-   Fix typo in Makefile.am
-   Disable connection callbacks when going online
-   Change default min\_id to 1
-   Allow ldap\_access\_filter values wrapped in parentheses
-   Properly handle read() and write() throughout the SSSD
-   Fix misuse of errno in find\_uid.c
-   Avoid potential NULL dereference
-   Properly handle missing originalMemberOf entry in initgroups
-   Don't leak directory access resources on errors in directory\_list()
-   Check the correct variable for NULL after creating timer
-   Properly check that the timeout event was created for cleanup/enum
-   Check return code of hash\_delete in proxy\_child\_destructor
-   Eliminate unused variable from pc\_init\_timeout()
-   Make sure to close varargs before returning from a function
-   Properly null-terminate socket path
-   Don't segfault if ldap\_access\_filter is unspecified
-   Add ldap\_force\_upper\_case\_realm to example AD config
-   Handle (ignore) unknown options in get\_domain() and get\_service()
-   Remove references to the DP service from the SSSDConfig API tests
-   Standardize on correct spelling of "principal" for krb5
-   Initialize len before looping to read the pidfile
-   Refactor the negative cache
-   Move setup of filter\_users and filter\_groups to negcache.c
-   Honor filter\_users in PAM
-   Fix potential resource leak in remove\_tree\_with\_ctx()
-   Fix return value from remove\_connection\_callback() destructor
-   Protect against segfault in remove\_ldap\_connection\_callbacks
-   Releasing SSSD 1.2.1

Sumit Bose (10):

-   Fix handling of ccache file when going offline
-   Compare full service name
-   Add sysdb\_attrs\_get\_string\_array()
-   Use sysdb\_attrs\_get\_string\_array() instead of
    sysdb\_attrs\_get\_el()
-   Initialize pam\_data in Kerberos child.
-   Avoid a potential double-free
-   Add a missing return value
-   Add a missing initializer
-   Add a missing break
-   Add a missing free()

