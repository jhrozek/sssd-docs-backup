Description {#Description}
-----------

This test ensures that users stored in native LDB backend can log in
using SSSD.

How to test {#Howtotest}
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
    messages, as they are erroneous).

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

5.  Create a new local user with the following command (as root). You
    don't need to create this user again if you followed the [NSS Local
    Native
    testcase](https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/NSS_Local_Native.html){.wiki}

    ``` {.wiki}
    /usr/sbin/sss_useradd nativelocaluser
    ```

    (Again, you can disregard the
    "`Unable to register control with rootdse!`" messages.)

6.  Change password of this new user (as root)

    ``` {.wiki}
    passwd nativelocaluser
    ```

7.  Start the OpenSSH server if not running (as root)

    ``` {.wiki}
    service sshd start
    ```

    The reason, we're testing logging in via ssh and not virtual
    consoles is that the VTs read PAM config on startup.

8.  Try logging in as nativelocaluser

    ``` {.wiki}
    ssh nativelocaluser@localhost
    ```

9.  When logged in as nativelocaluser, let the user change his own
    password

    ``` {.wiki}
    passwd
    ```

10. Log out and log back in using the new password

    ``` {.wiki}
    logout
    ssh nativelocaluser@localhost
    ```


