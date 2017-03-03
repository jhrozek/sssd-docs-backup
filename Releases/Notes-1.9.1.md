Highlights {#Highlights}
----------

-   The distribution tarball was fixed to include a missing file, which
    prevented "make rpms" from running correctly.
-   Handle gracefully the situation where the namingContext is
    zero-length, such as when connected to the Novell eDirectory server.
-   A new option default\_domain\_suffix was added. This option is
    mainly useful for environments whose users come from a trusted
    domain so that the user doesn't have to specify that trusted domain
    with every user lookup.
-   Many man page fixes that were held from the 1.9.0 release during the
    string freeze
-   The entries in the generated known\_hosts file are now expired
    preventing the file from growing indefinitely
-   The PID file is now created after all the SSSD services start up to
    avoid notifying the user via the init system before SSSD is able to
    handle requests.

Tickets Fixed {#TicketsFixed}
-------------

<div>

[\#1303](/sssd/ticket/1303 "SSSD is slow at startup"){.closed}
:   SSSD is slow at startup

[\#1471](/sssd/ticket/1471 "Range Retrieval: Unable to retrieve all members when filter is used in ..."){.closed}
:   Range Retrieval: Unable to retrieve all members when filter is used
    in search base.

[\#1483](/sssd/ticket/1483 "Mention ldap_schema types on newlines or comma separate them."){.closed}
:   Mention ldap\_schema types on newlines or comma separate them.

[\#1494](/sssd/ticket/1494 "ldap_chpass_update_last_change is not included in the manual page"){.closed}
:   ldap\_chpass\_update\_last\_change is not included in the manual
    page

[\#1525](/sssd/ticket/1525 "Explain default re_expression in IPA and AD provider man pages"){.closed}
:   Explain default re\_expression in IPA and AD provider man pages

[\#1529](/sssd/ticket/1529 "[RFE] Login with users from a trusted domain always requires a FQ name"){.closed}
:   \[RFE\] Login with users from a trusted domain always requires a FQ
    name

[\#1533](/sssd/ticket/1533 "Improve recreating new ccache file when the old one is not accessible any ..."){.closed}
:   Improve recreating new ccache file when the old one is not
    accessible any more

[\#1535](/sssd/ticket/1535 "Flip the default value of ldap_initgroups_use_matching_rule_in_chain"){.closed}
:   Flip the default value of
    ldap\_initgroups\_use\_matching\_rule\_in\_chain

[\#1537](/sssd/ticket/1537 "Fix sssd-ad id ranges"){.closed}
:   Fix sssd-ad id ranges

[\#1540](/sssd/ticket/1540 "[man sssd-ldap] 'ldap_access_filter'  description needs to be updated"){.closed}
:   \[man sssd-ldap\] 'ldap\_access\_filter' description needs to be
    updated

[\#1541](/sssd/ticket/1541 "Manpage has ldap_autofs_search_base as experimental feature"){.closed}
:   Manpage has ldap\_autofs\_search\_base as experimental feature

[\#1542](/sssd/ticket/1542 "User authentication using LDAP doesn't work"){.closed}
:   User authentication using LDAP doesn't work

[\#1546](/sssd/ticket/1546 "sss_seed "-h" and "--help" options should output similar results"){.closed}
:   sss\_seed "-h" and "--help" options should output similar results

[\#1548](/sssd/ticket/1548 "User authentication fails when password is read from a file using -p ..."){.closed}
:   User authentication fails when password is read from a file using -p
    option of SSS\_SEED tool.

[\#1549](/sssd/ticket/1549 "Providing invalid UID/GID values, terminates sss_seed tool without any ..."){.closed}
:   Providing invalid UID/GID values, terminates sss\_seed tool without
    any error message

[\#1553](/sssd/ticket/1553 "Improve error message of sss_seed when the domain does not exist"){.closed}
:   Improve error message of sss\_seed when the domain does not exist

[\#1554](/sssd/ticket/1554 "sss_seed should not allow blank passwords"){.closed}
:   sss\_seed should not allow blank passwords

[\#1562](/sssd/ticket/1562 "Domains overlap in range 1 - 4294967295"){.closed}
:   Domains overlap in range 1 - 4294967295

[\#1563](/sssd/ticket/1563 "Document the need to restart autofs service."){.closed}
:   Document the need to restart autofs service.

</div>

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (11):

-   Bumping the version to 1.9.1 release
-   Document ldap\_chpass\_update\_last\_change
-   sudo and autofs search bases should not be marked experimental
-   Flip the default value of
    ldap\_initgroups\_use\_matching\_rule\_in\_chain
-   Include param\_help\_py.xml in the list of po4a sources
-   Note that Range Retrieval is not supported when filter is used in
    the search base.
-   Change the log level of two DEBUG messages in check\_domain\_ranges
-   Remove unused variable
-   Check for existing pidfile before starting the providers
-   man: Note that automounter must be restarted to re-read the master
    map
-   Updating the translations for 1.9.1 release

Jan Cholasta (2):

-   SSH: Refactor sysdb and related code
-   SSH: Expire hosts in known\_hosts

Michal Zidek (7):

-   Change option to display help message in man pages.
-   sss\_seed: Option --debug did not work in sss\_seed tool.
-   sss\_seed: Show error message when interactive input fails.
-   sss\_seed: Make only first line of password file valid.
-   sss\_seed: Passwords longer then PASS\_MAX not allowed.
-   sss\_seed: Improved error message when the domain does not exist.
-   Variable in sdap\_sudo\_rules\_refresh\_send could be used,
    uninitialized.

Ondrej Kos (4):

-   sssd-ldap manpage: ldap\_scheme formatting
-   Log possibly non-randomizable ccache file template
-   Slices calculation is alway wrong for default values
-   Fix default upper limit of slices

Pavel Březina (5):

-   Fix few coding style issues
-   monitor: create pid file after all responders are started
-   remove left over principal selection
-   manpage: ldap\_access\_filter is not always mandatory
-   do not create pid file twice

Stephen Gallagher (2):

-   LDAP: Handle empty namingContexts values safely
-   BUILD: Include the patch file in the tarball

Sumit Bose (4):

-   Add new option default\_domain\_suffix
-   Use flat name for master domain as well
-   sysdb\_master\_domain\_get\_info: fix copy-and-paste error
-   Add man page section about provider specific re\_expression

