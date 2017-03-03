Highlights
----------

-  This release focuses on delivering bug fixes and a subset of the DBus
   interface from 1.12.
-  A new responder, called InfoPipe was added. This responder provides a
   public D-Bus interface accessible over the system bus. In this
   release, only methods for retrieving user attributes and list of
   groups were added. The full interface is being developed in the 1.12
   series. The primary consumer if this interface subset are Apache
   modules such as ``mod_lookup_identity`` or
   ``mod_intercept_form_submit``
-  Fixed bug in the AD responder that caused crashes when authenticating
   as a user from a trusted domain to a system enrolled to a trusted
   domain other than the forest root
-  A potential crash on timeout in the autofs client library was fixed.
-  Several patches that improve portability of SSSD, especially with
   consideration of BSD systems have been included

Packaging Changes
-----------------

-  The InfoPipe responder is packaged in its own subpackage

Documentation Changes
---------------------

-  The new InfoPipe responder has several configuration options. Refer
   to the sssd-ifp manual page for details.
-  The LDAP provider has a new option ldap\_user\_extra\_attrs that
   enables the administrator to extend the map of attributes downloaded
   when looking up a user. These custom attributes can then be retrieved
   with the new DBus API.
-  A new pam\_sss option ``ignore_authinfo_unavail`` was added. Setting
   this option makes pam\_sss return ``PAM_IGNORE`` when SSSD is not
   running instead of ``PAM_AUTHINFO_UNAVAIL``. This option is mostly
   useful for BSD systems.

Tickets Fixed
-------------

.. raw:: html

   <div>

`#1853 </sssd/ticket/1853>`__
    [RFE] Allow sssd to replace macro (ie. %H) with value specified in
    config file
`#2114 </sssd/ticket/2114>`__
    refresh\_expired\_interval man page doc is not clear
`#2294 </sssd/ticket/2294>`__
    In sssd.conf, setting "ldap\_group\_nesting\_level = 0" does not
    appear to work
`#2305 </sssd/ticket/2305>`__
    SSSD Crashes when storage experiences high latency
`#2312 </sssd/ticket/2312>`__
    Fails to start in interactive mode when stdin isn't a pts device
`#2322 </sssd/ticket/2322>`__
    segfault in sssd\_be when cross forest users are queried
`#2333 </sssd/ticket/2333>`__
    Expanding home directory fails when the request comes from the PAC
    responder
`#2334 </sssd/ticket/2334>`__
    Simple access fails to look up primary group when using sssd-ad
    until running the id command.

.. raw:: html

   </div>

Detailed Changelog
------------------

Alexander Bokovoy (1):

-  ipa subdomains provider: make sure search by SID works for homedir

Benjamin Franzke (1):

-  BUILD: Link libsss\_krb5\_common.so to libkeyutils.so

Jakub Hrozek (36):

-  Updating the version for the 1.11.6 development
-  LDAP: Check the LDAP handle before using it
-  AD: Do not remove non-root domains when looking up root domain
-  Remove duplicate declaration
-  UTIL: Move sss\_parse\_name\_for\_domains declaration to util.h
-  IFP: Fix a typo in the Makefile
-  IFP: Re-add the
   `InfoPipe? <https://docs.pagure.org/sssd-test2/InfoPipe.html>`__
   server
-  IFP: Connect to the system bus
-  TESTS: Create a default sss\_names\_ctx in create\_dom\_test\_ctx
-  TESTS: Split a separate common\_mock\_resp\_dp module
-  RESPONDERS: Add a new request sss\_parse\_inp\_send
-  LDAP: Fix off-by-one bug in sdap\_copy\_opts
-  LDAP: Make it possible to extend an attribute map
-  AD: Initialize user\_map\_cnt in server mode
-  Add a unit test for sss\_parse\_name\_for\_domains
-  SBUS: Generate introspection from the interface meta structure
-  SBUS: Create an sbus\_method\_meta instance for Introspection
-  IFP: Close memstream handle in introspect destructor
-  SBUS: several trivial style fixes
-  SBUS: Fix error handling condition
-  SBUS: Add a convenience function sbus\_error\_new
-  SBUS: Split out dbus\_conn\_send
-  SBUS: Add SBUS\_CONN\_TYPE\_SYSBUS
-  SBUS: Add an async request to retrieve the caller ID
-  SBUS: Refactor sbus\_message\_handler to retrieve caller ID
-  IFP: Add utility functions
-  IFP: use a list of allowed\_uids for authentication
-  IFP: Initialize negative cache timeout
-  IFP: Add
   `GetUserAttrs? <https://docs.pagure.org/sssd-test2/GetUserAttrs.html>`__
   call
-  IFP: Per-attribute ACL for users
-  SYSDB: return SYSDB\_NAME from sysdb\_initgroups
-  IFP: Add a
   `GetGroupsList? <https://docs.pagure.org/sssd-test2/GetGroupsList.html>`__
   method
-  MAN: Add sssd-ifp to the list of translatable manual pages
-  BUILD: Disable dbus tests when running distcheck
-  Updating the translations for the 1.11.6 release
-  Updating the translations again for the 1.11.6 release

Lukas Slebodnik (38):

-  AUTOMAKE: Do not include generated files into tarball
-  UTIL: Use constant instead of value for stdin.
-  MONITOR: Fix start up with empty standard input
-  BUILD: Make samba4 libraries optional
-  BUILD: Explicitly link libsss\_ad.so with sasl libs
-  sss\_autofs: Check return value of autofs make request
-  sss\_autofs: Do not try to free empty autofs context
-  man: Substitute entity values for entity references
-  TEST: Some macros aren't defined in older version of check.
-  TEST: Link ipa\_ldap\_opt test with openldap libs
-  UTIL: Add function sss\_parse\_name\_const
-  NSS: Refactor expand\_homedir\_template
-  NSS: Add option to expand homedir template format
-  TEST: Add test for expand homedir
-  SPEC: Remove duplicate sssd\_ifp.
-  SBUS: Fix warning declaration shadows a global declaration
-  Remove unused parameter from ifp\_user\_get\_attr\_handle\_reply
-  Remove unused parameter from ifp\_user\_get\_groups\_reply
-  resolv: Do not try to free addrinfo in case of error
-  CONFIGURE: Remove duplicate detection of pam
-  CRYPTO: Use unprefixed version of function stpncpy
-  PAM: macro PAM\_DATA\_REPLACE isn't available in openpam.
-  PAM: Fix problem with missing declaration.
-  UTIL: Fix order of header files.
-  LDAP: Don't use macro \_XOPEN\_SOURCE for extra features
-  PAM: add ignore\_authinfo\_unavail option
-  SDAP: Use portable constant as level in setsockopt
-  PAM: Include header file security/pam\_appl.h
-  MAKE: Remove PAM libraries from libsss\_simple
-  CONFIGURE: Enhance detection of pam
-  PAM: Fix compilation of pam\_test\_client with openpam
-  PAM: Use fallback version of some pam macros
-  PAM: Define compatible macros for some functions.
-  SBUS: Define DBUS\_ERROR\_INIT for old version of dbus
-  SBUS: Include config.h for enabling function in stdio.h
-  Unify usage of function gethostname
-  MAN: Add reference to manual page sssd-sudo
-  KRB: Prevent dereference of a null pointer

Nikolai Kondrashov (12):

-  Add cscope inverted index files to .gitignore
-  Move DEBUG macro body to debug\_fn
-  Remove extra flushing from debug message output
-  Cleanup debug\_fn
-  Make DEBUG macro definition variadic
-  Make DEBUG macro invocations variadic
-  Fixup DEBUG macro invocations update
-  Update DEBUG\* invocations to use new levels
-  Update debug levels in sss\_semanage\_error\_callback
-  Update debug level in sysdb\_check\_upgrade\_02
-  Remove DEBUG macro support for old debug levels
-  build: Switch to AM\_DISTCHECK\_CONFIGURE\_FLAGS

Pavel Březina (6):

-  man: clarify refresh\_expired\_interval
-  IFP: do not create client socket
-  tests: add confdb\_path to sss\_test\_ctx
-  sbus\_tests: fix missing invoker in initializer
-  sbus request: fix error initialization
-  SBUS: remove unused variables

Pavel Reichl (10):

-  SDAP: augmented logging for group saving
-  AD Provider: bug-fix uninitialized variable
-  AD Provider: bugfix use-after-free
-  SYSDB: augmented logging when adding new group
-  LDAP: fix - find primary group by gid
-  MAN: Detailed ldap\_group\_nesting\_level option
-  SDAP: Make nesting\_level = 0 to ignore nested groups
-  SDAP: Add option to disable use of Token-Groups
-  refactor calls of sss\_parse\_name
-  TEST: Remove unused variable

Stef Walter (13):

-  sbus: Add meta data structures and code generator
-  sbus: Add sbus\_vtable and update codegen to support it
-  nss: Stop using one DBus interface with totally different methods
-  sbus: Rework sbus to use interface metadata and vtables
-  sbus: Generate constants from interface definitions
-  sbus: Use constants to make dbus calls
-  sbus: Add struct sbus\_request to represent a DBus invocation
-  sbus: Refactor how we export DBus interfaces
-  sbus: Make sbus\_new\_server() work for non-priveleged processes
-  sbus\_tests: Add some testing of dispatch and handler code
-  sbus: Add the sbus\_request\_parse\_or\_finish() method
-  sbus: Add type-safe DBus method handlers and finish functions
-  sbus\_codegen\_tests: Add test case type-safe handler args

Sumit Bose (1):

-  Make LDAP extra attributes available to IPA and AD
