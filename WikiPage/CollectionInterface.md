Collection Interface {#CollectionInterface}
====================

Under the hood a lot of the functionality of the
[ELAPI](https://docs.pagure.org/sssd-test2/WikiPage/ELAPIInterface.html){.wiki}
and
[INI](https://docs.pagure.org/sssd-test2/WikiPage/INIInterface.html){.wiki}
is built around the collection interface.

The collection is a list of the key-value pairs. The collections are
used in many different ways in
[ELAPI](https://docs.pagure.org/sssd-test2/WikiPage/ELAPIInterface.html){.wiki}
and
[INI](https://docs.pagure.org/sssd-test2/WikiPage/INIInterface.html){.wiki}.
The ELAPI events and templates are collections. The set of targets in
dispatcher is also implemented as a “collection”.\
The content of the configuration file is also stored in the hierarchical
collection inside INI object.

The collection interface allows:

-   creating collections
-   adding properties (key – value pairs) to collections
-   deleting properties
-   updating properties
-   nesting collections
-   serializing collections (to text, to XML, to binary blob like RADIUS
    uses)
-   traversing collections (including nesting)
-   searching collections
-   checking that property is in the collection
-   getting property value from the collection
-   copying collections
-   ...

The collections are implemented as light weight link lists. The
collections can be easily used as a robust implementation of “set” or
“bag” object. Collection also provides implementation of "stack" and
"queue" objects. Collection uses hashing to optimize search but it
should be noted that it is not as robust as a hash table. When there are
not many items (hundreds not thousands) and they are well distinguished
by name the “collection” interface is a good choice. Anyone is welcome
to use this interface. For bigger and more complex situations consider
using other types of the primitives (hash tables, dictionaries, trees
etc.).
