`InterMapTxt <https://docs.pagure.org/sssd-test2/InterMapTxt.html>`__
=====================================================================

This is the place for defining `InterWiki <https://docs.pagure.org/sssd-test2/InterWiki.html>`__ prefixes
---------------------------------------------------------------------------------------------------------

This page was modelled after the
`​MeatBall:InterMapTxt <http://www.usemod.com/cgi-bin/mb.pl?InterMapTxt>`__
page. In addition, an optional comment is allowed after the mapping.

This page is interpreted in a special way by Trac, in order to support
InterWiki links in a flexible and dynamic way.

The code block after the first line separator in this page will be
interpreted as a list of InterWiki specifications:

.. code:: wiki

    prefix <space> URL [<space> # comment]

By using ``$1``, ``$2``, etc. within the URL, it is possible to create
`InterWiki <https://docs.pagure.org/sssd-test2/InterWiki.html>`__ links
which support multiple arguments, e.g. Trac:ticket:40. The URL itself
can be optionally followed by a comment, which will subsequently be used
for decorating the links using that prefix.

New InterWiki links can be created by adding to that list, in real time.
Note however that *deletions* are also taken into account immediately,
so it may be better to use comments for disabling prefixes.

Also note that InterWiki prefixes are case insensitive.

List of Active Prefixes
-----------------------

+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| *Prefix*                                                                                                 | *Site*                                                                                                                        |
+==========================================================================================================+===============================================================================================================================+
| `Acronym <http://www.acronymfinder.com/af-query.asp?String=exact&Acronym=RecentChanges>`__               | http://www.acronymfinder.com/af-query.asp?String=exact&Acronym=                                                               |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `C2find <http://c2.com/cgi/wiki?FindPage&value=RecentChanges>`__                                         | http://c2.com/cgi/wiki?FindPage&value=                                                                                        |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `c2Wiki <http://c2.com/cgi/wiki?RecentChanges>`__                                                        | http://c2.com/cgi/wiki?                                                                                                       |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `Cache <http://www.google.com/search?q=cache:RecentChanges>`__                                           | http://www.google.com/search?q=cache:                                                                                         |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `CPAN <http://search.cpan.org/perldoc?RecentChanges>`__                                                  | http://search.cpan.org/perldoc?                                                                                               |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `DebianBug <http://bugs.debian.org/RecentChanges>`__                                                     | http://bugs.debian.org/                                                                                                       |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `DebianPackage <http://packages.debian.org/RecentChanges>`__                                             | http://packages.debian.org/                                                                                                   |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `Dictionary <http://www.dict.org/bin/Dict?Database=*&Form=Dict1&Strategy=*&Query=RecentChanges>`__       | http://www.dict.org/bin/Dict?Database=*&Form=Dict1&Strategy=*&Query=                                                          |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `Google <http://www.google.com/search?q=RecentChanges>`__                                                | http://www.google.com/search?q=                                                                                               |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `GoogleGroups <http://groups.google.com/group/RecentChanges/msg/>`__                                     | `Message $2 in $1 Google Group <http://groups.google.com/group/$1/msg/$2>`__                                                  |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `JargonFile <http://downlode.org/perl/jargon-redirect.cgi?term=RecentChanges>`__                         | http://downlode.org/perl/jargon-redirect.cgi?term=                                                                            |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `MeatBall <http://www.usemod.com/cgi-bin/mb.pl?RecentChanges>`__                                         | http://www.usemod.com/cgi-bin/mb.pl?                                                                                          |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `Mercurial <http://www.selenic.com/mercurial/wiki/index.cgi/RecentChanges>`__                            | `the wiki for the Mercurial distributed SCM <http://www.selenic.com/mercurial/wiki/index.cgi/>`__                             |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `MetaWiki <http://sunir.org/apps/meta.pl?RecentChanges>`__                                               | http://sunir.org/apps/meta.pl?                                                                                                |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `MetaWikiPedia <http://meta.wikipedia.org/wiki/RecentChanges>`__                                         | http://meta.wikipedia.org/wiki/                                                                                               |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `MoinMoin <http://moinmoin.wikiwikiweb.de/RecentChanges>`__                                              | http://moinmoin.wikiwikiweb.de/                                                                                               |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `PEP <http://www.python.org/peps/pep-RecentChanges.html>`__                                              | `Python Enhancement Proposal <http://www.python.org/peps/pep-$1.html>`__                                                      |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `RFC <http://rfc.net/rfcRecentChanges.html>`__                                                           | `IETF's RFC $1 <http://rfc.net/rfc$1.html>`__                                                                                 |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `trac-dev <http://thread.gmane.org/gmane.comp.version-control.subversion.trac.devel/RecentChanges>`__    | `Message $1 in Trac Development Mailing List <http://thread.gmane.org/gmane.comp.version-control.subversion.trac.devel/>`__   |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `Trac-ML <http://thread.gmane.org/gmane.comp.version-control.subversion.trac.general/RecentChanges>`__   | `Message $1 in Trac Mailing List <http://thread.gmane.org/gmane.comp.version-control.subversion.trac.general/>`__             |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `WhoIs <http://www.whois.sc/RecentChanges>`__                                                            | http://www.whois.sc/                                                                                                          |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `Why <http://clublet.com/c/c/why?RecentChanges>`__                                                       | http://clublet.com/c/c/why?                                                                                                   |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| `WikiPedia <http://en.wikipedia.org/wiki/RecentChanges>`__                                               | http://en.wikipedia.org/wiki/                                                                                                 |
+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

--------------

Prefix Definitions
------------------

.. code:: wiki

    PEP     http://www.python.org/peps/pep-$1.html                                       # Python Enhancement Proposal 
    Trac-ML  http://thread.gmane.org/gmane.comp.version-control.subversion.trac.general/ # Message $1 in Trac Mailing List
    trac-dev http://thread.gmane.org/gmane.comp.version-control.subversion.trac.devel/   # Message $1 in Trac Development Mailing List

    Mercurial http://www.selenic.com/mercurial/wiki/index.cgi/ # the wiki for the Mercurial distributed SCM
    RFC       http://rfc.net/rfc$1.html # IETF's RFC $1

    #
    # A arbitrary pick of InterWiki prefixes...
    #
    Acronym          http://www.acronymfinder.com/af-query.asp?String=exact&Acronym=
    C2find           http://c2.com/cgi/wiki?FindPage&value=
    Cache            http://www.google.com/search?q=cache:
    CPAN             http://search.cpan.org/perldoc?
    DebianBug        http://bugs.debian.org/
    DebianPackage    http://packages.debian.org/
    Dictionary       http://www.dict.org/bin/Dict?Database=*&Form=Dict1&Strategy=*&Query=
    Google           http://www.google.com/search?q=
    GoogleGroups     http://groups.google.com/group/$1/msg/$2        # Message $2 in $1 Google Group
    JargonFile       http://downlode.org/perl/jargon-redirect.cgi?term=
    MeatBall         http://www.usemod.com/cgi-bin/mb.pl?
    MetaWiki         http://sunir.org/apps/meta.pl?
    MetaWikiPedia    http://meta.wikipedia.org/wiki/
    MoinMoin         http://moinmoin.wikiwikiweb.de/
    WhoIs            http://www.whois.sc/
    Why              http://clublet.com/c/c/why?
    c2Wiki             http://c2.com/cgi/wiki?
    WikiPedia        http://en.wikipedia.org/wiki/
