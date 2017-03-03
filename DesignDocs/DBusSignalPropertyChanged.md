D-Bus Signal: Notify Property Changed {#D-BusSignal:NotifyPropertyChanged}
=====================================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2233](https://fedorahosted.org/sssd/ticket/2233){.ext-link}

Related design page(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/wiki/DesignDocs/DBusResponder](https://docs.pagure.org/sssd-test2/DesignDocs/DBusResponder.html){.ext-link}

### Problem statement {#Problemstatement}

This design document describes how to implement
org.freedesktop.DBus.Properties.PropertiesChanged signal for SSSD
objects exported in the IFP responder.

D-Bus Interface {#D-BusInterface}
---------------

### org.freedesktop.DBus.Properties {#org.freedesktop.DBus.Properties}

#### Signals {#Signals}

-   PropertiesChanged(s interface\_name, {sv} changed\_properties, as
    invalidated\_properties)
    -   interface\_name: name of the interface on which the properties
        are defined
    -   changed\_properties: changed properties with new values
    -   invalidated\_properties: changed properties but the new values
        are not send with them
    -   this signal is emitted for every property annotated with
        org.freedesktop.DBus.Property.EmitsChangedSignal, this
        annotation may be also used for the whole interface meaning that
        every property within this interface emits the signal

### Overview of the solution {#Overviewofthesolution}

Changes in properties are detected in new LDB plugin inside a *mod*
hook. The plugin writes list of changed properties in a TDB-based
changelog which is periodically consumed by IFP responder. IFP then
emits PropertiesChanged signal per each modified object.

### Implementation details {#Implementationdetails}

#### TDB Format {#TDBFormat}

-   **TDB Name**: *ifp\_changelog.tdb*
-   **Key**: dn of modified object
-   **Value**: chained list of modified properties in the form
    *total\_num\\0prop1\\0prop2\\0...\\0*

#### IFP Side {#IFPSide}

1.  TDB database is created on IFP start and deleted on IFP termination.
    -   on IFP start:
        -   if TDB file does not exist it is created
        -   if TDB file exist (unexpected termination of IFP) it is
            flushed, we do not care about the data inside
    -   on correct IFP termination
        -   the TDB file is deleted
2.  A periodic task *IFP: notify properties changed* is created, it is
    responsible for emitting the *PropertiesChanged* signal
    -   Periodic task flow:
        1.  Lock TDB for read-only access
        2.  Traverse the TDB and remember dn and properties for all
            modified objects
        3.  Flush TDB
        4.  Release the lock
        5.  Create and emit D-Bus signal per each object that is
            exported on IFP bus and supports *PropertiesChanged* signal

#### LDB Plugin Side {#LDBPluginSide}

1.  If TDB file does not exist just quit
2.  If modified object supports the signal store it in the TDB

### Configuration changes {#Configurationchanges}

In IFP section:

-   **ifp\_notification\_interval**: period of *IFP: notify properties
    changed*, disabled if 0, default 300 (5 minutes)

### How To Test {#HowToTest}

1.  Hook onto *PropertiesChanged* signal, e. g. with *dbus-monitor'̈́'*
2.  Trigger change of user/group
3.  Signal should be recieved

### Questions {#Questions}

1.  Do we want to use *changed\_properties* or *invalidated\_properties*

### Authors {#Authors}

-   Pavel Březina
    &lt;[[​]{.icon}pbrezina@redhat.com](mailto:pbrezina@redhat.com){.mail-link}&gt;

