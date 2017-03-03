<div class="wiki-toc">

1.  [Classes](#Classes)
    1.  [Exception Classes](#ExceptionClasses)
2.  [Usage Examples](#UsageExamples)
    1.  [Modify a single option for a
        domain](#Modifyasingleoptionforadomain)
    2.  [Add a new ID domain and make it
        active](#AddanewIDdomainandmakeitactive)

</div>

Classes {#Classes}
=======

-   [SSSDConfig](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html){.wiki}
-   [SSSDConfigSchema?](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html){.missing
    .wiki}
-   [SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
-   [SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}

Exception Classes {#ExceptionClasses}
-----------------

-   SSSDConfigException
    -   NotInitializedError
    -   AlreadyInitializedError
    -   NoOutputFileError
    -   NoServiceError
    -   ServiceNotRecognizedError
    -   ServiceAlreadyExistsError
    -   NoDomainError
    -   DomainAlreadyExistsError

Usage Examples {#UsageExamples}
==============

Modify a single option for a domain {#Modifyasingleoptionforadomain}
-----------------------------------

We want to switch the enumerate option for our LDAP domain to false.

``` {.wiki}
from SSSDConfig import SSSDConfig

sssdconfig = SSSDConfig()
sssdconfig.import_config('/etc/sssd/sssd.conf')

ldap_domain = sssdconfig.get_domain('LDAP')
ldap_domain.set_option('enumerate', false)
sssdconfig.save_domain(ldap_domain)

sssdconfig.write()
```

Add a new ID domain and make it active {#AddanewIDdomainandmakeitactive}
--------------------------------------

``` {.wiki}
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
```
