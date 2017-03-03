Highlights {#Highlights}
----------

-   Eliminate segfaults when using credential caching for offline
    authentication
-   Fix upgrade issues from old versions of SSSD
-   Ensure that the upgrade script eliminates the 'dp' service from the
    services list, since it's been removed

Detailed changes since 0.7.0 {#Detailedchangessince0.7.0}
----------------------------

Jakub Hrozek (2):

-   Fix migration script for pre-0.5 local domains
-   Do not migrate Data Provider

Piotr Drąg (1):

-   Updating polish translation for 0.7.0

Simo Sorce (4):

-   Zero pointers on free
-   Use standard coding practice to set last login
-   Fix segfault
-   Read the right buffer, avoids potential segfaults

Stephen Gallagher (3):

-   Remove DP from example configuration
-   Remove \[dp\] section from example config
-   Update version to 0.7.1

