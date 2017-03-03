Using HTML in Wiki Text
=======================

Trac supports inserting HTML into any wiki context, accomplished using
the ``#!html``
`WikiProcessor <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__.

However a constraint is that this HTML has to be well-formed. In
particular you can't insert a start tag in an ``#!html`` block, resume
normal wiki text and insert the corresponding end tag in a second
``#!html`` block.

Fortunately, for creating styled <div>s, <span>s or even complex tables
containing arbitrary Wiki text, there's a powerful alternative: use of
dedicated ``#!div``, ``#!span`` and ``#!table``, ``#!tr``, ``#!td`` and
``#!th`` blocks.

Those Wiki processors are built-in, and does not require installing any
additional packages.

How to use ``#!html``
---------------------

To inform the wiki engine that a block of text should be treated as
HTML, use the *html* processor.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. rubric:: HTML Test                |
|                                      |    :name: html-test                  |
|     {{{                              |                                      |
|     #!html                           |                                      |
|     <h1 style="text-align: right; co |                                      |
| lor: blue">HTML Test</h1>            |                                      |
|     }}}                              |                                      |
+--------------------------------------+--------------------------------------+

Note that Trac sanitizes your HTML code before displaying it. That means
that if you try to use potentially dangerous constructs such as
Javascript event handlers, those will be removed from the output.

Since 0.11, the filtering is done by Genshi, and as such, the produced
output will be a well-formed fragment of HTML. As noted above in the
introduction, this mean that you can no longer use two HTML blocks, one
for opening a <div>, the second for closing it, in order to wrap
arbitrary wiki text. The new way to wrap any wiki content inside a <div>
is to use the ``#!div`` Wiki processor.

How to use ``#!div`` and ``#!span``
-----------------------------------

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div class="important">           |
|     #!div class="important"          |                                      |
|     **important** is a predefined cl | **important** is a predefined class. |
| ass.                                 |                                      |
|     }}}                              | .. raw:: html                        |
|                                      |                                      |
| .. code:: wiki                       |    </div>                            |
|                                      |                                      |
|     {{{                              | .. raw:: html                        |
|     #!div style="border: 1pt dotted; |                                      |
|  margin: 1em"                        |    <div class="wikipage"             |
|     **wikipage** is another predefin |    style="border: 1pt dotted; margin |
| ed class that will                   | : 1em">                              |
|     be used when no class is specifi |                                      |
| ed.                                  | **wikipage** is another predefined   |
|     }}}                              | class that will be used when no      |
|                                      | class is specified.                  |
| .. code:: wiki                       |                                      |
|                                      | .. raw:: html                        |
|     {{{                              |                                      |
|     #!div class="compact" style="bor |    </div>                            |
| der: 1pt dotted; margin: 1em"        |                                      |
|     **compact** is another predefine | .. raw:: html                        |
| d class reducing                     |                                      |
|     the padding within the `<div>` t |    <div class="compact"              |
| o a minimum.                         |    style="border: 1pt dotted; margin |
|     }}}                              | : 1em">                              |
|                                      |                                      |
| .. code:: wiki                       | **compact** is another predefined    |
|                                      | class reducing the padding within    |
|     {{{                              | the ``<div>`` to a minimum.          |
|     #!div class="wikipage compact" s |                                      |
| tyle="border: 1pt dotted"            | .. raw:: html                        |
|     Classes can be combined (here ** |                                      |
| wikipage** and **compact**)          |    </div>                            |
|     which results in this case in re |                                      |
| duced //vertical//                   | .. raw:: html                        |
|     padding but there's still some h |                                      |
| orizontal space for coping           |    <div class="wikipage compact"     |
|     with headings.                   |    style="border: 1pt dotted">       |
|     }}}                              |                                      |
|                                      | Classes can be combined (here        |
| .. code:: wiki                       | **wikipage** and **compact**) which  |
|                                      | results in this case in reduced      |
|     {{{                              | *vertical* padding but there's still |
|     #!div class="" style="border: 1p | some horizontal space for coping     |
| t dotted; margin: 1em"               | with headings.                       |
|     Explicitly specifying no classes |                                      |
|  is //not// the same                 | .. raw:: html                        |
|     as specifying no class attribute |                                      |
| , as this will remove                |    </div>                            |
|     the //wikipage// default class.  |                                      |
|     }}}                              | .. raw:: html                        |
|                                      |                                      |
|                                      |    <div                              |
|                                      |    style="border: 1pt dotted; margin |
|                                      | : 1em">                              |
|                                      |                                      |
|                                      | Explicitly specifying no classes is  |
|                                      | *not* the same as specifying no      |
|                                      | class attribute, as this will remove |
|                                      | the *wikipage* default class.        |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

Note that the contents of a ``#!div`` block are contained in one or more
paragraphs, which have a non-zero top and bottom margin. This leads to
the top and bottom padding in the example above. To remove the top and
bottom margin of the contents, add the ``compact`` class to the
``#!div``. Another predefined class besides ``wikipage`` and ``compact``
is ``important``, which can be used to make a paragraph stand out. Extra
CSS classes can be defined via the ``site/style.css`` file for example,
see
`TracInterfaceCustomization#SiteAppearance <https://docs.pagure.org/sssd-test2/TracInterfaceCustomization.html#SiteAppearance>`__.

For spans, you should rather use the Macro call syntax:

+--------------------------------------------------------------------------+
| Wiki Markup                                                              |
+==========================================================================+
| .. code:: wiki                                                           |
|                                                                          |
|     Hello                                                                |
|     [[span(''WORLD'' (click [#anchor here]), style=color: green; font-si |
| ze: 120%, id=anchor)]]!                                                  |
+--------------------------------------------------------------------------+
| Display                                                                  |
+--------------------------------------------------------------------------+
|     Hello *WORLD* (click                                                 |
|     `here <https://fedorahosted.org/sssd#anchor>`__)!                    |
+--------------------------------------------------------------------------+

How to use ``#!td`` and other table related processors
------------------------------------------------------

``#!td`` or ``#!th`` processors are actually the main ones, for creating
table data and header cells, respectively. The other processors
``#!table`` and ``#!tr`` are not required for introducing a table
structure, as ``#!td`` and ``#!th`` will do this automatically. The
``|-`` row separator can be used to start a new row when needed, but
some may prefer to use a ``#!tr`` block for that, as this introduces a
more formal grouping and offers the possibility to use an extra level of
indentation. The main purpose of the ``#!table`` and ``#!tr`` is to give
the possibility to specify HTML attributes, like *style* or *valign* to
these elements.

Wiki Markup

Display

.. code:: wiki

    Simple 2x2 table with rich content:
    {{{#!th align=left
     - Left
     - Header
    }}}
    {{{#!th align=left
     - Right
     - Header
    }}}
    |----------------------------------
    {{{#!td style="background: #ffd"
     - Left
     - Content
    }}}
    {{{#!td style="vertical-align: top"
    !RightContent
    }}}
    |----------------------------------
    || ... and this can be mixed||\
    ||with pipe-based cells ||
    {{{#!td colspan=2
    Pick the style the more appropriate
    to your content

    See WikiFormatting#Tables for details
    on the pipe-based table syntax.
    }}}

    If one needs to add some 
    attributes to the table itself...

    {{{
    #!table style="border:none;text-align:center;margin:auto"
      {{{#!tr ====================================
        {{{#!th style="border: none"
        Left header
        }}}
        {{{#!th style="border: none"
        Right header
        }}}
      }}}
      {{{#!tr ==== style="border: 1px dotted grey"
        {{{#!td style="border: none"
        1.1
        }}}
        {{{#!td style="border: none"
        1.2
        }}}
      }}}
      {{{#!tr ====================================
        {{{#!td style="border: none"
        2.1
        }}}
        {{{#!td
        2.2
        }}}
      }}}
    }}}

Simple 2x2 table with rich content:

-  Left
-  Header

-  Right
-  Header

-  Left
-  Content

RightContent

... and this can be mixed

with pipe-based cells

Pick the style the more appropriate to your content

See
`WikiFormatting#Tables <https://docs.pagure.org/sssd-test2/WikiFormatting.html#Tables>`__
for details on the pipe-based table syntax.

If one needs to add some attributes to the table itself...

+--------------------------------------+--------------------------------------+
| Left header                          | Right header                         |
+======================================+======================================+
| 1.1                                  | 1.2                                  |
+--------------------------------------+--------------------------------------+
| 2.1                                  | 2.2                                  |
+--------------------------------------+--------------------------------------+

Note that by default tables are assigned the "wiki" CSS class, which
gives a distinctive look to the header cells and a default border to the
table and cells (as can be seen for the tables on this page). By
removing this class (``#!table class=""``), one regains complete control
on the table presentation. In particular, neither the table, the rows
nor the cells will have a border, so this is a more effective way to get
such an effect than having to specify a ``style="border: no"`` parameter
everywhere.

Wiki Markup

Display

.. code:: wiki

    {{{#!table class=""
    ||  0||  1||  2||
    || 10|| 20|| 30||
    || 11|| 22|| 33||
    ||||||=  numbers  =||
    }}}

0

1

2

10

20

30

11

22

33

numbers

Other classes can be specified as alternatives (remember that you can
define your own in
`site/style.css <https://docs.pagure.org/sssd-test2/TracInterfaceCustomization.html#SiteAppearance>`__).

Wiki Markup

Display

.. code:: wiki

    {{{#!table class="listing"
    ||  0||  1||  2||
    || 10|| 20|| 30||
    || 11|| 22|| 33||
    ||||||=  numbers  =||
    }}}

0

1

2

10

20

30

11

22

33

numbers

HTML comments
-------------

HTML comments are stripped from the output of the ``html`` processor. To
add an HTML comment to a wiki page, use the ``htmlcomment`` processor
(available since 0.12). For example, the following code block:

+--------------------------------------------------------------------------+
| Wiki Markup                                                              |
+==========================================================================+
| .. code:: wiki                                                           |
|                                                                          |
|     {{{                                                                  |
|     #!htmlcomment                                                        |
|     This block is translated to an HTML comment.                         |
|     It can contain <tags> and &entities; that will not be escaped in the |
|  output.                                                                 |
|     }}}                                                                  |
+--------------------------------------------------------------------------+
| Display                                                                  |
+--------------------------------------------------------------------------+
| .. code:: wiki                                                           |
|                                                                          |
|     <!--                                                                 |
|     This block is translated to an HTML comment.                         |
|     It can contain <tags> and &entities; that will not be escaped in the |
|  output.                                                                 |
|     -->                                                                  |
+--------------------------------------------------------------------------+

Please note that the character sequence "``--``" is not allowed in HTML
comments, and will generate a rendering error.

More Information
----------------

-  `​http://www.w3.org/ <http://www.w3.org/>`__ -- World Wide Web
   Consortium
-  `​http://www.w3.org/MarkUp/ <http://www.w3.org/MarkUp/>`__ -- HTML
   Markup Home Page

--------------

See also:
`WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__,
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__,
`WikiRestructuredText <https://docs.pagure.org/sssd-test2/WikiRestructuredText.html>`__
