Important sudo attributes {#Importantsudoattributes}
=========================

-   **sudoHost** - to what host does the rule apply
    -   *ALL* - all hostnames
    -   *hostname*
    -   *IP address*
    -   *+netgroup*
    -   *regular expression* - contains one of "\\?\*\[\]"
-   **sudoUser** - to what user does the rule apply
    -   *username*
    -   *\#uid*
    -   *%group*
    -   *+netgroup*
-   **sudoOrder** - rules ordering
-   **sudoNotBefore** and **sudoNotAfter** - time constraints

Complete LDAP schema can be found
[[​]{.icon}here](http://www.gratisoft.us/sudo/man/1.8.4/sudoers.ldap.man.html){.ext-link}.

Common {#Common}
======

Per host update {#Perhostupdate}
---------------

Per host update returns all rules that:

-   sudoHost equals to ALL
-   direct match with sudoHost (by hostname or address)
-   contains regular expression (will be filtered by sudo)
-   contains netgroup (will be filtered by sudo)

Hostname match is performed in sudo source in
*plugin/sudoers/ldap.c/sudo\_ldap\_check\_host()*.

Per user update {#Peruserupdate}
---------------

Per user update returns all rules that:

-   sudoUser equals to ALL
-   direct match with username, \#uid or %group names
-   contains +netgroup (will be filtered by sudo)

Username match is performed via LADP filter in sudo source in
*plugin/sudoers/ldap.c/sudo\_ldap\_result\_get()*.

Smart refresh {#Smartrefresh}
-------------

Download only rules that were modified or newly created since the last
refresh.

Implementation {#Implementation}
==============

We will be looking for modified and newly created rules in short
intervals. Expiration of the rules is handled per user during the
execution time of *sudo*. We will also do periodical full refresh to
ensure consistency even if the *sudo* command is not used.

SysDB attributes {#SysDBattributes}
----------------

**sudoLastSmartRefreshTime** on *ou=SUDOers* - when the last smart
refresh was performed\
**sudoLastFullRefreshTime** on *ou=SUDOers* - when the last full refresh
was performed\
**sudoNextFullRefreshTime** on *ou=SUDOers* - when the next full is
scheduled\
**dataExpireTimestamp** on each rule - when the rule will be considered
as expired

Data provider {#Dataprovider}
-------------

Data provider will be performing following actions:

### A. Periodical download of changed or newly created rules (per host smart refresh) {#A.Periodicaldownloadofchangedornewlycreatedrulesperhostsmartrefresh}

Interval is configurable via **ldap\_sudo\_changed\_refresh\_interval**
(default: 15 minutes)\
Enable *modifyTimestamp* with **ldap\_sudo\_modify\_timestamp\_enabled**
(default: false)

1.  **if** server has changed **then** do **C**
2.  **else if** *entryUSN* is available **then**
    1.  refresh rules per host, where entryUSN &gt; currentHighestUSN
    2.  **goto** 3.2.
3.  **else if** *modifyTimestamp* is enabled **then**
    1.  refresh rules per host, where entryUSN &gt; currentHighestUSN
    2.  *sudoLastSmartRefreshTime* := current time
    3.  nextrefrest := (current time +
        *ldap\_sudo\_changed\_refresh\_interval*)
    4.  **if** nextrefresh &gt;= *sudoNextFullRefreshTime* AND
        nextrefresh &lt; (*sudoNextFullRefreshTime* +
        *ldap\_sudo\_changed\_refresh\_interval*) **then**
        1.  nextrefresh := (*sudoNextFullRefreshTime* +
            *ldap\_sudo\_changed\_refresh\_interval*)
    5.  schedule next smart refresh
4.  **else** do nothing

### B. Periodical full refresh of all rules {#B.Periodicalfullrefreshofallrules}

Configurable via **ldap\_sudo\_full\_refresh\_interval** (default: 360
minutes)

1.  do **C**
2.  *sudoLastFullRefreshTime* := current time
3.  *sudoNextFullRefreshTime* := (current time +
    *ldap\_sudo\_full\_refresh\_interval*)
4.  schedule next full refresh

### C. On demand full refresh of all rules {#C.Ondemandfullrefreshofallrules}

1.  Download all rules per host
2.  Deletes all rules from the sysdb
3.  Store downloaded rule in the sysdb

### D. On demand refresh of specific rules {#D.Ondemandrefreshofspecificrules}

1.  Download the rules
2.  Delete them from the sysdb
3.  Store downloaded rule in the sysdb

Responder {#Responder}
---------

**sudo\_timed** (default: false) - filter rules by time constraints?

1.  search sysdb per user
2.  refresh all expired rules
3.  **if** any rule was deleted **then**
    1.  schedule **C** (out of band)
    2.  search sysdb per user
4.  **if** *sudo\_timed* = false **then** filter rules by time
    constraints
5.  sort rules
6.  return rules to sudo

Questions {#Questions}
=========

1.  Should we also do per user smart updates when the user runs *sudo*?
2.  Should we create a tool to force full refresh of the rules
    immediately?

