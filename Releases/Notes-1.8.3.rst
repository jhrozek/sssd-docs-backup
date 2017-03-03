.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Tickets Fixed <#TicketsFixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

-  Numerous manpage and translation updates
-  LDAP: Handle situations where the RootDSE isn't available anonymously
-  LDAP: Fix regression for users using non-standard LDAP attributes for
   user information

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1183 </sssd/ticket/1183>`__
    sssd.conf man page does not list autofs in the list of known
    services
`#1219 </sssd/ticket/1219>`__
    Warn on 'make update-po' if there are manpages not listed in
    po4a.cfg
`#1249 </sssd/ticket/1249>`__
    Unable to lookup user aliases with proxy provider.
`#1258 </sssd/ticket/1258>`__
    SSSD should attempt to get the RootDSE after binding
`#1265 </sssd/ticket/1265>`__
    document the possible performance gains of disabling referral
    chasing
`#1278 </sssd/ticket/1278>`__
    Inadequate info in man page for "ldap\_disable\_paging" feature
`#1290 </sssd/ticket/1290>`__
    No info in sssd manpages for "ldap\_sasl\_minssf"
`#1295 </sssd/ticket/1295>`__
    Fix erronous reference to the 'allow' access\_provider
`#1300 </sssd/ticket/1300>`__
    autofs: maximum key name must be PATH\_MAX
`#1307 </sssd/ticket/1307>`__
    sdap\_check\_aliases must not error when detects the same user
`#1312 </sssd/ticket/1312>`__
    group members are now lowercased in case insensitive domains
`#1315 </sssd/ticket/1315>`__
    New SSSD does not fetch renewable tickets
`#1320 </sssd/ticket/1320>`__
    Auth fails for user with non-default attribute names

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (14):

-  man: document that referral chasing might bring performance penalty
-  pam\_sss: improve error handling in SELinux code
-  Remove the "command" option from documentation
-  autofs: Raise the maximum key length to PATH\_MAX
-  MAN: timeout can be specified for services, too
-  MAN: document the hostid and autofs providers
-  proxy: Canonicalize user and group names
-  proxy: new option proxy\_fast\_alias
-  sdap\_check\_aliases must not error when detects the same user
-  Document sss\_tools better
-  Get the RootDSE after binding if not successfull before
-  confdb\_get\_bool needs a TALLOC\_CTX in sssd-1.8
-  Lowercase group members in case-insensitive domains
-  Read sysdb attribute name, not LDAP attribute map name

Marco Pizzoli (1):

-  Two manual pages fixes

Pavel Březina (1):

-  sudo api: check sss\_status instead of errnop in
   sss\_sudo\_send\_recv\_generic()

Stef Walter (1):

-  Fix erronous reference to the 'allow' access\_provider

Stephen Gallagher (6):

-  Bumping version to 1.8.3
-  MAN: Improve ldap\_disable\_paging documentation
-  MAN: Add ldap\_sasl\_minssf to the manpage
-  Update translation files
-  Fix typo in translation file
-  Update translations for 1.8.3 release

Yuri Chornoivan (1):

-  Fix typo: retreiving->retrieving
