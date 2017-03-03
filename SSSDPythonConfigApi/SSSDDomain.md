<div class="wiki-toc">

1.  [class SSSDDomain](#classSSSDDomain)
    1.  [`__init__(name, apischema)`](#__init__nameapischema)
        1.  [Returns](#Returns)
        2.  [Errors](#Errors)
    2.  [`set_name(name)`](#set_namename)
        1.  [Returns](#Returns1)
        2.  [Errors](#Errors1)
    3.  [set\_active(active)](#set_activeactive)
        1.  [Returns](#Returns2)
        2.  [Errors](#Errors2)
    4.  [`list_options()`](#list_options)
        1.  [Returns](#Returns3)
        2.  [Errors](#Errors3)
    5.  [list\_provider\_options(type\[,
        subtype\])](#list_provider_optionstypesubtype)
        1.  [Returns](#Returns4)
        2.  [Errors](#Errors4)
    6.  [list\_providers()](#list_providers)
        1.  [Returns](#Returns5)
        2.  [Errors](#Errors5)
    7.  [add\_provider(type, subtype)](#add_providertypesubtype)
        1.  [Returns](#Returns6)
        2.  [Errors](#Errors6)
    8.  [remove\_provider(type, subtype)](#remove_providertypesubtype)
        1.  [Returns](#Returns7)
        2.  [Errors](#Errors7)
    9.  [set\_option(optionname, value)](#set_optionoptionnamevalue)
        1.  [Returns](#Returns8)
        2.  [Errors](#Errors8)
    10. [get\_option(optionname)](#get_optionoptionname)
        1.  [Returns](#Returns9)
        2.  [Errors](#Errors9)
    11. [remove\_option](#remove_option)
        1.  [Returns](#Returns10)
        2.  [Errors](#Errors10)

</div>

class SSSDDomain {#classSSSDDomain}
================

`__init__(name, apischema)` {#__init__nameapischema}
---------------------------

*Creates a new, empty
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html#classSSSDDomain){.wiki}.
This domain is inactive by default. This constructor should not be used
directly. Use
[SSSDConfig.new\_domain()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_domainname){.wiki}
instead.*

**name**
:   The domain name.

**apischema**
:   An
    [SSSDConfigSchema?](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html){.missing
    .wiki} object created by
    [SSSDConfig.\_\_init\_\_()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#__init__schemafileschemaplugindir){.wiki}

### Returns {#Returns}

The newly-created
[SSSDDomain](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDDomain.html#classSSSDDomain){.wiki}
object.

### Errors {#Errors}

No errors\
\
\

`set_name(name)`
----------------

*Change the name of the domain. This will update the active domain list
as appropriate when saved to an SSSDConfig*

**name**
:   The new name for the domain.

### Returns {#Returns1}

No return value.

### Errors {#Errors1}

No errors\
\
\

set\_active(active)
-------------------

*Enable or disable this domain*

**active**
:   Boolean value. If True, this domain will be added to the active
    domains list when it is saved. If False, it will be removed from the
    active domains list when it is saved.

### Returns {#Returns2}

No return value

### Errors {#Errors2}

No errors\
\
\

`list_options()`
----------------

*List options available for the currently-configured providers.*

### Returns {#Returns3}

A dictionary of configurable options. This dictionary is keyed on the
option name with a tuple of the variable type and subtype (if the type
is a collection type) as the value.

### Errors {#Errors3}

No errors\
\
\

list\_provider\_options(type\[, subtype\]) {#list_provider_optionstypesubtype}
------------------------------------------

*If target is specified, list all options applicable to that target,
otherwise list all possible options available for a provider.*

**type**
:   Provider backend type. (e.g. `local`, `ldap`, `krb5`, etc.)

**subtype**
:   Subtype of the backend type. (e.g. `id`, `auth`, `chpass`)

### Returns {#Returns4}

A dictionary of configurable options for the specified provider type.
This dictionary is keyed on the option name with a tuple of the variable
type and subtype (if the type is a collection type) as the value.

### Errors {#Errors4}

**NoSuchProviderError**
:   The specified provider is not listed in the schema or plugins

**NoSuchProviderSubtypeError**
:   The specified provider subtype is not listed in the schema

\
\

list\_providers()
-----------------

*Return a dictionary of providers.*

### Returns {#Returns5}

Returns a dictionary of providers, keyed on the primary type, with the
value being a tuple of the subtypes it supports.

### Errors {#Errors5}

No Errors\
\
\

add\_provider(type, subtype) {#add_providertypesubtype}
----------------------------

*Add a new provider type to the domain*

**type**
:   Provider backend type. (e.g. `local`, `ldap`, `krb5`, etc.)

**subtype**
:   Subtype of the backend type. (e.g. `id`, `auth`, `chpass`)

### Returns {#Returns6}

No return value.

### Errors {#Errors6}

**ProviderSubtypeInUse**
:   Another backend is already providing this subtype

**NoSuchProviderError**
:   The specified provider is not listed in the schema or plugins

**NoSuchProviderSubtypeError**
:   The specified provider subtype is not listed in the schema

\
\

remove\_provider(type, subtype) {#remove_providertypesubtype}
-------------------------------

*Remove a provider from the domain. This will also remove any options
specific to this `subtype`, or all of `type` if no more providers of
`type` are present. If this provider type and subtype are not present,
no changes occur.*

**type**
:   Provider backend type. (e.g. `local`, `ldap`, `krb5`, etc.)

**subtype**
:   Subtype of the backend type. (e.g. `id`, `auth`, `chpass`)

### Returns {#Returns7}

No return value.

### Errors {#Errors7}

No Errors\
\
\

set\_option(optionname, value) {#set_optionoptionnamevalue}
------------------------------

*Set a domain option to the specified value (or values)*

**optionname**
:   The option to change.

**value**
:   The value to set. This may be a single value or a list of values. If
    it is set to None, it resets the option to its default.

### Returns {#Returns8}

No return value.

### Errors {#Errors8}

**NoOptionError**
:   The specified option is not listed in the schema

**TypeError**
:   The value specified was not of the expected type

\
\

get\_option(optionname)
-----------------------

*Return the value of a domain option*

### Returns {#Returns9}

A list of values for the specified service option.

### Errors {#Errors9}

**NoOptionError**
:   The specified option was not listed in the service

\
\

remove\_option
--------------

*Remove an option from the domain. If the option does not exist, it is
ignored.*

### Returns {#Returns10}

No return value

### Errors {#Errors10}

No errors
