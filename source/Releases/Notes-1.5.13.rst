Highlights
----------

-  Fixes a serious issue with LDAP connections when the communication is
   dropped (e.g. VPN disconnection, waking from sleep)
-  SSSD is now less strict when dealing with users/groups with multiple
   names when a definitive primary name cannot be determined
-  The LDAP provider will no longer attempt to canonicalize by default
   when using SASL. An option to re-enable this has been provided.
-  Fixes for non-standard LDAP attribute names (e.g. those used by
   Active Directory)
-  Three HBAC regressions have been fixed.

Detailed Changelog
------------------

Jakub Hrozek (5):

-  Prevent segfault if vetoed\_shells are specified without
   allowed\_shells
-  Handle timeout during sss\_ldap\_init\_send
-  Return the first value of name if the multivalued name attribute does
   not match RDN
-  Add LDAP provider option to set LDAP\_OPT\_X\_SASL\_NOCANON
-  Use the default Kerberos realm for LDAP with GSSAPI auth

Ralf Haferkamp (1):

-  Allow the O\_NONBLOCK flag to be reset correctly

Stephen Gallagher (6):

-  Bumping version to 1.5.13
-  Use sysdb attribute name for GID, not LDAP attribute
-  HBAC: Handle saving groups that have no members
-  HBAC: Use of hostgroups for targethost or sourcehost was broken
-  HBAC: Properly skip all non-group memberOf entries
-  Updating translation files for SSSD 1.5.13

Sumit Bose (1):

-  Improve password policy error code and message
