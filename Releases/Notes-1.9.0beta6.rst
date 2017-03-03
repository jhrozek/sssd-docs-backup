.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Highlights <#Highlights>`__
   #. `Packaging Changes <#PackagingChanges>`__
   #. `Tickets Fixed <#TicketsFixed>`__
   #. `Detailed Changelog <#DetailedChangelog>`__

.. raw:: html

   </div>

.. code:: wiki

    ================= A security bug in 1.9.0 beta6 ===============
    =
    = Subject:          HBAC rules ignored if SELinux processing
    =                   is enabled
    =
    = CVE ID#:          CVE-2012-3462
    =
    = Summary:          A flaw in the SSSD's access-provider
    =                   logic causes the result of the HBAC
    =                   rule processing to be ignored in the
    =                   event that the access-provider is
    =                   also handling the setup of the user's
    =                   SELinux user context.
    =                   
    =
    =
    = Impact:           moderate
    =
    = Affects default
    =  configuration:   yes (IPA provider only)
    =
    = Introduced with:  1.9.0 beta6
    =
    ===============================================================

    ==== DESCRIPTION ====

    The latest development release of the SSSD is vulnerable to a security bug.

    When the SSSD is configured as an IPA client and the access provider is
    also handling the evaluation of user's SELinux user context, the result
    of Host Based Access Control rules is ignored.

    We decided not to release a full release, for two reasons:
        * the number of users running the beta is very small. Furthermore,
          the beta releases are not fully tested and suitable for production
          anyway
        * the next release - 1.9.0 RC1 is coming very soon. It is tentatively
          scheduled for 2012-08-23

    ==== WORKAROUND ====

    If you don't rely on the evaluation of user's SELinux user context, you
    can turn off their processing by setting:

        selinux_provider = none

    in the sssd.conf config file. That would cause the correct access control
    code to be returned to the PAM service.

    ==== PATCH AVAILABILITY ====

    The patch is available at:
    http://git.fedorahosted.org/cgit/sssd.git/commit/?id=ffcf27b0b773b580289d596f796aaf86c45ba920

Highlights
----------

-  A new option, override\_shell was added. If this option is set, all
   users managed by SSSD will have their shell set to its value.
-  Many fixes for the support for setting default SELinux user context
   from FreeIPA. Most notably, the SELinux mappings can now link to HBAC
   rules as the source of users and hosts they apply to.
-  Fixed a regression introduced in beta 5 that prevented LDAP SASL
   binds from working unless the value of ldap\_sasl\_minssf was
   explicitly specified.
-  The SSSD supports the concept of a Primary Server and a Back Up
   Server. Certain servers in the fail over list can be marked as back
   up only. If the SSSD switches to a back up server because a primary
   server is not available, it would later try to re-establish a
   connection to the primary server. This feature would mainly benefit
   users who configure fail over servers from different data centers or
   geographies.
-  A new command-line tool sss\_seed is available. This tool is able to
   prime the internal cache with a user record and a cached password to
   support the scenario when a user needs to log in to the client before
   the network connection to the centralized identity source is
   established, such as the first log in to a new machine.
-  In scenarios, where the SSSD is acting as an IPA client, it is able
   to discover and save the DNS domain-Kerberos realm mappings between
   an IPA server and a trusted Active Directory server.

Packaging Changes
-----------------

-  a new binary, called sss\_seed is available. The binary is installed
   to /usr/sbin/sss\_seed by default and includes its own manual page.
-  The SSSD uses a new directory to store the DNS domain - Kerberos
   realm mappings. The default location is
   /var/lib/sss/pubconf/krb5.include.d

Tickets Fixed
-------------

.. raw:: html

   <div>

`#904 </sssd/ticket/904>`__
    Create tool to seed a user for first-boot
`#1087 </sssd/ticket/1087>`__
    RFE: Allow Forcing User Shell
`#1128 </sssd/ticket/1128>`__
    Introduce the concept of a Primary Server in SSSD
`#1185 </sssd/ticket/1185>`__
    [Feature] AD Extensions
`#1318 </sssd/ticket/1318>`__
    RFE: make the NSS memory cache timeout configurable
`#1368 </sssd/ticket/1368>`__
    Missing hostid and subdomains sections in sssd-ipa.conf
`#1380 </sssd/ticket/1380>`__
    domain\_realm mappings manipulation by sssd
`#1418 </sssd/ticket/1418>`__
    document how sudo works with sssd
`#1420 </sssd/ticket/1420>`__
    sudo: provide automatic configuration of machine hostnames
`#1427 </sssd/ticket/1427>`__
    Don't refersh HBAC rules when looking up SELinux rules
`#1429 </sssd/ticket/1429>`__
    IPA session code returns error when SELinux mapping rule links to an
    HBAC rule
`#1432 </sssd/ticket/1432>`__
    Mention AD Provider in manpage of sssd.conf
`#1433 </sssd/ticket/1433>`__
    Suggested additions to manpage of sssd-ad
`#1435 </sssd/ticket/1435>`__
    SELinux specifity does not work with HBAC rules
`#1439 </sssd/ticket/1439>`__
    sss\_pam needs to write out SELinux login file during the account
    phase
`#1445 </sssd/ticket/1445>`__
    The SELinux login file needs to be created by the responder, not PAM
    module
`#1448 </sssd/ticket/1448>`__
    sss\_seed tool review issues

.. raw:: html

   </div>

Detailed Changelog
------------------

Jakub Hrozek (6):

-  Bumping version to 1.9.0 beta 6
-  Fix sysdb\_search\_selinux\_usermap\_by\_username return value
-  Fix SSSDConfigTest
-  Fix bad check
-  Create a domain-realm mapping for krb5.conf to be included
-  Update translations for 1.9.0 beta 6 release

Jan Zeleny (25):

-  Added some DEBUG statements into SELinux related code
-  Extend category support in SELinux user maps
-  Remove ipa\_selinux\_map\_merge()
-  Fix linking of HBAC rules and SELinux user maps
-  Provide counter of possible matches in SELinux IPA provider
-  Always free request in data provider PAM callback
-  Renamed session provider to selinux provider
-  Move SELinux processing from session to account PAM stack
-  Remove unused member of be\_req
-  Write SELinux config files in responder instead of PAM module
-  Modify hbac\_get\_cached\_rules() so it can be used outside of HBAC
   code
-  Support fetching of HBAC rules from sysdb in SELinux code
-  Support fetching of host from sysdb in SELinux code
-  Primary server support: introduce concept of reconnection
-  Primary server support: basic support in failover code
-  Primary server support: support for "disconnecting" connections in
   LDAP
-  Primary server support: IPA adaptation
-  Primary server support: krb5 adaptation
-  Primary server support: LDAP adaptation
-  Primary server support: AD adaptation
-  Primary server support: man page, failover section
-  Primary server support: new option in ldap provider
-  Primary server support: new options in krb5 provider
-  Primary server support: new option in IPA provider
-  Primary server support: new option in AD provider

Michal Zidek (1):

-  Added unit test for sysdb\_ssh.c

Nick Guay (1):

-  First-boot sss\_seed tool

Pavel Březina (7):

-  sdap\_sudo.c: add missing end of line in few debug messages
-  add hostid and subdomains sections in sssd-ipa.conf
-  manpage: seealso - include ssh conditionally
-  tests: allow changing cwd in all tests
-  manpage: sssd-sudo - documents how sudo works with sssd
-  sudo ldap provider: support autoconfiguration of hostnames
-  Unbreak SASL

Simo Sorce (16):

-  Change subdomain\_info
-  tests: Remove useless consts
-  80 columns police
-  Fix double semi-colons
-  Fix wrong elements used in comparison
-  Use ldb\_msg\_add\_string with bare strings
-  Fix return error and debug message
-  Make structure initializer more readable
-  80 col and style fixes
-  Use a more tractable name for subdomain request
-  Add realm paramter to subdomain list
-  Expose an initializer function from subdomain
-  Change refreshing of subdomains
-  Limit refreshes keeping track of last refresh time
-  Add online callback to enumerate subdomains
-  Add automatic periodic retrieval of subdomains

Stephen Gallagher (4):

-  MAN: List all available backends for provider options
-  MAN: Improvements to the AD provider manpage
-  NSS: Add override\_shell option
-  SYSDB: Add log message for unexpected LDB errors

Ville Skyttä (1):

-  Require and call ldconfig from subpackages if appropriate
