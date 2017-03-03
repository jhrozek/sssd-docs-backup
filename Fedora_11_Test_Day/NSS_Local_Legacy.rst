.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Description <#Description>`__
   #. `How to Test <#HowtoTest>`__

.. raw:: html

   </div>

Description
-----------

This test will verify whether the SSSD is appropriately serving legacy
local users through NSS.

How to Test
-----------

#. Follow the steps in `Installing the
   SSSD <https://docs.pagure.org/sssd-test2/Fedora_11_Test_Day/Installation.html>`__.
   If you are running the Test Day LiveCD, you may skip this step.
#. Restart the SSSD service (as root):

   .. code:: wiki

       service sssd restart

#. Verify that the SSSD services are running:

   .. code:: wiki

       ps -e |grep sss

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

#. Verify that your local users are served to NSS from the SSSD
   (``-s sss`` specifies that NSS should search only the sss provider)

   .. code:: wiki

       getent -s sss passwd

   You should see all users from your /etc/passwd file whose UIDs are in
   the range 500-5000 (as specified in the sssd.conf)

#. Request a specific user from the SSSD (pick one from the list
   returned in the previous step)

   .. code:: wiki

       getent passwd validlocaluser@LEGACYLOCAL

   You should see something similar to the following output:

   .. code:: wiki

       validlocaluser:x:500:500:Local User:/home/validlocaluser:/bin/bash

#. Verify that your local groups are served to NSS from the SSSD

   .. code:: wiki

       getent -s sss group

   You should see all groups fom your /etc/group file whose GIDs are in
   the range 500-5000 (as specified in the sssd.conf)

#. Verify that you can request the information from a single valid group

   .. code:: wiki

       getent group validgroup@LEGACYLOCAL
