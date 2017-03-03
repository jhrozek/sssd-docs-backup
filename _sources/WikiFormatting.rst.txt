`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__
===========================================================================

.. raw:: html

   <div class="system-message">

**Error: Macro TracGuideToc(None) failed**
::

    'NoneType' object has no attribute 'find'

.. raw:: html

   </div>

Wiki markup is a core feature in Trac, tightly integrating all the other
parts of Trac into a flexible and powerful whole.

Trac has a built in small and powerful wiki rendering engine. This wiki
engine implements an ever growing subset of the commands from other
popular Wikis, especially `​MoinMoin <http://moinmo.in/>`__ and
`​WikiCreole <http://trac.edgewall.org/intertrac/WikiCreole>`__.

This page will give you an in-depth explanation of the wiki markup
available anywhere
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__
is allowed.

The *Cheat sheet* below gives you a quick overview for the most common
syntax, each link in the *Category* column will lead you to the more
detailed explanation later in this page.

A few other wiki pages present the advanced features of the Trac wiki
markup in more depth:

-  `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__
   covers all the possible ways to refer precisely to any Trac resource
   or parts thereof,
-  `WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__
   talks about the various names a wiki page can take,
   `CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__ or
   not
-  `WikiMacros <https://docs.pagure.org/sssd-test2/WikiMacros.html>`__
   lists the macros available for generating dynamic content,
-  `WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__
   and `WikiHtml <https://docs.pagure.org/sssd-test2/WikiHtml.html>`__
   details how parts of the wiki text can be processed in special ways

Cheat sheet
-----------

**Category**

**Wiki Markup**

**Display**

`Font Styles <https://fedorahosted.org/sssd#FontStyles>`__

``'''bold'''``, ``''italic''``, ``'''''Wikipedia style'''''``

**bold**, *italic*, ***Wikipedia style***

```monospaced (''other markup ignored'')```

``monospaced (''other markup ignored'')``

``**bold**``, ``//italic//``, ``**//!WikiCreole style//**``

**bold**, *italic*, ***WikiCreole style***

`Headings <https://fedorahosted.org/sssd#Headings>`__

.. code:: wiki

    == Level 2 ==
    === Level 3 ^([#hn note])^

Level 2
-------

Level 3 :sup:`(`note <https://fedorahosted.org/sssd#hn>`__)`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Paragraphs <https://fedorahosted.org/sssd#Paragraphs>`__

.. code:: wiki

    First paragraph
    on multiple lines.

    Second paragraph.

First paragraph on multiple lines.

Second paragraph.

`Lists <https://fedorahosted.org/sssd#Lists>`__

.. code:: wiki

    * bullets list
      on multiple lines
      1. nested list
        a. different numbering 
           styles

-  bullets list on multiple lines

   #. nested list

      #. different numbering styles

`Definition Lists <https://fedorahosted.org/sssd#DefinitionLists>`__

.. code:: wiki

     term:: definition on
            multiple lines

term
    definition on multiple lines

`Preformatted Text <https://fedorahosted.org/sssd#PreformattedText>`__

.. code:: wiki

    {{{
    multiple lines, ''no wiki''
          white space respected
    }}}

.. code:: wiki

    multiple lines, ''no wiki''
          white space respected

`Blockquotes <https://fedorahosted.org/sssd#Blockquotes>`__

.. code:: wiki

      if there's some leading
      space the text is quoted

    if there's some leading space the text is quoted

`Discussion
Citations <https://fedorahosted.org/sssd#DiscussionCitations>`__

.. code:: wiki

    >> ... (I said)
    > (he replied)

        ... (I said)

    (he replied)

`Tables <https://fedorahosted.org/sssd#Tables>`__

.. code:: wiki

    ||= Table Header =|| Cell ||
    ||||  (details below)  ||

Table Header

Cell

(details below)

`Links <https://fedorahosted.org/sssd#Links>`__

``http://trac.edgewall.org``

`​http://trac.edgewall.org <http://trac.edgewall.org>`__

``WikiFormatting (CamelCase)``

`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__
(`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__)

`TracLinks <https://fedorahosted.org/sssd#TracLinks>`__

``wiki:WikiFormatting``, ``wiki:"WikiFormatting"``

`wiki:WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__,
`wiki:"WikiFormatting" <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__

``#1 (ticket)``, ``[1] (changeset)``, ``{1} (report)``

`#1 <https://fedorahosted.org/sssd/ticket/1>`__ (ticket), [1]
(changeset), `{1} <https://fedorahosted.org/sssd/report/1>`__ (report)

``ticket:1, ticket:1#comment:1``

`ticket:1 <https://fedorahosted.org/sssd/ticket/1>`__,
`ticket:1#comment:1 <https://fedorahosted.org/sssd/ticket/1#comment:1>`__

``Ticket [ticket:1]``, ``[ticket:1 ticket one]``

Ticket `1 <https://fedorahosted.org/sssd/ticket/1>`__,
`ticket one <https://fedorahosted.org/sssd/ticket/1>`__

``Ticket [[ticket:1]]``, ``[[ticket:1|ticket one]]``

Ticket `1 <https://fedorahosted.org/sssd/ticket/1>`__,
`ticket one <https://fedorahosted.org/sssd/ticket/1>`__

`Setting Anchors <https://fedorahosted.org/sssd#SettingAnchors>`__

``[=#point1 (1)] First...``

(1) First...

``see [#point1 (1)]``

see `(1) <https://fedorahosted.org/sssd#point1>`__

`Escaping Markup <https://fedorahosted.org/sssd#Escaping>`__

``!'' doubled quotes``

'' doubled quotes

``!wiki:WikiFormatting``, ``!WikiFormatting``

wiki:WikiFormatting, WikiFormatting

`````\ ``{{{-}}}``\ `````\ `` triple curly brackets``

``{{{-}}}`` triple curly brackets

`Images <https://fedorahosted.org/sssd#Images>`__

``[[Image(``\ *link*\ ``)]]``

|trac\_logo\_mini.png|

`Macros <https://fedorahosted.org/sssd#Macros>`__

``[[MacroList(*)]]``

*(short list of all available macros)*

``[[Image?]]``

*(help for the Image macro)*

`Processors <https://fedorahosted.org/sssd#Processors>`__

.. code:: wiki

    {{{
    #!div style="font-size: 80%"
    Code highlighting:
      {{{#!python
      hello = lambda: "world"
      }}}
    }}}

.. raw:: html

   <div class="wikipage" style="font-size: 80%">

Code highlighting:

.. raw:: html

   <div class="code">

::

    hello = lambda: "world"

.. raw:: html

   </div>

.. raw:: html

   </div>

`Comments <https://fedorahosted.org/sssd#Comments>`__

.. code:: wiki

    {{{#!comment
    Note to Editors: ...
    }}}

`Miscellaneous <https://fedorahosted.org/sssd#Miscellaneous>`__

.. code:: wiki

    Line [[br]] break 
    Line \\ break
    ----

| Line
| break Line
| break

--------------

Font Styles
-----------

The Trac wiki supports the following font styles:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | -  **bold**, **triple quotes ''' can |
|                                      |    be bold too if prefixed by !** ,  |
|      * '''bold''',                   | -  *italic*                          |
|        ''' triple quotes !'''        | -  ***bold italic*** or *italic and  |
|        can be bold too if prefixed b |    **italic bold***                  |
| y ! ''',                             | -  underline                         |
|      * ''italic''                    | -  ``monospace`` or ``monospace``    |
|      * '''''bold italic''''' or ''it |    (hence ``{{{`` or ````` quoting)  |
| alic and                             | -  [STRIKEOUT:strike-through]        |
|        ''' italic bold ''' ''        | -  :sup:`superscript`                |
|      * __underline__                 | -  :sub:`subscript`                  |
|      * {{{monospace}}} or `monospace | -  **also bold**, *italic as well*,  |
| `                                    |    and ***bold italic*** ** *(since  |
|        (hence `{{{` or {{{`}}} quoti |    0.12)*                            |
| ng)                                  |                                      |
|      * ~~strike-through~~            |                                      |
|      * ^superscript^                 |                                      |
|      * ,,subscript,,                 |                                      |
|      * **also bold**, //italic as we |                                      |
| ll//,                                |                                      |
|        and **'' bold italic **'' //( |                                      |
| since 0.12)//                        |                                      |
+--------------------------------------+--------------------------------------+

Notes:

-  ``{{{...}}}`` and ```...``` commands not only select a monospace
   font, but also treat their content as verbatim text, meaning that no
   further wiki processing is done on this text.
-  `` ! `` tells wiki parser to not take the following characters as
   wiki format, so pay attention to put a space after !, e.g. when
   ending bold.
-  all the font styles marks have to be used in opening/closing pairs,
   and they must nest properly (in particular, an ``''`` italic can't be
   paired with a ``//`` one, and ``'''`` can't be paired with ``**``)

Headings
--------

You can create heading by starting a line with one up to six *equal*
characters ("=") followed by a single space and the headline text.

 The headline text can be followed by the same number of "=" characters,
but this is no longer mandatory.

Finally, the heading might optionally be followed by an explicit id. If
not, an implicit but nevertheless readable id will be generated.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     = Heading =                      |    <div class="wikipage">            |
|     == Subheading                    |                                      |
|     === About ''this'' ===           | .. rubric:: Heading                  |
|     === Explicit id === #using-expli |    :name: Heading                    |
| cit-id-in-heading                    |                                      |
|     == Subheading #sub2              | .. rubric:: Subheading               |
|                                      |    :name: Subheading                 |
|                                      |                                      |
|                                      | .. rubric:: About *this*             |
|                                      |    :name: Aboutthis                  |
|                                      |                                      |
|                                      | .. rubric:: Explicit id              |
|                                      |    :name: using-explicit-id-in-headi |
|                                      | ng                                   |
|                                      |                                      |
|                                      | .. rubric:: Subheading               |
|                                      |    :name: sub2                       |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

Paragraphs
----------

A new text paragraph is created whenever two blocks of text are
separated by one or more empty lines.

A forced line break can also be inserted, using:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       |     | Line 1                         |
|                                      |     | Line 2                         |
|     Line 1[[BR]]Line 2               |                                      |
|                                      |     Paragraph one                    |
| .. code:: wiki                       |                                      |
|                                      |     Paragraph two                    |
|     Paragraph                        |                                      |
|     one                              |                                      |
|                                      |                                      |
|     Paragraph                        |                                      |
|     two                              |                                      |
+--------------------------------------+--------------------------------------+

Lists
-----

The wiki supports both ordered/numbered and unordered lists.

Example:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | -  Item 1                            |
|                                      |                                      |
|      * Item 1                        |    -  Item 1.1                       |
|        * Item 1.1                    |                                      |
|           * Item 1.1.1               |       -  Item 1.1.1                  |
|           * Item 1.1.2               |       -  Item 1.1.2                  |
|           * Item 1.1.3               |       -  Item 1.1.3                  |
|        * Item 1.2                    |                                      |
|      * Item 2                        |    -  Item 1.2                       |
|     - items can start at the beginni |                                      |
| ng of a line                         | -  Item 2                            |
|       and they can span multiple lin |                                      |
| es                                   | -  items can start at the beginning  |
|       - be careful though to continu |    of a line and they can span       |
| e the line                           |    multiple lines                    |
|       with the appropriate indentati |                                      |
| on, otherwise                        |    -  be careful though to continue  |
|     that will start a new paragraph. |       the line with the appropriate  |
| ..                                   |       indentation, otherwise         |
|                                      |                                      |
|      1. Item 1                       | that will start a new paragraph...   |
|        a. Item 1.a                   |                                      |
|        a. Item 1.b                   | #. Item 1                            |
|           i. Item 1.b.i              |                                      |
|           i. Item 1.b.ii             |    #. Item 1.a                       |
|      1. Item 2                       |    #. Item 1.b                       |
|     And numbered lists can also be r |                                      |
| estarted                             |       #. Item 1.b.i                  |
|     with an explicit number:         |       #. Item 1.b.ii                 |
|      3. Item 3                       |                                      |
|                                      | #. Item 2                            |
|                                      |                                      |
|                                      | And numbered lists can also be       |
|                                      | restarted with an explicit number:   |
|                                      |                                      |
|                                      | 3. Item 3                            |
+--------------------------------------+--------------------------------------+

Definition Lists
----------------

The wiki also supports definition lists.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | llama                                |
|                                      |     some kind of mammal, with hair   |
|      llama::                         | ppython                              |
|        some kind of mammal, with hai |     some kind of reptile, without    |
| r                                    |     hair (can you spot the typo?)    |
|      ppython::                       |                                      |
|        some kind of reptile, without |                                      |
|  hair                                |                                      |
|        (can you spot the typo?)      |                                      |
+--------------------------------------+--------------------------------------+

Note that you need a space in front of the defined term.

Preformatted Text
-----------------

Block containing preformatted text are suitable for source code
snippets, notes and examples. Use three *curly braces* wrapped around
the text to define a block quote. The curly braces need to be on a
separate line.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. code:: wiki                       |
|                                      |                                      |
|     {{{                              |     def HelloWorld():                |
|     def HelloWorld():                |         print '''Hello World'''      |
|         print '''Hello World'''      |                                      |
|     }}}                              |                                      |
+--------------------------------------+--------------------------------------+

Note that this kind of block is also used for selecting lines that
should be processed through
`WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__.

Blockquotes
-----------

In order to mark a paragraph as blockquote, indent that paragraph with
two spaces.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | Paragraph                            |
|                                      |                                      |
|     Paragraph                        |     This text is a quote from        |
|       This text is a quote from some |     someone else.                    |
| one else.                            |                                      |
+--------------------------------------+--------------------------------------+

Discussion Citations
--------------------

To delineate a citation in an ongoing discussion thread, such as the
ticket comment area, e-mail-like citation marks (">", ">>", etc.) may be
used.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       |         Someone's original text      |
|                                      |                                      |
|     >> Someone's original text       |     Someone else's reply text        |
|     > Someone else's reply text      |                                      |
|     >  - which can be any kind of Wi |     -  which can be any kind of Wiki |
| ki markup                            |        markup                        |
|     My reply text                    |                                      |
|                                      | My reply text                        |
+--------------------------------------+--------------------------------------+

Tables
------

Simple Tables
~~~~~~~~~~~~~

Simple tables can be created like this:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | +----------+----------+----------+   |
|                                      | | Cell 1   | Cell 2   | Cell 3   |   |
|     ||Cell 1||Cell 2||Cell 3||       | +----------+----------+----------+   |
|     ||Cell 4||Cell 5||Cell 6||       | | Cell 4   | Cell 5   | Cell 6   |   |
|                                      | +----------+----------+----------+   |
+--------------------------------------+--------------------------------------+

Cell headings can be specified by wrapping the content in a pair of '='
characters. Note that the '=' characters have to stick to the cell
separators, like this:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | +--------+----------+-------------+  |
|                                      | |        | stable   | latest      |  |
|     ||        ||= stable =||= latest | +--------+----------+-------------+  |
|  =||                                 | | 0.10   | 0.10.5   | 0.10.6dev   |  |
|     ||= 0.10 =||  0.10.5  || 0.10.6d | +--------+----------+-------------+  |
| ev||                                 | | 0.11   | 0.11.6   | 0.11.7dev   |  |
|     ||= 0.11 =||  0.11.6  || 0.11.7d | +--------+----------+-------------+  |
| ev||                                 |                                      |
+--------------------------------------+--------------------------------------+

Finally, specifying an empty cell means that the next non empty cell
will span the empty cells. For example:

Wiki Markup

Display

.. code:: wiki

    || 1 || 2 || 3 ||
    |||| 1-2 || 3 ||
    || 1 |||| 2-3 ||
    |||||| 1-2-3 ||

1

2

3

1-2

3

1

2-3

1-2-3

Note that if the content of a cell "sticks" to one side of the cell and
only one, then the text will be aligned on that side. Example:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | +---------------------+-----------+  |
|                                      | | Text                | Numbers   |  |
|     ||=Text =||= Numbers =||         | +=====================+===========+  |
|     ||left align    ||        1.0||  | | left align          | 1.0       |  |
|     ||  center      ||        4.5||  | +---------------------+-----------+  |
|     ||      right align||     4.5||  | | center              | 4.5       |  |
|     || default alignment ||   2.5||  | +---------------------+-----------+  |
|     ||default||         2.5||        | | right align         | 4.5       |  |
|     ||  default ||      2.5||        | +---------------------+-----------+  |
|     || default ||       2.5||        | | default alignment   | 2.5       |  |
|                                      | +---------------------+-----------+  |
|                                      | | default             | 2.5       |  |
|                                      | +---------------------+-----------+  |
|                                      | | default             | 2.5       |  |
|                                      | +---------------------+-----------+  |
|                                      | | default             | 2.5       |  |
|                                      | +---------------------+-----------+  |
+--------------------------------------+--------------------------------------+

If contrary to the example above, the cells in your table contain more
text, it might be convenient to spread a table row over multiple lines
of markup. The ``\`` character placed at the end of a line after a cell
separator tells Trac to not start a new row for the cells on the next
line.

+--------------------------------------------------------------------------+
| Wiki Markup                                                              |
+==========================================================================+
| .. code:: wiki                                                           |
|                                                                          |
|     || this is column 1 [http://trac.edgewall.org/newticket new ticket]  |
| || \                                                                     |
|     || this is column 2 [http://trac.edgewall.org/roadmap the road ahead |
| ] || \                                                                   |
|     || that's column 3 and last one ||                                   |
+--------------------------------------------------------------------------+
| Display                                                                  |
+--------------------------------------------------------------------------+
| +----------------------------------------------------------------------- |
| --+--------------------------------------------------------------------- |
| ------+--------------------------------+                                 |
| | this is column 1 `​new ticket <http://trac.edgewall.org/newticket>`__  |
|   | this is column 2 `​the road ahead <http://trac.edgewall.org/roadmap> |
| `__   | that's column 3 and last one   |                                 |
| +----------------------------------------------------------------------- |
| --+--------------------------------------------------------------------- |
| ------+--------------------------------+                                 |
+--------------------------------------------------------------------------+

Complex Tables
~~~~~~~~~~~~~~

If the possibilities offered by the simple "pipe"-based markup for
tables described above are not enough for your needs, you can create
more elaborated tables by using `WikiProcessor based
tables <https://fedorahosted.org/sssd#Processors-example-tables>`__.

Links
-----

Hyperlinks are automatically created for
`WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__
and URLs. WikiPageLinks can be disabled by prepending an exclamation
mark "!" character, such as ``!WikiPageLink``.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | `TitleIndex <https://docs.pagure.org |
|                                      | /sssd-test2/TitleIndex.html>`__,     |
|     TitleIndex, http://www.edgewall. | `​http://www.edgewall.com/ <http://w |
| com/, !NotAlink                      | ww.edgewall.com/>`__,                |
|                                      | NotAlink                             |
+--------------------------------------+--------------------------------------+

Links can be given a more descriptive title by writing the link followed
by a space and a title and all this inside square brackets. If the
descriptive title is omitted, then the explicit prefix is discarded,
unless the link is an external link. This can be useful for wiki pages
not adhering to the
`WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__
convention.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | -  `​Edgewall                        |
|                                      |    Software <http://www.edgewall.com |
|      * [http://www.edgewall.com Edge | >`__                                 |
| wall Software]                       | -  `Title                            |
|      * [wiki:TitleIndex Title Index] |    Index <https://docs.pagure.org/ss |
|                                      | sd-test2/TitleIndex.html>`__         |
|      * [wiki:TitleIndex]             | -  `TitleIndex <https://docs.pagure. |
|      * [wiki:ISO9000]                | org/sssd-test2/TitleIndex.html>`__   |
|                                      | -  `ISO9000? <https://docs.pagure.or |
|                                      | g/sssd-test2/ISO9000.html>`__        |
+--------------------------------------+--------------------------------------+

Following the
`​WikiCreole <http://trac.edgewall.org/intertrac/WikiCreole>`__ trend,
the descriptive title can also be specified by writing the link followed
by a pipe ('\|') and a title and all this inside *double* square
brackets.

+--------------------------------------+--------------------------------------+
| .. code:: wiki                       | -  `​Edgewall                        |
|                                      |    Software <http://www.edgewall.com |
|      * [[http://www.edgewall.com|Edg | >`__                                 |
| ewall Software]]                     | -  `Title                            |
|      * [[wiki:TitleIndex|Title Index |    Index <https://docs.pagure.org/ss |
| ]]                                   | sd-test2/TitleIndex.html>`__         |
|        or even [[TitleIndex|Title In |    or even `Title                    |
| dex]]                                |    Index <https://docs.pagure.org/ss |
|      * [[wiki:TitleIndex]]           | sd-test2/TitleIndex.html>`__         |
|        ''' but not ![[TitleIndex]]!  | -  `TitleIndex <https://docs.pagure. |
| '''                                  | org/sssd-test2/TitleIndex.html>`__   |
|      * [[ISO9000]]                   |    **but not [[TitleIndex]]!**       |
|                                      | -  `ISO9000? <https://docs.pagure.or |
|                                      | g/sssd-test2/ISO9000.html>`__        |
+--------------------------------------+--------------------------------------+

**Note**: the
`​WikiCreole <http://trac.edgewall.org/intertrac/WikiCreole>`__ style
for links is quick to type and certainly looks familiar as it's the one
used on Wikipedia and in many other wikis. Unfortunately it conflicts
with the syntax for `macros <https://fedorahosted.org/sssd#Macros>`__.
So in the rare case when you need to refer to a page which is named
after a macro (typical examples being
`TitleIndex <https://docs.pagure.org/sssd-test2/TitleIndex.html>`__,
`InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__ and
`InterWiki <https://docs.pagure.org/sssd-test2/InterWiki.html>`__), by
writing ``[[TitleIndex]]`` you will actually call the macro instead of
linking to the page.

Trac Links
----------

Wiki pages can link directly to other parts of the Trac system. Pages
can refer to tickets, reports, changesets, milestones, source files and
other Wiki pages using the following notations:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | -  Tickets:                          |
|                                      |    `#1 <https://fedorahosted.org/sss |
|      * Tickets: #1 or ticket:1       | d/ticket/1>`__                       |
|      * Reports: {1} or report:1      |    or                                |
|      * Changesets: r1, [1] or change |    `ticket:1 <https://fedorahosted.o |
| set:1                                | rg/sssd/ticket/1>`__                 |
|      * ...                           | -  Reports:                          |
|      * targeting other Trac instance |    `{1} <https://fedorahosted.org/ss |
| s,                                   | sd/report/1>`__                      |
|        so called InterTrac links:    |    or                                |
|        - Tickets: #Trac1 or Trac:tic |    `report:1 <https://fedorahosted.o |
| ket:1                                | rg/sssd/report/1>`__                 |
|        - Changesets: [Trac1] or Trac | -  Changesets: r1, [1] or            |
| :changeset:1                         |    changeset:1                       |
|                                      | -  ...                               |
|                                      | -  targeting other Trac instances,   |
|                                      |    so called                         |
|                                      |    `InterTrac <https://docs.pagure.o |
|                                      | rg/sssd-test2/InterTrac.html>`__     |
|                                      |    links:                            |
|                                      |                                      |
|                                      |    -  Tickets: #Trac1 or             |
|                                      |       Trac:ticket:1                  |
|                                      |    -  Changesets: [Trac1] or         |
|                                      |       Trac:changeset:1               |
+--------------------------------------+--------------------------------------+

There are many more flavors of Trac links, see
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__ for
more in-depth information and a reference for all the default link
resolvers.

Setting Anchors
---------------

An anchor, or more correctly speaking, an `​anchor
name <http://www.w3.org/TR/REC-html40/struct/links.html#h-12.2.1>`__ can
be added explicitly at any place in the Wiki page, in order to uniquely
identify a position in the document:

.. code:: wiki

    [=#point1]

This syntax was chosen to match the format for explicitly naming the
header id `documented above <https://fedorahosted.org/sssd#Headings>`__.
For example:

.. code:: wiki

    == Long title == #title

It's also very close to the syntax for the corresponding link to that
anchor:

.. code:: wiki

    [#point1]

Optionally, a label can be given to the anchor:

.. code:: wiki

    [[=#point1 '''Point 1''']]

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       |     `jump to the second              |
|                                      |     point <https://fedorahosted.org/ |
|     [#point2 jump to the second poin | sssd#point2>`__                      |
| t]                                   |                                      |
|                                      |     ...                              |
|     ...                              |                                      |
|                                      |     Point2: Jump here                |
|     Point2:  [=#point2] Jump here    |                                      |
+--------------------------------------+--------------------------------------+

For more complex anchors (e.g. when a custom title is wanted), one can
use the Span macro, e.g.
``[[span(id=point2, class=wikianchor, title=Point 2, ^(2)^)]]``.

Escaping Links, `WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__ and other Markup
----------------------------------------------------------------------------------------------------------

You may avoid making hyperlinks out of
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__ by
preceding an expression with a single "!" (exclamation mark).

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       |     NoHyperLink #42 is not a link    |
|                                      |                                      |
|      !NoHyperLink                    | Various forms of escaping for list   |
|      !#42 is not a link              | markup:                              |
|                                      |                                      |
| .. code:: wiki                       |     | ``-`` escaped minus sign       |
|                                      |     | ````\ 1. escaped number        |
|     Various forms of escaping for li |     | ``*`` escaped asterisk sign    |
| st markup:                           |                                      |
|      `-` escaped minus sign \\       |                                      |
|      ``1. escaped number  \\         |                                      |
|      {{{*}}} escaped asterisk sign   |                                      |
+--------------------------------------+--------------------------------------+

Images
------

Urls ending with ``.png``, ``.gif`` or ``.jpg`` are no longer
automatically interpreted as image links, and converted to ``<img>``
tags.

You now have to use the [[Image]] macro. The simplest way to include an
image is to upload it as attachment to the current page, and put the
filename in a macro call like ``[[Image(picture.gif)]]``.

In addition to the current page, it is possible to refer to other
resources:

-  ``[[Image(wiki:WikiFormatting:picture.gif)]]`` (referring to
   attachment on another page)
-  ``[[Image(ticket:1:picture.gif)]]`` (file attached to a ticket)
-  ``[[Image(htdocs:picture.gif)]]`` (referring to a file inside the
   `environment <https://docs.pagure.org/sssd-test2/TracEnvironment.html>`__
   ``htdocs`` directory)
-  ``[[Image(source:/trunk/trac/htdocs/trac_logo_mini.png)]]`` (a file
   in repository)

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | |trac\_logo\_mini.png|               |
|                                      |                                      |
|     [[Image(htdocs:../common/trac_lo |                                      |
| go_mini.png)]]                       |                                      |
+--------------------------------------+--------------------------------------+

See `WikiMacros <https://docs.pagure.org/sssd-test2/WikiMacros.html>`__
for further documentation on the ``[[Image()]]`` macro, which has
several useful options (``title=``, ``link=``, etc.)

Macros
------

Macros are *custom functions* to insert dynamic content in a page.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     [[RecentChanges(Trac,3)]]        |    <div>                             |
|                                      |                                      |
|                                      | .. rubric:: 06/08/15                 |
|                                      |    :name: section                    |
|                                      |                                      |
|                                      | -  `TracUpgrade <https://docs.pagure |
|                                      | .org/sssd-test2/TracUpgrade.html>`__ |
|                                      |    (`diff <https://docs.pagure.org/s |
|                                      | ssd-test2/TracUpgrade?action=diff&ve |
|                                      | rsion=3.html>`__)                    |
|                                      | -  `TracRoadmap <https://docs.pagure |
|                                      | .org/sssd-test2/TracRoadmap.html>`__ |
|                                      |    (`diff <https://docs.pagure.org/s |
|                                      | ssd-test2/TracRoadmap?action=diff&ve |
|                                      | rsion=3.html>`__)                    |
|                                      | -  `TracTickets <https://docs.pagure |
|                                      | .org/sssd-test2/TracTickets.html>`__ |
|                                      |    (`diff <https://docs.pagure.org/s |
|                                      | ssd-test2/TracTickets?action=diff&ve |
|                                      | rsion=3.html>`__)                    |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
|                                      |                                      |
+--------------------------------------+--------------------------------------+

See `WikiMacros <https://docs.pagure.org/sssd-test2/WikiMacros.html>`__
for more information, and a list of installed macros.

The detailed help for a specific macro can also be obtained more
directly by appending a "?" to the macro name.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     [[MacroList?]]                   |    <div class="trac-macrolist">      |
|                                      |                                      |
|                                      | .. rubric:: ``[[MacroList]]``        |
|                                      |    :name: MacroList-macro            |
|                                      |                                      |
|                                      | Display a list of all installed Wiki |
|                                      | macros, including documentation if   |
|                                      | available.                           |
|                                      |                                      |
|                                      | Optionally, the name of a specific   |
|                                      | macro can be provided as an          |
|                                      | argument. In that case, only the     |
|                                      | documentation for that macro will be |
|                                      | rendered.                            |
|                                      |                                      |
|                                      | Note that this macro will not be     |
|                                      | able to display the documentation of |
|                                      | macros if the ``PythonOptimize``     |
|                                      | option is enabled for mod\_python!   |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
|                                      |                                      |
+--------------------------------------+--------------------------------------+

Processors
----------

Trac supports alternative markup formats using
`WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__.
For example, processors are used to write pages in
`reStructuredText <https://docs.pagure.org/sssd-test2/WikiRestructuredText.html>`__
or `HTML <https://docs.pagure.org/sssd-test2/WikiHtml.html>`__.

Wiki Markup

Display

    Example 1: HTML

.. code:: wiki

    {{{
    #!html
    <h1 style="text-align: right; color: blue">
     HTML Test
    </h1>
    }}}

HTML Test
=========

    Example 2: Code Highlighting

.. code:: wiki

    {{{
    #!python
    class Test:

        def __init__(self):
            print "Hello World"
    if __name__ == '__main__':
       Test()
    }}}

.. raw:: html

   <div class="code">

::

    class Test:
        def __init__(self):
            print "Hello World"
    if __name__ == '__main__':
       Test()

.. raw:: html

   </div>

    Example 3: Complex Tables

.. code:: wiki

    {{{#!th rowspan=4 align=justify
    With the `#td` and `#th` processors,
    table cells can contain any content:
    }}}
    |----------------
    {{{#!td
      - lists
      - embedded tables
      - simple multiline content
    }}}
    |----------------
    {{{#!td
    As processors can be easily nested, 
    so can be tables:
      {{{#!th
      Example:
      }}}
      {{{#!td style="background: #eef"
      || must be at the third level now... ||
      }}}
    }}}
    |----------------
    {{{#!td
    Even when you don't have complex markup,
    this form of table cells can be convenient
    to write content on multiple lines.
    }}}

With the ``#td`` and ``#th`` processors, table cells can contain any
content:

-  lists
-  embedded tables
-  simple multiline content

As processors can be easily nested, so can be tables:

+--------------------------------------+--------------------------------------+
| Example:                             | +----------------------------------- |
|                                      | --+                                  |
|                                      | | must be at the third level now...  |
|                                      |   |                                  |
|                                      | +----------------------------------- |
|                                      | --+                                  |
+--------------------------------------+--------------------------------------+

Even when you don't have complex markup, this form of table cells can be
convenient to write content on multiple lines.

See
`WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__
for more information.

Comments
--------

Comments can be added to the plain text. These will not be rendered and
will not display in any other format than plain text.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       |     Nothing to                       |
|                                      |                                      |
|     Nothing to                       |     see ;-)                          |
|     {{{                              |                                      |
|     #!comment                        |                                      |
|     Your comment for editors here    |                                      |
|     }}}                              |                                      |
|     see ;-)                          |                                      |
+--------------------------------------+--------------------------------------+

Miscellaneous
-------------

An horizontal line can be used to separated different parts of your
page:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | Four or more dashes will be replaced |
|                                      | by an horizontal line (<HR>)         |
|     Four or more dashes will be repl |                                      |
| aced                                 | --------------                       |
|     by an horizontal line (<HR>)     |                                      |
|     ----                             | See?                                 |
|     See?                             |                                      |
+--------------------------------------+--------------------------------------+
| .. code:: wiki                       | | "macro" style                      |
|                                      | | line break                         |
|     "macro" style [[br]] line break  |                                      |
+--------------------------------------+--------------------------------------+
| .. code:: wiki                       | | WikiCreole style                   |
|                                      | | line                               |
|     !WikiCreole style \\ line\\break | | break                              |
+--------------------------------------+--------------------------------------+

.. |trac\_logo\_mini.png| image:: https://fedorahosted.org/sssd/chrome/site/../common/trac_logo_mini.png
   :target: https://fedorahosted.org/sssd/chrome/site/../common/trac_logo_mini.png
