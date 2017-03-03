Highlights
----------

-  Fixes
   `​CVE-2010-0014 <https://bugzilla.redhat.com/show_bug.cgi?id=553233>`__

   -  When a user had a valid TGT, but the SSSD was in the offline state
      (such as after a VPN disconnect or a DoS of the KDC), SSSD would
      accept any password as valid for that user.

-  Also includes a very minor fix for an SSSDConfig API bug. **This
   patch has no impact on any system not consuming the SSSDConfig API.**

Detailed Changelog
------------------

-  Stephen Gallagher (2):

   -  Allow debug\_timestamps setting on a per-domain basis
   -  Releasing version 1.0.1

-  Sumit Bose (1):

   -  Fix return value when offline and TGT is valid
