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

-  Fixed a potential segfault when SRV records are used to discover
   services
-  The client libraries now use robust mutexes to avoid a potential
   deadlock if a thread was cancelled while holding a mutex
-  Do not return an error when the SELinux support is not configured
-  Fixed returning an error to the PAM stack when the SSSD was
   performing authentication but the kpasswd server was unreachable
-  The SSSD used to skip a whole nesting level instead of a single
   already processed group when loading nested group membership
   structure
-  Added support for terminating idle connections and make the idle
   timeout configurable
-  The sss\_ssh\_knownostsproxy command no longer aborts when processing
   a host without DNS records
-  The shadowLastChange attribute is noe correctly updated with days
   since the Epoch, not seconds

Tickets Fixed
-------------

-  `​https://fedorahosted.org/sssd/ticket/1356 <https://fedorahosted.org/sssd/ticket/1356>`__
   SSH: Don't abort connection in sss\_ssh\_knownhostsproxy when DNS
   records are missing
-  `​https://fedorahosted.org/sssd/ticket/1271 <https://fedorahosted.org/sssd/ticket/1271>`__
   Use HTML\_TIMESTAMP instead of HTML\_FOOTER\_DESCRIPTION
-  `​https://fedorahosted.org/sssd/ticket/1360 <https://fedorahosted.org/sssd/ticket/1360>`__
   Provide "service filter" for SELinux context
-  `​https://fedorahosted.org/sssd/ticket/1354 <https://fedorahosted.org/sssd/ticket/1354>`__
   Add support for terminating idle connections
-  `​https://fedorahosted.org/sssd/ticket/1452 <https://fedorahosted.org/sssd/ticket/1452>`__
   KRB5: Only return PAM error for unreachable kpasswd when performing
   chpass
-  `​https://fedorahosted.org/sssd/ticket/1419 <https://fedorahosted.org/sssd/ticket/1419>`__
   Fixed wrong number in shadowLastChange
-  `​https://fedorahosted.org/sssd/ticket/1460 <https://fedorahosted.org/sssd/ticket/1460>`__
   Use PTHREAD\_MUTEX\_ROBUST to avoid deadlock in the client
-  `​https://fedorahosted.org/sssd/ticket/1515 <https://fedorahosted.org/sssd/ticket/1515>`__
   KRB5: Return PAM\_AUTH\_ERR on incorrect password
-  `​https://fedorahosted.org/sssd/ticket/1364 <https://fedorahosted.org/sssd/ticket/1364>`__
   FO: Check server validity before setting status

Detailed Changelog
------------------

Jakub Hrozek (8):

-  Use HTML\_TIMESTAMP instead of HTML\_FOOTER\_DESCRIPTION
-  Send the correct enumeration request
-  Process all groups from a single nesting level
-  SYSDB: Make sysdb\_attrs\_get\_el\_int() public
-  KRB5: Only return PAM error for unreachable kpasswd when performing
   chpass
-  Use PTHREAD\_MUTEX\_ROBUST to avoid deadlock in the client
-  KRB5: Return PAM\_AUTH\_ERR on incorrect password
-  FO: Check server validity before setting status

Jan Cholasta (3):

-  SSH: Update sss\_ssh\_knownhostsproxy manual page
-  SSH: Supress error message output in sss\_ssh\_knownhostsproxy
-  SSH: Don't abort connection in sss\_ssh\_knownhostsproxy when DNS
   records are missing

Jan Zeleny (2):

-  Provide "service filter" for SELinux context
-  Fixed wrong number in shadowLastChange

Shantanu Goel (4):

-  Set return errno to the value prior to calling close().
-  Log message if close() fails in destructor.
-  Do not send SIGPIPE on disconnection
-  Add support for terminating idle connections

Stephen Gallagher (2):

-  Bumping version to 1.8.5
-  Make the client idle timeout configurable

Timo Aaltonen (1):

-  Move SELinux processing from session to account PAM stack
