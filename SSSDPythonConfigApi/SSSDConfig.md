<div class="wiki-toc">

1.  [class SSSDConfig](#classSSSDConfig)
    1.  [`__init__([schemafile, schemaplugindir])`](#__init__schemafileschemaplugindir)
        1.  [Internal Implementation
            Notes](#InternalImplementationNotes)
        2.  [Returns](#Returns)
        3.  [Errors](#Errors)
    2.  [`import_config([configfile])`](#import_configconfigfile)
        1.  [Returns](#Returns1)
        2.  [Errors](#Errors1)
    3.  [`new_config()`](#new_config)
        1.  [Returns](#Returns2)
        2.  [Errors](#Errors2)
    4.  [`write([outputfile]`](#writeoutputfile)
        1.  [Returns](#Returns3)
        2.  [Errors](#Errors3)
    5.  [`list_services()`](#list_services)
        1.  [Returns](#Returns4)
        2.  [Errors](#Errors4)
    6.  [`get_service(name)`](#get_servicename)
        1.  [Returns](#Returns5)
        2.  [Errors](#Errors5)
    7.  [`new_service(name)`](#new_servicename)
        1.  [Returns](#Returns6)
        2.  [Errors](#Errors6)
    8.  [`delete_service(name)`](#delete_servicename)
        1.  [Returns](#Returns7)
        2.  [Errors](#Errors7)
    9.  [save\_service(SSSDService
        …](#save_serviceSSSDServiceservice_object)
        1.  [Returns](#Returns8)
        2.  [Errors](#Errors8)
    10. [`list_active_domains()`](#list_active_domains)
        1.  [Returns](#Returns9)
        2.  [Errors](#Errors9)
    11. [`list_inactive_domains()`](#list_inactive_domains)
        1.  [Returns](#Returns10)
        2.  [Errors](#Errors10)
    12. [`list_domains()`](#list_domains)
        1.  [Returns](#Returns11)
        2.  [Errors](#Errors11)
    13. [`get_domain(name)`](#get_domainname)
        1.  [Returns](#Returns12)
        2.  [Errors](#Errors12)
    14. [`new_domain(name)`](#new_domainname)
        1.  [Returns](#Returns13)
        2.  [Errors](#Errors13)
    15. [`delete_domain(name)`](#delete_domainname)
        1.  [Returns](#Returns14)
        2.  [Errors](#Errors14)
    16. [`save_domain(SSSDDomain domain_object)`](#save_domainSSSDDomaindomain_object)
        1.  [Returns](#Returns15)
        2.  [Errors](#Errors15)

</div>

class SSSDConfig {#classSSSDConfig}
================

`__init__([schemafile, schemaplugindir])` {#__init__schemafileschemaplugindir}
-----------------------------------------

*Initialize the SSSD config parser/editor. This constructor does not
open or create a config file. If the schemafile and schemaplugindir are
not passed, it will use the system defaults.*

**schemafile**
:   The path to the api schema config file. Usually
    /etc/sssd/sssd.api.conf

**schemaplugindir**
:   The path the directory containing the provider schema config files.
    Usually /etc/sssd/sssd.api.d

### Internal Implementation Notes {#InternalImplementationNotes}

This function will create a
[SSSDConfigSchema?](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html){.missing
.wiki} object internally that will be passed to
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}
and
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
objects when they are created or requested.

### Returns {#Returns}

The newly-created SSSDConfig object.

### Errors {#Errors}

**IOError**
:   Exception raised when the schema file could not be opened for
    reading. Note: provider schema files in the schemaplugindir that
    cannot be read will be ignored.

**ParsingError**
:   The main schema file or one of those in the plugin directory could
    not be parsed.

\
\

`import_config([configfile])`
-----------------------------

*Read in a config file, populating all of the service and domain objects
with the read values.*

**configfile**
:   The path to the SSSD config file. If not specified, use the system
    default, usually /etc/sssd/sssd.conf

### Returns {#Returns1}

No return value

### Errors {#Errors1}

**IOError**
:   Exception raised when the file could not be opened for reading

**ParsingError**
:   Exception raised when errors occur attempting to parse a file.

**AlreadyInitializedError**
:   This SSSDConfig object was already initialized by a call to
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}

\
\

`new_config()`
--------------

*Initialize the SSSDConfig object with the defaults from the schema.*

### Returns {#Returns2}

No return value

### Errors {#Errors2}

**AlreadyInitializedError**
:   This SSSDConfig object was already initialized by a call to
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}

\
\

`write([outputfile]`
--------------------

*Write out the configuration to a file.*

**outputfile**
:   The path to write the new config file. If it is not specified, it
    will use the path specified by the import() call.

### Returns {#Returns3}

No return value

### Errors {#Errors3}

**IOError**
:   Exception raised when the file could not be opened for writing

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

**NoOutputFileError**
:   No outputfile was specified and this SSSDConfig object was not
    initialized by import()

\
\

`list_services()`
-----------------

*Retrieve a list of known services.*

### Returns {#Returns4}

The list of known services.

### Errors {#Errors4}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`get_service(name)`
-------------------

*Get an
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}
object to edit a service.*

**name**
:   The name of the service to return.

### Returns {#Returns5}

An
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}
instance containing the current state of a service in the SSSDConfig

### Errors {#Errors5}

**NoServiceError****
:   There is no such service with the specified name in the SSSDConfig.

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`new_service(name)`
-------------------

*Create a new service from the defaults and return the
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}
object for it. This function will also add this service to the list of
active services in the \[SSSD\] section.*

**name**
:   The name of the service to create and return.

### Returns {#Returns6}

The newly-created
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}
object

### Errors {#Errors6}

**ServiceNotRecognizedError**
:   There is no such service in the schema.

**ServiceAlreadyExistsError**
:   The service being created already exists in the SSSDConfig object.

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`delete_service(name)`
----------------------

*Remove a service from the SSSDConfig object. This function will also
remove this service from the list of active services in the \[SSSD\]
section. Has no effect if the service does not exist.*

### Returns {#Returns7}

No return value

### Errors {#Errors7}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

save\_service([SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki} service\_object) {#save_serviceSSSDServiceservice_object}
----------------------------------------------------------------------------------------------------------------------------

*Save the changes made to the service object back to the SSSDConfig
object.*

**service\_object**
:   The
    [SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html){.wiki}
    object to save to the configuration.

### Returns {#Returns8}

No return value

### Errors {#Errors8}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

**TypeError**
:   `service_object` was not of the type SSSDService

\
\

`list_active_domains()`
-----------------------

*Return a list of all active domains.*

### Returns {#Returns9}

The list of configured, active domains.

### Errors {#Errors9}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`list_inactive_domains()`
-------------------------

*Return a list of all configured, but disabled domains.*

### Returns {#Returns10}

The list of configured, inactive domains.

### Errors {#Errors10}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`list_domains()`
----------------

*Return a list of all configured domains, including inactive domains.*

### Returns {#Returns11}

The list of configured domains, both active and inactive.

### Errors {#Errors11}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`get_domain(name)`
------------------

*Get an
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
object to edit a domain.*

**name**
:   The name of the domain to return.

### Returns {#Returns12}

An
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
instance containing the current state of a domain in the SSSDConfig

### Errors {#Errors12}

**NoDomainError****
:   There is no such domain with the specified name in the SSSDConfig.

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`new_domain(name)`
------------------

*Create a new, empty domain and return the
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
object for it.*

**name**
:   The name of the domain to create and return.

### Returns {#Returns13}

The newly-created
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
object

### Errors {#Errors13}

**DomainAlreadyExistsError**
:   The service being created already exists in the SSSDConfig object.

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`delete_domain(name)`
---------------------

*Remove a domain from the SSSDConfig object. This function will also
remove this domain from the list of active domains in the \[SSSD\]
section, if it is there.*

### Returns {#Returns14}

No return value

### Errors {#Errors14}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

\
\

`save_domain(SSSDDomain domain_object)` {#save_domainSSSDDomaindomain_object}
---------------------------------------

*Save the changes made to the domain object back to the SSSDConfig
object. If this domain is marked active, ensure it is present in the
active domain list in the \[SSSD\] section*

**domain\_object**
:   The
    [SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}
    object to save to the configuration.

### Returns {#Returns15}

No return value

### Errors {#Errors15}

**NotInitializedError**
:   This SSSDConfig object has not had
    [import\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile){.wiki}
    or
    [new\_config()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config){.wiki}
    run on it yet.

**TypeError**
:   `domain_object` was not of type
    [SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html){.wiki}

\
\

