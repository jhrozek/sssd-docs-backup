.. raw:: html

   <div class="wiki-toc">

#. `class SSSDService <#classSSSDService>`__

   #. ```__init__(name, apischema)`` <#__init__nameapischema>`__

      #. `Returns <#Returns>`__
      #. `Errors <#Errors>`__

   #. ```list_options()`` <#list_options>`__

      #. `Returns <#Returns1>`__
      #. `Errors <#Errors1>`__

   #. ```set_option(optionname, value)`` <#set_optionoptionnamevalue>`__

      #. `Returns <#Returns2>`__
      #. `Errors <#Errors2>`__

   #. ```get_option(optionname)`` <#get_optionoptionname>`__

      #. `Returns <#Returns3>`__
      #. `Errors <#Errors3>`__

   #. ```get_all_options()`` <#get_all_options>`__

      #. `Returns <#Returns4>`__
      #. `Errors <#Errors4>`__

   #. ```remove_option(optionname)`` <#remove_optionoptionname>`__

      #. `Returns <#Returns5>`__
      #. `Errors <#Errors5>`__

.. raw:: html

   </div>

class SSSDService
=================

``__init__(name, apischema)``
-----------------------------

*Create a new
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html#classSSSDService>`__,
setting its defaults to those found in the scema. This constructor
should not be used directly. Use
`SSSDConfig.new\_service() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_servicename>`__
instead.*

**name**
    The service name
**apischema**
    An
    `SSSDConfigSchema? <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html>`__
    object created by
    `SSSDConfig.\_\_init\_\_() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#__init__schemafileschemaplugindir>`__

Returns
~~~~~~~

The newly-created
`SSSDService <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html#classSSSDService>`__
object.

Errors
~~~~~~

**TypeError**
    The API schema passed in was unusable or the name was not a string.
**ServiceNotRecognizedError**
    The service was not listed in the schema

| 

``list_options()``
------------------

*List all options that apply to this service*

Returns
~~~~~~~

A dictionary of configurable options. This dictionary is keyed on the
option name with a tuple of the variable type and subtype (if the type
is a collection type) as the value.

Errors
~~~~~~

| No Errors

``set_option(optionname, value)``
---------------------------------

*Set a service option to the specified value (or values)*

**optionname**
    The option to change
**value**
    The value to set. This may be a single value or a list of values. If
    it is set to None, it resets the option to its default.

Returns
~~~~~~~

No return value

Errors
~~~~~~

**NoOptionError**
    The specified option is not listed in the schema
**TypeError**
    The value specified was not of the expected type

| 

``get_option(optionname)``
--------------------------

*Return the value of a service option*

**optionname**
    The option to get.

Returns
~~~~~~~

The value for the requested option.

Errors
~~~~~~

**NoOptionError**
    The specified option was not listed in the service

| 

``get_all_options()``
---------------------

*Return a dictionary of name/value pairs for this service*

Returns
~~~~~~~

A dictionary of name/value pairs currently in use for this service

Errors
~~~~~~

| 

``remove_option(optionname)``
-----------------------------

*Remove an option from the service. If the option does not exist, it is
ignored.*

Returns
~~~~~~~

No return value.

Errors
~~~~~~

No errors
