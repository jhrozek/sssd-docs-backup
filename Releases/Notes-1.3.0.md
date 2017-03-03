Highlights {#Highlights}
----------

-   All of the enhancements and bugfixes from
    [1.2.91](https://docs.pagure.org/sssd-test2/Releases/Notes-1.2.91.html){.wiki}
-   Fixes to the HBAC backend for obsolete or removed HBAC entries
-   Improvements to log messages around TLS and GSSAPI for LDAP
-   Support for building in environments using --as-needed LDFLAGS
-   Vast performance improvement for initgroups on RFC2307 LDAP servers
-   Long-running SSSD clients (e.g. GDM) will now reconnect properly to
    the daemon if SSSD is restarted

Detailed Changelog {#DetailedChangelog}
------------------

Héctor Daniel Cabrera (2):

-   Updating es translation
-   Updating es translation

Jakub Hrozek (5):

-   Fix getting default realm in the ldap child
-   Validate keytab at startup
-   Fix two problems with --as-needed
-   Fix check\_time\_rule() return value on failure
-   Return proper error value when SRV lookup fails

Piotr Drąg (1):

-   Updating pl translation

Stephen Gallagher (13):

-   Add sss\_log() function
-   Add log notifications for startup and shutdown.
-   Add syslog messages for LDAP GSSAPI bind
-   Log TLS errors to syslog
-   Require -ltalloc for tevent configure check
-   be\_pam\_handler(): Fix potential NULL dereference
-   Add sysdb\_attrs\_to\_list() utility function
-   Add diff\_string\_lists utility function
-   Add sysdb\_group\_dn\_name utility function
-   Add dup\_string\_list() utility function
-   Add sysdb\_update\_members function
-   Clean up initgroups processing for RFC2307
-   Releasing SSSD 1.3.0

Sumit Bose (2):

-   Do not treat missing HBAC rules as an error
-   Allow sssd clients to reconnect

Yuri Chornoivan (1):

-   Updating uk translation

eindenbom (1):

-   Fix IPA access backend handling of obsolete and missing HBAC
    entries:

