Highlights
----------

-  This release focuses primarily on bug fixes.
-  The release addresses an issue where the SSSD was not able to detect
   all domains in the forest if it was connected to an AD DC which was
   not the forest root
-  A new AD sudo provider was introduced. Setting ``sudo_provider=ad``
   uses the same connection options as ``id_provider=ad``, which
   simplifies the configuration for users who store sudo rules on an
   Active Directory server.
-  The ID mapping ranges are checked for collisions before being used,
   making SSSD more robust in cases where the ranges would collide
-  Password changes when using OTPs with an IPA server are now
   supported. Please note that this functionality is not present in the
   released FreeIPA versions yet.
-  Several bugs related to setting an SELinux user context from an IPA
   server were fixed

Documentation Changes
---------------------

-  A new pam\_sss option ``ignore_unknown_user`` was added. Setting this
   option makes pam\_sss return ``PAM_IGNORE`` when processing an uknown
   user instead of ``PAM_USER_UNKNOWN``. This option is mostly useful
   for BSD systems.

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1955 </sssd/ticket/1955>`__
    SSSD pam module accepts usernames with leading spaces
`#1958 </sssd/ticket/1958>`__
    [RFE] Expose the list of trusted domains to IPA
`#2153 </sssd/ticket/2153>`__
    If both IPA and LDAP are set up with enumeration on, two enum tasks
    are running
`#2218 </sssd/ticket/2218>`__
    sssd.conf man pages don't list a configuration option.
`#2226 </sssd/ticket/2226>`__
    Make SSSD compilable on systems with non-standard paths to krb5
    includes
`#2232 </sssd/ticket/2232>`__
    [freebsd] pam\_sss: add ignore\_unknown\_user option
`#2235 </sssd/ticket/2235>`__
    MAN: Remove misleading memberof example from ldap\_access\_filter
    example
`#2251 </sssd/ticket/2251>`__
    not retrieving homedirs of AD users with posix attributes
`#2252 </sssd/ticket/2252>`__
    Document that \`sssd\` cache needs to be cleared manually, if ID
    mapping configuration changes
`#2253 </sssd/ticket/2253>`__
    Check IPA idranges before saving them to the cache
`#2256 </sssd/ticket/2256>`__
    Evaluate usage of sudo LDAP provider together with the AD provider
`#2257 </sssd/ticket/2257>`__
    Setting int option to 0 yields the default value
`#2263 </sssd/ticket/2263>`__
    ipa-server-mode: Use lower-case user name component in home dir path
`#2264 </sssd/ticket/2264>`__
    SSSD Does not cache SELinux map from FreeIPA correctly
`#2270 </sssd/ticket/2270>`__
    IPA SELinux code looks for the host in the wrong sysdb subdir when a
    trusted user logs in
`#2271 </sssd/ticket/2271>`__
    sssd fails to handle expired passwords when OTP is used
`#2279 </sssd/ticket/2279>`__
    Add another Kerberos error code to trigger IPA password migration
`#2280 </sssd/ticket/2280>`__
    Double OK when starting the service
`#2282 </sssd/ticket/2282>`__
    SSSD should create the SELinux mapping file with format expected by
    pam\_selinux
`#2284 </sssd/ticket/2284>`__
    Valgrind: Invalid read of int while processing netgroup
`#2285 </sssd/ticket/2285>`__
    other subdomains are unavailable when joined to a subdomain in the
    ad forest
`#2289 </sssd/ticket/2289>`__
    Error during password change
`#2293 </sssd/ticket/2293>`__
    configure time variables not expanded when running ./configure
`#2300 </sssd/ticket/2300>`__
    RHEL7 IPA selinuxusermap hbac rule not always matching

.. raw:: html

   </div>

Detailed Changelog
------------------

Alexey Shabalin (1):

-  Use KRB5\_CFLAGS where appropriate

Jakub Hrozek (16):

-  Updating the version for the 1.11.5 release
-  IPA: Don't call tevent\_req\_post outside \_send
-  IPA: Don't fail if apply\_subdomain\_homedir returns ENOENT
-  OPTS: Allow using defaults for blobs
-  DP: Provide separate dp\_copy\_defaults function
-  MAN: Clarify the ldap\_access\_filter option further
-  MAN: Clarify that changing ID mapping options might require purging
   the cache
-  IPA: Do not save intermediate data to sysdb
-  AD: Only connect to GC for subdomain users
-  MAN: Clarify the GC support a bit
-  IPA: Use the correct domain when processing SELinux rules
-  IPA: Write SELinux usernames in the right case
-  KRB5: Do not attempt to get a TGT after a password change using OTP
-  AD: connect to forest root when downloading the list of subdomains
-  IPA: Fix SELinux mapping order memory hierarchy
-  Updating the translations for the 1.11.5 release

Lukas Slebodnik (10):

-  SPEC: Use systemd on available platforms
-  LDAP: Setup periodic task only once.
-  UTIL: Sanitize whitespaces.
-  DOC: Fix names of arguments in doxygen comments
-  AD: Continue if sssd failes to check extra members
-  SYSV: Do not call functions success and fail itself
-  IPA: Use function sysdb\_attrs\_get\_el in safe way
-  Makefile: Add missing library to the dp\_opt\_tests
-  TESTS: Link libsss\_test\_common with tevent
-  Makefile: Use alternative method to replace \*bindir

Michal Zidek (1):

-  Possible null dereference in SELinux code

Nathaniel McCallum (1):

-  Fix krb5 changepw when FAST-only preauth methods are used (like OTP)

Pete Fritchman (1):

-  PAM: add ignore\_unknown\_user option

Stef Walter (1):

-  providers: Fix types passed to dbus varargs functions

Sumit Bose (13):

-  IDMAP: add sss\_idmap\_check\_collision(\_ex)
-  IPA: refactor idmap code and add test
-  IPA: check ranges for collisions before saving them
-  libsss\_idmap: bump version-info
-  config API: add missing subdomain target to AD provider test
-  SUDO: AD provider
-  ipa-server-mode: use lower-case user name for home dir
-  IPA: Use GC for AD initgroup requests
-  IPA/KRB5: handle KRB5\_PROG\_ETYPE\_NOSUPP during IPA password
   migration
-  krb5\_child: remove unused option lifetime\_str from
   k5c\_setup\_fast()
-  krb5-child: extract lifetime settings into set\_lifetime\_options()
-  krb5\_client: rename krb5\_set\_canonicalize() to
   set\_canonicalize\_option()
-  krb5-child: add revert\_changepw\_options()
