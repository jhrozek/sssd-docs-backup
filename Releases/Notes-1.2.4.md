Highlights {#Highlights}
----------

-   Resolves long-standing issues related to group processing with
    RFC2307bis LDAP servers
-   Fixed bugs in RFC2307bis group memberships related to initgroups
-   Fix tight-loop bug on systems with older OpenLDAP client libraries
    (such as Red Hat Enterprise Linux 5)

Detailed Changelog {#DetailedChangelog}
------------------

Héctor Daniel Cabrera (1):

-   Updating ES translation

Jakub Hrozek (9):

-   Fix sysdb\_group\_dn\_name
-   Fix sysdb\_attrs\_to\_list
-   Request the correct attribute name
-   End update\_members request if there's nothing to do
-   sysdb interface for adding incomplete group entries
-   Add fake groups during initgroups
-   sysdb interface for adding expired user entries
-   Shortcut for save\_group() to accept sysdb DNs as member attributes
-   Add fake users during saving of RFC2307 group

Jan Zeleny (1):

-   Disable events on ldap fd when offline.

Simo Sorce (1):

-   Add option to limit nested groups

Stephen Gallagher (8):

-   Request all group attributes during initgroups processing
-   Add common hash table setup
-   Make sdap\_save\_users\_send handle zero users gracefully
-   Handle nested groups in RFC2307bis
-   Make user argument of sysdb\_update\_members\_send a const
-   Modify sysdb\_add\_group\_member\_send to accept users and groups
-   Add proper nested initgroup support for RFC2307bis servers
-   Releasing version 1.2.4

