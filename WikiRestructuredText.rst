reStructuredText Support in Trac
================================

Trac supports using *reStructuredText* (RST) as an alternative to wiki
markup in any context
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__
is used.

From the reStucturedText webpage:

    "*reStructuredText is an easy-to-read, what-you-see-is-what-you-get
    plaintext markup syntax and parser system. It is useful for in-line
    program documentation (such as Python docstrings), for quickly
    creating simple web pages, and for standalone documents.
    reStructuredText is designed for extensibility for specific
    application domains.* "

If you want a file from your Subversion repository be displayed as
reStructuredText in Trac's source browser, set ``text/x-rst`` as value
for the Subversion property ``svn:mime-type``. See `​this
example <http://trac.edgewall.org/intertrac/source%3A/trunk/INSTALL>`__.

Requirements
~~~~~~~~~~~~

Note that to activate RST support in Trac, the python docutils package
must be installed. If not already available on your operating system,
you can download it at the `​RST
Website <http://docutils.sourceforge.net/rst.html>`__.

Install docutils using ``easy_install docutils``. Do not use the package
manager of your OS (e.g. ``apt-get install python-docutils``), because
Trac will not find docutils then.

More information on RST
~~~~~~~~~~~~~~~~~~~~~~~

-  reStructuredText Website --
   `​http://docutils.sourceforge.net/rst.html <http://docutils.sourceforge.net/rst.html>`__
-  RST Quick Reference --
   `​http://docutils.sourceforge.net/docs/rst/quickref.html <http://docutils.sourceforge.net/docs/rst/quickref.html>`__

--------------

Using RST in Trac
-----------------

To specify that a block of text should be parsed using RST, use the
*rst* processor.

`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__ in reStructuredText
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Trac provides a custom RST directive ``trac::`` to allow
   `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__
   from within RST text.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div class="document">            |
|     #!rst                            |                                      |
|     This is a reference to |a ticket | This is a reference to               |
| |                                    | `#42 <https://fedorahosted.org/sssd/ |
|                                      | ticket/42>`__                        |
|     .. |a ticket| trac:: #42         |                                      |
|     }}}                              | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

-  Trac allows an even easier way of creating
   `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__ in
   RST, using the custom ``:trac:`` role.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div class="document">            |
|     #!rst                            |                                      |
|     This is a reference to ticket `# | This is a reference to ticket        |
| 12`:trac:                            | `#12 <https://fedorahosted.org/sssd/ |
|                                      | ticket/12>`__                        |
|     To learn how to use Trac, see `T |                                      |
| racGuide`:trac:                      | To learn how to use Trac, see        |
|     }}}                              | `TracGuide <https://docs.pagure.org/ |
|                                      | sssd-test2/TracGuide.html>`__        |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

    For a complete example of all uses of the ``:trac:`` role, please
    see
    `WikiRestructuredTextLinks <https://docs.pagure.org/sssd-test2/WikiRestructuredTextLinks.html>`__.

Syntax highlighting in reStructuredText
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There is a directive for doing
`TracSyntaxColoring <https://docs.pagure.org/sssd-test2/TracSyntaxColoring.html>`__
in RST as well. The directive is called code-block

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div class="document">            |
|     #!rst                            |                                      |
|                                      | .. raw:: html                        |
|     .. code-block:: python           |                                      |
|                                      |    <div class="code">                |
|        class Test:                   |                                      |
|                                      | ::                                   |
|            def TestFunction(self):   |                                      |
|                pass                  |     class Test:                      |
|                                      |         def TestFunction(self):      |
|     }}}                              |             pass                     |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

Note the need to indent the code at least one character after the
``.. code-block`` directive.

Wiki Macros in reStructuredText
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For doing `Wiki
Macros <https://docs.pagure.org/sssd-test2/WikiMacros.html>`__ in RST
you use the same directive as for syntax highlighting i.e code-block.

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div class="document">            |
|     #!rst                            |                                      |
|                                      | .. raw:: html                        |
|     .. code-block:: RecentChanges    |                                      |
|                                      |    <div>                             |
|        Trac,3                        |                                      |
|                                      | .. rubric:: 06/08/15                 |
|     }}}                              |    :name: section                    |
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
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

Or a more concise Wiki Macro like syntax is also available, using the
``:code-block:`` role:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div class="document">            |
|     #!rst                            |                                      |
|                                      | .. raw:: html                        |
|     :code-block:`RecentChanges:Trac, |                                      |
| 3`                                   |    <div>                             |
|     }}}                              |                                      |
|                                      | .. rubric:: 06/08/15                 |
|                                      |    :name: section-1                  |
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
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

Bigger RST Example
~~~~~~~~~~~~~~~~~~

The example below should be mostly self-explanatory:

+--------------------------------------+--------------------------------------+
| Wiki Markup                          | Display                              |
+======================================+======================================+
| .. code:: wiki                       | .. raw:: html                        |
|                                      |                                      |
|     {{{                              |    <div id="foobar-header"           |
|     #!rst                            |    class="document">                 |
|     FooBar Header                    |                                      |
|     =============                    | reStructuredText is **nice**. It has |
|     reStructuredText is **nice**. It | its own                              |
|  has its own webpage_.               | `webpage <http://docutils.sourceforg |
|                                      | e.net/rst.html>`__.                  |
|     A table:                         |                                      |
|                                      | A table:                             |
|     =====  =====  ======             |                                      |
|        Inputs     Output             | Inputs                               |
|     ------------  ------             | Output                               |
|       A      B    A or B             | A                                    |
|     =====  =====  ======             | B                                    |
|     False  False  False              | A or B                               |
|     True   False  True               | False                                |
|     False  True   True               | False                                |
|     True   True   True               | False                                |
|     =====  =====  ======             | True                                 |
|                                      | False                                |
|     RST TracLinks                    | True                                 |
|     -------------                    | False                                |
|                                      | True                                 |
|     See also ticket `#42`:trac:.     | True                                 |
|                                      | True                                 |
|     .. _webpage: http://docutils.sou | True                                 |
| rceforge.net/rst.html                | True                                 |
|     }}}                              |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    <div id="rst-traclinks"           |
|                                      |    class="section">                  |
|                                      |                                      |
|                                      | .. rubric:: RST TracLinks            |
|                                      |    :name: rst-traclinks              |
|                                      |                                      |
|                                      | See also ticket                      |
|                                      | `#42 <https://fedorahosted.org/sssd/ |
|                                      | ticket/42>`__.                       |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
|                                      |                                      |
|                                      | .. raw:: html                        |
|                                      |                                      |
|                                      |    </div>                            |
+--------------------------------------+--------------------------------------+

--------------

See also:
`WikiRestructuredTextLinks <https://docs.pagure.org/sssd-test2/WikiRestructuredTextLinks.html>`__,
`WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__,
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__
