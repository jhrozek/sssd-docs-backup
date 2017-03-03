Highlights
----------

-  The LDAP provider no longer requires access to the LDAP RootDSE. If
   it is unavailable, we will continue on with our best guess
-  The LDAP provider will now log issues with TLS and GSSAPI to the
   syslog
-  Significant performance improvement when performing initgroups on
   users who are members of large groups in LDAP.
-  The sss\_client will now reconnect properly to the SSSD if the daemon
   is restarted.

   -  This resolves an issue causing GDM to crash when logging out of a
      user after the SSSD had been restarted.

Detailed Release Notes
----------------------

Alexander Gordeev (1):

-  Add explicit requests for several operational attrs

Dmitri Pal (1):

-  Fixing types in queue and stack interfaces

Stephen Gallagher (14):

-  Drop release requirement from versions
-  Bump libini\_config version to 0.5.1
-  Make RootDSE optional
-  Add sss\_log() function
-  Add log notifications for startup and shutdown.
-  Add syslog messages for LDAP GSSAPI bind
-  Log TLS errors to syslog
-  Add sysdb\_attrs\_to\_list() utility function
-  Add diff\_string\_lists utility function
-  Add sysdb\_group\_dn\_name utility function
-  Add dup\_string\_list() utility function
-  Add sysdb\_update\_members function
-  Clean up initgroups processing for RFC2307
-  Release SSSD 1.2.2

Sumit Bose (2):

-  Fix SASL authentication
-  Allow sssd clients to reconnect
