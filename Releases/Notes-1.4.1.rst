Highlights
----------

-  Add support for netgroups to the proxy provider
-  Fixes a minor bug with UIDs/GIDs ``>= 2^31``
-  Fixes a segfault in the kerberos provider
-  Fixes a segfault in the NSS responder if a data provider crashes
-  Correctly use sdap\_netgroup\_search\_base

Detailed Changelog
------------------

Jakub Hrozek (1):

-  Always use uint32\_t for UID/GID numbers

Moritz Baumann (1):

-  Fix misused SDAP\_SEARCH\_BASE

Piotr Drąg (1):

-  Updating pl translation

Stephen Gallagher (2):

-  Bumping version to 1.4.1 dev
-  Fix incorrect free of req in krb5\_auth.c

Sumit Bose (7):

-  Add netgroups infrastructure to proxy provider
-  Implement netgroups for proxy provider
-  Remove all nss requests after a reconnect
-  Always use talloc\_zero() to allocate cmdctx
-  Fix double free issue
-  Mention ding-libs in BUILD.txt
-  Fix two return value checks
