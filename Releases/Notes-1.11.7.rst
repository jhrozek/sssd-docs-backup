Highlights
----------

-  This release focuses on delivering bug fixes and smaller features
   backported from the 1.12 line
-  Several fixes related to retrieving the correct group memberships in
   the AD provider configured to use POSIX attributes were fixed.
-  The Active Directory provider now correctly detects Windows Server
   2012 R2. Previous versions would fall back to the slower non-AD path
   with 2012 R2.
-  Groups without full POSIX information can now be used to enroll group
   membership (fixes
   `​CVE-2014-0249 <http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0249>`__)
-  Detection of transition from offline to online state was improved,
   resulting in fewer timeouts when SSSD is offline.
-  If referrals are disabled with a config option (or by default in the
   AD provider), any returned referral would be ignored. Previously, the
   back end would switch to offline mode on encountering a referral.

Documentation Changes
---------------------

-  A new option override\_space was added. When this option is set, a
   space character in user or group names is replaced by the character
   specified in this option
-  A small random value is now added to the offline\_timeout parameter
   value to avoid flooding servers with periodical online checks

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1854 </sssd/ticket/1854>`__
    [RFE] Add option for sssd to replace space with specified character
    in LDAP group
`#2212 </sssd/ticket/2212>`__
    [RFE] Add fallback to sudoRunAs when sudoRunAsUser is not defined
    and no ldap\_sudorule\_runasuser mapping has been defined in SSSD
`#2323 </sssd/ticket/2323>`__
    Expired shadow policy user(shadowLastChange=0) is not prompted for
    password change
`#2343 </sssd/ticket/2343>`__
    CVE-2014-0249 sssd: incorrect expansion of group membership when
    encountering a non-POSIX group [fedora-all]
`#2345 </sssd/ticket/2345>`__
    tokengroups do not work with id\_provider=ldap
`#2349 </sssd/ticket/2349>`__
    public key validator is too strict and does not allow newlines
    anywhere in the public key string, not even at the end
`#2355 </sssd/ticket/2355>`__
    Requests queued during transition from offline to online mode
`#2360 </sssd/ticket/2360>`__
    The SSSD dbus service should retry system bus connection if it fails
`#2364 </sssd/ticket/2364>`__
    RFE: Be able to configure sssd to honor openldap account lock to
    restrict access via ssh key
`#2377 </sssd/ticket/2377>`__
    sudo: invalid sudoHost filter with asterisk
`#2380 </sssd/ticket/2380>`__
    Race condition in the client code
`#2383 </sssd/ticket/2383>`__
    dereferencing control failure against openldap server
`#2385 </sssd/ticket/2385>`__
    ad: group membership is empty when id mapping is off and tokengroups
    are enabled
`#2389 </sssd/ticket/2389>`__
    Problems with tokengroups and ldap\_group\_search\_base
`#2390 </sssd/ticket/2390>`__
    Failover does not always happen from SRV to hostname resolution(via
    /etc/hosts)
`#2391 </sssd/ticket/2391>`__
    sssd\_be segfaults in ldb\_msg\_find\_element
`#2397 </sssd/ticket/2397>`__
    Auth fails when space in username is replaced with character set by
    override\_default\_whitespace
`#2399 </sssd/ticket/2399>`__
    RHEL6.6 sssd not running after upgrade
`#2400 </sssd/ticket/2400>`__
    sssd can't retrieve sudo rules when using the
    "default\_domain\_suffix" option
`#2401 </sssd/ticket/2401>`__
    clarify the offline timeout in man page
`#2402 </sssd/ticket/2402>`__
    IFP: FQDN lookups are broken
`#2405 </sssd/ticket/2405>`__
    use-after-free in dyndns code
`#2406 </sssd/ticket/2406>`__
    Saving group membership fails if provider is AD, POSIX attributes
    are used and primary group contains the user as a member
`#2407 </sssd/ticket/2407>`__
    simple\_allow\_groups does not lookup groups from other AD domains
`#2409 </sssd/ticket/2409>`__
    On error, libnss\_sss can mistakenly close descriptors it doesn't
    "own"
`#2410 </sssd/ticket/2410>`__
    Race condition between sudo refresh
`#2418 </sssd/ticket/2418>`__
    sssd does not recognize Windows server 2012 R2's LDAP as AD
`#2421 </sssd/ticket/2421>`__
    Dereference code errors out when dereferencing entries protected by
    ACIs
`#2436 </sssd/ticket/2436>`__
    ipa user private group not found

.. raw:: html

   </div>

Detailed Changelog
------------------

Ian Lee (1):

-  Add user lookup and session dependencies to systemd service file.

Jakub Hrozek (32):

-  Updating the version for the 1.11.7 release
-  BUILD: dbusintrospectdir is not used anymore
-  IFP: Fix DEBUG messages
-  IFP: Return a specific value on failure connecting to the system bus
-  IFP: Provide a SBUS method to reconnect to sysbus
-  MONITOR: Signal
   `InfoPipe? <https://docs.pagure.org/sssd-test2/InfoPipe.html>`__ to
   reconnect on SIGUSR2
-  TOOLS: New helper tool sss\_signal
-  BUILD: Add the DBus service activation
-  IFP: Fix lookups with fully-qualified names
-  RPM: Restart service in %posttrans, not %post
-  NSS: Ignore default\_domain for netgroups
-  Only replace space with the specified substitution
-  Make the space override responder-agnostic
-  PAM: Use the override\_space option
-  IFP: Use the override\_space option
-  SUDO: Use the override\_space option
-  IPA: handle searches by SID in apply\_subdomain\_homedir
-  Revert "IPA: new attribute map for non-posix groups"
-  Revert "IPA: process non-posix nested groups"
-  Revert "IPA: try to resolve nested groups as poxix group"
-  LDAP: Do not shortcut on ret != EOK during password expiry check
-  LDAP: Split out linking primary group members into a separate
   function
-  LDAP: Don't add a user member twice when adding a primary group
-  LDAP: Use tmp\_ctx in ldap\_child for temporary data
-  LDAP: Use randomized ccname for storing credentials
-  LDAP: Add Windows Server 2012 R2 functional level
-  LDAP: Fall back to functional level of Windows Server 2003
-  LDAP: Enable tokenGroups with Windows Server 2003
-  LDAP: Ignore returned referrals if referral support is disabled
-  LDAP: Skip dereferenced entries that we are not permitted to read
-  Ignore referrals in deref and ASQ, too
-  Updating the translations for the 1.11.7 release

Jan Cholasta (1):

-  SSH: Allow newline at the end of public key values in LDAP

Lukas Slebodnik (19):

-  Don't use macro \_XOPEN\_SOURCE for function strptime
-  sss\_client: thread safe initialisation of sss\_cli\_mc\_ctx
-  sss\_client: Fix memory leak in nss\_mc\_{group,passwd}
-  LDAP: Remove unused option ldap\_netgroup\_uuid
-  LDAP: Remove unused option ldap\_group\_uuid
-  LDAP: Remove unused option ldap\_user\_uuid
-  test\_utils: Use common header file for libsss\_util tests.
-  UTIL: Add functions for replacing whitespaces.
-  NSS: Replace spaces with specified string in names.
-  dyndns\_test: Use right socket length of for IPv4 address.
-  responder-get-domains-tests: fix checking of leaks
-  test\_dyndns: Use different talloc context in wrapped functions.
-  TESTS: leak\_check functions shouldn't be called with NULL context
-  dyndns: Fix talloc hierarchy of "struct sss\_iface\_addr"
-  test\_dyndns: sss\_iface\_addr\_list\_get can return more values
-  SDAP: free subrequest in sdap\_dyndns\_update\_addrs\_done
-  SDAP: Immediately finish request for empty array
-  SDAP: Use different talloc\_context for array of names
-  SDAP: Update groups for user just once.

Michal Zidek (6):

-  ptask: Allow adding random\_offset to scheduled execution time
-  ptask: Add backoff feature to the ptask api.
-  Exit offline mode only if server is available.
-  MAN: How much time sssd spends offline
-  Add alternative objectClass to group attribute maps
-  Use the alternative objectclass in group maps.

Michal Šrubař (1):

-  LDAP SUDO: sudo provider doesn't fetch 'EntryUSN'

Nalin Dahyabhai (1):

-  sss\_client: Fix "struct sss\_cli\_mc\_ctx" reinitialize-on-errors

Nikolai Kondrashov (1):

-  build: Switch back to DISTCHECK\_CONFIGURE\_FLAGS

Pavel Březina (9):

-  sbus\_request: fix potential NULL dereference
-  ad: comment ENOENT when id mapping is disabled
-  ad: update membership after SIDs are resolved
-  sudo: fetch sudoRunAs attribute
-  sudo: use dbus array for rules refresh
-  sudo: replace asterisk with escape sequence in host filter
-  failover: set port status to not working if previous srv lookup
   failed
-  ad initgroups: continue if resolved SID is still missing
-  sudo: work with correct D-Bus iterator

Pavel Reichl (18):

-  TESTS: sss\_ssh - textual public key format
-  LDAP: tokengroups do not work with id\_provider=ldap
-  SDAP: Continue resolving SID even if some fail
-  IPA: new attribute map for non-posix groups
-  IPA: process non-posix nested groups
-  IPA: try to resolve nested groups as poxix group
-  SDAP: split sdap\_access\_filter\_get\_access\_done
-  SDAP: refactor sdap\_access\_filter\_send
-  SDAP: nitpicks in sdap\_access\_filter\_get\_access\_done
-  SDAP: refactor sdap\_access\_filter\_done
-  SDAP: don't log error on access denied
-  SDAP: refactor AC offline checks
-  SDAP: new option - DN to ppolicy on LDAP
-  SDAP: account lockout to restrict access via ssh key
-  MAN: options 'lockout' and 'ldap\_pwdlockout\_dn'
-  IPA: process non-posix nested groups
-  AD: process non-posix nested groups w/o tokenGroups
-  AD: process non-posix nested groups using tokenGroups

Sumit Bose (1):

-  Replace space: add some checks
