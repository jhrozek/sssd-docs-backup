[InterMapTxt](https://docs.pagure.org/sssd-test2/InterMapTxt.html){.wiki} {#InterMapTxt}
=========================================================================

This is the place for defining [InterWiki](https://docs.pagure.org/sssd-test2/InterWiki.html){.wiki} prefixes {#ThisistheplacefordefiningInterWikiprefixes}
-------------------------------------------------------------------------------------------------------------

This page was modelled after the
[[​]{.icon}MeatBall:InterMapTxt](http://www.usemod.com/cgi-bin/mb.pl?InterMapTxt "InterMapTxt in MeatBall"){.ext-link}
page. In addition, an optional comment is allowed after the mapping.

This page is interpreted in a special way by Trac, in order to support
InterWiki links in a flexible and dynamic way.

The code block after the first line separator in this page will be
interpreted as a list of InterWiki specifications:

``` {.wiki}
prefix <space> URL [<space> # comment]
```

By using `$1`, `$2`, etc. within the URL, it is possible to create
[InterWiki](https://docs.pagure.org/sssd-test2/InterWiki.html){.wiki}
links which support multiple arguments, e.g. Trac:ticket:40. The URL
itself can be optionally followed by a comment, which will subsequently
be used for decorating the links using that prefix.

New InterWiki links can be created by adding to that list, in real time.
Note however that *deletions* are also taken into account immediately,
so it may be better to use comments for disabling prefixes.

Also note that InterWiki prefixes are case insensitive.

List of Active Prefixes {#ListofActivePrefixes}
-----------------------

  *Prefix*                                                                                              *Site*
  ----------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------
  [Acronym](http://www.acronymfinder.com/af-query.asp?String=exact&Acronym=RecentChanges)               <http://www.acronymfinder.com/af-query.asp?String=exact&Acronym=>
  [C2find](http://c2.com/cgi/wiki?FindPage&value=RecentChanges)                                         <http://c2.com/cgi/wiki?FindPage&value=>
  [c2Wiki](http://c2.com/cgi/wiki?RecentChanges)                                                        <http://c2.com/cgi/wiki?>
  [Cache](http://www.google.com/search?q=cache:RecentChanges)                                           <http://www.google.com/search?q=cache:>
  [CPAN](http://search.cpan.org/perldoc?RecentChanges)                                                  <http://search.cpan.org/perldoc?>
  [DebianBug](http://bugs.debian.org/RecentChanges)                                                     <http://bugs.debian.org/>
  [DebianPackage](http://packages.debian.org/RecentChanges)                                             <http://packages.debian.org/>
  [Dictionary](http://www.dict.org/bin/Dict?Database=*&Form=Dict1&Strategy=*&Query=RecentChanges)       <http://www.dict.org/bin/Dict?Database=*&Form=Dict1&Strategy=*&Query=>
  [Google](http://www.google.com/search?q=RecentChanges)                                                <http://www.google.com/search?q=>
  [GoogleGroups](http://groups.google.com/group/RecentChanges/msg/)                                     [Message \$2 in \$1 Google Group](http://groups.google.com/group/$1/msg/$2)
  [JargonFile](http://downlode.org/perl/jargon-redirect.cgi?term=RecentChanges)                         <http://downlode.org/perl/jargon-redirect.cgi?term=>
  [MeatBall](http://www.usemod.com/cgi-bin/mb.pl?RecentChanges)                                         <http://www.usemod.com/cgi-bin/mb.pl?>
  [Mercurial](http://www.selenic.com/mercurial/wiki/index.cgi/RecentChanges)                            [the wiki for the Mercurial distributed SCM](http://www.selenic.com/mercurial/wiki/index.cgi/)
  [MetaWiki](http://sunir.org/apps/meta.pl?RecentChanges)                                               <http://sunir.org/apps/meta.pl?>
  [MetaWikiPedia](http://meta.wikipedia.org/wiki/RecentChanges)                                         <http://meta.wikipedia.org/wiki/>
  [MoinMoin](http://moinmoin.wikiwikiweb.de/RecentChanges)                                              <http://moinmoin.wikiwikiweb.de/>
  [PEP](http://www.python.org/peps/pep-RecentChanges.html)                                              [Python Enhancement Proposal](http://www.python.org/peps/pep-$1.html)
  [RFC](http://rfc.net/rfcRecentChanges.html)                                                           [IETF's RFC \$1](http://rfc.net/rfc$1.html)
  [trac-dev](http://thread.gmane.org/gmane.comp.version-control.subversion.trac.devel/RecentChanges)    [Message \$1 in Trac Development Mailing List](http://thread.gmane.org/gmane.comp.version-control.subversion.trac.devel/)
  [Trac-ML](http://thread.gmane.org/gmane.comp.version-control.subversion.trac.general/RecentChanges)   [Message \$1 in Trac Mailing List](http://thread.gmane.org/gmane.comp.version-control.subversion.trac.general/)
  [WhoIs](http://www.whois.sc/RecentChanges)                                                            <http://www.whois.sc/>
  [Why](http://clublet.com/c/c/why?RecentChanges)                                                       <http://clublet.com/c/c/why?>
  [WikiPedia](http://en.wikipedia.org/wiki/RecentChanges)                                               <http://en.wikipedia.org/wiki/>

------------------------------------------------------------------------

Prefix Definitions {#PrefixDefinitions}
------------------

``` {.wiki}
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
```
