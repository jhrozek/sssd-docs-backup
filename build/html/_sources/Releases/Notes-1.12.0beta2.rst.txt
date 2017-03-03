.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Documentation Changes <#DocumentationChanges>`__
   #. `Tickets Fixed <#TicketsFixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

-  This releases merges the enhacements that were included in 1.11.6 and
   stabilizes the strings before releasing 1.12.0. With this beta2, SSSD
   enters a string freeze period before the final 1.12.0 release
-  Several patches that improve portability of SSSD, especially with
   consideration of BSD systems have been included
-  The sss\_usermod tool was enhanced to add or modify custom attributes
   for entries in domains configured with ``id_provider=local``. This
   feature is mostly useful for testing the InfoPipe responder without
   having to configure a remote server.
-  Fixed unit tests on big-endian architectures

Documentation Changes
---------------------

-  A new option ldap\_use\_tokengroups was added. Setting this option to
   False disables the support for tokenGroups, which is useful for
   environments that wish to restrict the group nesting level. Doing so
   with tokenGroups enabled is nontrivial since the tokenGroups
   attribute flattens the group memberships.
-  A new option homedir\_substring makes it possible to substitute a
   templatized home directory attribute for a client-side defined value

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1503 </sssd/ticket/1503>`__
    Document the IPC between different SSSD processes
`#2182 </sssd/ticket/2182>`__
    [RFE] Add the possibility to add custom attributes for the local
    provider
`#2308 </sssd/ticket/2308>`__
    document that simple access provider supports group nesting

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (6):

-  Updating the version to 1.12beta2
-  TOOLS: Allow adding and modifying custom attributes with sss\_usermod
-  TESTS: fgetc returns int, not char
-  MAN: Fix a typo in the ldap\_id\_mapping page
-  LDAP: Fix DEBUG message
-  Updating the translations for the 1.12beta2 release

Lukas Slebodnik (14):

-  UTIL: Add function sss\_parse\_name\_const
-  NSS: Refactor expand\_homedir\_template
-  NSS: Add option to expand homedir template format
-  TEST: Add test for expand homedir
-  PAM: Include header file security/pam\_appl.h
-  MAKE: Remove PAM libraries from libsss\_simple
-  CONFIGURE: Enhance detection of pam
-  PAM: Fix compilation of pam\_test\_client with openpam
-  PAM: Use fallback version of some pam macros
-  PAM: Define compatible macros for some functions.
-  PAM: add ignore\_authinfo\_unavail option
-  SDAP: Use portable constant as level in setsockopt
-  Unify usage of function gethostname
-  MAN: Add reference to manual page sssd-sudo

Pavel Březina (1):

-  man: clarify refresh\_expired\_interval

Pavel Reichl (5):

-  LDAP: fix - find primary group by gid
-  MAN: Detailed ldap\_group\_nesting\_level option
-  SDAP: Make nesting\_level = 0 to ignore nested groups
-  SDAP: Add option to disable use of Token-Groups
-  MAN: hint nested groups by simple access provider
