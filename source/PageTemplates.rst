Wiki Page Templates
===================

    *(since `​0.11 <http://trac.edgewall.org/milestone/0.11>`__)*

The default content for a new wiki page can be chosen from a list of
page templates.

That list is made up from all the existing wiki pages having a name
starting with
*`PageTemplates/ <https://docs.pagure.org/sssd-test2/PageTemplates.html>`__*.
The initial content of a new page will simply be the content of the
chosen template page, or a blank page if the special *(blank page)*
entry is selected. When there's actually no wiki pages matching that
prefix, the initial content will always be the blank page and the list
selector will not be shown (i.e. this matches the behavior we had up to
now).

To create a new template, simply create a new page having a name
starting with
*`PageTemplates/ <https://docs.pagure.org/sssd-test2/PageTemplates.html>`__*.

(Hint: one could even create a *PageTemplates/Template* for facilitating
the creation of new templates!)

After you have created your new template, a drop-down selection box will
automatically appear on any new wiki pages that are created. By default
it is located on the right side of the 'Create this page' button.

Available templates:

.. raw:: html

   <div class="titleindex">

-  `PageTemplates/FeatureDesign <https://docs.pagure.org/sssd-test2/PageTemplates/FeatureDesign.html>`__
-  `PageTemplates/ReleaseNotes <https://docs.pagure.org/sssd-test2/PageTemplates/ReleaseNotes.html>`__

.. raw:: html

   </div>

--------------

See also:
`TracWiki <https://docs.pagure.org/sssd-test2/TracWiki.html>`__
