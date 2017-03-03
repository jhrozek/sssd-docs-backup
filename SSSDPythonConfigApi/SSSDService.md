<div class="wiki-toc">

1.  [class SSSDService](#classSSSDService)
    1.  [`__init__(name, apischema)`](#__init__nameapischema)
        1.  [Returns](#Returns)
        2.  [Errors](#Errors)
    2.  [`list_options()`](#list_options)
        1.  [Returns](#Returns1)
        2.  [Errors](#Errors1)
    3.  [`set_option(optionname, value)`](#set_optionoptionnamevalue)
        1.  [Returns](#Returns2)
        2.  [Errors](#Errors2)
    4.  [`get_option(optionname)`](#get_optionoptionname)
        1.  [Returns](#Returns3)
        2.  [Errors](#Errors3)
    5.  [`get_all_options()`](#get_all_options)
        1.  [Returns](#Returns4)
        2.  [Errors](#Errors4)
    6.  [`remove_option(optionname)`](#remove_optionoptionname)
        1.  [Returns](#Returns5)
        2.  [Errors](#Errors5)

</div>

class SSSDService {#classSSSDService}
=================

`__init__(name, apischema)` {#__init__nameapischema}
---------------------------

*Create a new
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html#classSSSDService){.wiki},
setting its defaults to those found in the scema. This constructor
should not be used directly. Use
[SSSDConfig.new\_service()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#new_servicename){.wiki}
instead.*

**name**
:   The service name

**apischema**
:   An
    [SSSDConfigSchema?](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfigSchema.html){.missing
    .wiki} object created by
    [SSSDConfig.\_\_init\_\_()](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDConfig.html#__init__schemafileschemaplugindir){.wiki}

### Returns {#Returns}

The newly-created
[SSSDService](https://docs.pagure.org/sssd-test2/SSSDPythonConfigApi/SSSDService.html#classSSSDService){.wiki}
object.

### Errors {#Errors}

**TypeError**
:   The API schema passed in was unusable or the name was not a string.

**ServiceNotRecognizedError**
:   The service was not listed in the schema

\
\

`list_options()`
----------------

*List all options that apply to this service*

### Returns {#Returns1}

A dictionary of configurable options. This dictionary is keyed on the
option name with a tuple of the variable type and subtype (if the type
is a collection type) as the value.

### Errors {#Errors1}

No Errors\
\
\

`set_option(optionname, value)` {#set_optionoptionnamevalue}
-------------------------------

*Set a service option to the specified value (or values)*

**optionname**
:   The option to change

**value**
:   The value to set. This may be a single value or a list of values. If
    it is set to None, it resets the option to its default.

### Returns {#Returns2}

No return value

### Errors {#Errors2}

**NoOptionError**
:   The specified option is not listed in the schema

**TypeError**
:   The value specified was not of the expected type

\
\

`get_option(optionname)`
------------------------

*Return the value of a service option*

**optionname**
:   The option to get.

### Returns {#Returns3}

The value for the requested option.

### Errors {#Errors3}

**NoOptionError**
:   The specified option was not listed in the service

\
\

`get_all_options()`
-------------------

*Return a dictionary of name/value pairs for this service*

### Returns {#Returns4}

A dictionary of name/value pairs currently in use for this service

### Errors {#Errors4}

\
\
\

`remove_option(optionname)`
---------------------------

*Remove an option from the service. If the option does not exist, it is
ignored.*

### Returns {#Returns5}

No return value.

### Errors {#Errors5}

No errors
