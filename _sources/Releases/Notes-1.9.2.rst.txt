Highlights
----------

-  Users or groups from trusted domains can be retrieved by UID or GID
   as well
-  Several fixes that mitigate file descriptor leak during logins
-  SSH host keys are also removed from the cache after being removed
   from the server
-  Fix intermittent crash in responders if the responder was shutting
   down while requests were still pending
-  Catch an error condition that might have caused a tight loop in the
   sssd\_nss process while refreshing expired enumeration request
-  Fixed memory hierarchy of subdomains discovery requests that caused
   use-after-free access bugs
-  The krb5\_child and ldap\_child processes can print libkrb5 tracing
   information in the debug logs

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1008 </sssd/ticket/1008>`__
    Make sssd api conf file location configurable
`#1319 </sssd/ticket/1319>`__
    group lookups optimizations for IPA
`#1361 </sssd/ticket/1361>`__
    sssd\_pam file descriptor leak /var/lib/sss/pipes/private/pam
`#1499 </sssd/ticket/1499>`__
    Add details about TGT validation to sssd-krb5 man page
`#1514 </sssd/ticket/1514>`__
    [abrt] sssd-1.8.4-13.fc16: \_\_GI\_exit: Process
    /usr/libexec/sssd/sssd\_pam was killed by signal 6 (SIGABRT)
`#1539 </sssd/ticket/1539>`__
    Collect Krb5 Trace on High Debug Levels
`#1551 </sssd/ticket/1551>`__
    sssd\_nss process hangs, stuck in loop; "self restart" does recover,
    but old process hangs around using 100% CPU
`#1561 </sssd/ticket/1561>`__
    getting user/group entry by uid/gid sometimes fails
`#1569 </sssd/ticket/1569>`__
    Use pam\_set\_data to close the fd in the pam module
`#1571 </sssd/ticket/1571>`__
    sssd\_nss intermittent crash
`#1574 </sssd/ticket/1574>`__
    SSH host keys are not being removed from the cache

.. raw:: html

   </div>

Packaging Changes
-----------------

-  The libsss\_sudo-devel package no longer contains the package-config
   file. The libsss\_sudo-devel shared object has been moved to the
   libsss\_sudo package.

Detailed Changelog
------------------

E Deon Lackey (1):

-  Fix language errors in the sssd-krb5.conf man page

Jakub Hrozek (14):

-  Bumping the version to 1.9.1 release
-  Fix uninitialized pointer read in
   ssh\_host\_pubkeys\_update\_known\_hosts
-  Fix segfault when ID-mapping an entry without a SID
-  Fix memory hierarchy in subdomains discovery
-  PAM: close socket fd with pam\_set\_data
-  Couple of specfile fixes
-  Remove libsss\_sudo.pc and move libsss\_sudo.so to libsss\_sudo
-  Two fixes to child processes
-  Collect krb5 trace on high debug levels
-  PAM: fix handling the client fd in pam destructor
-  Create ghost users when a user DN is encountered in IPA
-  Only call krb5\_set\_trace\_callback on platforms that support it
-  MAN: improve wording of default\_domain parameter
-  Updating the translations for the 1.9.2 release

Jan Cholasta (1):

-  SSH: When host keys are removed from LDAP, remove them from the cache
   as well

Ondrej Kos (1):

-  Add more info about ticket validation

Pavel Březina (3):

-  do not fail if POLLHUP occurs while reading data
-  do not call dp callbacks when responder is shutting down
-  nss\_cmd\_retpwent(): do not go into infinite loop if n < 0

Sumit Bose (3):

-  Save time of last get\_domains request
-  Check for subdomains if getpwuid or getgrgid are the first requests
-  Allow extdom exop to return flat domain name as well

Thorsten Scherf (1):

-  Fixed: translation bug

Yuri Chornoivan (1):

-  Fix typos
