.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Description <#Description>`__
   #. `How to Test <#HowtoTest>`__

.. raw:: html

   </div>

Description
-----------

This test will verify whether the SSSD is appropriately serving native
local users through NSS.

How to Test
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
   messages, as they are erroneous.

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

#. Enable the use of the SSSD in nsswitch.conf. Change the following
   lines of /etc/nsswitch.conf from:

   .. code:: wiki

       passwd:     files
       shadow:     files
       group:      files

   to

   .. code:: wiki

       passwd:     files sss
       shadow:     files
       group:      files sss

#. Create a new local user with the following command (as root)

   .. code:: wiki

       /usr/sbin/sss_useradd nativelocaluser

   (Again, you can disregard the
   "``Unable to register control with rootdse!``" messages.)

#. Verify that this user is enumerated by NSS:

   .. code:: wiki

       getent passwd |grep nativelocaluser

   You should see:

   .. code:: wiki

       nativelocaluser:x:5000:5000:nativelocaluser:/home/nativelocaluser:/bin/bash

#. Verify that this user's information can be seen by directly
   requesting it

   .. code:: wiki

       getent passwd nativelocaluser@LOCAL

   The output should be the same as previous.

#. Verify that this user's information can be seen by searching all
   domains

   .. code:: wiki

       getent passwd nativelocaluser

   The output should be the same as previous.

#. Verify that a group with the same name exists

   .. code:: wiki

       getent group |grep nativelocaluser

   The output should be:

   .. code:: wiki

       nativelocaluser:x:5000:

#. Verify that this group can be requested directly

   .. code:: wiki

       getent group nativelocaluser@LOCAL

   The output should be the same as the previous.

#. Verify that this group can be seen by searching all domains

   .. code:: wiki

       getent group nativelocaluser

   The output should be the same as the previous.

#. Create a new group (as root)

   .. code:: wiki

       /usr/sbin/sss_groupadd nativelocalgroup

#. Add the nativelocaluser to the group

   .. code:: wiki

       /usr/sbin/sss_usermod -a nativelocalgroup nativelocaluser

#. Verify the contents of this group using getent as above:

   .. code:: wiki

       nativelocalgroup:x:5001:nativelocaluser
