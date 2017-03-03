<div class="wiki-toc">

1.  1.  [Description](#Description)
    2.  [How to Test](#HowtoTest)

</div>

Description {#Description}
-----------

This test will verify whether the SSSD is appropriately serving legacy
local users through NSS.

How to Test {#HowtoTest}
-----------

1.  Follow the steps in [Installing the
    SSSD](https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html){.wiki}.
    If you are running the Test Day LiveCD, you may skip this step.
2.  Restart the SSSD service (as root):

    ``` {.wiki}
    service sssd restart
    ```

3.  Verify that the SSSD services are running:

    ``` {.wiki}
    ps -e |grep sss
    ```

4.  Enable the use of the SSSD in nsswitch.conf. Change the following
    lines of /etc/nsswitch.conf from:

    ``` {.wiki}
    passwd:     files
    shadow:     files
    group:      files
    ```

    to

    ``` {.wiki}
    passwd:     files sss
    shadow:     files
    group:      files sss
    ```

5.  Verify that your local users are served to NSS from the SSSD
    (`-s sss` specifies that NSS should search only the sss provider)

    ``` {.wiki}
    getent -s sss passwd
    ```

    You should see all users from your /etc/passwd file whose UIDs are
    in the range 500-5000 (as specified in the sssd.conf)

6.  Request a specific user from the SSSD (pick one from the list
    returned in the previous step)

    ``` {.wiki}
    getent passwd validlocaluser@LEGACYLOCAL
    ```

    You should see something similar to the following output:

    ``` {.wiki}
    validlocaluser:x:500:500:Local User:/home/validlocaluser:/bin/bash
    ```

7.  Verify that your local groups are served to NSS from the SSSD

    ``` {.wiki}
    getent -s sss group
    ```

    You should see all groups fom your /etc/group file whose GIDs are in
    the range 500-5000 (as specified in the sssd.conf)

8.  Verify that you can request the information from a single valid
    group

    ``` {.wiki}
    getent group validgroup@LEGACYLOCAL
    ```


