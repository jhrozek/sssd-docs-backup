D-Bus Interface: Domains {#D-BusInterface:Domains}
========================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2187](https://fedorahosted.org/sssd/ticket/2187){.ext-link}

Related design page(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/wiki/DesignDocs/DBusResponder](https://docs.pagure.org/sssd-test2/DesignDocs/DBusResponder.html){.ext-link}

### Problem statement {#Problemstatement}

This design document describes how domain objects are exposed on the
bus.

D-Bus Interface {#D-BusInterface}
---------------

### org.freedesktop.sssd.infopipe.Domains {#org.freedesktop.sssd.infopipe.Domains}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface}

-   /org/freedesktop/sssd/infopipe/Domains

#### Methods {#Methods}

-   ao List()
    -   Returns list of domains.
-   ao FindByName(s:domain\_name)
    -   Returns object path of *domain\_name*.

#### Signals {#Signals}

None.

#### Properties {#Properties}

None.

### org.freedesktop.sssd.infopipe.Domains.Domain {#org.freedesktop.sssd.infopipe.Domains.Domain}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface1}

-   /org/freedesktop/sssd/infopipe/Domains/\*

#### Methods {#Methods1}

-   ao ListSubdomains()
    -   Returns all subdomains associated with this domain.

#### Signals {#Signals1}

None.

#### Properties {#Properties1}

-   **property** String name
    -   The name of this domain. Same as the domain stanza in the
        sssd.conf
-   **property** String\[\] primary\_servers
    -   Array of primary servers associated with this domain
-   **property** String\[\] backup\_servers
    -   Array of backup servers associated with this domain
-   **property** Uint32 min\_id
    -   Minimum uid and gid value for this domain
-   **property** Uint32 max\_id
    -   Maximum uid and gid value for this domain
-   **property** String realm
    -   The Kerberos realm this domain is configured with
-   **property** String forest
    -   The domain forest this domain belongs to
-   **property** String login\_format
    -   The login format this domain expects.
-   **property** String fully\_qualified\_name\_format
    -   The format of fully qualified names this domain uses
-   **property** Boolean enumerable
    -   Whether this domain can be enumarated or not
-   **property** Boolean use\_fully\_qualified\_names
    -   Whether this domain requires fully qualified names
-   **property** Boolean subdomain
    -   Whether the domain is an autodiscovered subdomain or a
        user-defined domain
-   **property** ObjectPath parent\_domain
    -   Object path of a parent domain or empty string if this is a root
        domain

### How To Test {#HowToTest}

Call the D-Bus methods and properties. For example with **dbus-send**
tool.

### Authors {#Authors}

-   Pavel Březina
    &lt;[[​]{.icon}pbrezina@redhat.com](mailto:pbrezina@redhat.com){.mail-link}&gt;

