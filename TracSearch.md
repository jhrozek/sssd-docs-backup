Using Search {#UsingSearch}
============

Trac has a built-in search engine to allow finding occurrences of
keywords and substrings in wiki pages, tickets and changeset properties
(author, revision and log message).

Using the Trac search facility is straightforward and its interface
should be familiar to most users.

Apart from the [Search
module](https://fedorahosted.org/sssd/search){.search}, you will also
find a small search field above the navigation bar at all time. It
provides convenient access to the search module from all pages.

The search results show the most recent modifications ranked first in
the results rather than the most relevant result.

"Quickjump" searches {#Quickjumpsearches}
--------------------

For quick access to various project resources, the quick-search field at
the top of every page can be used to enter a [wiki
link](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}, which
will take you directly to the resource identified by that link.

For example:

-   \[42\] -- Opens change set 42
-   \#42 -- Opens ticket number 42
-   {1} -- Opens report 1
-   /trunk -- Opens the browser for the `trunk` directory

Advanced {#Advanced}
--------

### Disabling Quickjumps {#DisablingQuickjumps}

To disable the quickjump feature for a search keyword - for example when
searching for occurences of the literal word TracGuide - begin the query
with an exclamation mark (`!`).

### Search Links {#SearchLinks}

From the Wiki, it is possible to link to a specific search, using
`search:` links:

-   `search:?q=crash` will search for the string "crash"
-   `search:?q=trac+link&wiki=on` will search for "trac" and "link" in
    wiki pages only

------------------------------------------------------------------------

See also:
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki},
[TracQuery](https://docs.pagure.org/sssd-test2/TracQuery.html){.wiki}