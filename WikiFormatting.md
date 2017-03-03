[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki} {#WikiFormatting}
===============================================================================

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

Wiki markup is a core feature in Trac, tightly integrating all the other
parts of Trac into a flexible and powerful whole.

Trac has a built in small and powerful wiki rendering engine. This wiki
engine implements an ever growing subset of the commands from other
popular Wikis, especially
[[​]{.icon}MoinMoin](http://moinmo.in/){.ext-link} and
[[​]{.icon}WikiCreole](http://trac.edgewall.org/intertrac/WikiCreole "WikiCreole in Trac project trac"){.ext-link}.

This page will give you an in-depth explanation of the wiki markup
available anywhere
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}
is allowed.

The *Cheat sheet* below gives you a quick overview for the most common
syntax, each link in the *Category* column will lead you to the more
detailed explanation later in this page.

A few other wiki pages present the advanced features of the Trac wiki
markup in more depth:

-   [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
    covers all the possible ways to refer precisely to any Trac resource
    or parts thereof,
-   [WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki}
    talks about the various names a wiki page can take,
    [CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki}
    or not
-   [WikiMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki}
    lists the macros available for generating dynamic content,
-   [WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki}
    and
    [WikiHtml](https://docs.pagure.org/sssd-test2/WikiHtml.html){.wiki}
    details how parts of the wiki text can be processed in special ways

Cheat sheet {#Cheatsheet}
-----------

**Category**

**Wiki Markup**

**Display**

[Font Styles](https://fedorahosted.org/sssd#FontStyles)

`'''bold'''`, `''italic''`, `'''''Wikipedia style'''''`

**bold**, *italic*, ***Wikipedia style***

`` `monospaced (''other markup ignored'')` ``

`monospaced (''other markup ignored'')`

`**bold**`, `//italic//`, `**//!WikiCreole style//**`

**bold**, *italic*, ***WikiCreole style***

[Headings](https://fedorahosted.org/sssd#Headings)

``` {.wiki}
== Level 2 ==
=== Level 3 ^([#hn note])^
```

Level 2 {#Level2}
-------

### Level 3 ^([note](https://fedorahosted.org/sssd#hn))^ {#Level3note}

[Paragraphs](https://fedorahosted.org/sssd#Paragraphs)

``` {.wiki}
First paragraph
on multiple lines.

Second paragraph.
```

First paragraph on multiple lines.

Second paragraph.

[Lists](https://fedorahosted.org/sssd#Lists)

``` {.wiki}
* bullets list
  on multiple lines
  1. nested list
    a. different numbering 
       styles
```

-   bullets list on multiple lines
    1.  nested list
        1.  different numbering styles

[Definition Lists](https://fedorahosted.org/sssd#DefinitionLists)

``` {.wiki}
 term:: definition on
        multiple lines
```

term
:   definition on multiple lines

[Preformatted Text](https://fedorahosted.org/sssd#PreformattedText)

``` {.wiki}
{{{
multiple lines, ''no wiki''
      white space respected
}}}
```

``` {.wiki}
multiple lines, ''no wiki''
      white space respected
```

[Blockquotes](https://fedorahosted.org/sssd#Blockquotes)

``` {.wiki}
  if there's some leading
  space the text is quoted
```

> if there's some leading space the text is quoted

[Discussion
Citations](https://fedorahosted.org/sssd#DiscussionCitations)

``` {.wiki}
>> ... (I said)
> (he replied)
```

> > ... (I said)
>
> (he replied)

[Tables](https://fedorahosted.org/sssd#Tables)

``` {.wiki}
||= Table Header =|| Cell ||
||||  (details below)  ||
```

Table Header

Cell

(details below)

[Links](https://fedorahosted.org/sssd#Links)

`http://trac.edgewall.org`

[[​]{.icon}http://trac.edgewall.org](http://trac.edgewall.org){.ext-link}

`WikiFormatting (CamelCase)`

[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}
([CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki})

[TracLinks](https://fedorahosted.org/sssd#TracLinks)

`wiki:WikiFormatting`, `wiki:"WikiFormatting"`

[wiki:WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki},
[wiki:"WikiFormatting"](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}

`#1 (ticket)`, `[1] (changeset)`, `{1} (report)`

[\#1](https://fedorahosted.org/sssd/ticket/1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket} (ticket), [\[1\]]{.missing .changeset} (changeset),
[{1}](https://fedorahosted.org/sssd/report/1){.report} (report)

`ticket:1, ticket:1#comment:1`

[ticket:1](https://fedorahosted.org/sssd/ticket/1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket},
[ticket:1\#comment:1](https://fedorahosted.org/sssd/ticket/1#comment:1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket}

`Ticket [ticket:1]`, `[ticket:1 ticket one]`

Ticket
[1](https://fedorahosted.org/sssd/ticket/1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket},
[ticket one](https://fedorahosted.org/sssd/ticket/1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket}

`Ticket [[ticket:1]]`, `[[ticket:1|ticket one]]`

Ticket
[1](https://fedorahosted.org/sssd/ticket/1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket},
[ticket one](https://fedorahosted.org/sssd/ticket/1 "defect: Services restarted after dying are pinged more than once (closed: fixed)"){.closed
.ticket}

[Setting Anchors](https://fedorahosted.org/sssd#SettingAnchors)

`[=#point1 (1)] First...`

[(1)]{#point1 .wikianchor} First...

`see [#point1 (1)]`

see [(1)](https://fedorahosted.org/sssd#point1)

[Escaping Markup](https://fedorahosted.org/sssd#Escaping)

`!'' doubled quotes`

'' doubled quotes

`!wiki:WikiFormatting`, `!WikiFormatting`

wiki:WikiFormatting, WikiFormatting

`` ` ```{{{-}}}``` ` ``` triple curly brackets`

`{{{-}}}` triple curly brackets

[Images](https://fedorahosted.org/sssd#Images)

`[[Image(`*link*`)]]`

[![trac\_logo\_mini.png](https://fedorahosted.org/sssd/chrome/site/../common/trac_logo_mini.png "trac_logo_mini.png")](https://fedorahosted.org/sssd/chrome/site/../common/trac_logo_mini.png)

[Macros](https://fedorahosted.org/sssd#Macros)

`[[MacroList(*)]]`

*(short list of all available macros)*

`[[Image?]]`

*(help for the Image macro)*

[Processors](https://fedorahosted.org/sssd#Processors)

``` {.wiki}
{{{
#!div style="font-size: 80%"
Code highlighting:
  {{{#!python
  hello = lambda: "world"
  }}}
}}}
```

<div class="wikipage" style="font-size: 80%">

Code highlighting:

<div class="code">

    hello = lambda: "world"

</div>

</div>

[Comments](https://fedorahosted.org/sssd#Comments)

``` {.wiki}
{{{#!comment
Note to Editors: ...
}}}
```

[Miscellaneous](https://fedorahosted.org/sssd#Miscellaneous)

``` {.wiki}
Line [[br]] break 
Line \\ break
----
```

Line\
break Line\
break

------------------------------------------------------------------------

Font Styles {#FontStyles}
-----------

The Trac wiki supports the following font styles:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | -   **bold**, **triple quotes ''' |
|  * '''bold''',                    |     can be bold too if prefixed   |
|    ''' triple quotes !'''         |     by !** ,                      |
|    can be bold too if prefixed by | -   *italic*                      |
|  ! ''',                           | -   ***bold italic*** or *italic  |
|  * ''italic''                     |     and **italic bold***          |
|  * '''''bold italic''''' or ''ita | -   [underline]{.underline}       |
| lic and                           | -   `monospace` or `monospace`    |
|    ''' italic bold ''' ''         |     (hence `{{{` or `` ` ``       |
|  * __underline__                  |     quoting)                      |
|  * {{{monospace}}} or `monospace` | -   ~~strike-through~~            |
|    (hence `{{{` or {{{`}}} quotin | -   ^superscript^                 |
| g)                                | -   ~subscript~                   |
|  * ~~strike-through~~             | -   **also bold**, *italic as     |
|  * ^superscript^                  |     well*, and ***bold italic***  |
|  * ,,subscript,,                  |     ** *(since 0.12)*             |
|  * **also bold**, //italic as wel |                                   |
| l//,                              |                                   |
|    and **'' bold italic **'' //(s |                                   |
| ince 0.12)//                      |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Notes:

-   `{{{...}}}` and `` `...` `` commands not only select a monospace
    font, but also treat their content as verbatim text, meaning that no
    further wiki processing is done on this text.
-   ` ! ` tells wiki parser to not take the following characters as wiki
    format, so pay attention to put a space after !, e.g. when ending
    bold.
-   all the font styles marks have to be used in opening/closing pairs,
    and they must nest properly (in particular, an `''` italic can't be
    paired with a `//` one, and `'''` can't be paired with `**`)

Headings {#Headings}
--------

You can create heading by starting a line with one up to six *equal*
characters ("=") followed by a single space and the headline text.

[]{#hn .wikianchor} The headline text can be followed by the same number
of "=" characters, but this is no longer mandatory.

Finally, the heading might optionally be followed by an explicit id. If
not, an implicit but nevertheless readable id will be generated.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="wikipage">            |
| = Heading =                       |                                   |
| == Subheading                     | Heading {#Heading}                |
| === About ''this'' ===            | =======                           |
| === Explicit id === #using-explic |                                   |
| it-id-in-heading                  | Subheading {#Subheading}          |
| == Subheading #sub2               | ----------                        |
| ```                               |                                   |
|                                   | ### About *this* {#Aboutthis}     |
|                                   |                                   |
|                                   | ### Explicit id {#using-explicit- |
|                                   | id-in-heading}                    |
|                                   |                                   |
|                                   | Subheading {#sub2}                |
|                                   | ----------                        |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

Paragraphs {#Paragraphs}
----------

A new text paragraph is created whenever two blocks of text are
separated by one or more empty lines.

A forced line break can also be inserted, using:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | > Line 1\                         |
| Line 1[[BR]]Line 2                | > Line 2                          |
| ```                               |                                   |
|                                   | > Paragraph one                   |
| ``` {.wiki}                       |                                   |
| Paragraph                         | > Paragraph two                   |
| one                               |                                   |
|                                   |                                   |
| Paragraph                         |                                   |
| two                               |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Lists {#Lists}
-----

The wiki supports both ordered/numbered and unordered lists.

Example:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | -   Item 1                        |
|  * Item 1                         |     -   Item 1.1                  |
|    * Item 1.1                     |         -   Item 1.1.1            |
|       * Item 1.1.1                |         -   Item 1.1.2            |
|       * Item 1.1.2                |         -   Item 1.1.3            |
|       * Item 1.1.3                |     -   Item 1.2                  |
|    * Item 1.2                     | -   Item 2                        |
|  * Item 2                         |                                   |
| - items can start at the beginnin | <!-- -->                          |
| g of a line                       |                                   |
|   and they can span multiple line | -   items can start at the        |
| s                                 |     beginning of a line and they  |
|   - be careful though to continue |     can span multiple lines       |
|  the line                         |     -   be careful though to      |
|   with the appropriate indentatio |         continue the line with    |
| n, otherwise                      |         the appropriate           |
| that will start a new paragraph.. |         indentation, otherwise    |
| .                                 |                                   |
|                                   | that will start a new             |
|  1. Item 1                        | paragraph...                      |
|    a. Item 1.a                    |                                   |
|    a. Item 1.b                    | 1.  Item 1                        |
|       i. Item 1.b.i               |     1.  Item 1.a                  |
|       i. Item 1.b.ii              |     2.  Item 1.b                  |
|  1. Item 2                        |         1.  Item 1.b.i            |
| And numbered lists can also be re |         2.  Item 1.b.ii           |
| started                           | 2.  Item 2                        |
| with an explicit number:          |                                   |
|  3. Item 3                        | And numbered lists can also be    |
| ```                               | restarted with an explicit        |
|                                   | number:                           |
|                                   |                                   |
|                                   | 3.  Item 3                        |
+-----------------------------------+-----------------------------------+

Definition Lists {#DefinitionLists}
----------------

The wiki also supports definition lists.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | llama                             |
|  llama::                          | :   some kind of mammal, with     |
|    some kind of mammal, with hair |     hair                          |
|  ppython::                        |                                   |
|    some kind of reptile, without  | ppython                           |
| hair                              | :   some kind of reptile, without |
|    (can you spot the typo?)       |     hair (can you spot the typo?) |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Note that you need a space in front of the defined term.

Preformatted Text {#PreformattedText}
-----------------

Block containing preformatted text are suitable for source code
snippets, notes and examples. Use three *curly braces* wrapped around
the text to define a block quote. The curly braces need to be on a
separate line.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | ``` {.wiki}                       |
| {{{                               | def HelloWorld():                 |
| def HelloWorld():                 |     print '''Hello World'''       |
|     print '''Hello World'''       | ```                               |
| }}}                               |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Note that this kind of block is also used for selecting lines that
should be processed through
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki}.

Blockquotes {#Blockquotes}
-----------

In order to mark a paragraph as blockquote, indent that paragraph with
two spaces.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | Paragraph                         |
| Paragraph                         |                                   |
|   This text is a quote from someo | > This text is a quote from       |
| ne else.                          | > someone else.                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Discussion Citations {#DiscussionCitations}
--------------------

To delineate a citation in an ongoing discussion thread, such as the
ticket comment area, e-mail-like citation marks ("&gt;", "&gt;&gt;",
etc.) may be used.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | > > Someone's original text       |
| >> Someone's original text        | >                                 |
| > Someone else's reply text       | > Someone else's reply text       |
| >  - which can be any kind of Wik | >                                 |
| i markup                          | > -   which can be any kind of    |
| My reply text                     | >     Wiki markup                 |
| ```                               |                                   |
|                                   | My reply text                     |
+-----------------------------------+-----------------------------------+

Tables {#Tables}
------

### Simple Tables {#SimpleTables}

Simple tables can be created like this:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       |   -------- -------- --------      |
| ||Cell 1||Cell 2||Cell 3||        |   Cell 1   Cell 2   Cell 3        |
| ||Cell 4||Cell 5||Cell 6||        |   Cell 4   Cell 5   Cell 6        |
| ```                               |   -------- -------- --------      |
+-----------------------------------+-----------------------------------+

Cell headings can be specified by wrapping the content in a pair of '='
characters. Note that the '=' characters have to stick to the cell
separators, like this:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       |   ------ -------- -----------     |
| ||        ||= stable =||= latest  |          stable   latest          |
| =||                               |   0.10   0.10.5   0.10.6dev       |
| ||= 0.10 =||  0.10.5  || 0.10.6de |   0.11   0.11.6   0.11.7dev       |
| v||                               |   ------ -------- -----------     |
| ||= 0.11 =||  0.11.6  || 0.11.7de |                                   |
| v||                               |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Finally, specifying an empty cell means that the next non empty cell
will span the empty cells. For example:

Wiki Markup

Display

``` {.wiki}
|| 1 || 2 || 3 ||
|||| 1-2 || 3 ||
|| 1 |||| 2-3 ||
|||||| 1-2-3 ||
```

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

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       |   Text                Numbers     |
| ||=Text =||= Numbers =||          |   ------------------- ---------   |
| ||left align    ||        1.0||   |   left align          1.0         |
| ||  center      ||        4.5||   |   center              4.5         |
| ||      right align||     4.5||   |   right align         4.5         |
| || default alignment ||   2.5||   |   default alignment   2.5         |
| ||default||         2.5||         |   default             2.5         |
| ||  default ||      2.5||         |   default             2.5         |
| || default ||       2.5||         |   default             2.5         |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

If contrary to the example above, the cells in your table contain more
text, it might be convenient to spread a table row over multiple lines
of markup. The `\` character placed at the end of a line after a cell
separator tells Trac to not start a new row for the cells on the next
line.

+-----------------------------------------------------------------------+
| Wiki Markup                                                           |
+=======================================================================+
| ``` {.wiki}                                                           |
| || this is column 1 [http://trac.edgewall.org/newticket new ticket] | |
| | \                                                                   |
| || this is column 2 [http://trac.edgewall.org/roadmap the road ahead] |
|  || \                                                                 |
| || that's column 3 and last one ||                                    |
| ```                                                                   |
+-----------------------------------------------------------------------+
| Display                                                               |
+-----------------------------------------------------------------------+
|   ------------------------------------------------------------------- |
| --------------------- ----------------------------------------------- |
| ------------------------------------------- ------------------------- |
| -----                                                                 |
|   this is column 1 [[​]{.icon}new ticket](http://trac.edgewall.org/ne |
| wticket){.ext-link}   this is column 2 [[​]{.icon}the road ahead](htt |
| p://trac.edgewall.org/roadmap){.ext-link}   that's column 3 and last  |
| one                                                                   |
|   ------------------------------------------------------------------- |
| --------------------- ----------------------------------------------- |
| ------------------------------------------- ------------------------- |
| -----                                                                 |
+-----------------------------------------------------------------------+

### Complex Tables {#ComplexTables}

If the possibilities offered by the simple "pipe"-based markup for
tables described above are not enough for your needs, you can create
more elaborated tables by using [WikiProcessor based
tables](https://fedorahosted.org/sssd#Processors-example-tables).

Links {#Links}
-----

Hyperlinks are automatically created for
[WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki}
and URLs. WikiPageLinks can be disabled by prepending an exclamation
mark "!" character, such as `!WikiPageLink`.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | [TitleIndex](https://docs.pagure. |
| TitleIndex, http://www.edgewall.c | org/sssd-test2/TitleIndex.html){. |
| om/, !NotAlink                    | wiki},                            |
| ```                               | [[​]{.icon}http://www.edgewall.co |
|                                   | m/](http://www.edgewall.com/){.ex |
|                                   | t-link},                          |
|                                   | NotAlink                          |
+-----------------------------------+-----------------------------------+

Links can be given a more descriptive title by writing the link followed
by a space and a title and all this inside square brackets. If the
descriptive title is omitted, then the explicit prefix is discarded,
unless the link is an external link. This can be useful for wiki pages
not adhering to the
[WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki}
convention.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | -   [[​]{.icon}Edgewall           |
|  * [http://www.edgewall.com Edgew |     Software](http://www.edgewall |
| all Software]                     | .com){.ext-link}                  |
|  * [wiki:TitleIndex Title Index]  | -   [Title                        |
|  * [wiki:TitleIndex]              |     Index](https://docs.pagure.or |
|  * [wiki:ISO9000]                 | g/sssd-test2/TitleIndex.html){.wi |
| ```                               | ki}                               |
|                                   | -   [TitleIndex](https://docs.pag |
|                                   | ure.org/sssd-test2/TitleIndex.htm |
|                                   | l){.wiki}                         |
|                                   | -   [ISO9000?](https://docs.pagur |
|                                   | e.org/sssd-test2/ISO9000.html){.m |
|                                   | issing                            |
|                                   |     .wiki}                        |
+-----------------------------------+-----------------------------------+

Following the
[[​]{.icon}WikiCreole](http://trac.edgewall.org/intertrac/WikiCreole "WikiCreole in Trac project trac"){.ext-link}
trend, the descriptive title can also be specified by writing the link
followed by a pipe ('|') and a title and all this inside *double* square
brackets.

+-----------------------------------+-----------------------------------+
| ``` {.wiki}                       | -   [[​]{.icon}Edgewall           |
|  * [[http://www.edgewall.com|Edge |     Software](http://www.edgewall |
| wall Software]]                   | .com){.ext-link}                  |
|  * [[wiki:TitleIndex|Title Index] | -   [Title                        |
| ]                                 |     Index](https://docs.pagure.or |
|    or even [[TitleIndex|Title Ind | g/sssd-test2/TitleIndex.html){.wi |
| ex]]                              | ki}                               |
|  * [[wiki:TitleIndex]]            |     or even [Title                |
|    ''' but not ![[TitleIndex]]! ' |     Index](https://docs.pagure.or |
| ''                                | g/sssd-test2/TitleIndex.html){.wi |
|  * [[ISO9000]]                    | ki}                               |
| ```                               | -   [TitleIndex](https://docs.pag |
|                                   | ure.org/sssd-test2/TitleIndex.htm |
|                                   | l){.wiki}                         |
|                                   |     **but not                     |
|                                   |     \[\[TitleIndex\]\]!**         |
|                                   | -   [ISO9000?](https://docs.pagur |
|                                   | e.org/sssd-test2/ISO9000.html){.m |
|                                   | issing                            |
|                                   |     .wiki}                        |
+-----------------------------------+-----------------------------------+

**Note**: the
[[​]{.icon}WikiCreole](http://trac.edgewall.org/intertrac/WikiCreole "WikiCreole in Trac project trac"){.ext-link}
style for links is quick to type and certainly looks familiar as it's
the one used on Wikipedia and in many other wikis. Unfortunately it
conflicts with the syntax for
[macros](https://fedorahosted.org/sssd#Macros). So in the rare case when
you need to refer to a page which is named after a macro (typical
examples being
[TitleIndex](https://docs.pagure.org/sssd-test2/TitleIndex.html){.wiki},
[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
and
[InterWiki](https://docs.pagure.org/sssd-test2/InterWiki.html){.wiki}),
by writing `[[TitleIndex]]` you will actually call the macro instead of
linking to the page.

Trac Links {#TracLinks}
----------

Wiki pages can link directly to other parts of the Trac system. Pages
can refer to tickets, reports, changesets, milestones, source files and
other Wiki pages using the following notations:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | -   Tickets:                      |
|  * Tickets: #1 or ticket:1        |     [\#1](https://fedorahosted.or |
|  * Reports: {1} or report:1       | g/sssd/ticket/1 "defect: Services |
|  * Changesets: r1, [1] or changes |  restarted after dying are pinged |
| et:1                              |  more than once (closed: fixed)") |
|  * ...                            | {.closed                          |
|  * targeting other Trac instances |     .ticket} or                   |
| ,                                 |     [ticket:1](https://fedorahost |
|    so called InterTrac links:     | ed.org/sssd/ticket/1 "defect: Ser |
|    - Tickets: #Trac1 or Trac:tick | vices restarted after dying are p |
| et:1                              | inged more than once (closed: fix |
|    - Changesets: [Trac1] or Trac: | ed)"){.closed                     |
| changeset:1                       |     .ticket}                      |
| ```                               | -   Reports:                      |
|                                   |     [{1}](https://fedorahosted.or |
|                                   | g/sssd/report/1){.report}         |
|                                   |     or                            |
|                                   |     [report:1](https://fedorahost |
|                                   | ed.org/sssd/report/1){.report}    |
|                                   | -   Changesets: [r1]{.missing     |
|                                   |     .changeset}, [\[1\]]{.missing |
|                                   |     .changeset} or                |
|                                   |     [changeset:1]{.missing        |
|                                   |     .changeset}                   |
|                                   | -   ...                           |
|                                   | -   targeting other Trac          |
|                                   |     instances, so called          |
|                                   |     [InterTrac](https://docs.pagu |
|                                   | re.org/sssd-test2/InterTrac.html) |
|                                   | {.wiki}                           |
|                                   |     links:                        |
|                                   |     -   Tickets: \#Trac1 or       |
|                                   |         Trac:ticket:1             |
|                                   |     -   Changesets: \[Trac1\] or  |
|                                   |         Trac:changeset:1          |
+-----------------------------------+-----------------------------------+

There are many more flavors of Trac links, see
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
for more in-depth information and a reference for all the default link
resolvers.

Setting Anchors {#SettingAnchors}
---------------

An anchor, or more correctly speaking, an [[​]{.icon}anchor
name](http://www.w3.org/TR/REC-html40/struct/links.html#h-12.2.1){.ext-link}
can be added explicitly at any place in the Wiki page, in order to
uniquely identify a position in the document:

``` {.wiki}
[=#point1]
```

This syntax was chosen to match the format for explicitly naming the
header id [documented above](https://fedorahosted.org/sssd#Headings).
For example:

``` {.wiki}
== Long title == #title
```

It's also very close to the syntax for the corresponding link to that
anchor:

``` {.wiki}
[#point1]
```

Optionally, a label can be given to the anchor:

``` {.wiki}
[[=#point1 '''Point 1''']]
```

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | > [jump to the second             |
| [#point2 jump to the second point | > point](https://fedorahosted.org |
| ]                                 | /sssd#point2)                     |
|                                   |                                   |
| ...                               | > ...                             |
|                                   |                                   |
| Point2:  [=#point2] Jump here     | > Point2: []{#point2 .wikianchor} |
| ```                               | > Jump here                       |
+-----------------------------------+-----------------------------------+

For more complex anchors (e.g. when a custom title is wanted), one can
use the Span macro, e.g.
`[[span(id=point2, class=wikianchor, title=Point 2, ^(2)^)]]`.

Escaping Links, [WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki} and other Markup {#Escaping}
--------------------------------------------------------------------------------------------------------------

You may avoid making hyperlinks out of
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki} by
preceding an expression with a single "!" (exclamation mark).

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | > NoHyperLink \#42 is not a link  |
|  !NoHyperLink                     |                                   |
|  !#42 is not a link               | Various forms of escaping for     |
| ```                               | list markup:                      |
|                                   |                                   |
| ``` {.wiki}                       | > `-` escaped minus sign\         |
| Various forms of escaping for lis | > ``1. escaped number\            |
| t markup:                         | > `*` escaped asterisk sign       |
|  `-` escaped minus sign \\        |                                   |
|  ``1. escaped number  \\          |                                   |
|  {{{*}}} escaped asterisk sign    |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Images {#Images}
------

Urls ending with `.png`, `.gif` or `.jpg` are no longer automatically
interpreted as image links, and converted to `<img>` tags.

You now have to use the \[\[Image\]\] macro. The simplest way to include
an image is to upload it as attachment to the current page, and put the
filename in a macro call like `[[Image(picture.gif)]]`.

In addition to the current page, it is possible to refer to other
resources:

-   `[[Image(wiki:WikiFormatting:picture.gif)]]` (referring to
    attachment on another page)
-   `[[Image(ticket:1:picture.gif)]]` (file attached to a ticket)
-   `[[Image(htdocs:picture.gif)]]` (referring to a file inside the
    [environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
    `htdocs` directory)
-   `[[Image(source:/trunk/trac/htdocs/trac_logo_mini.png)]]` (a file in
    repository)

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | [![trac\_logo\_mini.png](https:// |
| [[Image(htdocs:../common/trac_log | fedorahosted.org/sssd/chrome/site |
| o_mini.png)]]                     | /../common/trac_logo_mini.png "tr |
| ```                               | ac_logo_mini.png")](https://fedor |
|                                   | ahosted.org/sssd/chrome/site/../c |
|                                   | ommon/trac_logo_mini.png)         |
+-----------------------------------+-----------------------------------+

See
[WikiMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki}
for further documentation on the `[[Image()]]` macro, which has several
useful options (`title=`, `link=`, etc.)

Macros {#Macros}
------

Macros are *custom functions* to insert dynamic content in a page.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div>                             |
| [[RecentChanges(Trac,3)]]         |                                   |
| ```                               | ### 06/08/15                      |
|                                   |                                   |
|                                   | -   [TracUpgrade](https://docs.pa |
|                                   | gure.org/sssd-test2/TracUpgrade.h |
|                                   | tml)                              |
|                                   |     ([diff](https://docs.pagure.o |
|                                   | rg/sssd-test2/TracUpgrade?action= |
|                                   | diff&version=3.html))             |
|                                   | -   [TracRoadmap](https://docs.pa |
|                                   | gure.org/sssd-test2/TracRoadmap.h |
|                                   | tml)                              |
|                                   |     ([diff](https://docs.pagure.o |
|                                   | rg/sssd-test2/TracRoadmap?action= |
|                                   | diff&version=3.html))             |
|                                   | -   [TracTickets](https://docs.pa |
|                                   | gure.org/sssd-test2/TracTickets.h |
|                                   | tml)                              |
|                                   |     ([diff](https://docs.pagure.o |
|                                   | rg/sssd-test2/TracTickets?action= |
|                                   | diff&version=3.html))             |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

See
[WikiMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki}
for more information, and a list of installed macros.

The detailed help for a specific macro can also be obtained more
directly by appending a "?" to the macro name.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="trac-macrolist">      |
| [[MacroList?]]                    |                                   |
| ```                               | ### `[[MacroList]]` {#MacroList-m |
|                                   | acro}                             |
|                                   |                                   |
|                                   | Display a list of all installed   |
|                                   | Wiki macros, including            |
|                                   | documentation if available.       |
|                                   |                                   |
|                                   | Optionally, the name of a         |
|                                   | specific macro can be provided as |
|                                   | an argument. In that case, only   |
|                                   | the documentation for that macro  |
|                                   | will be rendered.                 |
|                                   |                                   |
|                                   | Note that this macro will not be  |
|                                   | able to display the documentation |
|                                   | of macros if the `PythonOptimize` |
|                                   | option is enabled for             |
|                                   | mod\_python!                      |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

Processors {#Processors}
----------

Trac supports alternative markup formats using
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki}.
For example, processors are used to write pages in
[reStructuredText](https://docs.pagure.org/sssd-test2/WikiRestructuredText.html){.wiki}
or [HTML](https://docs.pagure.org/sssd-test2/WikiHtml.html){.wiki}.

Wiki Markup

Display

> [Example 1:]{#Processors-example-html .wikianchor} HTML

``` {.wiki}
{{{
#!html
<h1 style="text-align: right; color: blue">
 HTML Test
</h1>
}}}
```

HTML Test {#html-test style="text-align: right; color: blue"}
=========

> [Example 2:]{#Processors-example-highlight .wikianchor} Code
> Highlighting

``` {.wiki}
{{{
#!python
class Test:

    def __init__(self):
        print "Hello World"
if __name__ == '__main__':
   Test()
}}}
```

<div class="code">

    class Test:
        def __init__(self):
            print "Hello World"
    if __name__ == '__main__':
       Test()

</div>

> [Example 3:]{#Processors-example-tables .wikianchor} Complex Tables

``` {.wiki}
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
```

With the `#td` and `#th` processors, table cells can contain any
content:

-   lists
-   embedded tables
-   simple multiline content

As processors can be easily nested, so can be tables:

+-----------------------------------+-----------------------------------+
| Example:                          |   ------------------------------- |
|                                   | ----                              |
|                                   |   must be at the third level now. |
|                                   | ..                                |
|                                   |   ------------------------------- |
|                                   | ----                              |
+-----------------------------------+-----------------------------------+

Even when you don't have complex markup, this form of table cells can be
convenient to write content on multiple lines.

See
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki}
for more information.

Comments {#Comments}
--------

Comments can be added to the plain text. These will not be rendered and
will not display in any other format than plain text.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | > Nothing to                      |
| Nothing to                        | >                                 |
| {{{                               | > see ;-)                         |
| #!comment                         |                                   |
| Your comment for editors here     |                                   |
| }}}                               |                                   |
| see ;-)                           |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Miscellaneous {#Miscellaneous}
-------------

An horizontal line can be used to separated different parts of your
page:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | Four or more dashes will be       |
| Four or more dashes will be repla | replaced by an horizontal line    |
| ced                               | (&lt;HR&gt;)                      |
| by an horizontal line (<HR>)      |                                   |
| ----                              | --------------------------------- |
| See?                              | --------------------------------- |
| ```                               | ------                            |
|                                   |                                   |
|                                   | See?                              |
+-----------------------------------+-----------------------------------+
| ``` {.wiki}                       | "macro" style\                    |
| "macro" style [[br]] line break   | line break                        |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+
| ``` {.wiki}                       | WikiCreole style\                 |
| !WikiCreole style \\ line\\break  | line\                             |
| ```                               | break                             |
+-----------------------------------+-----------------------------------+


