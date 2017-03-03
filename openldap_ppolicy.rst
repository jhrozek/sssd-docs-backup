.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Synopsis <#Synopsis>`__
   #. `Setting OpenLDAP <#SettingOpenLDAP>`__

      #. `Installing OpenLDAP packages <#InstallingOpenLDAPpackages>`__
      #. `Start LDAP server calling <#StartLDAPservercalling>`__
      #. `Load some basis schemas <#Loadsomebasisschemas>`__
      #. `Defining server back-end <#Definingserverback-end>`__
      #. `Defining server front-end <#Definingserverfront-end>`__
      #. `Quick test <#Quicktest>`__

   #. `Pasword policy (ppolicy) <#Paswordpolicyppolicy>`__

      #. `Loading ppolicy schema <#Loadingppolicyschema>`__
      #. `Loading ppolicy module <#Loadingppolicymodule>`__
      #. `Loading ppolicy overlay <#Loadingppolicyoverlay>`__
      #. `Setting default ppolicy
         settings <#Settingdefaultppolicysettings>`__

   #. `SSH keys in openldap <#SSHkeysinopenldap>`__
   #. `MISC <#MISC>`__

      #. `Permanently lock user account <#Permanentlylockuseraccount>`__

   #. `Sources <#Sources>`__

.. raw:: html

   </div>

Synopsis
--------

This page describes how to configure OpenLDAP with enabled password
policy and added support for user's SSH keys on Fedora. Main purpose for
creating such an environment is mainly for testing SSSD. This guide is a
work in progress.

Setting OpenLDAP
----------------

This is part is heavily based on article
`​OpenLDAP <https://help.ubuntu.com/10.04/serverguide/openldap-server.html>`__,
so please see it for more details.

Installing OpenLDAP packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Package openldap-clients useful command-line utilities such as ldapadd,
ldapsearch, ldapmodify, etc., package openldap-servers contains schemas.

.. raw:: html

   <div class="code">

::

    dnf install openldap openldap-clients openldap-servers

.. raw:: html

   </div>

Start LDAP server calling
~~~~~~~~~~~~~~~~~~~~~~~~~

To start with OpenLDAP configuration, server must be running.

.. raw:: html

   <div class="code">

::

    systemctl start slapd

.. raw:: html

   </div>

Load some basis schemas
~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <div class="code">

::

    ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/cosine.ldif
    ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap//schema/nis.ldif
    ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/inetorgperson.ldif

.. raw:: html

   </div>

Defining server back-end
~~~~~~~~~~~~~~~~~~~~~~~~

*backend.example.com.ldif* describes basic properties of server backend.
Please note the *olcRootPW* which holds administrator's password.

.. raw:: html

   <div class="code">

::

    cat <<EOF >backend.example.com.ldif
    # Load dynamic backend modules
    dn: cn=module,cn=config
    objectClass: olcModuleList
    cn: module
    olcModulepath: /usr/lib/ldap
    olcModuleload: back_hdb

    # Database settings
    dn: olcDatabase=hdb,cn=config
    objectClass: olcDatabaseConfig
    objectClass: olcHdbConfig
    olcDatabase: {1}hdb
    olcSuffix: dc=example,dc=com
    olcDbDirectory: /var/lib/ldap
    olcRootDN: cn=admin,dc=example,dc=com
    olcRootPW: aaa
    olcDbConfig: set_cachesize 0 2097152 0
    olcDbConfig: set_lk_max_objects 1500
    olcDbConfig: set_lk_max_locks 1500
    olcDbConfig: set_lk_max_lockers 1500
    olcDbIndex: objectClass eq
    olcLastMod: TRUE
    olcDbCheckpoint: 512 30
    olcAccess: to attrs=userPassword by dn="cn=admin,dc=example,dc=com" write by anonymous auth by self write by * none
    olcAccess: to attrs=shadowLastChange by self write by * read
    olcAccess: to dn.base="" by * read
    olcAccess: to * by dn="cn=admin,dc=example,dc=com" write by * read
    EOF

.. raw:: html

   </div>

Add LDIF file to the LDAP.

.. raw:: html

   <div class="code">

::

    ldapadd -Y EXTERNAL -H ldapi:/// -f backend.example.com.ldif

.. raw:: html

   </div>

Defining server front-end
~~~~~~~~~~~~~~~~~~~~~~~~~

This LDIF file populates LDAP server with users *admin* and *John* and
also add group *example*. Again - please note the attributes setting
passwords.

.. raw:: html

   <div class="code">

::

    cat <<EOF >frontend.example.com.ldif
    # Create top-level object in domain
    dn: dc=example,dc=com
    objectClass: top
    objectClass: dcObject
    objectclass: organization
    o: Example Organization
    dc: Example
    description: LDAP Example

    # Admin user.
    dn: cn=admin,dc=example,dc=com
    objectClass: simpleSecurityObject
    objectClass: organizationalRole
    cn: admin
    description: LDAP administrator
    userPassword: aaa

    dn: ou=people,dc=example,dc=com
    objectClass: organizationalUnit
    ou: people

    dn: ou=groups,dc=example,dc=com
    objectClass: organizationalUnit
    ou: groups

    dn: uid=john,ou=people,dc=example,dc=com
    objectClass: inetOrgPerson
    objectClass: posixAccount
    objectClass: shadowAccount
    uid: john
    sn: Doe
    givenName: John
    cn: John Doe
    displayName: John Doe
    uidNumber: 1000
    gidNumber: 10000
    userPassword: password
    gecos: John Doe
    loginShell: /bin/bash
    homeDirectory: /home/john
    shadowExpire: -1
    shadowFlag: 0
    shadowWarning: 7
    shadowMin: 8
    shadowMax: 999999
    shadowLastChange: 10877
    mail: john.doe@example.com
    postalCode: 31000
    l: Toulouse
    o: Example
    mobile: +33 (0)6 xx xx xx xx
    homePhone: +33 (0)5 xx xx xx xx
    title: System Administrator
    postalAddress:
    initials: JD

    dn: cn=example,ou=groups,dc=example,dc=com
    objectClass: posixGroup
    cn: example
    gidNumber: 10000
    EOF

.. raw:: html

   </div>

Add LDIF file to the LDAP.

.. raw:: html

   <div class="code">

::

    ldapadd -x -D cn=admin,dc=example,dc=com -W -f frontend.example.com.ldif

.. raw:: html

   </div>

Quick test
~~~~~~~~~~

.. raw:: html

   <div class="code">

::

    ldapsearch -xLLL -b "dc=example,dc=com" uid=john sn givenName cn

.. raw:: html

   </div>

Pasword policy (ppolicy)
------------------------

This section heavily draws from this how-to
`​ppolicy <http://www.flagword.net/2013/02/openldap-with-tls-ppolicy-and-master-master-replication-on-rhel6-3/comment-page-1/>`__.

Loading ppolicy schema
~~~~~~~~~~~~~~~~~~~~~~

Load schema describing ppolicy attributes.

.. raw:: html

   <div class="code">

::

    ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/ppolicy.ldif

.. raw:: html

   </div>

Loading ppolicy module
~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <div class="code">

::

    #load ppolicy module
    cat <<EOF >ppolicy_module.ldif
    dn: cn=module,cn=config
    objectClass: olcModuleList
    cn: module
    olcModuleLoad: ppolicy.la
    olcModulePath: /usr/lib64/openldap
    EOF

.. raw:: html

   </div>

Add LDIF file.

.. raw:: html

   <div class="code">

::

    ldapadd -Y EXTERNAL -H ldapi:/// -f ppolicy_module.ldif

.. raw:: html

   </div>

Restart LDAP server.

.. raw:: html

   <div class="code">

::

    #restart ldap
    systemctl restart slapd

.. raw:: html

   </div>

Loading ppolicy overlay
~~~~~~~~~~~~~~~~~~~~~~~

Please note the *olcPPolicyDefault* attribute which holds a DN to a
default ppolicy entry.

.. raw:: html

   <div class="code">

::

    #Add PPolicy Overlay:
    cat <<EOF >ppolicy-overlay.ldif
    dn: olcOverlay=ppolicy,olcDatabase={3}hdb,cn=config
    objectClass: olcPPolicyConfig
    olcOverlay: ppolicy
    olcPPolicyDefault: cn=ppolicy,ou=policies,dc=example,dc=com
    olcPPolicyUseLockout: TRUE
    olcPPolicyHashCleartext: TRUE
    EOF

.. raw:: html

   </div>

Add LDIF file.

.. raw:: html

   <div class="code">

::

    ldapadd -Y EXTERNAL -H ldapi:/// -f ./ppolicy-overlay.ldif

.. raw:: html

   </div>

Setting default ppolicy settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <div class="code">

::

    # create default policy
    cat <<EOF >default_ppolicy.ldif
    dn: ou=policies,dc=example,dc=com
    objectClass: top
    objectClass: organizationalUnit
    ou: policies

    dn: cn=ppolicy,ou=policies,dc=example,dc=com
    objectClass: top
    objectClass: device
    objectClass: pwdPolicyChecker
    objectClass: pwdPolicy
    cn: ppolicy
    pwdAttribute: userPassword
    pwdInHistory: 8
    pwdMinLength: 8
    pwdMaxFailure: 3
    pwdFailureCountInterval: 1800
    pwdCheckQuality: 0
    pwdMustChange: TRUE
    pwdGraceAuthNLimit: 0
    pwdMaxAge: 7776000
    pwdExpireWarning: 1209600
    pwdLockoutDuration: 900
    pwdLockout: TRUE
    EOF

.. raw:: html

   </div>

Add LDIF file.

.. raw:: html

   <div class="code">

::

    ldapadd -x -D 'cn=admin,dc=example,dc=com' -W -H ldapi:/// -f ./default_ppolicy.ldif

.. raw:: html

   </div>

SSH keys in openldap
--------------------

This section describes how to add SSH keys to user entries. LDIF listing
bellow is a converted schema file that can be found at
`​openssh-lpk <https://code.google.com/p/openssh-lpk/>`__.

.. raw:: html

   <div class="code">

::

    cat <<EOF >/etc/openldap/schema/openssh-lpk_openldap.ldif
    # AUTO-GENERATED FILE - DO NOT EDIT!! Use ldapmodify.
    # CRC32 42a543d1
    dn: cn=openssh-lpk_openldap,cn=schema,cn=config
    objectClass: olcSchemaConfig
    cn: openssh-lpk_openldap
    olcAttributeTypes: {0}( 1.3.6.1.4.1.24552.500.1.1.1.13 NAME 'sshPublicKey' DES
     C 'MANDATORY: OpenSSH Public key' EQUALITY octetStringMatch SYNTAX 1.3.6.1.4.
     1.1466.115.121.1.40 )
    olcObjectClasses: {0}( 1.3.6.1.4.1.24552.500.1.1.2.0 NAME 'ldapPublicKey' DESC
      'MANDATORY: OpenSSH LPK objectclass' SUP top AUXILIARY MAY ( sshPublicKey $
     uid ) )
    EOF

.. raw:: html

   </div>

Add schema file.

.. raw:: html

   <div class="code">

::

    ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/openssh-lpk_openldap.ldif

.. raw:: html

   </div>

MISC
----

Permanently lock user account
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

LDIF file which set John's account to be permanently locked.

.. raw:: html

   <div class="code">

::

    cat <<EOF >permlock.ldif
    dn: uid=john,ou=People,dc=example,dc=com
    replace: pwdAccountLockedTime
    pwdAccountLockedTime: 000001010000Z

.. raw:: html

   </div>

Modify John's account.

.. raw:: html

   <div class="code">

::

    ldapmodify -x -D 'cn=admin,dc=example,dc=com' -W -H ldapi:/// -f permlock.ldif
    Enter LDAP Password:
    modifying entry "uid=john,ou=People,dc=example,dc=com"

.. raw:: html

   </div>

Sources
-------

+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| OpenLDAP      | `​https://help.ubuntu.com/10.04/serverguide/openldap-server.html <https://help.ubuntu.com/10.04/serverguide/openldap-server.html>`__                                                                                                           |
+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ppolicy       | `​http://www.flagword.net/2013/02/openldap-with-tls-ppolicy-and-master-master-replication-on-rhel6-3/comment-page-1/ <http://www.flagword.net/2013/02/openldap-with-tls-ppolicy-and-master-master-replication-on-rhel6-3/comment-page-1/>`__   |
+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| openssh-lpk   | `​https://code.google.com/p/openssh-lpk/ <https://code.google.com/p/openssh-lpk/>`__                                                                                                                                                           |
+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
