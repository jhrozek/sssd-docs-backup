SSSD Tools
==========

SSSD Takes advantage of several common tools that can be found in the
source tree.

-  `Collection <https://docs.pagure.org/sssd-test2/WikiPage/CollectionInterface.html>`__
   - a set of interfaces to manage data in sets of key-value pairs
   ***(stable)***.
-  `INI <https://docs.pagure.org/sssd-test2/WikiPage/INIInterface.html>`__
   - interface to read ini files and retrieve values from them
   ***(stable)***
-  `DHASH <https://docs.pagure.org/sssd-test2/WikiPage/DHASHInterface.html>`__
   - API that implements a hash table object ***(stable)***.
-  `Path
   Utils <https://docs.pagure.org/sssd-test2/WikiPage/PathUtils.html>`__
   - API to manage directory and file paths ***(stable)***.

All these tools now have their own `​git
repository <http://git.fedorahosted.org/git/ding-libs.git>`__, but they
still use the SSSD Trac instance for tracking issues.

NOTE: ELAPI has been moved to its own project
`​ELAPI <https://fedorahosted.org/ELAPI>`__
