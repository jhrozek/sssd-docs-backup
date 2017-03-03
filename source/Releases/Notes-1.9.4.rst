Highlights
----------

-  This release focused mainly on fixing regressions compared to the 1.8
   series and bugfixes for features introduced in the 1.9 release cycle.
   The release also includes two security fixes
-  A security bug assigned CVE-2013-0219 was fixed - TOCTOU race
   conditions when creating or removing home directories for users in
   local domain
-  A security bug assigned CVE-2013-0220 was fixed - out-of-bounds reads
   in autofs and ssh responder
-  The sssd\_pam responder processes pending requests after reconnect
-  A serious memory leak in the NSS responder was fixed
-  Requests that were processing group entries with DNs pointing out of
   any configured search bases were not terminated correctly, causing
   long timeouts
-  Kerberos tickets are correctly renewed even after SSSD daemon restart
-  The autofs LDAP provider correctly updates entries that changed mount
   options on the LDAP server
-  Secondary groups are now reported correctly for a user coming from a
   trusted Active Directory server
-  Kerberos principal selection was fixed to behave correctly when
   accessing an Active Directory server
-  Multiple fixes related to SUDO integration, in particular fixing
   functionality when the sssd back end process was changing its
   online/offline status
-  The pwd\_exp\_warning option was fixed to function as documented in
   the manual page

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1564 </sssd/ticket/1564>`__
    pam\_sss(crond:account): Request to sssd failed. Timer expired
`#1592 </sssd/ticket/1592>`__
    always reread the master map from LDAP
`#1620 </sssd/ticket/1620>`__
    sss\_cache: fqdn not accepted
`#1624 </sssd/ticket/1624>`__
    sudoUser group and netgroup specifications don't work
`#1626 </sssd/ticket/1626>`__
    sssd caching not working as expected for selinux usermap contexts
`#1635 </sssd/ticket/1635>`__
    investigate the behaviour of ldap\_sasl\_authid in 1.9.x
`#1655 </sssd/ticket/1655>`__
    Login fails - sssd\_be module polling fd indefinitely and gets
    killed
`#1659 </sssd/ticket/1659>`__
    sss\_userdel doesn't remove entries from in-memory cache
`#1666 </sssd/ticket/1666>`__
    IPA Trust does not show secondary groups for AD Users for commands
    like id and getent
`#1672 </sssd/ticket/1672>`__
    Error in PAC responder
`#1677 </sssd/ticket/1677>`__
    memberUid required for primary groups to match sudo rule
`#1679 </sssd/ticket/1679>`__
    Primary server status is not always reset after failover to backup
    server happened
`#1680 </sssd/ticket/1680>`__
    krb5\_kpasswd failover doesn't work
`#1682 </sssd/ticket/1682>`__
    Offline sudo denies access with expired entry\_cache\_timeout
`#1685 </sssd/ticket/1685>`__
    Negative cache timeout is not working for proxy provider
`#1687 </sssd/ticket/1687>`__
    Disallow root SSH public key authentication
`#1689 </sssd/ticket/1689>`__
    sudo: if first full refresh fails, schedule another first full
    refresh
`#1690 </sssd/ticket/1690>`__
    Option ldap\_sudo\_include\_regexp named incorrectly
`#1694 </sssd/ticket/1694>`__
    Incorrect synchronization in mmap cache
`#1699 </sssd/ticket/1699>`__
    ldap\_chpass\_uri failover fails on using same hostname
`#1701 </sssd/ticket/1701>`__
    sudo denies access with disabled ldap\_sudo\_use\_host\_filter
`#1702 </sssd/ticket/1702>`__
    sssd\_nss crashes during enumeration
`#1703 </sssd/ticket/1703>`__
    Wrong variable check in the memberof plugin
`#1704 </sssd/ticket/1704>`__
    Wrong error handler in sss\_mc\_create\_file
`#1706 </sssd/ticket/1706>`__
    segfault in async\_resolv.c
`#1708 </sssd/ticket/1708>`__
    sssd components seem to mishandle sighup
`#1710 </sssd/ticket/1710>`__
    man sssd-sudo has wrong title
`#1714 </sssd/ticket/1714>`__
    user id lookup fails for case sensitive users using proxy provider
`#1716 </sssd/ticket/1716>`__
    Make functions manipulating with mmap cache more defensive
`#1717 </sssd/ticket/1717>`__
    Limit requests coalescing in time
`#1722 </sssd/ticket/1722>`__
    crash in memory cache
`#1724 </sssd/ticket/1724>`__
    Explicit null dereferenced
`#1727 </sssd/ticket/1727>`__
    AD provider: getgrgid removes nested group memberships
`#1728 </sssd/ticket/1728>`__
    Failure in memberof can lead to failed database update
`#1730 </sssd/ticket/1730>`__
    MEmory leak in new memcache initgr cleanup function
`#1731 </sssd/ticket/1731>`__
    krb5 ticket renewal does not read the renewable tickets from cache
`#1732 </sssd/ticket/1732>`__
    clarify the disadvantages of enumeration in sssd.conf
`#1735 </sssd/ticket/1735>`__
    Failover to krb5\_backup\_kpasswd doesn't work
`#1736 </sssd/ticket/1736>`__
    Smart refresh doesn't notice "defaults" addition with OpenLDAP
`#1740 </sssd/ticket/1740>`__
    Incorrect principal searched for in keytab
`#1754 </sssd/ticket/1754>`__
    wrong filter for autofs maps in sss\_cache
`#1757 </sssd/ticket/1757>`__
    memory cache is not updated after user is deleted from ldb cache
`#1758 </sssd/ticket/1758>`__
    sssd fails to update to changes on autofs maps
`#1760 </sssd/ticket/1760>`__
    Failover to ldap\_chpass\_backup\_uri doesn't work
`#1761 </sssd/ticket/1761>`__
    sssd\_be crashes looking up members with groups outside the nesting
    limit
`#1764 </sssd/ticket/1764>`__
    Modifications using sss\_usermod tool are not reflected in memory
    cache
`#1770 </sssd/ticket/1770>`__
    ipa-client-automount: autofs failed in s390x and ppc64 platform
`#1773 </sssd/ticket/1773>`__
    SSSD should warn when pam\_pwd\_expiration\_warning value is higher
    than passwordWarning LDAP attribute.
`#1775 </sssd/ticket/1775>`__
    local provider: All member users are not returned on looking up top
    level parent group.
`#1779 </sssd/ticket/1779>`__
    Rule mismatch isn't noticed before smart refresh on ppc64 and s390x
`#1781 </sssd/ticket/1781>`__
    sssd: Out-of-bounds read flaws in autofs and ssh services responders
`#1782 </sssd/ticket/1782>`__
    TOCTOU race conditions by copying and removing directory trees
`#1783 </sssd/ticket/1783>`__
    Group lookup fails and takes ~60s to return to shell if member dn is
    incorrect
`#1787 </sssd/ticket/1787>`__
    reset the release in upstream spec before releasing 1.9.4

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (47):

-  Updating the version for the 1.9.4 release
-  SUDO: strdup the input variable
-  PAC: check the return value of diff\_git\_lists
-  SYSDB: Move misplaced assignment
-  LDAP: remove dead assignment
-  MEMBEROF: Fix copy-n-paste error
-  NSS: Fix the error handler in sss\_mc\_create\_file
-  SYSDB: More debugging during the conversion to ghost users
-  MAN: Fix the title of sssd-sudo
-  MEMBEROF: silence compilation warnings
-  Set cloexec flag for log files
-  RESOLV: Do not steal the resulting hostent on error
-  SYSDB: fix copy-n-paste error
-  SYSDB: Add API to invalidate all map objects
-  DP: invalidate all cached maps if a request for auto.master comes in
-  AUTOFS: allow removing entries from hash table
-  AUTOFS: remove all maps from hash if request for auto.master comes in
-  RESPONDERS: Create a common file with service names and versions
-  AUTOFS: Clear enum cache if a request comes in from the sss\_cache
-  Add responder\_sbus.h to noinst\_HEADERS
-  Free resources if fileno failed
-  Search for SHORTNAME$@REALM instead of fqdn$@REALM by default
-  Potential resource leak in sss\_nss\_mc\_get\_record
-  SYSDB: Remove duplicate selinux defines
-  SYSDB: Split a function to read all SELinux maps
-  SELINUX: Process maps even when offline
-  IPA: Rename IPA\_CONFIG\_SELINUX\_DEFAULT\_MAP
-  AD: replace GID/UID, do not add another one
-  AD: Add user as a direct member of his primary group
-  TOOLS: move memcache related functions to tools\_mc\_utils.c
-  TOOLS: Split querying nss responder into a separate function
-  TOOLS: Provide a convenience function to refresh a list of groups
-  TOOLS: Refresh memcache after changes to local users and groups
-  LDAP: avoid complex realloc logic in
   save\_rfc2307bis\_group\_memberships
-  autofs: Use SAFEALIGN\_SET\_UINT32 instead of SAFEALIGN\_COPY\_UINT32
-  NSS: invalidate memcache user entry on initgr, too
-  Invalidate user entry even if there are no groups
-  LDAP: Compare lists of DNs when saving autofs entries
-  TOOLS: invalidate parent groups in memory cache, too
-  Convert the value of pwd\_exp\_warning to seconds
-  TOOLS: Use openat/unlinkat when removing the homedir
-  TOOLS: Use file descriptor to avoid races when creating a home
   directory
-  SYSDB: make the sss\_ldb\_modify\_permissive function public
-  SYSDB: Expire group if adding ghost users fails with EEXIST
-  MAN: Clarify that saving users after enumerating large domain might
   be CPU intensive
-  TOOLS: Compile on old platforms such as RHEL5
-  Updating the translations for the 1.9.4 release

Jan Cholasta (2):

-  SSH: Reject requests for authorized keys of root
-  Check that strings do not go beyond the end of the packet body in
   autofs and SSH requests.

Michal Zidek (4):

-  sssd\_nss: Remove entries from memory cache if not found in sysdb
-  tools: sss\_userdel and groupdel remove entries from memory cache
-  sss\_cache: fqdn not accepted
-  sss\_userdel and sss\_groupdel with use\_fully\_qualified\_names

Ondrej Kos (4):

-  PROXY: fix negative cache
-  PROXY: fix groups caching
-  LDAP: initialize refresh function handler
-  SYSDB: Modify ghosts in permissive mode

Pavel Březina (22):

-  sudo manpage: clarify that sudoHost may contain wildcards and not
   regular expression
-  let krb5\_kpasswd failover work
-  sudo: don't get stuck in rules and smart refresh when offline
-  sysdb\_get\_sudo\_user\_info() initialize attrs on declaration
-  sudo: include primary group in user group list
-  sudo: support generalized time format
-  let ldap\_chpass\_uri failover work when using same hostname
-  try primary server after retry\_timeout + 1 seconds when switching to
   backup
-  add sdap\_sudo\_schedule\_refresh()
-  check dp error in sdap\_sudo\_full\_refresh\_done()
-  sudo: schedule another full refresh in short interval if the first
   fails
-  sudo: do full refresh when data provider is back online
-  let krb5\_backup\_kpasswd failover work
-  memcache: add macro that validates record length
-  explicit null dereferenced in sss\_nss\_mc\_get\_record()
-  memcache: make MC\_PTR\_TO\_SLOT() more readable
-  sudo smart refresh: do not include usn in filter if no valid usn is
   known
-  sudo smart refresh: fix debug message
-  let ldap\_backup\_chpass\_uri work
-  fix backend callbacks: remove callback properly from dlist
-  sudo responder: change num\_rules type from size\_t to uint32\_t
-  nested groups: fix group lookup hangs if member dn is incorrect

Simo Sorce (12):

-  Add a macro to copy with barriers
-  Allow mmap calls to gracefully return absent ctx
-  sssd\_pam: Cleanup requests cache on sbus reconect
-  responder\_dp: Add timeout to side requets
-  memberof: Prevent unneded failure case
-  sssd\_nss: Plug memory leaks
-  nss\_mc: Add extra checks when dereferencing records
-  Update free table when records are invalidated.
-  Carefully check records when forcibly invalidating
-  mmap cache: invalidate cache on fatal error
-  Remove unused header
-  Fix invalidating autofs maps

Sumit Bose (18):

-  select\_principal\_from\_keytab() look for plain input as well
-  select\_principal\_from\_keytab() do wildcard lookups after specific
   ones
-  Fix a 'shadows a global declaration' warning
-  Add default section to switch statement
-  krb5 tgt renewal: fix usage of ldb\_dn\_get\_component\_val()
-  Use struct pac\_grp instead of gid\_t for groups from PAC
-  Add find\_domain\_by\_id()
-  IDMAP: add sss\_idmap\_smb\_sid\_to\_unix()
-  Update domain ID for local domain as well
-  Always get user data from PAC
-  Save domain and GID for groups from the configured domain
-  Remote groups do not have an original DN attribute
-  Read remote groups from PAC
-  Translate LDB\_ERR\_ATTRIBUTE\_OR\_VALUE\_EXISTS to EEXIST
-  Use hash table to collect GIDs from PAC to avoid dups
-  Add tests for get\_gids\_from\_pac()
-  PAC responder: check if existing user differs
-  Refactor gid handling in the PAC responder
