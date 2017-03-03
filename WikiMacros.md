Trac Macros {#TracMacros}
===========

<div class="wiki-toc">

1.  [Trac Macros](#TracMacros)
    1.  [Using Macros](#UsingMacros)
        1.  [Getting Detailed Help](#GettingDetailedHelp)
        2.  [Example](#Example)
    2.  [Available Macros](#AvailableMacros)
    3.  [Macros from around the world](#Macrosfromaroundtheworld)
    4.  [Developing Custom Macros](#DevelopingCustomMacros)
        1.  [Macro without arguments](#Macrowithoutarguments)
        2.  [Macro with arguments](#Macrowitharguments)

</div>

Trac macros are plugins to extend the Trac engine with custom
'functions' written in Python. A macro inserts dynamic HTML data in any
context supporting
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}.

Another kind of macros are
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki}.
They typically deal with alternate markup formats and representation of
larger blocks of information (like source code highlighting).

Using Macros {#UsingMacros}
------------

Macro calls are enclosed in two *square brackets*. Like Python
functions, macros can also have arguments, a comma separated list within
parentheses.

### Getting Detailed Help {#GettingDetailedHelp}

The list of available macros and the full help can be obtained using the
MacroList macro, as seen
[below](https://fedorahosted.org/sssd#AvailableMacros).

A brief list can be obtained via \[\[MacroList(\*)\]\] or \[\[?\]\].

Detailed help on a specific macro can be obtained by passing it as an
argument to MacroList, e.g. \[\[MacroList(MacroList)\]\], or, more
conveniently, by appending a question mark (?) to the macro's name, like
in \[\[MacroList?\]\].

### Example {#Example}

A list of 3 most recently changed wiki pages starting with 'Trac':

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
| ``` {.wiki}                       | <div class="trac-macrolist">      |
| [[RecentChanges?(Trac,3)]]        |                                   |
| ```                               | ### `[[RecentChanges]]` {#RecentC |
|                                   | hanges-macro}                     |
|                                   |                                   |
|                                   | List all pages that have recently |
|                                   | been modified, grouping them by   |
|                                   | the day they were last modified.  |
|                                   |                                   |
|                                   | This macro accepts two            |
|                                   | parameters. The first is a prefix |
|                                   | string: if provided, only pages   |
|                                   | with names that start with the    |
|                                   | prefix are included in the        |
|                                   | resulting list. If this parameter |
|                                   | is omitted, all pages are listed. |
|                                   |                                   |
|                                   | The second parameter is a number  |
|                                   | for limiting the number of pages  |
|                                   | returned. For example, specifying |
|                                   | a limit of 5 will result in only  |
|                                   | the five most recently changed    |
|                                   | pages to be included in the list. |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+
| ``` {.wiki}                       | <div class="trac-macrolist"       |
| [[?]]                             | style="font-size: 80%">           |
| ```                               |                                   |
|                                   | ### `[[Image]]`                   |
|                                   |                                   |
|                                   | Embed an image in wiki-formatted  |
|                                   | text. The first argument is the   |
|                                   | file …                            |
|                                   | ### `[[InterTrac]]`               |
|                                   |                                   |
|                                   | Provide a list of known           |
|                                   | [InterTrac](/wiki/InterTrac){.wik |
|                                   | i}                                |
|                                   | prefixes.                         |
|                                   | ### `[[InterWiki]]`               |
|                                   |                                   |
|                                   | Provide a description list for    |
|                                   | the known                         |
|                                   | [InterWiki](/wiki/InterWiki){.wik |
|                                   | i}                                |
|                                   | prefixes.                         |
|                                   | ### `[[KnownMimeTypes]]`          |
|                                   |                                   |
|                                   | List all known mime-types which   |
|                                   | can be used as                    |
|                                   | [WikiProcessors](/wiki/WikiProces |
|                                   | sors){.wiki}.                     |
|                                   | Can be …                          |
|                                   |                                   |
|                                   | </div>                            |
|                                   |                                   |
|                                   | etc.                              |
+-----------------------------------+-----------------------------------+

Available Macros {#AvailableMacros}
----------------

*Note that the following list will only contain the macro documentation
if you've not enabled `-OO` optimizations, or not set the
`PythonOptimize` option for
[mod\_python](https://docs.pagure.org/sssd-test2/TracModPython.html){.wiki}.*

<div class="trac-macrolist">

### `[[Branches]]` {#Branches-macro}

Render a list of available branches.

### `[[Image]]` {#Image-macro}

Embed an image in wiki-formatted text.

The first argument is the file specification. The file specification may
reference attachments in three ways:

-   `module:id:file`, where module can be either **wiki** or **ticket**,
    to refer to the attachment named *file* of the specified wiki page
    or ticket.
-   `id:file`: same as above, but id is either a ticket shorthand or a
    Wiki page name.
-   `file` to refer to a local attachment named 'file'. This only works
    from within that wiki page or a ticket.

Also, the file specification may refer to repository files, using the
`source:file` syntax (`source:file@rev` works also).

Files can also be accessed with a direct URLs; `/file` for a
project-relative, `//file` for a server-relative, or
`http://server/file` for absolute location of the file.

The remaining arguments are optional and allow configuring the
attributes and style of the rendered `<img>` element:

-   digits and unit are interpreted as the size (ex. 120, 25%) for the
    image
-   `right`, `left`, `center`, `top`, `bottom` and `middle` are
    interpreted as the alignment for the image (alternatively, the first
    three can be specified using `align=...` and the last three using
    `valign=...`)
-   `link=some TracLinks...` replaces the link to the image source by
    the one specified using a
    [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}.
    If no value is specified, the link is simply removed.
-   `nolink` means without link to image source (deprecated, use
    `link=`)
-   `key=value` style are interpreted as HTML attributes or CSS style
    indications for the image. Valid keys are:
    -   align, valign, border, width, height, alt, title, longdesc,
        class, margin, margin-(left,right,top,bottom), id and usemap
    -   `border`, `margin`, and `margin-`\* can only be a single number
    -   `margin` is superseded by `center` which uses auto margins

Examples:

``` {.wiki}
    [[Image(photo.jpg)]]                           # simplest
    [[Image(photo.jpg, 120px)]]                    # with image width size
    [[Image(photo.jpg, right)]]                    # aligned by keyword
    [[Image(photo.jpg, nolink)]]                   # without link to source
    [[Image(photo.jpg, align=right)]]              # aligned by attribute
```

You can use image from other page, other ticket or other module.

``` {.wiki}
    [[Image(OtherPage:foo.bmp)]]    # if current module is wiki
    [[Image(base/sub:bar.bmp)]]     # from hierarchical wiki page
    [[Image(#3:baz.bmp)]]           # if in a ticket, point to #3
    [[Image(ticket:36:boo.jpg)]]
    [[Image(source:/images/bee.jpg)]] # straight from the repository!
    [[Image(htdocs:foo/bar.png)]]   # image file in project htdocs dir.
```

*Adapted from the Image.py macro created by Shun-ichi Goto
&lt;[[​]{.icon}gotoh@taiyo.co.jp](mailto:gotoh@taiyo.co.jp){.mail-link}&gt;*

### `[[InterTrac]]` {#InterTrac-macro}

Provide a list of known
[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
prefixes.

### `[[InterWiki]]` {#InterWiki-macro}

Provide a description list for the known
[InterWiki](https://docs.pagure.org/sssd-test2/InterWiki.html){.wiki}
prefixes.

### `[[KnownMimeTypes]]` {#KnownMimeTypes-macro}

List all known mime-types which can be used as
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki}.

Can be given an optional argument which is interpreted as mime-type
filter.

### `[[MacroList]]` {#MacroList-macro}

Display a list of all installed Wiki macros, including documentation if
available.

Optionally, the name of a specific macro can be provided as an argument.
In that case, only the documentation for that macro will be rendered.

Note that this macro will not be able to display the documentation of
macros if the `PythonOptimize` option is enabled for mod\_python!

### `[[PageOutline]]` {#PageOutline-macro}

Display a structural outline of the current wiki page, each item in the
outline being a link to the corresponding heading.

This macro accepts three optional parameters:

-   The first is a number or range that allows configuring the minimum
    and maximum level of headings that should be included in the
    outline. For example, specifying "1" here will result in only the
    top-level headings being included in the outline. Specifying "2-3"
    will make the outline include all headings of level 2 and 3, as a
    nested list. The default is to include all heading levels.
-   The second parameter can be used to specify a custom title (the
    default is no title).
-   The third parameter selects the style of the outline. This can be
    either `inline` or `pullout` (the latter being the default). The
    `inline` style renders the outline as normal part of the content,
    while `pullout` causes the outline to be rendered in a box that is
    by default floated to the right side of the other content.

### `[[RecentChanges]]` {#RecentChanges-macro}

List all pages that have recently been modified, grouping them by the
day they were last modified.

This macro accepts two parameters. The first is a prefix string: if
provided, only pages with names that start with the prefix are included
in the resulting list. If this parameter is omitted, all pages are
listed.

The second parameter is a number for limiting the number of pages
returned. For example, specifying a limit of 5 will result in only the
five most recently changed pages to be included in the list.

### `[[RepositoryIndex]]` {#RepositoryIndex-macro}

Display the list of available repositories.

Can be given the following named arguments:

*format*
:   Select the rendering format:
    -   *compact* produces a comma-separated list of repository prefix
        names (default)
    -   *list* produces a description list of repository prefix names
    -   *table* produces a table view, similar to the one visible in the
        *Browse View* page

*glob*
:   Do a glob-style filtering on the repository names (defaults to '\*')

*order*
:   Order repositories by the given column (one of "name", "date" or
    "author")

*desc*
:   When set to 1, order by descending order

(*since 0.12*)

### `[[TOC]]` {#TOC-macro}

Generate a table of contents for the current page or a set of pages. If
no arguments are given, a table of contents is generated for the current
page, with the top-level title stripped:

``` {.wiki}
    [[TOC]] 
```

To generate a table of contents for a set of pages, simply pass them as
comma separated arguments to the TOC macro, e.g. as in

``` {.wiki}
[[TOC(TracGuide, TracInstall, TracUpgrade, TracIni, TracAdmin, TracBackup,
      TracLogging, TracPermissions, TracWiki, WikiFormatting, TracBrowser,
      TracRoadmap, TracChangeset, TracTickets, TracReports, TracQuery,
      TracTimeline, TracRss, TracNotification)]]
```

A wildcard '\*' can be used to fetch a sorted list of all pages starting
with the preceding pagename stub:

``` {.wiki}
[[TOC(Trac*, WikiFormatting, WikiMacros)]]
```

The following *control* arguments change the default behaviour of the
TOC macro:

  ---------------- ----------------------------------------------------------------------------------------------------------------------------------------
  **Argument**     **Meaning**
  `heading=<x>`    Override the default heading of "Table of Contents"
  `noheading`      Suppress display of the heading.
  `depth=<n>`      Display headings of *subsequent* pages to a maximum depth of **&lt;n&gt;**.
  `inline`         Display TOC inline rather than as a side-bar.
  `sectionindex`   Only display the page name and title of each page in the wiki section.
  `titleindex`     Only display the page name and title of each page, similar to [TitleIndex](https://docs.pagure.org/sssd-test2/TitleIndex.html){.wiki}.
  `notitle`        Supress display of page title.
  ---------------- ----------------------------------------------------------------------------------------------------------------------------------------

For 'titleindex' argument, an empty pagelist will evaluate to all pages:

``` {.wiki}
[[TOC(titleindex, notitle, heading=All pages)]]
```

'sectionindex' allows to generate a title index for all pages in a given
section of the wiki. A section is defined by wiki page name, using '/'
as a section level delimiter (like directories in a file system). Giving
'/' or '\*' as the page name produces the same result as 'titleindex'
(title of all pages). If a page name ends with a '/', only children of
this page will be processed. Else the page given in the argument is also
included, if it exists. For 'sectionindex' argument, an empty pagelist
will evaluate to all page below the same parent as the current page:

``` {.wiki}
[[TOC(sectionindex, notitle, heading=This section pages)]]
```

### `[[TicketQuery]]` {#TicketQuery-macro}

Wiki macro listing tickets that match certain criteria.

This macro accepts a comma-separated list of keyed parameters, in the
form "key=value".

If the key is the name of a field, the value must use the syntax of a
filter specifier as defined in
[TracQuery\#QueryLanguage](https://docs.pagure.org/sssd-test2/TracQuery.html#QueryLanguage){.wiki}.
Note that this is *not* the same as the simplified URL syntax used for
`query:` links starting with a `?` character. Commas (`,`) can be
included in field values by escaping them with a backslash (`\`).

Groups of field constraints to be OR-ed together can be separated by a
litteral `or` argument.

In addition to filters, several other named parameters can be used to
control how the results are presented. All of them are optional.

The `format` parameter determines how the list of tickets is presented:

-   **list** -- the default presentation is to list the ticket ID next
    to the summary, with each ticket on a separate line.
-   **compact** -- the tickets are presented as a comma-separated list
    of ticket IDs.
-   **count** -- only the count of matching tickets is displayed
-   **table** -- a view similar to the custom query view (but without
    the controls)

The `max` parameter can be used to limit the number of tickets shown
(defaults to **0**, i.e. no maximum).

The `order` parameter sets the field used for ordering tickets (defaults
to **id**).

The `desc` parameter indicates whether the order of the tickets should
be reversed (defaults to **false**).

The `group` parameter sets the field used for grouping tickets (defaults
to not being set).

The `groupdesc` parameter indicates whether the natural display order of
the groups should be reversed (defaults to **false**).

The `verbose` parameter can be set to a true value in order to get the
description for the listed tickets. For **table** format only.
*deprecated in favor of the `rows` parameter*

The `rows` parameter can be used to specify which field(s) should be
viewed as a row, e.g. `rows=description|summary`

For compatibility with Trac 0.10, if there's a last positional parameter
given to the macro, it will be used to specify the `format`. Also, using
"&" as a field separator still works (except for `order`) but is
deprecated.

### `[[TitleIndex]]` {#TitleIndex-macro}

Insert an alphabetic list of all wiki pages into the output.

Accepts a prefix string as parameter: if provided, only pages with names
that start with the prefix are included in the resulting list. If this
parameter is omitted, all pages are listed. If the prefix is specified,
a second argument of value 'hideprefix' can be given as well, in order
to remove that prefix from the output.

Alternate `format` and `depth` named parameters can be specified:

-   `format=compact`: The pages are displayed as comma-separated links.
-   `format=group`: The list of pages will be structured in groups
    according to common prefix. This format also supports a `min=n`
    argument, where `n` is the minimal number of pages for a group.
-   `format=hierarchy`: The list of pages will be structured according
    to the page name path hierarchy. This format also supports a `min=n`
    argument, where higher `n` flatten the display hierarchy
-   `depth=n`: limit the depth of the pages to list. If set to 0, only
    toplevel pages will be shown, if set to 1, only immediate children
    pages will be shown, etc. If not set, or set to -1, all pages in the
    hierarchy will be shown.

### `[[TracAdminHelp]]` {#TracAdminHelp-macro}

Display help for trac-admin commands.

Examples:

``` {.wiki}
[[TracAdminHelp]]               # all commands
[[TracAdminHelp(wiki)]]         # all wiki commands
[[TracAdminHelp(wiki export)]]  # the "wiki export" command
[[TracAdminHelp(upgrade)]]      # the upgrade command
```

### `[[TracGuideToc]]` {#TracGuideToc-macro}

Display a table of content for the Trac guide.

This macro shows a quick and dirty way to make a table-of-contents for
the
[Help/Guide?](https://docs.pagure.org/sssd-test2/Help/Guide.html){.missing
.wiki}. The table of contents will contain the Trac\* and
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}
pages, and can't be customized. Search for
[TocMacro?](https://docs.pagure.org/sssd-test2/TocMacro.html){.missing
.wiki} for a a more customizable table of contents.

### `[[TracIni]]` {#TracIni-macro}

Produce documentation for the Trac configuration file.

Typically, this will be used in the
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki} page.
Optional arguments are a configuration section filter, and a
configuration option name filter: only the configuration options whose
section and name start with the filters are output.

</div>

Macros from around the world {#Macrosfromaroundtheworld}
----------------------------

The [[​]{.icon}Trac Hacks](http://trac-hacks.org/){.ext-link} site
provides a wide collection of macros and other Trac
[plugins](https://docs.pagure.org/sssd-test2/TracPlugins.html){.wiki}
contributed by the Trac community. If you're looking for new macros, or
have written one that you'd like to share with the world, please don't
hesitate to visit that site.

Developing Custom Macros {#DevelopingCustomMacros}
------------------------

Macros, like Trac itself, are written in the [[​]{.icon}Python
programming language](http://python.org/){.ext-link} and are developed
as part of
[TracPlugins](https://docs.pagure.org/sssd-test2/TracPlugins.html){.wiki}.

For more information about developing macros, see the
[[​]{.icon}development
resources](http://trac.edgewall.org/intertrac/TracDev "TracDev in Trac project trac"){.ext-link}
on the main project site.

Here are 2 simple examples showing how to create a Macro with Trac 0.11.

Also, have a look at
[[​]{.icon}Timestamp.py](http://trac.edgewall.org/intertrac/source%3Atags/trac-0.11/sample-plugins/Timestamp.py "source:tags/trac-0.11/sample-plugins/Timestamp.py in Trac project trac"){.ext-link}
for an example that shows the difference between old style and new style
macros and at the
[[​]{.icon}macros/README](http://trac.edgewall.org/intertrac/source%3Atags/trac-0.11/wiki-macros/README "source:tags/trac-0.11/wiki-macros/README in Trac project trac"){.ext-link}
which provides a little more insight about the transition.

### Macro without arguments {#Macrowithoutarguments}

To test the following code, you should saved it in a
`timestamp_sample.py` file located in the
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}'s
`plugins/` directory.

<div class="code">

    from datetime import datetime
    # Note: since Trac 0.11, datetime objects are used internally

    from genshi.builder import tag

    from trac.util.datefmt import format_datetime, utc
    from trac.wiki.macros import WikiMacroBase

    class TimeStampMacro(WikiMacroBase):
        """Inserts the current time (in seconds) into the wiki page."""

        revision = "$Rev$"
        url = "$URL$"

        def expand_macro(self, formatter, name, text):
            t = datetime.now(utc)
            return tag.b(format_datetime(t, '%c'))

</div>

### Macro with arguments {#Macrowitharguments}

To test the following code, you should saved it in a
`helloworld_sample.py` file located in the
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}'s
`plugins/` directory.

<div class="code">

    from genshi.core import Markup

    from trac.wiki.macros import WikiMacroBase

    class HelloWorldMacro(WikiMacroBase):
        """Simple HelloWorld macro.

        Note that the name of the class is meaningful:
         - it must end with "Macro"
         - what comes before "Macro" ends up being the macro name

        The documentation of the class (i.e. what you're reading)
        will become the documentation of the macro, as shown by
        the !MacroList macro (usually used in the WikiMacros page).
        """

        revision = "$Rev$"
        url = "$URL$"

        def expand_macro(self, formatter, name, text, args):
            """Return some output that will be displayed in the Wiki content.

            `name` is the actual name of the macro (no surprise, here it'll be
            `'HelloWorld'`),
            `text` is the text enclosed in parenthesis at the call of the macro.
              Note that if there are ''no'' parenthesis (like in, e.g.
              [[HelloWorld]]), then `text` is `None`.
            `args` are the arguments passed when HelloWorld is called using a
            `#!HelloWorld` code block.
            """
            return 'Hello World, text = %s, args = %s' % \
                (Markup.escape(text), Markup.escape(repr(args)))

</div>

Note that `expand_macro` optionally takes a 4^th^ parameter *`args`*.
When the macro is called as a
[WikiProcessor](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki},
it's also possible to pass `key=value` [processor
parameters](https://docs.pagure.org/sssd-test2/WikiProcessors.html#UsingProcessors){.wiki}.
If given, those are stored in a dictionary and passed in this extra
`args` parameter. On the contrary, when called as a macro, `args` is
`None`. (*since 0.12*).

For example, when writing:

``` {.wiki}
{{{#!HelloWorld style="polite"
<Hello World!>
}}}

{{{#!HelloWorld
<Hello World!>
}}}

[[HelloWorld(<Hello World!>)]]
```

One should get:

``` {.wiki}
Hello World, text = <Hello World!> , args = {'style': u'polite'}
Hello World, text = <Hello World!> , args = {}
Hello World, text = <Hello World!> , args = None
```

Note that the return value of `expand_macro` is **not** HTML escaped.
Depending on the expected result, you should escape it by yourself
(using `return Markup.escape(result)`) or, if this is indeed HTML, wrap
it in a Markup object (`return Markup(result)`) with `Markup` coming
from Genshi, (`from genshi.core import Markup`).

You can also recursively use a wiki Formatter
(`from trac.wiki import Formatter`) to process the `text` as wiki
markup, for example by doing:

<div class="code">

    from genshi.core import Markup
    from trac.wiki.macros import WikiMacroBase
    from trac.wiki import Formatter
    import StringIO

    class HelloWorldMacro(WikiMacroBase):
            def expand_macro(self, formatter, name, text, args):
                    text = "whatever '''wiki''' markup you want, even containing other macros"
                    # Convert Wiki markup to HTML, new style
                    out = StringIO.StringIO()
                    Formatter(self.env, formatter.context).format(text, out)
                    return Markup(out.getvalue())

</div>
