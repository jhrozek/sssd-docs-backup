.. raw:: html

   <div class="wiki-toc">

#. `class SSSDConfig <#classSSSDConfig>`__

   #. ```__init__([schemafile, schemaplugindir])`` <#__init__schemafileschemaplugindir>`__

      #. `Internal Implementation
         Notes <#InternalImplementationNotes>`__
      #. `Returns <#Returns>`__
      #. `Errors <#Errors>`__

   #. ```import_config([configfile])`` <#import_configconfigfile>`__

      #. `Returns <#Returns1>`__
      #. `Errors <#Errors1>`__

   #. ```new_config()`` <#new_config>`__

      #. `Returns <#Returns2>`__
      #. `Errors <#Errors2>`__

   #. ```write([outputfile]`` <#writeoutputfile>`__

      #. `Returns <#Returns3>`__
      #. `Errors <#Errors3>`__

   #. ```list_services()`` <#list_services>`__

      #. `Returns <#Returns4>`__
      #. `Errors <#Errors4>`__

   #. ```get_service(name)`` <#get_servicename>`__

      #. `Returns <#Returns5>`__
      #. `Errors <#Errors5>`__

   #. ```new_service(name)`` <#new_servicename>`__

      #. `Returns <#Returns6>`__
      #. `Errors <#Errors6>`__

   #. ```delete_service(name)`` <#delete_servicename>`__

      #. `Returns <#Returns7>`__
      #. `Errors <#Errors7>`__

   #. `save\_service(SSSDService
      … <#save_serviceSSSDServiceservice_object>`__

      #. `Returns <#Returns8>`__
      #. `Errors <#Errors8>`__

   #. ```list_active_domains()`` <#list_active_domains>`__

      #. `Returns <#Returns9>`__
      #. `Errors <#Errors9>`__

   #. ```list_inactive_domains()`` <#list_inactive_domains>`__

      #. `Returns <#Returns10>`__
      #. `Errors <#Errors10>`__

   #. ```list_domains()`` <#list_domains>`__

      #. `Returns <#Returns11>`__
      #. `Errors <#Errors11>`__

   #. ```get_domain(name)`` <#get_domainname>`__

      #. `Returns <#Returns12>`__
      #. `Errors <#Errors12>`__

   #. ```new_domain(name)`` <#new_domainname>`__

      #. `Returns <#Returns13>`__
      #. `Errors <#Errors13>`__

   #. ```delete_domain(name)`` <#delete_domainname>`__

      #. `Returns <#Returns14>`__
      #. `Errors <#Errors14>`__

   #. ```save_domain(SSSDDomain domain_object)`` <#save_domainSSSDDomaindomain_object>`__

      #. `Returns <#Returns15>`__
      #. `Errors <#Errors15>`__

.. raw:: html

   </div>

class SSSDConfig
================

``__init__([schemafile, schemaplugindir])``
-------------------------------------------

*Initialize the SSSD config parser/editor. This constructor does not
open or create a config file. If the schemafile and schemaplugindir are
not passed, it will use the system defaults.*

**schemafile**
    The path to the api schema config file. Usually
    /etc/sssd/sssd.api.conf
**schemaplugindir**
    The path the directory containing the provider schema config files.
    Usually /etc/sssd/sssd.api.d

Internal Implementation Notes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This function will create a
`SSSDConfigSchema? <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html>`__
object internally that will be passed to
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__
and
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
objects when they are created or requested.

Returns
~~~~~~~

The newly-created SSSDConfig object.

Errors
~~~~~~

**IOError**
    Exception raised when the schema file could not be opened for
    reading. Note: provider schema files in the schemaplugindir that
    cannot be read will be ignored.
**ParsingError**
    The main schema file or one of those in the plugin directory could
    not be parsed.

| 

``import_config([configfile])``
-------------------------------

*Read in a config file, populating all of the service and domain objects
with the read values.*

**configfile**
    The path to the SSSD config file. If not specified, use the system
    default, usually /etc/sssd/sssd.conf

Returns
~~~~~~~

No return value

Errors
~~~~~~

**IOError**
    Exception raised when the file could not be opened for reading
**ParsingError**
    Exception raised when errors occur attempting to parse a file.
**AlreadyInitializedError**
    This SSSDConfig object was already initialized by a call to
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__

| 

``new_config()``
----------------

*Initialize the SSSDConfig object with the defaults from the schema.*

Returns
~~~~~~~

No return value

Errors
~~~~~~

**AlreadyInitializedError**
    This SSSDConfig object was already initialized by a call to
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__

| 

``write([outputfile]``
----------------------

*Write out the configuration to a file.*

**outputfile**
    The path to write the new config file. If it is not specified, it
    will use the path specified by the import() call.

Returns
~~~~~~~

No return value

Errors
~~~~~~

**IOError**
    Exception raised when the file could not be opened for writing
**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.
**NoOutputFileError**
    No outputfile was specified and this SSSDConfig object was not
    initialized by import()

| 

``list_services()``
-------------------

*Retrieve a list of known services.*

Returns
~~~~~~~

The list of known services.

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``get_service(name)``
---------------------

*Get an
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__
object to edit a service.*

**name**
    The name of the service to return.

Returns
~~~~~~~

An
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__
instance containing the current state of a service in the SSSDConfig

Errors
~~~~~~

**NoServiceError\ ****
    There is no such service with the specified name in the SSSDConfig.
**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``new_service(name)``
---------------------

*Create a new service from the defaults and return the
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__
object for it. This function will also add this service to the list of
active services in the [SSSD] section.*

**name**
    The name of the service to create and return.

Returns
~~~~~~~

The newly-created
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__
object

Errors
~~~~~~

**ServiceNotRecognizedError**
    There is no such service in the schema.
**ServiceAlreadyExistsError**
    The service being created already exists in the SSSDConfig object.
**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``delete_service(name)``
------------------------

*Remove a service from the SSSDConfig object. This function will also
remove this service from the list of active services in the [SSSD]
section. Has no effect if the service does not exist.*

Returns
~~~~~~~

No return value

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

save\_service(\ `SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__ service\_object)
--------------------------------------------------------------------------------------------------------------------------

*Save the changes made to the service object back to the SSSDConfig
object.*

**service\_object**
    The
    `SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html>`__
    object to save to the configuration.

Returns
~~~~~~~

No return value

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.
**TypeError**
    ``service_object`` was not of the type SSSDService

| 

``list_active_domains()``
-------------------------

*Return a list of all active domains.*

Returns
~~~~~~~

The list of configured, active domains.

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``list_inactive_domains()``
---------------------------

*Return a list of all configured, but disabled domains.*

Returns
~~~~~~~

The list of configured, inactive domains.

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``list_domains()``
------------------

*Return a list of all configured domains, including inactive domains.*

Returns
~~~~~~~

The list of configured domains, both active and inactive.

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``get_domain(name)``
--------------------

*Get an
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
object to edit a domain.*

**name**
    The name of the domain to return.

Returns
~~~~~~~

An
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
instance containing the current state of a domain in the SSSDConfig

Errors
~~~~~~

**NoDomainError\ ****
    There is no such domain with the specified name in the SSSDConfig.
**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``new_domain(name)``
--------------------

*Create a new, empty domain and return the
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
object for it.*

**name**
    The name of the domain to create and return.

Returns
~~~~~~~

The newly-created
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
object

Errors
~~~~~~

**DomainAlreadyExistsError**
    The service being created already exists in the SSSDConfig object.
**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``delete_domain(name)``
-----------------------

*Remove a domain from the SSSDConfig object. This function will also
remove this domain from the list of active domains in the [SSSD]
section, if it is there.*

Returns
~~~~~~~

No return value

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.

| 

``save_domain(SSSDDomain domain_object)``
-----------------------------------------

*Save the changes made to the domain object back to the SSSDConfig
object. If this domain is marked active, ensure it is present in the
active domain list in the [SSSD] section*

**domain\_object**
    The
    `SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__
    object to save to the configuration.

Returns
~~~~~~~

No return value

Errors
~~~~~~

**NotInitializedError**
    This SSSDConfig object has not had
    `import\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#import_configconfigfile>`__
    or
    `new\_config() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_config>`__
    run on it yet.
**TypeError**
    ``domain_object`` was not of type
    `SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html>`__

| 
