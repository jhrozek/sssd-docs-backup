CamelCase {#CamelCase}
=========

New words created by smashing together capitalized words.

[CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki} is
the original wiki convention for creating hyperlinks, with the
additional requirement that the capitals are followed by a lower-case
letter; hence “AlabamA” and “ABc” will not be links.

Customizing the Wiki behavior {#CustomizingtheWikibehavior}
-----------------------------

Some people dislike linking by
[CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki}.
While Trac remains faithful to the original Wiki style, it provides a
number of ways to accomodate users with different preferences:

-   There's an option (`ignore_missing_pages` in the
    [\[wiki\]](https://docs.pagure.org/sssd-test2/TracIni.html#wiki-section){.wiki}
    section of
    [TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki})
    to simply ignore links to missing pages when the link is written
    using the
    [CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki}
    style, instead of that word being replaced by a gray link followed
    by a question mark.\
    That can be useful when
    [CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki}
    style is used to name code artifacts like class names and there's no
    corresponding page for them.
-   There's an option (`split_page_names` in the
    [\[wiki\]](https://docs.pagure.org/sssd-test2/TracIni.html#wiki-section){.wiki}
    section of
    [TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki})
    to automatically insert space characters between the words of a
    [CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki}
    link when rendering the link.
-   Creation of explicit Wiki links is also easy, see
    [WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki}
    for details.
-   In addition, Wiki formatting can be disabled completely in some
    places (e.g. when rendering commit log messages). See
    `wiki_format_messages` in the
    [\[changeset\]](https://docs.pagure.org/sssd-test2/TracIni.html#changeset-section){.wiki}
    section of
    [TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki}.

See [TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki}
for more information on the available options.

More information on CamelCase {#MoreinformationonCamelCase}
-----------------------------

-   [[​]{.icon}http://c2.com/cgi/wiki?WikiCase](http://c2.com/cgi/wiki?WikiCase){.ext-link}
-   [[​]{.icon}http://en.wikipedia.org/wiki/CamelCase](http://en.wikipedia.org/wiki/CamelCase){.ext-link}

------------------------------------------------------------------------

See also:
[WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki},
[WikiNewPage](https://docs.pagure.org/sssd-test2/WikiNewPage.html){.wiki},
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki},
[TracWiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki}
