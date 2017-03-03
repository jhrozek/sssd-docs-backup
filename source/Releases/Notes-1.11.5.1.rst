Highlights
----------

-  Fixes an issue producing the systemd unit file while building from
   the tarball.
-  Fixes a regression that caused a segfault when connecting to a Samba
   4 domain controller.

Tickets Fixed
-------------

.. raw:: html

   <div>

`#2311 </sssd/ticket/2311>`__
    sssd crashes after upgrade from 1.11.4 to 1.11.5 when using a samba4
    domain
`#2314 </sssd/ticket/2314>`__
    sssd-1.11.5-1.fc20 has wrong systmd service file

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (3):

-  Updating the version for the 1.11.6 release
-  Setting the version to 1.11.5.1 for the release
-  Updating the translations for the 1.11.5.1 release

Lukas Slebodnik (1):

-  AUTOMAKE: Do not include makefile generated files into tarball

Stephen Gallagher (1):

-  AD Provider: Fix crash looking up forest on Samba 4
