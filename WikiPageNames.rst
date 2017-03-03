Wiki Page Names
===============

.. raw:: html

   <div class="system-message">

**Error: Macro TracGuideToc(None) failed**
::

    'NoneType' object has no attribute 'find'

.. raw:: html

   </div>

Wiki page names commonly use the
`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__
convention. Within wiki text, any word in
`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__
automatically becomes a hyperlink to the wiki page with that name.

`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__ page
names must follow these rules:

#. The name must consist of **alphabetic characters only**. No digits,
   spaces, punctuation, or underscores are allowed.
#. A name must have at least two capital letters.
#. The first character must be capitalized.
#. Every capital letter must be followed by one or more lower-case
   letters.
#. The use of slash ( / ) is permitted in page names (possibly
   representing a hierarchy).

If you want to create a wiki page that doesn't follow
`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__ rules
you can use the following syntax:

.. code:: wiki

     * [wiki:Wiki_page], [wiki:ISO9000],
       and with a label: [wiki:ISO9000 ISO 9000 standard]
     * [wiki:"Space Matters"]
       and with a label: [wiki:"Space Matters" all about white space]
     * or simply: ["WikiPageName"]s
     * even better, the new [[WikiCreole link style]]
       and with a label: [[WikiCreole link style|WikiCreole style links]]

This will be rendered as:

-  `Wiki\_page? <https://docs.pagure.org/sssd-test2/Wiki_page.html>`__,
   `ISO9000? <https://docs.pagure.org/sssd-test2/ISO9000.html>`__, and
   with a label: `ISO 9000
   standard? <https://docs.pagure.org/sssd-test2/ISO9000.html>`__
-  `Space
   Matters? <https://docs.pagure.org/sssd-test2/Space%20Matters.html>`__
   *(that page name embeds space characters)* and with a label: `all
   about white
   space? <https://docs.pagure.org/sssd-test2/Space%20Matters.html>`__
-  or simply:
   `WikiPageName? <https://docs.pagure.org/sssd-test2/WikiPageName.html>`__\ s
   *(old MoinMoin's internal free links style)*
-  even better, the new `WikiCreole link
   style? <https://docs.pagure.org/sssd-test2/WikiCreole%20link%20style.html>`__
   and with a label: `WikiCreole style
   links? <https://docs.pagure.org/sssd-test2/WikiCreole%20link%20style.html>`__
   *(since 0.12, also now adopted by MoinMoin)*

Starting with Trac 0.11, it's also possible to link to a specific
*version* of a Wiki page, as you would do for a specific version of a
file, for example:
`WikiStart@1 <https://docs.pagure.org/sssd-test2/WikiStart?version=1.html>`__.

You can also prevent a
`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__ name
to be interpreted as a
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__, by
quoting it. See
`TracLinks#EscapingLinks <https://docs.pagure.org/sssd-test2/TracLinks.html#EscapingLinks>`__.

As visible in the example above, one can also append an anchor to a Wiki
page name, in order to link to a specific section within that page. The
anchor can easily be seen by hovering the mouse over a section heading,
then clicking on the ¶ sign that appears at its end. The anchor is
usually generated automatically, but it's also possible to specify it
explicitly: see
`WikiFormatting#using-explicit-id-in-heading <https://docs.pagure.org/sssd-test2/WikiFormatting.html#using-explicit-id-in-heading>`__.

--------------

See also:
`WikiNewPage <https://docs.pagure.org/sssd-test2/WikiNewPage.html>`__,
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__,
`TracWiki <https://docs.pagure.org/sssd-test2/TracWiki.html>`__,
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__
