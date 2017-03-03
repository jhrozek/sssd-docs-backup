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

-  Add a new PAC responder for dealing with cross-realm Kerberos trusts
-  Terminate idle connections to the NSS and PAM responders
-  Switch from libunistring to glib2 for unicode support

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1163 </sssd/ticket/1163>`__
    [Feature] SSSD AD Integration Feature (Cross Realm Kerberos Trusts)
`#1354 </sssd/ticket/1354>`__
    Add support for terminating idle connections in sssd\_nss
`#1383 </sssd/ticket/1383>`__
    sssd\_nss segfaults performing netgroup lookups without a specified
    domain

.. raw:: html

   </div>

Detailed Changelog
------------------

Jan Zeleny (5):

-  Fix possible segfault in sdap\_save\_group()
-  PAC responder: add some utility functions
-  PAC responder: test suite
-  Fix re\_expression matching with subdomains
-  SELinux user maps: pick just one map

Shantanu Goel (4):

-  Set return errno to the value prior to calling close().
-  Log message if close() fails in destructor.
-  Do not send SIGPIPE on disconnection
-  Add support for terminating idle connections

Simo Sorce (2):

-  Do not leak file descriptors in client libs.
-  Add close on exec support for old platforms

Stef Walter (1):

-  Move some debug lines to new debug log levels

Stephen Gallagher (6):

-  Bumping version to 1.9.0 beta 3
-  Fix typo breaking DIR cache detection
-  Make the client idle timeout configurable
-  UTILS: Fix segfault due to sss\_parse\_name\_for\_domains
-  BUILD: Change default unicode library to glib2
-  Update translations for 1.9.0 beta 3 release

Sumit Bose (11):

-  PAC responder: add basic infrastructure
-  PAC responder: add the core functionality
-  PAC responder: support in spec file
-  PAC client: add basic support in common client code
-  PAC client: add krb5 authdata plugin
-  Add support for ID ranges
-  Add range support to PAC responder
-  Try to build PAC responder only if all dependencies are available
-  Build pac responder tests only if pac responder is build
-  Add man page section for the PAC responder
-  Set default for subdomain\_homedir
