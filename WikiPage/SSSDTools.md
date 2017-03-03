SSSD Tools {#SSSDTools}
==========

SSSD Takes advantage of several common tools that can be found in the
source tree.

-   [Collection](https://docs.pagure.org/sssd-test2/WikiPage/CollectionInterface.html){.wiki} -
    a set of interfaces to manage data in sets of key-value pairs
    ***(stable)***.
-   [INI](https://docs.pagure.org/sssd-test2/WikiPage/INIInterface.html){.wiki} -
    interface to read ini files and retrieve values from them
    ***(stable)***
-   [DHASH](https://docs.pagure.org/sssd-test2/WikiPage/DHASHInterface.html){.wiki} -
    API that implements a hash table object ***(stable)***.
-   [Path
    Utils](https://docs.pagure.org/sssd-test2/WikiPage/PathUtils.html){.wiki} -
    API to manage directory and file paths ***(stable)***.

All these tools now have their own [[​]{.icon}git
repository](http://git.fedorahosted.org/git/ding-libs.git){.ext-link},
but they still use the SSSD Trac instance for tracking issues.

NOTE: ELAPI has been moved to its own project
[[​]{.icon}ELAPI](https://fedorahosted.org/ELAPI){.ext-link}
