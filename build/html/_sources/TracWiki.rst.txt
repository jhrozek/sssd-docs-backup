The Trac Wiki System
====================

.. raw:: html

   <div class="system-message">

**Error: Macro TracGuideToc(None) failed**
::

    'NoneType' object has no attribute 'find'

.. raw:: html

   </div>

Trac has a built-in wiki system which you can use for organizing
knowledge and information in a very flexible way by `creating
pages <https://docs.pagure.org/sssd-test2/WikiNewPage.html>`__
containing an intuitive and easy to learn textual markup. This text
markup is also used in all other parts of the system, not only in `wiki
pages <https://docs.pagure.org/sssd-test2/TitleIndex.html>`__, but also
in `ticket <https://docs.pagure.org/sssd-test2/TracTickets.html>`__
description and comments, `check-in log
messages <https://docs.pagure.org/sssd-test2/TracChangeset.html>`__,
`milestone <https://docs.pagure.org/sssd-test2/TracRoadmap.html>`__
descriptions and
`report <https://docs.pagure.org/sssd-test2/TracReports.html>`__
descriptions, even in third-party extensions. It allows for formatted
text and hyperlinks in and between all Trac modules.

Editing wiki text is easy, using any web browser and a simple
`formatting
system <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__,
rather than more complex markup languages like HTML. The reasoning
behind its design is that HTML, with its large collection of nestable
tags, is too complicated to allow fast-paced editing, and distracts from
the actual content of the pages. Note though that Trac also supports
`HTML <https://docs.pagure.org/sssd-test2/WikiHtml.html>`__,
`reStructuredText <https://docs.pagure.org/sssd-test2/WikiRestructuredText.html>`__
and `​Textile <http://www.textism.com/tools/textile/>`__ as alternative
markup formats, which can eventually be used in parts of a page (so
called wiki “blocks”).

The main goal of the wiki is to make editing text easier and *encourage*
people to contribute and annotate text content for a project. Trac also
provides a simple toolbar to make formatting text even easier, and
supports the `​universal edit
button <http://universaleditbutton.org/Universal_Edit_Button>`__ of your
browser.

The wiki itself does not enforce any structure, but rather resembles a
stack of empty sheets of paper, where you can organize information and
documentation as you see fit, and later reorganize if necessary. As
contributing to a wiki is essentially building hypertext, general advice
regarding HTML authoring apply here as well. For example, the *`​Style
Guide for online hypertext <http://www.w3.org/Provider/Style>`__*
explains how to think about the `​overall structure of a
work <http://www.w3.org/Provider/Style/Structure.html>`__ and how to
organize information `​within each
document <http://www.w3.org/Provider/Style/WithinDocument.html>`__. One
of the most important tip is “make your HTML page such that you can read
it even if you don't follow any links.”

Learn more about:

-  `WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__
   rules, including advanced topics like
   `WikiMacros <https://docs.pagure.org/sssd-test2/WikiMacros.html>`__
   and
   `WikiProcessors <https://docs.pagure.org/sssd-test2/WikiProcessors.html>`__
-  How to use
   `WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__
   and other forms of
   `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__
   which are used to refer in a precise way to any resource within Trac

If you want to practice editing, please use the
`SandBox <https://docs.pagure.org/sssd-test2/SandBox.html>`__. Note that
not all Trac wikis are editable by anyone, this depends on the local
policy; check with your Trac administrators.

Before saving your changes, you can *Preview* the page or *Review the
Changes* you've made. You can get an automatic preview of the formatting
as you type when you activate the *Edit Side-by-side* mode (you have to
Preview the page for the setting to take effect). *There is a
`configurable
delay <https://docs.pagure.org/sssd-test2/TracIni.html#trac-section>`__
between when you make your edit and when the automatic preview will
update.*

Some more information about wikis on the web:

-  A definition of `​Wiki <http://wikipedia.org/wiki/Wiki>`__, in a
   famous wiki encyclopedia
-  The `​History <http://c2.com/cgi/wiki?WikiHistory>`__ of the original
   wiki
-  A wiki page explaining `​why wiki
   works <http://www.usemod.com/cgi-bin/mb.pl?WhyWikiWorks>`__

--------------

See also:
`TracGuide <https://docs.pagure.org/sssd-test2/TracGuide.html>`__
