Description
-----------

This test ensures that users stored in native LDB backend can log in
using SSSD.

How to test
-----------

#. Follow the steps in `Installing the
   SSSD <https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html>`__.
   If you are running the Test Day LiveCD, you may skip this step.
#. Copy
   `sssd.conf <https://fedorahosted.org/sssd/attachment/wiki/Fedora_11_Test_Day/sssd.conf>`__\ `​ <https://fedorahosted.org/sssd/raw-attachment/wiki/Fedora_11_Test_Day/sssd.conf>`__
   to /etc/sssd/sssd.conf
#. Restart the SSSD service (as root):

   .. code:: wiki

       service sssd restart

   (Please disregard the "``Unable to register control with rootdse!``"
   messages, as they are erroneous).

#. Verify that the SSSD services are running:

   .. code:: wiki

       ps -e |grep sss

   You should see:

   .. code:: wiki

       30968 pts/0    00:00:00 sssd
       30970 pts/0    00:00:00 sssd_dp
       30972 pts/0    00:00:00 sssd_be
       30973 pts/0    00:00:00 sssd_be
       30974 pts/0    00:00:00 sssd_be
       30975 pts/0    00:00:00 sssd_nss
       30976 pts/0    00:00:00 sssd_pam

#. Create a new local user with the following command (as root). You
   don't need to create this user again if you followed the `NSS Local
   Native
   testcase <https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/NSS_Local_Native.html>`__

   .. code:: wiki

       /usr/sbin/sss_useradd nativelocaluser

   (Again, you can disregard the
   "``Unable to register control with rootdse!``" messages.)

#. Change password of this new user (as root)

   .. code:: wiki

       passwd nativelocaluser

#. Start the OpenSSH server if not running (as root)

   .. code:: wiki

       service sshd start

   The reason, we're testing logging in via ssh and not virtual consoles
   is that the VTs read PAM config on startup.

#. Try logging in as nativelocaluser

   .. code:: wiki

       ssh nativelocaluser@localhost

#. When logged in as nativelocaluser, let the user change his own
   password

   .. code:: wiki

       passwd

#. Log out and log back in using the new password

   .. code:: wiki

       logout
       ssh nativelocaluser@localhost
