.. raw:: html

   <div class="wiki-toc">

#. `Introduction <#Introduction>`__
#. `Why Coding Guidelines? <#WhyCodingGuidelines>`__

   #. `Maintainability <#Maintainability>`__
   #. `Readability <#Readability>`__

#. `Definitions <#Definitions>`__
#. `Note on C99 <#NoteonC99>`__
#. `Rules <#Rules>`__

   #. `General Rules <#GeneralRules>`__
   #. `Spaces and Indentation <#SpacesandIndentation>`__
   #. `Length of Line <#LengthofLine>`__
   #. `Comments <#Comments>`__
   #. `IFDEF <#IFDEF>`__
   #. `Include Files <#IncludeFiles>`__
   #. `Macros <#Macros>`__
   #. `Use of goto <#Useofgoto>`__

      #. `Label done <#Labeldone>`__
      #. `Label fail <#Labelfail>`__

   #. `Variables <#Variables>`__

      #. `Naming <#Naming>`__
      #. `Declaring <#Declaring>`__
      #. `Use of Typedefs <#UseofTypedefs>`__
      #. `Declaring Structures <#DeclaringStructures>`__
      #. `Global Variables <#GlobalVariables>`__

   #. `Functions <#Functions>`__

      #. `External Function
         Declarations <#ExternalFunctionDeclarations>`__
      #. `Declaring Module Functions <#DeclaringModuleFunctions>`__
      #. `Order of the Functions <#OrderoftheFunctions>`__
      #. `Naming Functions <#NamingFunctions>`__
      #. `Indenting Functions <#IndentingFunctions>`__
      #. `Function Declaration <#FunctionDeclaration>`__
      #. `Function Parameters <#FunctionParameters>`__
      #. `Use of Const <#UseofConst>`__
      #. `Tools to Use <#ToolstoUse>`__

   #. `Conditions and Statements <#ConditionsandStatements>`__

      #. `Condition <#Condition>`__
      #. `IF Statements <#IFStatements>`__
      #. `Loops <#Loops>`__

         #. `Switch <#Switch>`__

   #. `Strings <#Strings>`__

      #. `Internationalized (i18n)
         Strings <#Internationalizedi18nStrings>`__

.. raw:: html

   </div>

This guide is work in progress and should replace the older FreeIPA
guide.

Introduction
============

This manual contains coding standards and guidelines for SSSD and
FreeIPA contributors. It is updated based heavily on the FreeIPA style
which was based on `​389 Directory Server style
guide <http://directory.fedoraproject.org/wiki?title=Coding_Style>`__
but deviates from it and covers more aspects.

All new code should adhere to these standards but please do not go back
and make wholesale formatting changes to the old code. It just confuses
things and is generally a waste of time.

Why Coding Guidelines?
======================

The Coding Guidelines are necessary to improve maintainability and
readability of the code.

Maintainability
---------------

If you're merging changes from a patch it's much easier if everyone is
using the same coding style. This isn't the reality for a lot of our
code, but we're trying to get to the point where most of it uses the
same style.

Readability
-----------

Remember, code isn't just for compilers, it's for people, too. If it
wasn't for people, we would all be programming in assembly. Coding style
and consistency mean that if you go from one part of the code to another
you don't spend time having to re-adjust from one style to another.
Blocks are consistent and readable and the flow of the code is apparent.
Coding style adds value for people who have to read your code after
you've been hit by a bus. Remember that.

Definitions
===========

The following guidelines apply to developing code in the SSSD project.
Some rules are mandatory some rules are just suggestions or
recommendations. We will use following terminology to identify whether
this or that rule is mandatory or not.

-  MUST – everybody must follow the rule
-  HIGHLY RECOMMENDED – the rule should be followed unless there are
   some serious reasons why they should not be followed.
-  RECOMMENDED – it is a best practice to use this rule. It is not
   required but strongly encouraged.
-  DISCRETION – follow this at developer discretion.

Note on C99
===========

We compile code with -std=gnu99 flag. It is OK to use C99 features
supported by GCC and Clang, however C++ style line comments (*) should
still be avoided. Using variable length arrays should be done with
caution and only be used for smaller arrays.*

Rules
=====

General Rules
-------------

-  MUST: All source and header files must include a copy of the license.
-  HIGHLY RECOMMENDED: Stick to a K&R coding style for C.
-  HIGHLY RECOMMENDED: Curly braces on same line as if/while.
-  MUST: All code should be peer reviewed before being checked in.
-  MUST: If you are fixing a bug, attach the patch to the bug report.
-  HIGHLY RECOMMENDED: For Python we have an enforced style in many
   cases already but consistency is important.

Spaces and Indentation
----------------------

-  MUST: No tabs all indentation 4 spaces.
-  HIGHLY RECOMMENDED: When wrapping lines, try to break it:

   -  after a comma
   -  before an operator
   -  align the new line with the beginnigng of the expression at the
      same level in the previous line
   -  in case of long "if" statements, wrap the line before an operator
      and indent the new line
   -  if all else fails, just indent 8 spaces.

Length of Line
--------------

MUST: Do not make lines longer than 120 characters.

HIGHLY RECOMMENDED: Keep lines within 80 character boundary for better
readability.

Comments
--------

MUST: Use only C style comments /\* \*/ not C++.

MUST: When commenting use the following styles:

.. code:: wiki

        /*
         * VERY important single-line comments look like this.
         */

        /* Most single-line comments look like this. */

        /*
         * Multi-line comments look like this. Make them real sentences. Fill
         * them so they look like real paragraphs.
         */

Avoid:

.. code:: wiki

        /* Multiline comments
           that look like this */

HIGHLY RECOMMENDED: Avoid useless comments that do not add value to the
code.

HIGHLY RECOMMENDED: Each function should be preceded with a block
comment describing what the function is supposed to do.

HIGHLY RECOMMENDED: Block comments should be preceded by a blank line to
set it apart. Line up the \* characters in the block comment.

HIGHLY RECOMMENDED: Python comments can use either the # or """ form

IFDEF
-----

HIGHLY RECOMMENDED: When using #ifdefs, it's nice to add comments in the
pairing #endif:

.. code:: wiki

       #ifndef _HEADER_H_
       #define _HEADER_H_
       
       /* something here */
       
       #endif /* !_HEADER_H_ */

or:

.. code:: wiki

       #ifdef HAVE_PTHREADS
       
       /* some code here */
       
       #else /* !HAVE_PTHREADS */
       
       /* some other code here */
       
       #endif /* HAVE_PTHREADS */

Include Files
-------------

RECOMMENDED: Includes should be grouped properly. Standard headers and
local headers should definitely be separated by a blank line. Other
logical grouping should be reasonably done if needed. Files inside the
groups should be sorted alphabetically, unless a specific order is
required - this however is very rare, and must not happen. Also, one
shouldn't depend on the fact that one header file includes other one,
unless it is really obvious and/or desirable, like in cases when one
header file practically "enhances" the other one, for example with more
error codes, etc.

Macros
------

HIGHLY RECOMMENDED: Macros that are unsafe should be in upper-case. This
also applies to macros that span multiple lines:

.. code:: wiki

       #define MY_MACRO(a, b) do {   \
                    foo((a) + (b));  \
                    bar(a);          \
       } while (0)

Notice that arguments should be in parentheses if there's a risk. Also
notice that a is referenced two times, and hence the macro is dangerous.
Wrapping the body in do { } while (0) makes it safe to use it like this:

.. code:: wiki

       if (expr)
           MY_MACRO(x, y);

Notice the semicolon is used after the invocation, not in the macro
definition.

Otherwise, if a macro is safe (for example a simple wrapping function),
then the case can be lower-case.

Use of goto
-----------

We use goto to simplify cleanup operations and some other tasks that
need to be done before leaving the function.

MUST: Never use goto to jump backwards in the code

HIGHLY RECOMMENDED: If goto is needed in the code, use one of the
following labels: done, fail (TBD: add other allowed labels)

RECOMMENDED: Do not use more than one goto label per function.

Label done
~~~~~~~~~~

Label done is used as jump target before exit. Clean-up operations, such
as freeing local talloc context, usually follow the done label. Both
successful and unsuccessful function executions pass this label.

Label fail
~~~~~~~~~~

Used as special exit path when function fails. Successful function
execution typically does not execute statements after this label.

Variables
---------

Naming
~~~~~~

HIGHLY RECOMMENDED: Use low case multi word underscore separated
notation for naming variables.

HIGHLY RECOMMENDED: Make name meaningful.

MUST: Never use Hungarian notation when naming variables.

Declaring
~~~~~~~~~

.. code:: wiki

    RECOMMENDED: One declaration per line is preferred.
        int foo;
        int bar;

instead of

.. code:: wiki

       int foo, bar;

HIGHLY RECOMMENDED: Initialize at declaration time when possible.

RECOMMENDED: Avoid complex variable initializations (like calling
functions) when declaring variables like:

.. code:: wiki

       int foobar = get_foobar(baz);

    but split it in:

       int foobar;
       
       foobar = get_foobar(baz);
       ...

MUST: Always declare variables at the top of the function or block. If
you find yourself declaring many variables inside inner block or loop,
consider refactoring the block into helper function. HIGHLY RECOMMENDED:
Avoid shadowing variables. Use different name even if the shadowed
variable is not important for the inner blocks.

RECOMMENDED: Don't initialize static or global variables to 0 or NULL.

Use of Typedefs
~~~~~~~~~~~~~~~

HIGHLY RECOMMENDED: Avoid using typedefs. Typedefs obscure structures
and make it harder to understand and debug.

Declaring Structures
~~~~~~~~~~~~~~~~~~~~

DISCRETION: When defining structure or union try make it easy to read.
You may use some form of alignment if you see that this might make it
more readable.

Global Variables
~~~~~~~~~~~~~~~~

HIGHLY RECOMMENDED: Avoid using global variables. They make for very
poor code. Should be used only if no other way can be found. They tend
to be not thread/async safe

Functions
---------

External Function Declarations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HIGHLY RECOMMENDED: Avoid situations where you have to explicitly list
out external function. The header files should in general take care of
the external function declaration. If this is not the case it is subject
for review of the header file hierarchy.

Declaring Module Functions
~~~~~~~~~~~~~~~~~~~~~~~~~~

DISCRETION: It up to the developer to define the order of the functions
in the module and thus declare functions at the top or use a native flow
of the module and avoid forward function declarations.

Order of the Functions
~~~~~~~~~~~~~~~~~~~~~~

DISCRETION: It is up to the developer which approach to use: whether to
write the main function at the top of the module and then all the
supporting functions or start with supporting functions and have the
main one at the bottom. Both approaches are acceptable. One can use
additional comments to help identify how the module is structured.

Naming Functions
~~~~~~~~~~~~~~~~

MUST: For function names use multi word underscore separate naming
convention like this monitor\_task\_init(struct task\_server \*task);

MUST: Never use Hungarian notation when naming functions.

Indenting Functions
~~~~~~~~~~~~~~~~~~~

DISCRETION: It is up to the developer which pattern to use when
indenting the function parameters if function has long name and has to
be split between multiple lines. The pattern however MUST be consistent
across the module so if you are fixing somebodies code continue with the
pattern used in the module.

Function Declaration
~~~~~~~~~~~~~~~~~~~~

DISCRETION: It is up to the developer whether to put the return type of
the function and modifiers (static for example) in front of the function
on the same line or start the line with the an actual function name. In
any case the pattern MUST be consistent across the module. If you are
adding function to an already existing module follow its pattern. MUST:
Put opening “{“ of the function body on the beginning of the new line
after the function declaration. HIGHLY RECOMMENDED: Do not put spaces
before or after parenthesis in the declaration of the parameters. For
example:

    OK: `` int foo(int bar, int baz); `` NOT OK:
    `` int bad ( arg1 , arg2 ); ``

Function Parameters
~~~~~~~~~~~~~~~~~~~

RECOMMENDED: Try to always put "input" arguments before "output"
arguments, if you have arguments that provide both input an output put
them between the pure-input and the pure-output ones. Add underscore
prefix "\_" to output arguments.

    OK: `` foo(int in1, void *in2, char **_ou1); `` NOT OK:
    `` voo(char **ou1, int in1); ``

Use of Const
~~~~~~~~~~~~

RECOMMENDED: If appropriate, always use the const modifier for pointers
passed to the function. This makes the intentions of the function more
clearer, plus allows the compiler to catch more bugs and make some
optimizations.

Tools to Use
~~~~~~~~~~~~

RECOMMENDED: Creating lists and queues was already done a lot of times.
When possible, use some common functions for manipulating these to avoid
mistakes.

Conditions and Statements
-------------------------

Condition
~~~~~~~~~

RECOMMENDED: Use the full condition syntax like (str == NULL) rather
than (!str).

IF Statements
~~~~~~~~~~~~~

HIGHLY RECOMMENDED: If-else statements should have the following form:

.. code:: wiki

        if (''condition'') {
            /* do some work */
        }

        if (''condition'') {
            /* do some work */
        } else {
            /* do some other work */
        }

HIGHLY RECOMMENDED: Balance the braces in the if and else in an if-else
statement if either has only one line:

.. code:: wiki

        if (condition) {
            /*
             * stuff that takes up more than one
             * line
             */
        } else {
            /* stuff that only uses one line */
        }

HIGHLY RECOMMENDED: Use braces even if there s just one line in the if
statement.

DISCRETION: You can avoid the braces if entire if statement is on one
line.

NOT OK:

.. code:: wiki

        if (foo)
            bar();

OK:

.. code:: wiki

        if (foo) {
            bar();
        }

Also OK:

.. code:: wiki

        if (foo) bar();

Always use braces if there is an else part:

.. code:: wiki

        if (foo) {
            bar();
        } else {
            baz();
        }

HIGHLY RECOMMENDED: Avoid last-return-in-else problem. Code should look
like this:

.. code:: wiki

        int foo(int bar)
        {
            if (something) {
                /* stuff done here */
                return 1;            
            }
        
            return 0;
        }

**NOT** like this:

.. code:: wiki

        int foo(int bar)
        {
            if (something) {
                /* stuff done here */
                return 1;            
            } else {
                return 0;
            }
        }

HIGHLY RECOMMENDED: Conditions with <, <=, >= or == operators should
isolate the value being checked (untrusted value) on the left hand side
of the comparison. The right hand side should contain trusted values
(thus avoiding overflows/underflows). Use unsigned types when storing
sizes or lengths. For example if variable len is untrusted and variables
size and p are trusted (NOTE: sizes and length should be stored in
unsigned types):

    NOT OK: `` if ((p + len ) > size) return EINVAL; `` OK:
    `` if (len > size - p) return EINVAL; ``

Loops
~~~~~

HIGHLY RECOMMENDED: For, while and until statements should take a
similar form:

.. code:: wiki

        for (''initialization; condition; update'') {
            /* iterate here */
        }

        while (''condition'') {
            /* do some work */
        }

Switch
^^^^^^

HIGHLY RECOMMENDED: Use the following style for the switch statements.
Add comments if missing break is intentional.

.. code:: wiki

       switch (var) {
       case 0:
           break;
       case 1:
           printf("meh.\n");
           /* FALLTHROUGH */
       case 2:
           printf("2\n");
           break;
       default:
           /* Always have default */
           break;
       }

Strings
-------

Internationalized (i18n) Strings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the string will be internationalized (e.g. is marked with \_()) and
it has more than one format substitution you ***MUST*** use *index*
format specifiers, not positional format specifiers. Translators need
the option to reorder where substitutions appear in a string because the
ordering of nouns, verbs, phrases, etc. differ between languages. If
conventional positional format conversion specifiers (e.g. %s %d) are
used the string cannot be reordered because the ordering of the format
specifiers must match the ordering of the printf arguments supplying the
substitutions. The fix for this is easy, use indexed format specifiers.
An indexed specifier includes an (1 based) index to the % character that
introduces the format specifier (e.g. %1$ to indicate the first
argument). That index is used to select the matching argument from the
argument list. When indexed specifiers are used *all* format specifiers
and *all* \* width fields ***MUST*** use indexed specifiers.

Here is an example of incorrect usage with positional specifiers:

.. code:: wiki

      printf(_("item %s has %s value"), name, value);

Here is the correct usage using indexed specifiers:

.. code:: wiki

      printf(_("item %1$s has %2$s value"), name, value);

See man 3 printf as well as section 15.3.1 "C Format Strings" in the GNU
gettext manual for more details.
