1.  Follow the steps in [Installing the
    SSSD](https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html){.wiki}.
2.  As root, open the file `/etc/sssd/sssd.conf`. In the
    `[domains/LDAP]` section, change:

    ``` {.wiki}
    enumerate = 0
    ```

    to

    ``` {.wiki}
    enumerate = 3
    ```

    and save the file

3.  Test enumeration of LDAP users

    ``` {.wiki}
    getent -s sss passwd
    ```

    You should see 100 users named sssdtestNNNNN, as well as a few
    others:

    ``` {.wiki}
    sssd-test:x:11004:11004:SSSD 1 test user:/home/sssd-test:/bin/bash
    sssd.test:x:11001:11001:SSSD 1 test user:/home/sssd.test:/bin/bash
    sssd:test:x:11003:11003:SSSD 1 test user:/home/sssd:test:/bin/bash
    sssd@test:x:11002:11002:SSSD 1 test user:/home/sssd@test:/bin/bash
    sssd_test:x:11005:11005:SSSD 1 test user:/home/sssd_test:/bin/bash
    ```

4.  Test retrieval of individual users, specifying the domain

    ``` {.wiki}
    getent passwd sssdtest10001@LDAP
    ```

    This should return:

    ``` {.wiki}
    sssdtest10001:x:10001:10001:SSSD 1 test user:/home/sssdtest10001:/bin/bash
    ```

5.  Repeat the above test with the users listed in
    step[\#3](https://fedorahosted.org/sssd/ticket/3 "task: Fake ticket to verify CC-list (closed: invalid)"){.closed
    .ticket}. It is expected that `sssd@test` will fail.
6.  Test retrieval of individual users, without specifying the domain

    ``` {.wiki}
    getent passwd sssdtest10002
    ```

    This should return:

    ``` {.wiki}
    sssdtest10002:x:10002:10002:SSSD 1 test user:/home/sssdtest10002:/bin/bash
    ```

7.  Repeat the above test with the users listed in step2. It is expected
    that `sssd@test` will fail.
8.  Test enumeration of LDAP groups

    ``` {.wiki}
    getent -s sss group
    ```

    This should return a large number of groups of varying membership

9.  Test retrieval of a specific group, specifying the domain

    ``` {.wiki}
    getent group sssdtestgroup10@LDAP
    ```

    This should return one group with ten members (sssdtest10001 through
    sssdtest10010)

    ``` {.wiki}
    sssdtestgroup10:x:11010:sssdtest10001,sssdtest10002,sssdtest10003,sssdtest10004,sssdtest10005,sssdtest10006,sssdtest10007,sssdtest10008,sssdtest10009,sssdtest10010
    ```

10. Test retrieval of a specific group, without specifying the domain

    ``` {.wiki}
    getent group sssdtestgroup11
    ```

    This should return one group with eleven members (sssdtest10001
    through sssdtest10011)

    ``` {.wiki}
    sssdtestgroup10:x:11010:sssdtest10001,sssdtest10002,sssdtest10003,sssdtest10004,sssdtest10005,sssdtest10006,sssdtest10007,sssdtest10008,sssdtest10009,sssdtest10010,sssdtest10011
    ```

11. Test that we do not truncate NSS data

    ``` {.wiki}
    getent group sssdtestgroup100@LDAP
    ```

    There will be a lot of output. Verify that it ends with
    `sssdtest10100`

12. Test offline support by terminating your network connection (e.g.
    unplugging your network cable or turning off your WiFI card), then
    rerun the above tests and verify that they return the same results.
    To minimize delays while offline, consider the following settings
    for your /etc/ldap.conf:

    ``` {.wiki}
    timelimit 10
    bind_timelimit 5
    nss_reconnect_maxsleeptime 2
    nss_reconnect_sleeptime 1
    ```


