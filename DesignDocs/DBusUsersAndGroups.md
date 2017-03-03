D-Bus Interface: Users and Groups {#D-BusInterface:UsersandGroups}
=================================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2150](https://fedorahosted.org/sssd/ticket/2150){.ext-link}

Related design page(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/wiki/DesignDocs/DBusResponder](https://docs.pagure.org/sssd-test2/DesignDocs/DBusResponder.html){.ext-link}

### Problem statement {#Problemstatement}

This design document describes how users and groups are represented on
SSSD D-Bus interface.

### Use cases {#Usecases}

-   Listing users and groups in access control GUI
-   Obtaining extra information about user that is not available through
    standard APIs

D-Bus Interface {#D-BusInterface}
---------------

### org.freedesktop.sssd.infopipe.Users {#org.freedesktop.sssd.infopipe.Users}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface}

-   /org/freedesktop/sssd/infopipe/Users

#### Methods {#Methods}

-   o FindByName(s:name)
-   o FindByID(u:id)
-   ao ListByName(s:filter, u:limit)
    -   filter: possible asterisk as wildcard character; minimum length
        is required
    -   limit: maximum number of entries returned, 0 means unlimited or
        to maximum allowed number
-   ao ListByDomainAndName(s:domain\_name, s:filter, u:limit)
    -   filter: possible asterisk as wildcard character; minimum length
        is required
    -   limit: maximum number of entries returned, 0 means unlimited or
        to maximum allowed number

#### Signals {#Signals}

None.

#### Properties {#Properties}

None.

### org.freedesktop.sssd.infopipe.Users.User {#org.freedesktop.sssd.infopipe.Users.User}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface1}

-   /org/freedesktop/sssd/infopipe/Users/\$DOMAIN/\$UID

#### Methods {#Methods1}

-   void UpdateGroupsList()
    -   Performs initgroups on the user.

#### Signals {#Signals1}

None.

#### Properties {#Properties1}

-   s name
    -   The user's login name.
-   u uidNumber
    -   The user's UID.
-   u gidNumber
    -   The user's primary GID.
-   s gecos
    -   The user's real name.
-   s homeDirectory
    -   The user's home directory
-   s loginShell
    -   The user's login shell
-   a{sas} extraAttributes
    -   Extra attributes as configured by the SSSD. The key is the
        attribute name, value is array of strings that contains the
        values.
-   ao groups
    -   An array of object paths representing the groups the user is a
        member of.

### org.freedesktop.sssd.infopipe.Groups {#org.freedesktop.sssd.infopipe.Groups}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface2}

-   /org/freedesktop/sssd/infopipe/Groups

#### Methods {#Methods2}

-   o FindByName(s:name)
-   o FindByID(u:id)
-   ao ListByName(s:filter, u:limit)
    -   filter: possible asterisk as wildcard character; minimum length
        is required
    -   limit: maximum number of entries returned, 0 means unlimited or
        to maximum allowed number
-   ao ListByDomainAndName(s:domain\_name, s:filter, u:limit)
    -   filter: possible asterisk as wildcard character; minimum length
        is required
    -   limit: maximum number of entries returned, 0 means unlimited or
        to maximum allowed number

#### Signals {#Signals2}

None.

#### Properties {#Properties2}

### org.freedesktop.sssd.infopipe.Groups.Group {#org.freedesktop.sssd.infopipe.Groups.Group}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface3}

-   /org/freedesktop/sssd/infopipe/Groups/\$DOMAIN/\$GID

#### Methods {#Methods3}

None.

#### Signals {#Signals3}

None.

#### Properties {#Properties3}

-   s name
    -   The group's name.
-   u gidNumber
    -   The groups's primary GID.
-   ao users
    -   A list of the group's member user objects.
-   ao groups
    -   A list of the group's member group objects.

### Overview of the solution {#Overviewofthesolution}

New D-Bus interfaces will be implemented in the IFP responder.

Find methods perform online lookup if the entry is missing or expired.

Listing methods always perform online lookup to ensure that even
recently added entries are in the list.

Listing methods can return only a limited number of entries. Number of
entries returned can be controlled by **limit** parameter with hard
limit set in sssd.conf with a new configuration option
**filter\_limit**. This option can be present in \[ifp\] and \[domain\]
sections to set this limit for data provider filter searches (\[domain\]
section) and also global hard limit for the listing methods itself
(\[ifp\] section). This limit is supposed to improve performace with
large databases so we process only a small number of records. If the
option is set to 0, the limit is disabled.

Filter may contain only '\*' asterisk as a wildcard character, it does
not support complete set of regular expressions. The asterisk can be
present on the beginning of the filter '\*filter', its end 'filter\*',
both sides '\*filter\*' or even in the middle '\*fil\*ter\*', since it
is supported by both LDAP and LDB. However, only prefix-filter
('filter\*'), can take the performace boost from indices so other filter
may not perform so good with huge databases.

### Configuration changes {#Configurationchanges}

The following options will be created in the \[ifp\] and \[domain\]
sections:

-   wildcard\_search\_limit (uint32)

See the [wildcard refresh design
page?](https://docs.pagure.org/sssd-test2/WildcardRefresh.html){.missing
.wiki} for more details.

### How To Test {#HowToTest}

Call the D-Bus methods and properties. For example with **dbus-send**
tool.

### Authors {#Authors}

-   Jakub Hrozek
    &lt;[[​]{.icon}jhrozek@redhat.com](mailto:jhrozek@redhat.com){.mail-link}&gt;
-   Pavel Březina
    &lt;[[​]{.icon}pbrezina@redhat.com](mailto:pbrezina@redhat.com){.mail-link}&gt;

