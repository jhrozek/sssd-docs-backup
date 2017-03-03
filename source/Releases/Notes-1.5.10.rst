Highlights
----------

-  Fixed a regression introduced in 1.5.9 that could result in blocking
   calls to LDAP

Detailed Changelog
------------------

Stephen Gallagher (2):

-  Bumping version to 1.5.10
-  Do not attempt to close() a file descriptor < 0

Sumit Bose (1):

-  Do not access state after tevent\_req\_done() is called.
