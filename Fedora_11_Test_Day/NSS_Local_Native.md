<div class="wiki-toc">

1.  1.  [Description](#Description)
    2.  [How to Test](#HowtoTest)

</div>

Description {#Description}
-----------

This test will verify whether the SSSD is appropriately serving native
local users through NSS.

How to Test {#HowtoTest}
-----------

1.  Follow the steps in [Installing the
    SSSD](https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html){.wiki}.
    If you are running the Test Day LiveCD, you may skip this step.
2.  Copy
    [sssd.conf](https://fedorahosted.org/sssd/attachment/wiki/Fedora_11_Test_Day/sssd.conf "Attachment 'sssd.conf' in Fedora_11_Test_Day"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Fedora_11_Test_Day/sssd.conf "Download"){.trac-rawlink}
    to /etc/sssd/sssd.conf
3.  Restart the SSSD service (as root):

    ``` {.wiki}
    service sssd restart
    ```

    (Please disregard the "`Unable to register control with rootdse!`"
    messages, as they are erroneous.

4.  Verify that the SSSD services are running:

    ``` {.wiki}
    ps -e |grep sss
    ```

    You should see:

    ``` {.wiki}
    30968 pts/0    00:00:00 sssd
    30970 pts/0    00:00:00 sssd_dp
    30972 pts/0    00:00:00 sssd_be
    30973 pts/0    00:00:00 sssd_be
    30974 pts/0    00:00:00 sssd_be
    30975 pts/0    00:00:00 sssd_nss
    30976 pts/0    00:00:00 sssd_pam
    ```

5.  Enable the use of the SSSD in nsswitch.conf. Change the following
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

6.  Create a new local user with the following command (as root)

    ``` {.wiki}
    /usr/sbin/sss_useradd nativelocaluser
    ```

    (Again, you can disregard the
    "`Unable to register control with rootdse!`" messages.)

7.  Verify that this user is enumerated by NSS:

    ``` {.wiki}
    getent passwd |grep nativelocaluser
    ```

    You should see:

    ``` {.wiki}
    nativelocaluser:x:5000:5000:nativelocaluser:/home/nativelocaluser:/bin/bash
    ```

8.  Verify that this user's information can be seen by directly
    requesting it

    ``` {.wiki}
    getent passwd nativelocaluser@LOCAL
    ```

    The output should be the same as previous.

9.  Verify that this user's information can be seen by searching all
    domains

    ``` {.wiki}
    getent passwd nativelocaluser
    ```

    The output should be the same as previous.

10. Verify that a group with the same name exists

    ``` {.wiki}
    getent group |grep nativelocaluser
    ```

    The output should be:

    ``` {.wiki}
    nativelocaluser:x:5000:
    ```

11. Verify that this group can be requested directly

    ``` {.wiki}
    getent group nativelocaluser@LOCAL
    ```

    The output should be the same as the previous.

12. Verify that this group can be seen by searching all domains

    ``` {.wiki}
    getent group nativelocaluser
    ```

    The output should be the same as the previous.

13. Create a new group (as root)

    ``` {.wiki}
    /usr/sbin/sss_groupadd nativelocalgroup
    ```

14. Add the nativelocaluser to the group

    ``` {.wiki}
    /usr/sbin/sss_usermod -a nativelocalgroup nativelocaluser
    ```

15. Verify the contents of this group using getent as above:

    ``` {.wiki}
    nativelocalgroup:x:5001:nativelocaluser
    ```


