.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__

      #. `New Features <#NewFeatures>`__
      #. `Important Bugfixes <#ImportantBugfixes>`__

   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

New Features
~~~~~~~~~~~~

-  Support for overriding home directory, shell and primary GID locally
-  Properly honor TTL values from SRV record lookups
-  Support non-POSIX groups in nested group chains (for RFC2307bis LDAP
   servers)

Important Bugfixes
~~~~~~~~~~~~~~~~~~

-  Properly escape IPv6 addresses in the failover code
-  Do not crash if inotify fails (e.g. resource exhaustion)
-  Don't add multiple TGT renewal callbacks (too many log messages)

Detailed Changelog
------------------

Jakub Hrozek (15):

-  Add utility function to return IP address as string
-  Add a utility function to escape IPv6 address for use in URIs
-  Use escaped IP addresses in LDAP provider
-  Escape IPv6 IP addresses in the IPA provider
-  Add a new option to override primary GID number
-  Add a new option to override home directory value
-  Add new options to override shell value
-  Add new resolv\_hostent data structure and utility functions
-  Resolve hosts by name from files into resolv\_hostent
-  Resolve hosts by name from DNS into resolv\_hostent
-  Switch resolver to using resolv\_hostent and honor TTL
-  Provide TTL structure names for c-ares < 1.7
-  Test NULL server hostname in fail over tests
-  Log nsupdate message
-  Don't pass NULL to printf for TLS errors

Jan Zeleny (4):

-  Added sysdb\_attrs\_get\_bool() function
-  Non-posix group processing - sysdb changes
-  Non-posix group processing - ldap provider and nss responder
-  Fall back to polling when inotify fails

Kaushik Banerjee (1):

-  Changing default to Default for consistency

Stephen Gallagher (6):

-  Update version to 1.5.9
-  Fix typo in initgroups negative cache check
-  Ensure that SSSD always Requires: the primary-arch sssd-client
-  Fix bad merge
-  Clear up -Wunused-but-set-variable warnings
-  Updating translation files for SSSD 1.5.9

Sumit Bose (7):

-  Add online callback only once for TGT renewal
-  Delete cached ccache file if password is expired
-  Do not check pwdAttribute
-  Add sockaddr\_storage to sdap\_service
-  Add sdap\_call\_conn\_cb() to call add connection callback directly
-  Use name based URI instead of IP address based URIs
-  Use ldap\_init\_fd() instead of ldap\_initialize() if available
