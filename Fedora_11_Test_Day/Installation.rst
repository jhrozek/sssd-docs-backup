.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Installation Instructions <#InstallationInstructions>`__

.. raw:: html

   </div>

Installation Instructions
-------------------------

#. Install the sssd package and its dependencies. You can skip this step
   if you are using the Test Day LiveCD.

   .. code:: wiki

       yum install sssd

#. Copy
   `sssd.conf <https://fedorahosted.org/sssd/attachment/wiki/Fedora_11_Test_Day/sssd.conf>`__\ `​ <https://fedorahosted.org/sssd/raw-attachment/wiki/Fedora_11_Test_Day/sssd.conf>`__
   to /etc/sssd/sssd.conf
#. Configure access to the Test Day LDAP server

   #. Verify connectivity to the LDAP server

      .. code:: wiki

          ping rawhide1.fedoraproject.org

      If you get a ping response, all is well.

   #. Launch system-config-authentication (or select
      System->Administration->Authentication from the menu)
   #. In the User Information tab, check ``Enable LDAP Support`` and
      then choose ``Configure LDAP``
   #. Leave the ``Use TLS to encrypt connections`` checkbox unchecked.
   #. Enter ``dc=fedoraproject, dc=org`` in the the
      ``LDAP Search Base DN`` field.
   #. Enter ``ldap://rawhide1.fedoraproject.org`` in the ``LDAP Server``
      field.
   #. Choose "OK" twice.
   #. Relaunch system-config-authentication and uncheck
      ``Enable LDAP Support``, then hit OK once more We do this to ease
      the configuration of the ldap.conf file, but then we disable it in
      favor of using the SSSD.

#. Enable the use of the SSSD in nsswitch.conf. Change the following
   lines of /etc/nsswitch.conf from:

   .. code:: wiki

       passwd:     files ldap
       shadow:     files ldap
       group:      files ldap

   to

   .. code:: wiki

       passwd:     files sss
       shadow:     files
       group:      files sss

   Please note that your ``/etc/nsswitch.conf`` may have different
   contents for passwd:, shadow: and group: databases if you had User
   Identity information configured differently. The desired state is to
   have ``files sss`` set for passwd: and group: databases for the
   tests.

#. Enable the use of the SSSD for PAM. Change the following lines of
   /etc/pam.d/system-auth from: If you are changing the default PAM
   config on Fedora, it should look like:

   .. code:: wiki

       #%PAM-1.0
       auth        required      pam_env.so
       auth        sufficient    pam_fprintd.so
       auth        sufficient    pam_unix.so nullok
       auth        sufficient    pam_sss.so use_first_pass
       auth        requisite     pam_succeed_if.so uid >= 500 quiet
       auth        required      pam_deny.so

       account     sufficient    pam_unix.so
       account     required      pam_sss.so
       account     sufficient    pam_localuser.so
       account     sufficient    pam_succeed_if.so uid < 500 quiet
       account     required      pam_permit.so

       password    requisite     pam_cracklib.so try_first_pass retry=3
       password    sufficient    pam_unix.so sha512 shadow nullok use_authtok
       password    sufficient    pam_sss.so use_first_pass
       password    required      pam_deny.so

       session     optional      pam_keyinit.so revoke
       session     required      pam_limits.so
       session     [success=1 default=ignore] pam_succeed_if.so service in crond quiet use_uid
       session     sufficient    pam_unix.so
       session     required      pam_sss.so

   If you are using a custom ``system-auth`` file, please adjust
   accordingly.

#. Prepare the legacy authentication for LDAP. Create the file
   /etc/pam.d/sssdproxyldap with the following contents

   .. code:: wiki

       #%PAM-1.0
       auth required pam_ldap.so
       session required pam_ldap.so
       account required pam_ldap.so
       password required pam_ldap.so

#. Prepare legacy authentication for native users. Create the file
   /etc/pam.d/sssdproxylocal

   .. code:: wiki

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

#. Turn off the Name Service Cache Daemon. SSSD provides its own caching
   mechanisms which may not interact with nscd's very well

   .. code:: wiki

       service nscd stop

#. There are still issues with SELinux interaction as of Fedora 11 Beta.
   To mitigate any possible SELinux denials, turn it into 'Permissive'
   state for the test (as root):

   .. code:: wiki

       setenforce 0

   Please `​report <https://fedorahosted.org/sssd/newticket>`__ any
   SELinux denials seen in setroubleshoot so we can fix them.

#. Restart the SSSD service (as root):

   .. code:: wiki

       service sssd restart

   (Please disregard the "``Unable to register control with rootdse!``"
   messages, as they are erroneous.)

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
