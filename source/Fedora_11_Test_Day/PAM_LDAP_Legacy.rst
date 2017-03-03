Description
-----------

This test ensures that users stored in LDAP can log in using the LDAP
proxy module for PAM.

How to test
-----------

#. Follow the steps in `Installing the
   SSSD <https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html>`__.
   If you are running the Test Day LiveCD, you may skip this step.
   Especially ensure that you have the right contents of
   /etc/pam.d/system-auth.
#. Edit /etc/sssd/sssd.conf. Find the [domains/LDAP] section and
   uncomment the following authentication settings:

   .. code:: wiki

       cache-credentials = TRUE
       auth-module = proxy
       pam-target = sssdproxyldap

#. As root, create file ``/etc/pam.d/sssdproxyldap`` with the following
   contents:

   .. code:: wiki

       #%PAM-1.0
       auth      required    pam_ldap.so
       account   required    pam_ldap.so
       password  required    pam_ldap.so
       session   required    pam_ldap.so

#. The LDAP server at ``rawhide1.fedoraproject.org`` provides users
   named sssdtestNNNNN where NNNNN is a number from 10000 to 10100. The
   server also provides a few other users with special usernames:

   .. code:: wiki

       sssd-test:x:11004:11004:SSSD 1 test user:/home/sssd-test:/bin/bash
       sssd.test:x:11001:11001:SSSD 1 test user:/home/sssd.test:/bin/bash
       sssd:test:x:11003:11003:SSSD 1 test user:/home/sssd:test:/bin/bash
       sssd@test:x:11002:11002:SSSD 1 test user:/home/sssd@test:/bin/bash
       sssd_test:x:11005:11005:SSSD 1 test user:/home/sssd_test:/bin/bash

#. Make sure the SSH deamon is running. If not, start it

   .. code:: wiki

       service sshd status
       service sshd start

#. Pick one of the sssdtestNNNNN users. All these users have the same
   password "sssdtest".
#. Try logging in via SSH using the username you chose and password
   "sssdtest"

   .. code:: wiki

       ssh localhost -l sssdtest10005@LDAP

#. Test offline support by terminating your network connection (e.g.
   unplugging your network cable or turning off your WiFI card), then
   rerun the above tests and verify that they return the same results.
   To minimize delays while the LDAP server is offline, consider the
   following settings for your ``/etc/ldap.conf``:

   .. code:: wiki

       timelimit 10
       bind_timelimit 5
       nss_reconnect_maxsleeptime 2
       nss_reconnect_sleeptime 1

#. Clean up after this test by commenting out the configuration entries
   in step 2, above.
