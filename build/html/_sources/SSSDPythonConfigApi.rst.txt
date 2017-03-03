.. raw:: html

   <div class="wiki-toc">

#. `Classes <#Classes>`__

   #. `Exception Classes <#ExceptionClasses>`__

#. `Usage Examples <#UsageExamples>`__

   #. `Modify a single option for a
      domain <#Modifyasingleoptionforadomain>`__
   #. `Add a new ID domain and make it
      active <#AddanewIDdomainandmakeitactive>`__

.. raw:: html

   </div>

Classes
=======

-  `SSSDConfig <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html>`__
-  `SSSDConfigSchema? <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html>`__
-  `SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
-  `SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__

Exception Classes
-----------------

-  SSSDConfigException

   -  NotInitializedError
   -  AlreadyInitializedError
   -  NoOutputFileError
   -  NoServiceError
   -  ServiceNotRecognizedError
   -  ServiceAlreadyExistsError
   -  NoDomainError
   -  DomainAlreadyExistsError

Usage Examples
==============

Modify a single option for a domain
-----------------------------------

We want to switch the enumerate option for our LDAP domain to false.

.. code:: wiki

    from SSSDConfig import SSSDConfig

    sssdconfig = SSSDConfig()
    sssdconfig.import_config('/etc/sssd/sssd.conf')

    ldap_domain = sssdconfig.get_domain('LDAP')
    ldap_domain.set_option('enumerate', false)
    sssdconfig.save_domain(ldap_domain)

    sssdconfig.write()

Add a new ID domain and make it active
--------------------------------------

.. code:: wiki

    from SSSDConfig import SSSDConfig

    sssdconfig = SSSDConfig()
    sssdconfig.import_config('/etc/sssd/sssd.conf')

    ldap_domain = sssdconfig.new_domain('LDAP')
    ldap_domain.add_provider('ldap', 'id')
    ldap_domain.set_option('ldap_uri', 'ldap://ldap.example.com')
    ldap_domain.set_option('ldap_user_search_base', 'cn=users,cn=Accounts,dc=example,dc=com')
    ldap_domain.set_option('ldap_group_search_base', 'cn=groups,cn=Accounts,dc=example,dc=com')
    ldap_domain.set_option('enumerate', true)
    ldap_domain.set_active(true)

    sssdconfig.save_domain(ldap_domain)
    sssdconfig.write()
