Highlights
----------

-  Fixed a regression in group enumeration since 1.7.0
-  Fixed several memory-corruption bugs
-  Finalized the ABI for the autofs support
-  Fixed a regression in the proxy provider

Detailed Changelog
------------------

Jakub Hrozek (5):

-  Fix group enumeration
-  Only fetch SELinux string if the user is found
-  Remove setent structure when callback is called
-  Allocate setent structure on state, not on the client context
-  Fix memory hierarchy when processing nested group memberships

Jan Cholasta (4):

-  Add methods for activating and deactivating services to SSSDConfig
-  Add ssh service to sssd.api.conf
-  SSH: Verify that names received from client are valid UTF-8 in
   responder
-  SSH: Build man pages conditionally

Jan Zeleny (1):

-  Fixed issue with netgroup update in IPA provider

Pavel Březina (3):

-  Improve debug messages in sysdb\_sudo\_check\_time()
-  SUDO responder: check if the input is a UTF-8 string
-  Refactor sss\_result into sss\_sudo\_result

Stephen Gallagher (13):

-  Remove dead code
-  Fix missing NULL check after malloc
-  Avoid uninitialized value comparison
-  Add missing breaks to switch statements
-  Fix uninitialized in\_transaction
-  Fix bad failure handling in be\_sudo\_handler()
-  Check for failure in sss\_packet\_grow()
-  Fix uninitialized value error in proxy provider
-  Ensure NULL-termination in get\_uid\_from\_pid()
-  Move sss\_ssh\_\* binaries to the main 'sssd' package
-  Always include all manpage XML files in the distribution tarball
-  Bumping version to 1.7.93 for beta 3
-  Fix missing %endif in sssd.spec.in

Sumit Bose (1):

-  Use curly braces in pkgconfig metadata file
