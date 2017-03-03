CamelCase
=========

New words created by smashing together capitalized words.

`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__ is the
original wiki convention for creating hyperlinks, with the additional
requirement that the capitals are followed by a lower-case letter; hence
“AlabamA” and “ABc” will not be links.

Customizing the Wiki behavior
-----------------------------

Some people dislike linking by
`CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__. While
Trac remains faithful to the original Wiki style, it provides a number
of ways to accomodate users with different preferences:

-  There's an option (``ignore_missing_pages`` in the
   `[wiki] <https://docs.pagure.org/sssd-test2/TracIni.html#wiki-section>`__
   section of
   `TracIni <https://docs.pagure.org/sssd-test2/TracIni.html>`__) to
   simply ignore links to missing pages when the link is written using
   the `CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__
   style, instead of that word being replaced by a gray link followed by
   a question mark.
   That can be useful when
   `CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__
   style is used to name code artifacts like class names and there's no
   corresponding page for them.
-  There's an option (``split_page_names`` in the
   `[wiki] <https://docs.pagure.org/sssd-test2/TracIni.html#wiki-section>`__
   section of
   `TracIni <https://docs.pagure.org/sssd-test2/TracIni.html>`__) to
   automatically insert space characters between the words of a
   `CamelCase <https://docs.pagure.org/sssd-test2/CamelCase.html>`__
   link when rendering the link.
-  Creation of explicit Wiki links is also easy, see
   `WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__
   for details.
-  In addition, Wiki formatting can be disabled completely in some
   places (e.g. when rendering commit log messages). See
   ``wiki_format_messages`` in the
   `[changeset] <https://docs.pagure.org/sssd-test2/TracIni.html#changeset-section>`__
   section of
   `TracIni <https://docs.pagure.org/sssd-test2/TracIni.html>`__.

See `TracIni <https://docs.pagure.org/sssd-test2/TracIni.html>`__ for
more information on the available options.

More information on CamelCase
-----------------------------

-  `​http://c2.com/cgi/wiki?WikiCase <http://c2.com/cgi/wiki?WikiCase>`__
-  `​http://en.wikipedia.org/wiki/CamelCase <http://en.wikipedia.org/wiki/CamelCase>`__

--------------

See also:
`WikiPageNames <https://docs.pagure.org/sssd-test2/WikiPageNames.html>`__,
`WikiNewPage <https://docs.pagure.org/sssd-test2/WikiNewPage.html>`__,
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__,
`TracWiki <https://docs.pagure.org/sssd-test2/TracWiki.html>`__
