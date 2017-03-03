.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Tickets fixed <#Ticketsfixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

Highlights
----------

-  A security bug assigned CVE-2013-0219 was fixed - TOCTOU race
   conditions when creating or removing home directories for users in
   local domain
-  Monitoring and restarting child processes was made more robust
-  The ipa\_hbac\_support\_srchost option was backported, defaulting to
   false.
-  The limit of file descriptors a responder is allowed to open is
   configurable using the fd\_limit option
-  Idle client connections are terminated in the responder

Tickets fixed
-------------

-  `​https://fedorahosted.org/sssd/ticket/1139 <https://fedorahosted.org/sssd/ticket/1139>`__
-  `​https://fedorahosted.org/sssd/ticket/1214 <https://fedorahosted.org/sssd/ticket/1214>`__
-  `​https://fedorahosted.org/sssd/ticket/1324 <https://fedorahosted.org/sssd/ticket/1324>`__
-  `​https://fedorahosted.org/sssd/ticket/1226 <https://fedorahosted.org/sssd/ticket/1226>`__
-  `​https://fedorahosted.org/sssd/ticket/1227 <https://fedorahosted.org/sssd/ticket/1227>`__
-  `​https://fedorahosted.org/sssd/ticket/1130 <https://fedorahosted.org/sssd/ticket/1130>`__
-  `​https://fedorahosted.org/sssd/ticket/1197 <https://fedorahosted.org/sssd/ticket/1197>`__
-  `​https://fedorahosted.org/sssd/ticket/1078 <https://fedorahosted.org/sssd/ticket/1078>`__
-  `​https://fedorahosted.org/sssd/ticket/1782 <https://fedorahosted.org/sssd/ticket/1782>`__

Detailed Changelog
------------------

Jakub Hrozek (8):

-  Rename fo\_get\_server\_name to fo\_get\_server\_str\_name
-  fo\_get\_server\_name() getter for a server name
-  Only do one cycle when resolving a server
-  Detect cycle in the fail over on subsequent resolve requests only
-  Try all KDCs when getting TGT for LDAP
-  HBAC: create empty groups with one NULL element
-  Process all groups from a single nesting level
-  TOOLS: Use openat/unlinkat when removing the homedir

Jan Zeleny (1):

-  Add ipa\_hbac\_support\_srchost option to IPA provider

Ondrej Kos (7):

-  Add common SIGCHLD handling for providers
-  Cancel ping-check if service goes away
-  MONITOR: use sigchld handler for monitoring SSSD services
-  Add new debug level macros
-  UTIL: Add function for atomic I/O
-  TOOLS: Use file descriptor to avoid races when creating a home
   directory
-  TOOLS: Compile on old platforms such as RHEL5

Shantanu Goel (4):

-  Set return errno to the value prior to calling close().
-  Log message if close() fails in destructor.
-  Do not send SIGPIPE on disconnection
-  Add support for terminating idle connections

Stephen Gallagher (14):

-  Bumping version to 1.5.17
-  Fix potential resource leak in backup\_file.c
-  Log fixes for sdap\_call\_conn\_cb
-  LDAP: Copy URI instead of pointing at failover service record
-  IPA: Detect nsupdate support for the realm directive
-  DP: Reorganize memory hierarchy of requests
-  Make the client idle timeout configurable
-  LDAP: Make sdap\_access\_send/recv public
-  IPA: Check nsAccountLock during PAM\_ACCT\_MGMT
-  Also expire connections on the privileged pipe
-  RESPONDERS: Allow increasing the file-descriptor limit
-  RESPONDERS: Make the fd\_limit setting configurable
-  Converge accept\_fd\_handler and accept\_priv\_fd\_handler
-  SYSDB: Make sysdb\_attrs\_get\_el\_int() public
