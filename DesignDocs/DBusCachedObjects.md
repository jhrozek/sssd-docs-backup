D-Bus Interface: Cached Objects {#D-BusInterface:CachedObjects}
===============================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2338](https://fedorahosted.org/sssd/ticket/2338){.ext-link}

Related design page(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/wiki/DesignDocs/DBusResponder](https://docs.pagure.org/sssd-test2/DesignDocs/DBusResponder.html){.ext-link}

### Problem statement {#Problemstatement}

This design document describes how objects can be marked as cached.

### Use cases {#Usecases}

-   Allow tools like graphical user management to display a list of
    users who recently logged in.

D-Bus Interface {#D-BusInterface}
---------------

### org.freedesktop.sssd.infopipe.Cache {#org.freedesktop.sssd.infopipe.Cache}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface}

-   /org/freedesktop/sssd/infopipe/Users
-   /org/freedesktop/sssd/infopipe/Groups

#### Methods {#Methods}

-   ao List()
-   ao ListByDomain(s:domain\_name)
    -   Returns list of objects that contains *cached* attribute.

#### Signals {#Signals}

None.

#### Properties {#Properties}

None.

### org.freedesktop.sssd.infopipe.Cache.Object {#org.freedesktop.sssd.infopipe.Cache.Object}

#### Object paths implementing this interface {#Objectpathsimplementingthisinterface1}

-   /org/freedesktop/sssd/infopipe/Users/\*
-   /org/freedesktop/sssd/infopipe/Groups/\*

#### Methods {#Methods1}

-   b Store()
-   b Remove()
    -   Those methods will add/remove *cached* attributed to the object
        under *path* implementing this interface.

#### Signals {#Signals1}

None.

#### Properties {#Properties1}

None.

### Overview of the solution {#Overviewofthesolution}

New sysdb attribute *ifp\_cached* is created for users and groups
objects. If this attribute is present, the object is considered to be
cached on IFP D-Bus. The introspection of an object path */obj/path*
will report all cached objects in the subtree */obj/path/\**.

### How To Test {#HowToTest}

Call the D-Bus methods and properties. For example with **dbus-send**
tool. A cached object is supposed to appear in introspection.

### Authors {#Authors}

-   Jakub Hrozek
    &lt;[[​]{.icon}jhrozek@redhat.com](mailto:jhrozek@redhat.com){.mail-link}&gt;
-   Pavel Březina
    &lt;[[​]{.icon}pbrezina@redhat.com](mailto:pbrezina@redhat.com){.mail-link}&gt;

