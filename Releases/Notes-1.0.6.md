Highlights {#Highlights}
----------

-   Fix a serious bug when operating in enumerate=false mode
    -   This configuration would occasionally result in periods of
        several minutes where the backend was operating at 100% CPU.

Detailed Changelog {#DetailedChangelog}
------------------

Jakub Hrozek (2):

-   Do not schedule enumeration after a cleanup
-   Do not check entries during cleanup task

Stephen Gallagher (2):

-   Revert "Change default for enumeration to TRUE"
-   Release version 1.0.6

