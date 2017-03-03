Description {#Description}
-----------

This test ensures that users stored in native LDB backend can log in
using SSSD.

How to test {#Howtotest}
-----------

1.  Follow the steps in [Installing the
    SSSD](https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html){.wiki}.
    If you are running the Test Day LiveCD, you may skip this step.
    Especially ensure that you have the right contents of
    `/etc/pam.d/system-auth`.
2.  As root, create the file /etc/pam.d/sssdproxylocal. **DUE TO
    OVERSIGHT, THIS FILE IS NOT ON THE LIVECD**

    ``` {.wiki}
    #%PAM-1.0
    auth        required      pam_env.so
    auth        sufficient    pam_fprintd.so
    auth        sufficient    pam_unix.so nullok
    auth        requisite     pam_succeed_if.so uid >= 500 quiet
    auth        required      pam_deny.so

    account     sufficient    pam_unix.so
    account     sufficient    pam_localuser.so
    account     sufficient    pam_succeed_if.so uid < 500 quiet
    account     required      pam_permit.so

    password    requisite     pam_cracklib.so try_first_pass retry=3
    password    sufficient    pam_unix.so sha512 shadow nullok use_authtok
    password    required      pam_deny.so

    session     optional      pam_keyinit.so revoke
    session     required      pam_limits.so
    session     [success=1 default=ignore] pam_succeed_if.so service in crond quiet use_uid
    session     sufficient    pam_unix.so
    ```

3.  Choose one user from `/etc/passwd`. It may be convenient to create
    one just for testing and assign him a known password

    ``` {.wiki}
    useradd validlocaluser -u 4999
    passwd validlocaluser
    ```

    If 4999 is taken, use something else in the 500-4999 range.

4.  Make sure the SSH deamon is running. If not, start it

    ``` {.wiki}
    service sshd status
    service sshd start
    ```

5.  Try logging in as validlocaluser

    ``` {.wiki}
    ssh localhost -l validlocaluser@LEGACYLOCAL
    ```

6.  While logged in as validlocaluser, try changing your password

    ``` {.wiki}
    passwd
    ```

7.  Log out and log back in using your new password

    ``` {.wiki}
    logout
    ssh localhost -l validlocaluser@LEGACYLOCAL
    ```


