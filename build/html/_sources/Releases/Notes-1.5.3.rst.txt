Highlights
----------

-  Support for libldb >= 1.0.0
-  Proper detection of manpage translations
-  Better support for building RPMs for RHEL5 (and other systems with
   old autotools)

Detailed Changelog
------------------

Stephen Gallagher (5):

-  Update version to 1.5.3
-  Fix module registration with newer LDB libraries.
-  Minor specfile changes
-  Detect the proper location for memberof.so
-  Fix specfile for RHEL5

Sumit Bose (4):

-  Fix handling of translated man pages in spec file
-  Make 'make check' look nice again
-  Introduce sysdb\_ldb\_connect()
-  Check LDB\_MODULES\_PATH for sysdb
