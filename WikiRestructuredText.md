reStructuredText Support in Trac {#reStructuredTextSupportinTrac}
================================

Trac supports using *reStructuredText* (RST) as an alternative to wiki
markup in any context
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}
is used.

From the reStucturedText webpage:

> "*reStructuredText is an easy-to-read, what-you-see-is-what-you-get
> plaintext markup syntax and parser system. It is useful for in-line
> program documentation (such as Python docstrings), for quickly
> creating simple web pages, and for standalone documents.
> reStructuredText is designed for extensibility for specific
> application domains.* "

If you want a file from your Subversion repository be displayed as
reStructuredText in Trac's source browser, set `text/x-rst` as value for
the Subversion property `svn:mime-type`. See [[​]{.icon}this
example](http://trac.edgewall.org/intertrac/source%3A/trunk/INSTALL "source:/trunk/INSTALL in Trac project trac"){.ext-link}.

### Requirements {#Requirements}

Note that to activate RST support in Trac, the python docutils package
must be installed. If not already available on your operating system,
you can download it at the [[​]{.icon}RST
Website](http://docutils.sourceforge.net/rst.html){.ext-link}.

Install docutils using `easy_install docutils`. Do not use the package
manager of your OS (e.g. `apt-get install python-docutils`), because
Trac will not find docutils then.

### More information on RST {#MoreinformationonRST}

-   reStructuredText Website --
    [[​]{.icon}http://docutils.sourceforge.net/rst.html](http://docutils.sourceforge.net/rst.html){.ext-link}
-   RST Quick Reference --
    [[​]{.icon}http://docutils.sourceforge.net/docs/rst/quickref.html](http://docutils.sourceforge.net/docs/rst/quickref.html){.ext-link}

------------------------------------------------------------------------

Using RST in Trac {#UsingRSTinTrac}
-----------------

To specify that a block of text should be parsed using RST, use the
*rst* processor.

### [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki} in reStructuredText {#TracLinksinreStructuredText}

-   Trac provides a custom RST directive `trac::` to allow
    [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
    from within RST text.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="document">            |
| {{{                               |                                   |
| #!rst                             | This is a reference to            |
| This is a reference to |a ticket| | [\#42](https://fedorahosted.org/s |
|                                   | ssd/ticket/42){.reference         |
| .. |a ticket| trac:: #42          | .external}                        |
| }}}                               |                                   |
| ```                               | </div>                            |
+-----------------------------------+-----------------------------------+

-   Trac allows an even easier way of creating
    [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
    in RST, using the custom `:trac:` role.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="document">            |
| {{{                               |                                   |
| #!rst                             | This is a reference to ticket     |
| This is a reference to ticket `#1 | [\#12](https://fedorahosted.org/s |
| 2`:trac:                          | ssd/ticket/12){.reference         |
|                                   | .external}                        |
| To learn how to use Trac, see `Tr |                                   |
| acGuide`:trac:                    | To learn how to use Trac, see     |
| }}}                               | [TracGuide](https://docs.pagure.o |
| ```                               | rg/sssd-test2/TracGuide.html){.re |
|                                   | ference                           |
|                                   | .external}                        |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

> For a complete example of all uses of the `:trac:` role, please see
> [WikiRestructuredTextLinks](https://docs.pagure.org/sssd-test2/WikiRestructuredTextLinks.html){.wiki}.

### Syntax highlighting in reStructuredText {#SyntaxhighlightinginreStructuredText}

There is a directive for doing
[TracSyntaxColoring](https://docs.pagure.org/sssd-test2/TracSyntaxColoring.html){.wiki}
in RST as well. The directive is called code-block

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="document">            |
| {{{                               |                                   |
| #!rst                             | <div class="code">                |
|                                   |                                   |
| .. code-block:: python            |     class Test:                   |
|                                   |         def TestFunction(self):   |
|    class Test:                    |             pass                  |
|                                   |                                   |
|        def TestFunction(self):    | </div>                            |
|            pass                   |                                   |
|                                   | </div>                            |
| }}}                               |                                   |
| ```                               |                                   |
+-----------------------------------+-----------------------------------+

Note the need to indent the code at least one character after the
`.. code-block` directive.

### Wiki Macros in reStructuredText {#WikiMacrosinreStructuredText}

For doing [Wiki
Macros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki} in
RST you use the same directive as for syntax highlighting i.e
code-block.

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="document">            |
| {{{                               |                                   |
| #!rst                             | <div>                             |
|                                   |                                   |
| .. code-block:: RecentChanges     | ### 06/08/15                      |
|                                   |                                   |
|    Trac,3                         | -   [TracUpgrade](https://docs.pa |
|                                   | gure.org/sssd-test2/TracUpgrade.h |
| }}}                               | tml)                              |
| ```                               |     ([diff](https://docs.pagure.o |
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
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

Or a more concise Wiki Macro like syntax is also available, using the
`:code-block:` role:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div class="document">            |
| {{{                               |                                   |
| #!rst                             | <div>                             |
|                                   |                                   |
| :code-block:`RecentChanges:Trac,3 | ### 06/08/15                      |
| `                                 |                                   |
| }}}                               | -   [TracUpgrade](https://docs.pa |
| ```                               | gure.org/sssd-test2/TracUpgrade.h |
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
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

### Bigger RST Example {#BiggerRSTExample}

The example below should be mostly self-explanatory:

+-----------------------------------+-----------------------------------+
| Wiki Markup                       | Display                           |
+===================================+===================================+
| ``` {.wiki}                       | <div id="foobar-header"           |
| {{{                               | class="document">                 |
| #!rst                             |                                   |
| FooBar Header                     | reStructuredText is **nice**. It  |
| =============                     | has its own                       |
| reStructuredText is **nice**. It  | [webpage](http://docutils.sourcef |
| has its own webpage_.             | orge.net/rst.html){.reference     |
|                                   | .external}.                       |
| A table:                          |                                   |
|                                   | A table:                          |
| =====  =====  ======              |                                   |
|    Inputs     Output              | Inputs                            |
| ------------  ------              | Output                            |
|   A      B    A or B              | A                                 |
| =====  =====  ======              | B                                 |
| False  False  False               | A or B                            |
| True   False  True                | False                             |
| False  True   True                | False                             |
| True   True   True                | False                             |
| =====  =====  ======              | True                              |
|                                   | False                             |
| RST TracLinks                     | True                              |
| -------------                     | False                             |
|                                   | True                              |
| See also ticket `#42`:trac:.      | True                              |
|                                   | True                              |
| .. _webpage: http://docutils.sour | True                              |
| ceforge.net/rst.html              | True                              |
| }}}                               | <div id="rst-traclinks"           |
| ```                               | class="section">                  |
|                                   |                                   |
|                                   | RST TracLinks                     |
|                                   | =============                     |
|                                   |                                   |
|                                   | See also ticket                   |
|                                   | [\#42](https://fedorahosted.org/s |
|                                   | ssd/ticket/42){.reference         |
|                                   | .external}.                       |
|                                   |                                   |
|                                   | </div>                            |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

------------------------------------------------------------------------

See also:
[WikiRestructuredTextLinks](https://docs.pagure.org/sssd-test2/WikiRestructuredTextLinks.html){.wiki},
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki},
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki}
