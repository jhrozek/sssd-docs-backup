INI Validator Design {#INIValidatorDesign}
====================

Concepts {#Concepts}
--------

The INI validator is going to be an INI library function that would
allow checking the configuration just read from the INI file against a
predefined set of rules. The set of rules is specific for each kind of
the configuration file so the validation interface should be able to
read these rules from the schema definition, check that schema
definition is consistent and then check that the configuration file
complies with the grammar.

Schema Definition {#SchemaDefinition}
-----------------

This section describes the schema definition grammar and rules. The
schema definition will be represented by a file or a series of files in
the INI format. This means that the structure of the schema definition
file(s) can be read by the same INI parsing functions as the application
configuration file. There are several main concepts related to schema

-   Schema defines rules about key value pairs (KVPs) of the application
    configuration file. This includes properties like type of the value,
    is it mandatory, is it a single value or a list of values etc.
-   Schema defines rules about relations between different parts of the
    configuration file. With the rules one would be able to describe
    complex business logic. This is acknowledged that it is not a high
    priority to support rules in grammar in the first implementation so
    we are not going to describe the semantics of the rules here.
-   Each KVP of the config file is described with the section in the
    schema file. The section in the schema file would have the following
    structure: The name of the section is a global (to the schema)
    unique name used to refer to the KVP inside the schema definition.
    Do not confuse it with the name of the key. Keys with same name can
    be used in different sections of the config file. We will use the
    term “label” when we will talk about this name. The section itself
    will consist of the set of predefined keys and values. The keys
    would define the properties of the KVP in the config file. So the
    structure will look like this: \[label\] property0 = value0
    property1 = value1 property2 = value2 property3 = value3 property4 =
    value4

> In real schema file the properties will be taken from a predefined set
> of properties described later on this page.

-   Schema definitions allows implications – this means that there are
    some properties that imply other properties. For example a special
    property that would identify KVP as a section list would imply that
    the KVP is a list and that the type of the KVP is a string. This
    will be described in more details later on the page.
-   Schema will be extensible. This means that it can be split between
    multiple files. Currently the logic implemented for the
    configuration file is the following: Read first files and then
    update the configuration using other files. So for config files the
    interface would automatically merge the configuration information.
    For the schema the logic is a bit different. The main schema file
    that comes with the application is the main file. It can't be
    altered only amended by the information read from the other schema
    file. The amending file would be able to describe KVPs that are not
    present in the main schema file or amend existing KVP definitions in
    a compliant way. The rules of compliance will be defined later on
    this page.

Catalog of the KVP properties {#CatalogoftheKVPproperties}
-----------------------------

<div class="document">

For now we will cover only properties that describe the configuration
file values not rules.

  Key                                                Description               Value type                                         Mandatory                                          Values                                                    Default                              Implies                                            Implied by                                         Collides                                                         Enabled by
  -------------------------------------------------- ------------------------- -------------------------------------------------- -------------------------------------------------- --------------------------------------------------------- ------------------------------------ -------------------------------------------------- -------------------------------------------------- ---------------------------------------------------------------- ---------------------------------------------------------
  type                                               Type of the section.      String                                             No                                                 “field” “extend”                                          field                                                                                   vtype                                                                                                                

</div>

Next table shows keys that can only be present in the section of the
type “field”

<div class="document">

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Key                                                Description               Value type                                         Mandatory                                   Values                                                    Default                              Implies                                            Implied by                                         Collides                                                         Enabled by
  -------------------------------------------------- ------------------------- -------------------------------------------------- ------------------------------------------- --------------------------------------------------------- ------------------------------------ -------------------------------------------------- -------------------------------------------------- ---------------------------------------------------------------- ----------------------------------------------------------------
  vtype                                              Type of the value         String                                             Yes                                         “string” “int” “unsigned” “long” “ulong” “double” “bool”                                       type                                               as string if seclist is yes                                                                                          
                                                                                                                                                                              “int32” “uint32” “int64” “uint64”                                                                                                                                                                                                                                     

  name                                               Name of the key           String                                             Yes                                         any                                                                                                                                                                                                                                                                    

  section                                            Name of the section       String                                             YC\*                                        any                                                                                                                                                                                                  secref                                                            

  secref                                             Reference to a            String                                             YC                                          label                                                                                                                                                                                                section                                                           
                                                     dynamically defined                                                                                                                                                                                                                                                                                                                                                                            
                                                     section                                                                                                                                                                                                                                                                                                                                                                                        

  required                                           Is the value required     Bool                                               No                                          yes/no                                                    no                                                                                                                                         requiredby                                                        

  requiredby                                         The value is              String                                             No                                          special\*                                                                                                                                                                                            required                                                          
                                                     conditionally required by                                                                                                                                                                                                                                                                                                                                                                      
                                                     another key. See what the                                                                                                                                                                                                                                                                                                                                                                      
                                                     value means in a separate                                                                                                                                                                                                                                                                                                                                                                      
                                                     section.                                                                                                                                                                                                                                                                                                                                                                                       

  list                                               Is the value actually a   Bool                                               No                                          yes/no                                                    no                                   sep (if true)                                      as yes if seclist is yes                                                                                             
                                                     list of values                                                                                                                                                                                                                                                                                                                                                                                 

  sep                                                How to parse lists        String                                             No                                          any                                                       “,”                                                                                     list if list= yes                                                                                                    

  min                                                Minimal value for a       Number                                             No                                          any                                                                                                                                                                                                                                                                   vtype is numeric
                                                     number For lists applies                                                                                                                                                                                                                                                                                                                                                                       
                                                     to every value                                                                                                                                                                                                                                                                                                                                                                                 

  max                                                Maximum value for a       Number                                             No                                          any                                                                                                                                                                                                                                                                   vtype is numeric
                                                     number For lists applies                                                                                                                                                                                                                                                                                                                                                                       
                                                     to every value                                                                                                                                                                                                                                                                                                                                                                                 

  enabledby                                          The list of other keys    String                                             No                                          special\*                                                                                                                                                                                                                                                              
                                                     that enable this key.                                                                                                                                                                                                                                                                                                                                                                          

  seclist                                            The value is list of the  Bool                                               No                                          yes/no                                                    no                                   list=yes vtype= string                                                                                                                                                  
                                                     subsection                                                                                                                                                                                                                                                                                                                                                                                     

  secpf                                              Prefix for the subsection String                                             No                                                                                                                                                                                                                                               secpfref                                                          

  secpfref                                           Reference to a single     String                                             No                                          label                                                                                                                                                                                                secpf                                                             
                                                     value key that defines                                                                                                                                                                                                                                                                                                                                                                         
                                                     prefix                                                                                                                                                                                                                                                                                                                                                                                         

  match                                              Multi value attribute     Strlist                                            No                                          regex\*                                                                                                                                                                                              choices                                                           
                                                     that defines a series of                                                                                                                                                                                                                                                                                                                                                                       
                                                     match patterns the KVP                                                                                                                                                                                                                                                                                                                                                                         
                                                     values should match.                                                                                                                                                                                                                                                                                                                                                                           

  choices                                            Multi value attribute     List                                               No                                          any                                                                                                                                                                                                  match                                                             
                                                     that defines a series of                                                                                                                                                                                                                                                                                                                                                                       
                                                     possible values for the                                                                                                                                                                                                                                                                                                                                                                        
                                                     KVP value.                                                                                                                                                                                                                                                                                                                                                                                     

  extensible                                         Can the value be extended Bool                                               No                                          yes/no                                                    no                                                                                                                                                                                                          list is yes
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

This table contains properties available in the section of the “extend”
type

<div class="document">

+-------------------------------------------------+------------------------+-------------------------------------------------+-------------------------------------------------+--------------------------------------------------------+-----------------------------------+-------------------------------------------------+-------------------------------------------------+---------------------------------------------------------------+--------------------------------------------------------+
| Key                                             | Description            | Value type                                      | Mandatory                                       | Values                                                 | Default                           | Implies                                         | Implied by                                      | Collides                                                      | Enabled by                                             |
+=================================================+========================+=================================================+=================================================+========================================================+===================================+=================================================+=================================================+===============================================================+========================================================+
| name                                            | Type of the value to   | String                                          | Yes                                             | label                                                  |                                   |                                                 |                                                 |                                                               |                                                        |
|                                                 | extend.                |                                                 |                                                 |                                                        |                                   |                                                 |                                                 |                                                               |                                                        |
+-------------------------------------------------+------------------------+-------------------------------------------------+-------------------------------------------------+--------------------------------------------------------+-----------------------------------+-------------------------------------------------+-------------------------------------------------+---------------------------------------------------------------+--------------------------------------------------------+
| value                                           | The value to use in    | -                                               | Yes                                             |                                                        |                                   |                                                 |                                                 |                                                               |                                                        |
|                                                 | extend The value is    |                                                 |                                                 |                                                        |                                   |                                                 |                                                 |                                                               |                                                        |
|                                                 | treated as the value   |                                                 |                                                 |                                                        |                                   |                                                 |                                                 |                                                               |                                                        |
|                                                 | of the same type as    |                                                 |                                                 |                                                        |                                   |                                                 |                                                 |                                                               |                                                        |
|                                                 | the referenced KVP.    |                                                 |                                                 |                                                        |                                   |                                                 |                                                 |                                                               |                                                        |
+-------------------------------------------------+------------------------+-------------------------------------------------+-------------------------------------------------+--------------------------------------------------------+-----------------------------------+-------------------------------------------------+-------------------------------------------------+---------------------------------------------------------------+--------------------------------------------------------+

</div>

Some of the clarification of the terms used above:

-   **special** – the following syntax of the value will be used: key =
    label1\[value1, ...\], label2\[value2, ...\] where:
    -   **key** - is for now “requiredby” or “enabledby”
    -   **label** - is a name of some other section
    -   **\[...\]** - optional section, if present should contain a list
        of values that trigger the requirement or enablement. If omitted
        the presence of the key

> > > would trigger the enablement.
> >
> > The list can consist of multiple enablers.

-   **YC** - means yes but only one of the colliding properties must be
    present
-   **regex** - is a pcre based regular expression, actually a list of
    them

Processing logic (high level) {#Processinglogichighlevel}
-----------------------------

-   Read schema
-   Read configuration (already available)
-   Validate

### Read Schema {#ReadSchema}

-   Open main schema file (do some permissions checks if needed)
-   Read it with INI parser
-   Validate grammar
-   For any additional schema file
    -   Read file into separate handle
    -   Validate grammar and references
-   Create a validation object which is a collection (can be done
    partially on the fly) It should include an expanded tree of possible
    dynamically defined subsections and possible KVP that can be found
    in those sections. It will be searchable by section+key combination.
    The extends are merged in at that point and all the implications are
    translated.

### Validate {#Validate}

-   For each key in each section
    -   Find its definition in validation object
    -   Check that value matches all defined properties
    -   Report error on failure

Outline of the work {#Outlineofthework}
-------------------

-   Preparation
    -   Add support for additional data types into conversion
        functions - patch is on the list
    -   Add support for sting lists with explicitly quoted elements -
        proposed approach is attached to the ticket
        [\#449](https://fedorahosted.org/sssd/ticket/449 "enhancement: INI allow trailing and leading spaces in the values (closed: wontfix)"){.closed
        .ticket}
-   Read the schema
    -   Create a twin of the ini\_to\_collection function and convert it
        to schema\_to\_collection
    -   Wrap it into high level interfaces similar to the config ones
    -   Define the internal representation of the value read from the
        schema. It should be decomposed for easier validation
-   Validate grammar itself
    -   For each KVP definition :
        -   Check:
            -   Mandatory properties are defined
            -   Not enabled properties are not defined
            -   Colliding properties are not defined
            -   Referenced properties are defined and they are not this
                same property (avoid reflexive references)
            -   Check collisions on implications
        -   Translate into internal representation
            -   Check the values match given type
            -   Check correctness of the default values and regular
                expressions
-   Construct or complete constructing the validation object
-   Validate
    -   For each key in each section of the config file
        -   Find its definition in the validation object
        -   Check that value matches all defined properties (details
            TBD)
        -   Report error on failure

