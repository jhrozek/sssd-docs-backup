Wiki Processors {#WikiProcessors}
===============

Processors are
[WikiMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki}
designed to provide alternative markup formats for the [Wiki
engine](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki}.
Processors can be thought of as *macro functions to process user-edited
text*.

Wiki processors can be used in any Wiki text throughout Trac, for
various different purposes, like:

-   [syntax
    highlighting](https://fedorahosted.org/sssd#CodeHighlightingSupport)
    or for rendering text verbatim,
-   rendering [Wiki markup inside a
    context](https://fedorahosted.org/sssd#HTMLrelated), like inside
    &lt;div&gt; blocks or &lt;span&gt; or within &lt;td&gt; or
    &lt;th&gt; table cells,
-   using an alternative markup syntax, like [raw
    HTML](https://docs.pagure.org/sssd-test2/WikiHtml.html){.wiki} and
    [Restructured
    Text](https://docs.pagure.org/sssd-test2/WikiRestructuredText.html){.wiki},
    or
    [[​]{.icon}textile](http://www.textism.com/tools/textile/){.ext-link}

Using Processors {#UsingProcessors}
----------------

To use a processor on a block of text, first delimit the lines using a
Wiki *code block*:

``` {.wiki}
{{{
The lines
that should be processed...
}}}
```

Immediately after the `{{{` or on the line just below, add `#!` followed
by the *processor name*.

``` {.wiki}
{{{
#!processorname
The lines
that should be processed...
}}}
```

This is the "shebang" notation, familiar to most UNIX users.

Besides their content, some Wiki processors can also accept
*parameters*, which are then given as `key=value` pairs after the
processor name, on the same line. If `value` has to contain space, as
it's often the case for the style parameter, a quoted string can be used
(`key="value with space"`).

As some processors are meant to process Wiki markup, it's quite possible
to *nest* processor blocks. You may want to indent the content of nested
blocks for increased clarity, this extra indentation will be ignored
when processing the content.

Examples {#Examples}
--------

Wiki Markup

Display

> [Example 1]{.underline}: Inserting raw HTML

``` {.wiki}
{{{
#!html
<h1 style="color: grey">This is raw HTML</h1>
}}}
```

This is raw HTML {#this-is-raw-html style="color: grey"}
================

> [Example 2]{.underline}: Highlighted Python code in a &lt;div&gt;
> block with custom style

``` {.wiki}
{{{#!div style="background: #ffd; border: 3px ridge"

This is an example of embedded "code" block:

  {{{
  #!python
  def hello():
      return "world"
  }}}

}}}
```

<div class="wikipage" style="background: #ffd; border: 3px ridge">

This is an example of embedded "code" block:

<div class="code">

    def hello():
        return "world"

</div>

</div>

> [Example 3]{.underline}: Searching tickets from a wiki page, by
> keywords.

``` {.wiki}
{{{
#!html
<form action="/query" method="get"><div>
<input type="text" name="keywords" value="~" size="30"/>
<input type="submit" value="Search by Keywords"/>
<!-- To control what fields show up use hidden fields
<input type="hidden" name="col" value="id"/>
<input type="hidden" name="col" value="summary"/>
<input type="hidden" name="col" value="status"/>
<input type="hidden" name="col" value="milestone"/>
<input type="hidden" name="col" value="version"/>
<input type="hidden" name="col" value="owner"/>
<input type="hidden" name="col" value="priority"/>
<input type="hidden" name="col" value="component"/>
-->
</div></form>
}}}
```

<div>

</div>

Available Processors {#AvailableProcessors}
--------------------

The following processors are included in the Trac distribution:

**`#!default`**

Present the text verbatim in a preformatted text block. This is the same
as specifying *no* processor name (and no `#!`)

**`#!comment`**

Do not process the text in this section (i.e. contents exist only in the
plain text - not in the rendered page).

**HTML related**

**`#!html`**

Insert custom HTML in a wiki page.

**`#!htmlcomment`**

Insert an HTML comment in a wiki page (*since 0.12*).

Note that `#!html` blocks have to be *self-contained*, i.e. you can't
start an HTML element in one block and close it later in a second block.
Use the following processors for achieving a similar effect.

**`#!div`**

Wrap an arbitrary Wiki content inside a &lt;div&gt; element (*since
0.11*).

**`#!span`**

Wrap an arbitrary Wiki content inside a &lt;span&gt; element (*since
0.11*).

**`#!td`**

Wrap an arbitrary Wiki content inside a &lt;td&gt; element (*since
0.12*)

**`#!th`**

Wrap an arbitrary Wiki content inside a &lt;th&gt; element (*since
0.12*)

**`#!tr`**

Can optionally be used for wrapping `#!td` and `#!th` blocks, either for
specifying row attributes of better visual grouping (*since 0.12*)

See [WikiHtml](https://docs.pagure.org/sssd-test2/WikiHtml.html){.wiki}
for example usage and more details about these processors.

**Other Markups**

**`#!rst`**

Trac support for Restructured Text. See
[WikiRestructuredText](https://docs.pagure.org/sssd-test2/WikiRestructuredText.html){.wiki}.

**`#!textile`**

Supported if
[[​]{.icon}Textile](http://cheeseshop.python.org/pypi/textile){.ext-link}
is installed. See [[​]{.icon}a Textile
reference](http://www.textism.com/tools/textile/){.ext-link}.

**Code Highlighting Support**

**`#!c`**\
**`#!cpp`** (C++)\
**`#!python`**\
**`#!perl`**\
**`#!ruby`**\
**`#!php`**\
**`#!asp`**\
**`#!java`**\
**`#!js`** (Javascript)\
**`#!sql`**\
**`#!xml`** (XML or HTML)\
**`#!sh`** (Bourne/Bash shell)\
**etc.**\

Trac includes processors to provide inline syntax highlighting for
source code in various languages.\
\
Trac relies on external software packages for syntax coloring, like
[[​]{.icon}Pygments](http://pygments.org){.ext-link}.\
\
See
[TracSyntaxColoring](https://docs.pagure.org/sssd-test2/TracSyntaxColoring.html){.wiki}
for information about which languages are supported and how to enable
support for more languages.

**MIME Type Processors**

Using the MIME type as processor, it is possible to syntax-highlight the
same languages that are supported when browsing source code.

Some examples:

``` {.wiki}
{{{
#!text/html
<h1>text</h1>
}}}
```

The result will be syntax highlighted HTML code:

<div class="code">

    <h1>text</h1>

</div>

The same is valid for all other [mime types
supported](https://docs.pagure.org/sssd-test2/TracSyntaxColoring.html#SyntaxColoringSupport){.wiki}.

``` {.wiki}
{{{
#!diff
--- Version 55
+++ Version 56
@@ -115,8 +115,9 @@
     name='TracHelloWorld', version='1.0',
     packages=find_packages(exclude=['*.tests*']),
-    entry_points = """
-        [trac.plugins]
-        helloworld = myplugs.helloworld
-    """,
+    entry_points = {
+        'trac.plugins': [
+            'helloworld = myplugs.helloworld',
+        ],
+    },
 )
}}}
```

**`#!diff`** has a particularly nice renderer:

<div class="diff" xmlns="http://www.w3.org/1999/xhtml">

-   [Version]{}
    -----------

    ** 

    115

    115

    [    name='TracHelloWorld', version='1.0',]{} 

    116

    116

    [    packages=find\_packages(exclude=\['\*.tests\*'\]),]{} 

    117

     

    [    entry\_points = """]{} 

    118

     

    [        \[trac.plugins\]]{} 

    119

     

    [        helloworld = myplugs.helloworld]{} 

    120

     

    [    """,]{} 

     

    117

    [    entry\_points = {]{} 

     

    118

    [        'trac.plugins': \[]{} 

     

    119

    [            'helloworld = myplugs.helloworld',]{} 

     

    120

    [        \],]{} 

     

    121

    [    },]{} 

    121

    122

    [)]{} 

</div>

For more processor macros developed and/or contributed by users, visit:

-   [[​]{.icon}ProcessorBazaar](http://trac.edgewall.org/intertrac/ProcessorBazaar "ProcessorBazaar in Trac project trac"){.ext-link}
-   [[​]{.icon}MacroBazaar](http://trac.edgewall.org/intertrac/MacroBazaar "MacroBazaar in Trac project trac"){.ext-link}
-   [[​]{.icon}Trac Hacks](http://trac-hacks.org){.ext-link} community
    site

Developing processors is no different from Wiki macros. In fact they
work the same way, only the usage syntax differs. See
[WikiMacros\#DevelopingCustomMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html#DevelopingCustomMacros){.wiki}
for more information.

------------------------------------------------------------------------

See also:
[WikiMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki},
[WikiHtml](https://docs.pagure.org/sssd-test2/WikiHtml.html){.wiki},
[WikiRestructuredText](https://docs.pagure.org/sssd-test2/WikiRestructuredText.html){.wiki},
[TracSyntaxColoring](https://docs.pagure.org/sssd-test2/TracSyntaxColoring.html){.wiki},
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki},
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki}
