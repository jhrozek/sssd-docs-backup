Highlights
----------

-  Removed the Data Provider process. All Data Provider backends will
   now speak directly to the responders.
-  Remove the MagicPrivateGroups option. This will be an internal
   feature of backends that support it.
-  Add first steps towards a native FreeIPA data provider.
-  Support password changing in LDAP and Kerberos providers.
-  Added Python API for managing SSSD configuration.

Detailed changes since 0.6.0
----------------------------

Dmitri Pal (10):

-  COLLECTION Adding item comparison and sorting
-  COLLECTION Realigning collection code
-  COLLECTION Making iterations pinnable
-  COLLECTION Enhancing hashing and iteration functions
-  ELAPI Event resolver
-  ELAPI Resolving message attribute
-  ELAPI Fixing warnings in the example
-  ELAPI Rename variables and functions not to use word template
-  ELAPI Fixed the host name resolution
-  ELAPI Compatibility code for getifaddr()

Jakub Hrozek (3):

-  Fix python sync operations and mem hierarchy
-  Fix error messages in tools
-  User home directories management

Martin Nagy (7):

-  Use correct talloc context in sss\_names\_init()
-  Fix potential memory leaks in the data provider
-  Resolver: Use talloc\_get\_type() for type safety
-  Use talloc to copy data from c-ares
-  Add a new set of helpful common functions for tests
-  Various improvements to the resolv test suite
-  Delete sssd-i18n.h and put it's old contents into util.h

Piotr Drąg (1):

-  Update polish translation for 0.6.0

Ralf Haferkamp (2):

-  LDAP provider needs to link against krb libraries
-  SUSE specific init script

Simo Sorce (21):

-  Tighten up permission.
-  Initial implementation of sasl bind support
-  Fix tools sync operations and mem hierarchy
-  Fix long timeout on ldap operation
-  Make dp requests more robust
-  Differentiate between search and network timeouts
-  Remove DP process
-  Start responders predictably after providers
-  Remove magicPrivateGroups option
-  Fix services startup when only LOCAL is configured
-  Make options parser available to all providers
-  Move ldap provider configuration into its own file
-  Fix offline authentication
-  Return the dp error from the providers
-  Move all ldap provider init functions
-  Move all krb5 provider init functions
-  Add first basic IPA provider
-  Always list inputs before outputs
-  Start implementing ipa specific options.
-  Better offline/enumeration behavior
-  Fix setting the schema in the ipa provider

Stephen Gallagher (24):

-  Update version to 0.6.0
-  Fix infinite loop with empty group enumeration
-  Updating release script to use the VERSION file
-  Change requirement on libldb to libldb >= 0.9.3
-  INI Add config\_from\_fd() to ini\_config
-  Remove unused btreemap code
-  Add new SSSDConfig python API
-  Add plugin configuration schema for proxy provider
-  Package SSSDConfig API
-  Clean up warnings in pysss.c
-  Remove warnings caused by
   `5e2301b8a75d10e5cbbe11e26e5192b894af6ad7 <https://fedorahosted.org/sssd/changeset/5e2301b8a75d10e5cbbe11e26e5192b894af6ad7/>`__
-  Remove two unused functions.
-  Fix segfault when using SSS tools with no local provider
-  Do not allow setting auth, access or chpass providers for LOCAL
-  Add krb5\_common.h to the list of headers to 'make dist'
-  Use Python 3-compatible sitearch and sitelib
-  Better detect installed language files
-  Clean up rpmlint errors and warnings in sssd-client package
-  Set the Default-Stop LSB option for the SSSD sysv init script
-  Fix RPM builds on older versions of rpmbuild
-  Bring SSSDConfig API options up-to-date
-  Add pam\_ctx (similar to nss\_ctx) for storing global PAM config
-  Add support for offline auth cache timeout
-  Update version to 0.7.0

Sumit Bose (28):

-  update sysdb tests to new config file version
-  add utility call check\_and\_open\_readonly
-  more documentation and test for sssd.conf
-  handle expired password during authentication
-  move password handling into subroutines
-  ask for new password if password is expired
-  remove redundant talloc\_free
-  add description of chpass\_provider option to sssd.conf man page
-  add support for server side LDAP password policies
-  add syslog message similar to pam\_unix
-  use the correct kerberos context for each target
-  fix a wrong argument to unpack\_buffer
-  add -Werror-implicit-function-declaration to default gcc flags
-  add a replacement if ldap\_control\_create is missing
-  use PYTHON\_PREFIX to install SSSDConfig python API
-  add missing %defattr to the filelist of the client package
-  make sdap\_id\_connect\_\* independent of sdap\_id\_ctx
-  send a message if a backend target is not configured
-  use old password if available during password change
-  set chpass\_provider implicit if not set explicit
-  more implicit provider target settings
-  enable debugging of krb5\_child
-  Check for expired passwords in LDAP provider
-  added generic LDAP search sdap\_get\_generic\_send/\_recv
-  add store/search/delete interface for custom sysdb objects
-  update krb5 option handling to new option scheme
-  update ipa auth options to new option scheme
-  fix a compiler warning about redefinition of DEBUG
