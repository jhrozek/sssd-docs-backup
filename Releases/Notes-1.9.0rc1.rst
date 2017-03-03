Highlights
----------

-  This is a bugfix release. No new features have been added. The most
   important bugs fixed include:
-  Potential crash when one of two parallel requests would expire the
   list of servers resolved from a SRV query
-  Fixed a crash that occured when a service was requested by both name
   and protocol
-  A sudo rules refresh is only scheduled when the sudo service is
   actually configured.
-  The evaluation of default SELinux rules was changed to match the IPA
   server expectations

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1331 </sssd/ticket/1331>`__
    Off-by-one error in sss\_hmac\_sha1
`#1364 </sssd/ticket/1364>`__
    [abrt] sssd-1.8.3-11.fc16: set\_server\_common\_status: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)
`#1438 </sssd/ticket/1438>`__
    SSSD crashes at boot time
`#1452 </sssd/ticket/1452>`__
    Authentication fails if kpasswd cannot be resolved
`#1454 </sssd/ticket/1454>`__
    if allocation fails, sss\_mmap\_cache\_init may dereference NULL
    pointer
`#1458 </sssd/ticket/1458>`__
    Full sudo refresh is scheduled even if there is no sudo responder
`#1466 </sssd/ticket/1466>`__
    Proxy: Cannot retrieve an user after a group he is a member of was
    retrieved
`#1467 </sssd/ticket/1467>`__
    enumeration is broken in the proxy provider
`#1479 </sssd/ticket/1479>`__
    Hbac logs show wrong rule name granting access
`#1486 </sssd/ticket/1486>`__
    [abrt] sssd-1.8.4-14.fc17: sss\_ldap\_init\_send: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)
`#1496 </sssd/ticket/1496>`__
    [abrt] sssd-1.8.4-14.fc17: ldap\_pvt\_sasl\_getmechs: Process
    /usr/libexec/sssd/sssd\_be was killed by signal 11 (SIGSEGV)
`#1505 </sssd/ticket/1505>`__
    sudo with sss backend should use ipa\_hostname
`#1509 </sssd/ticket/1509>`__
    libsss\_sudo is not updated when yum update sssd is called
`#1513 </sssd/ticket/1513>`__
    Change the processing of the SELinux default map
`#1515 </sssd/ticket/1515>`__
    pam\_sss report System Error on wrong password
`#1516 </sssd/ticket/1516>`__
    krb5\_mod\_ccname should cancel the transaction at one place only
`#1519 </sssd/ticket/1519>`__
    membership of IPA hostgroups is not evaluated when treating them as
    netgroups

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (12):

-  Bumping version for the 1.9.0 beta 7 release
-  libsss\_sudo should have a versioned dependency on SSSD
-  KRB5: cancel the sysdb transaction on one place only
-  KRB5: Return PAM\_AUTH\_ERR on incorrect password
-  RPM:
   `BuildRequire? <https://docs.pagure.org/sssd-test2/BuildRequire.html>`__
   selinux-policy-targeted
-  SYSDB: NULL-terminate the output of sysdb\_get\_{ranges,subdomains}
-  KRB5: Add a missing string argument
-  NSS: Fix off-by-one error in parse\_getservbyname
-  FO: Check server validity before setting status
-  DB: Always write the SELinux object to sysdb
-  SELinux: Always use the default if it exists on the server
-  Updating the translations for the 1.9.0 RC1 release

Ondrej Kos (1):

-  Out-of-bounds read fix in hmac-sha-1

Pavel Březina (3):

-  netgroup: resolve hostgroup membership correctly
-  be\_process\_init(): free ctx on error
-  backend: initialize sudo only when it is enabled in services

Simo Sorce (1):

-  Remove obsolete comment
