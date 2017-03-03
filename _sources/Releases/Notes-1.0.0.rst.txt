Highlights
----------

-  One serious security issue was resolved related to the kerberos
   provider.

   -  Users who authenticate against Kerberos and have cached
      credentials could log in with a zero-length password
   -  The network exposure of this bug was limited, as users logged in
      this way would not have valid network credentials (by lucky
      accident).
   -  This issue was present only in the 0.99.x preview releases and not
      in any of the stable releases (0.7.1 and earlier)

-  Stability fixes since the 0.99.1 preview release
-  Added or updated several translations
-  Fixed long-standing "I have no name!" issue with X-based terminals
-  SSSD now passes "make distcheck" cleanly
-  SSSD PAM now conforms better to standards regarding
   PAM\_PRELIM\_CHECK

Detailed Changelog
------------------

Göran Uddeborg (2):

-  Update SV translation
-  Update SV translation

Marina Latini (1):

-  Update IT translation

Martin Nagy (2):

-  Don't consider one address with different port numbers as the same
-  fail over: Change the first server pick logic

Sergei V. Kovylov (1):

-  sssd.spec for SLES

Simo Sorce (2):

-  Fix upgrade bug `#323 <https://fedorahosted.org/sssd/ticket/323>`__
-  Fix ldap child memory hierarchy and other issues

Stephen Gallagher (14):

-  Properly close STDERR when daemonizing
-  Fix tight loop in monitor
-  Don't set explicit default for "timeout" in domains
-  Fix warning in server.c
-  Raise DEBUG level of sdap\_get\_generic\_done()
-  Change default for enumeration to TRUE
-  Fix tight-loop in monitor part 2
-  Properly handle EINTR from poll()
-  Updating ES translation
-  Add DEBUG messages to getpwnam\_callback and getpwuid\_callback
-  Clarify access\_provider manpage entry
-  Do not blindly accept zero-length passwords
-  Fix broken password changes for local users
-  Release SSSD 1.0

Sumit Bose (9):

-  Use sys.exit instead of exit
-  Check for minimal version of check
-  Build python modules in builddir
-  Use --with-ldb-lib-dir while running make distcheck
-  Cleanup db files after test run
-  disable password migration code
-  Handle chauthtok with PAM\_PRELIM\_CHECK separately
-  Do not overwrite valid TGTs when offline
-  Fix for `#345 <https://fedorahosted.org/sssd/ticket/345>`__
