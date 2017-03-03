.. raw:: html

   <div class="wiki-toc">

#. `class SSSDDomain <#classSSSDDomain>`__

   #. ```__init__(name, apischema)`` <#__init__nameapischema>`__

      #. `Returns <#Returns>`__
      #. `Errors <#Errors>`__

   #. ```set_name(name)`` <#set_namename>`__

      #. `Returns <#Returns1>`__
      #. `Errors <#Errors1>`__

   #. `set\_active(active) <#set_activeactive>`__

      #. `Returns <#Returns2>`__
      #. `Errors <#Errors2>`__

   #. ```list_options()`` <#list_options>`__

      #. `Returns <#Returns3>`__
      #. `Errors <#Errors3>`__

   #. `list\_provider\_options(type[,
      subtype]) <#list_provider_optionstypesubtype>`__

      #. `Returns <#Returns4>`__
      #. `Errors <#Errors4>`__

   #. `list\_providers() <#list_providers>`__

      #. `Returns <#Returns5>`__
      #. `Errors <#Errors5>`__

   #. `add\_provider(type, subtype) <#add_providertypesubtype>`__

      #. `Returns <#Returns6>`__
      #. `Errors <#Errors6>`__

   #. `remove\_provider(type, subtype) <#remove_providertypesubtype>`__

      #. `Returns <#Returns7>`__
      #. `Errors <#Errors7>`__

   #. `set\_option(optionname, value) <#set_optionoptionnamevalue>`__

      #. `Returns <#Returns8>`__
      #. `Errors <#Errors8>`__

   #. `get\_option(optionname) <#get_optionoptionname>`__

      #. `Returns <#Returns9>`__
      #. `Errors <#Errors9>`__

   #. `remove\_option <#remove_option>`__

      #. `Returns <#Returns10>`__
      #. `Errors <#Errors10>`__

.. raw:: html

   </div>

class SSSDDomain
================

``__init__(name, apischema)``
-----------------------------

*Creates a new, empty
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html#classSSSDDomain>`__.
This domain is inactive by default. This constructor should not be used
directly. Use
`SSSDConfig.new\_domain() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_domainname>`__
instead.*

**name**
    The domain name.
**apischema**
    An
    `SSSDConfigSchema? <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html>`__
    object created by
    `SSSDConfig.\_\_init\_\_() <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#__init__schemafileschemaplugindir>`__

Returns
~~~~~~~

The newly-created
`SSSDDomain <https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html#classSSSDDomain>`__
object.

Errors
~~~~~~

| No errors

``set_name(name)``
------------------

*Change the name of the domain. This will update the active domain list
as appropriate when saved to an SSSDConfig*

**name**
    The new name for the domain.

Returns
~~~~~~~

No return value.

Errors
~~~~~~

| No errors

set\_active(active)
-------------------

*Enable or disable this domain*

**active**
    Boolean value. If True, this domain will be added to the active
    domains list when it is saved. If False, it will be removed from the
    active domains list when it is saved.

Returns
~~~~~~~

No return value

Errors
~~~~~~

| No errors

``list_options()``
------------------

*List options available for the currently-configured providers.*

Returns
~~~~~~~

A dictionary of configurable options. This dictionary is keyed on the
option name with a tuple of the variable type and subtype (if the type
is a collection type) as the value.

Errors
~~~~~~

| No errors

list\_provider\_options(type[, subtype])
----------------------------------------

*If target is specified, list all options applicable to that target,
otherwise list all possible options available for a provider.*

**type**
    Provider backend type. (e.g. ``local``, ``ldap``, ``krb5``, etc.)
**subtype**
    Subtype of the backend type. (e.g. ``id``, ``auth``, ``chpass``)

Returns
~~~~~~~

A dictionary of configurable options for the specified provider type.
This dictionary is keyed on the option name with a tuple of the variable
type and subtype (if the type is a collection type) as the value.

Errors
~~~~~~

**NoSuchProviderError**
    The specified provider is not listed in the schema or plugins
**NoSuchProviderSubtypeError**
    The specified provider subtype is not listed in the schema

| 

list\_providers()
-----------------

*Return a dictionary of providers.*

Returns
~~~~~~~

Returns a dictionary of providers, keyed on the primary type, with the
value being a tuple of the subtypes it supports.

Errors
~~~~~~

| No Errors

add\_provider(type, subtype)
----------------------------

*Add a new provider type to the domain*

**type**
    Provider backend type. (e.g. ``local``, ``ldap``, ``krb5``, etc.)
**subtype**
    Subtype of the backend type. (e.g. ``id``, ``auth``, ``chpass``)

Returns
~~~~~~~

No return value.

Errors
~~~~~~

**ProviderSubtypeInUse**
    Another backend is already providing this subtype
**NoSuchProviderError**
    The specified provider is not listed in the schema or plugins
**NoSuchProviderSubtypeError**
    The specified provider subtype is not listed in the schema

| 

remove\_provider(type, subtype)
-------------------------------

*Remove a provider from the domain. This will also remove any options
specific to this ``subtype``, or all of ``type`` if no more providers of
``type`` are present. If this provider type and subtype are not present,
no changes occur.*

**type**
    Provider backend type. (e.g. ``local``, ``ldap``, ``krb5``, etc.)
**subtype**
    Subtype of the backend type. (e.g. ``id``, ``auth``, ``chpass``)

Returns
~~~~~~~

No return value.

Errors
~~~~~~

| No Errors

set\_option(optionname, value)
------------------------------

*Set a domain option to the specified value (or values)*

**optionname**
    The option to change.
**value**
    The value to set. This may be a single value or a list of values. If
    it is set to None, it resets the option to its default.

Returns
~~~~~~~

No return value.

Errors
~~~~~~

**NoOptionError**
    The specified option is not listed in the schema
**TypeError**
    The value specified was not of the expected type

| 

get\_option(optionname)
-----------------------

*Return the value of a domain option*

Returns
~~~~~~~

A list of values for the specified service option.

Errors
~~~~~~

**NoOptionError**
    The specified option was not listed in the service

| 

remove\_option
--------------

*Remove an option from the domain. If the option does not exist, it is
ignored.*

Returns
~~~~~~~

No return value

Errors
~~~~~~

No errors
