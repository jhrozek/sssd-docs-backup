Syntax Coloring of Source Code {#SyntaxColoringofSourceCode}
==============================

Trac supports language-specific syntax highlighting of source code
within wiki formatted text in [wiki
processors](https://docs.pagure.org/sssd-test2/WikiProcessors.html#CodeHighlightingSupport){.wiki}
blocks and in the [repository
browser](https://docs.pagure.org/sssd-test2/TracBrowser.html){.wiki}.

To do this, Trac uses external libraries with support for a great number
of programming languages.

Currently Trac supports syntax coloring using one or more of the
following packages:

-   [[​]{.icon}Pygments](http://pygments.pocoo.org/){.ext-link}, by far
    the preferred system, as it covers a wide range of programming
    languages and other structured texts and is actively supported
-   [[​]{.icon}GNU
    Enscript](http://www.codento.com/people/mtr/genscript/){.ext-link},
    commonly available on Unix but somewhat unsupported on Windows
-   [[​]{.icon}SilverCity](http://silvercity.sourceforge.net/){.ext-link},
    legacy system, some versions can be
    [[​]{.icon}problematic](http://trac.edgewall.org/wiki/TracFaq#why-is-my-css-code-not-being-highlighted-even-though-i-have-silvercity-installed){.ext-link}

To activate syntax coloring, simply install either one (or more) of
these packages (see
[\#ExtraSoftware](https://fedorahosted.org/sssd#ExtraSoftware) section
below). If none of these packages is available, Trac will display the
data as plain text.

### About Pygments {#AboutPygments}

Starting with trac 0.11
[[​]{.icon}pygments](http://pygments.org/){.ext-link} will be the new
default highlighter. It's a highlighting library implemented in pure
python, very fast, easy to extend and [[​]{.icon}well
documented](http://pygments.org/docs/){.ext-link}.

The Pygments default style can specified in the
[mime-viewer](https://docs.pagure.org/sssd-test2/TracIni.html#mimeviewer-section){.wiki}
section of trac.ini. The default style can be overridden by setting a
Style preference on the [preferences
page](https://fedorahosted.org/sssd/prefs/pygments).

It's very likely that the list below is outdated because the list of
supported pygments lexers is growing weekly. Just have a look at the
page of [[​]{.icon}supported
lexers](http://pygments.org/docs/lexers/){.ext-link} on the pygments
webpage.

Syntax Coloring Support {#SyntaxColoringSupport}
-----------------------

### Known MIME Types {#KnownMIMETypes}

<div class="mimetypes">

  MIME Types                 [WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html)
  -------------------------- --------------------------------------------------------------------------
  `application/javascript`   `js`
  `application/msword`       `doc dot`
  `application/pdf`          `pdf`
  `application/postscript`   `ps`
  `application/rss+xml`      `rss`
  `application/rtf`          `rtf`
  `application/x-csh`        `csh`
  `application/x-sh`         `sh`
  `application/x-troff`      `nroff roff troff`
  `application/x-yaml`       `yaml yml`
  `application/xsl+xml`      `xsl`
  `application/xslt+xml`     `xslt`
  `image/svg+xml`            `svg`
  `image/x-icon`             `ico`
  `model/vrml`               `vrml wrl`
  `text/css`                 `css`
  `text/html`                `htm html`
  `text/plain`               `AUTHORS COPYING ChangeLog INSTALL README RELEASE TXT text txt`
  `text/x-ada`               `ada adb ads`
  `text/x-asm`               `asm`
  `text/x-asp`               `asp`
  `text/x-awk`               `awk`
  `text/x-c++hdr`            `H HH c++hdr hh hpp`
  `text/x-c++src`            `C C++ CC c++ c++src cc cpp`
  `text/x-chdr`              `chdr h`
  `text/x-csharp`            `C# c# cs csharp`
  `text/x-csrc`              `c csrc xs`
  `text/x-diff`              `diff patch`
  `text/x-dylan`             `dylan`
  `text/x-eiffel`            `e eiffel`
  `text/x-elisp`             `el elisp`
  `text/x-fortran`           `f fortran`
  `text/x-haskell`           `haskell hs`
  `text/x-idl`               `ice idl`
  `text/x-inf`               `inf`
  `text/x-ini`               `cfg ini`
  `text/x-java`              `java`
  `text/x-ksh`               `ksh`
  `text/x-lua`               `lua`
  `text/x-m4`                `m4`
  `text/x-mail`              `mail`
  `text/x-makefile`          `GNUMakefile Makefile make makefile mk`
  `text/x-objc`              `m mm objc`
  `text/x-ocaml`             `ml mli ocaml`
  `text/x-pascal`            `pas pascal`
  `text/x-perl`              `PL perl pl pm`
  `text/x-php`               `php php3 php4`
  `text/x-psp`               `psp`
  `text/x-pyrex`             `pyrex pyx`
  `text/x-python`            `py python`
  `text/x-rfc`               `rfc`
  `text/x-rst`               `rst`
  `text/x-ruby`              `rb ruby`
  `text/x-scheme`            `scheme scm`
  `text/x-sql`               `sql`
  `text/x-tcl`               `tcl`
  `text/x-tex`               `tex`
  `text/x-textile`           `textile txtl`
  `text/x-vba`               `bas vb vba`
  `text/x-verilog`           `v verilog`
  `text/x-vhdl`              `vhd vhdl`
  `text/x-zsh`               `zsh`
  `text/xml`                 `xml`

</div>

Note that the rich content may be directly *rendered* instead of syntax
highlighted. This usually depends on which auxiliary packages are
installed and on which components are activated in your setup. For
example a `text/x-rst` document will be rendered via `docutils` if it is
installed and the `trac.mimeview.rst.ReStructuredTextRenderer` is not
disabled, and will be syntax highlighted otherwise.

In a similar way, a document with the mimetype `text/x-trac-wiki` is
rendered using the Trac wiki formatter, unless the
`trac.mimeview.api.WikiTextRenderer` component is disabled.

HTML documents are directly rendered only if the `render_unsafe_html`
settings are enabled in the
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki} (those
settings are present in multiple sections, as there are different
security concerns depending where the document comes from). If you want
to ensure that an HTML document gets syntax highlighted and not
rendered, use the `text/xml` mimetype.

If mimetype such as 'svn:mime-type' is set to 'text/plain', there is no
coloring even if file is known type like 'java'.

### List of Languages Supported, by Highlighter {#language-supported}

This list is only indicative.

  -------------------------------------------------- --------------------------------------------- --------------------------------------------- ----------
                                                     SilverCity                                    Enscript                                      Pygments
  Ada                                                                                              ✓                                             
  Asm                                                                                              ✓                                             
  Apache Conf                                                                                                                                    ✓
  ASP                                                ✓                                             ✓                                             
  C                                                  ✓                                             ✓                                             ✓
  C\#                                                                                              ✓ ^[(1)](https://fedorahosted.org/sssd#a1)^   ✓
  C++                                                ✓                                             ✓                                             ✓
  CMake                                              ?                                             ?                                             ✓
  Java                                               ✓ ^[(2)](https://fedorahosted.org/sssd#a2)^   ✓                                             ✓
  Awk                                                                                              ✓                                             
  Boo                                                                                                                                            ✓
  CSS                                                ✓                                                                                           ✓
  Python Doctests                                                                                                                                ✓
  Diff                                                                                             ✓                                             ✓
  Eiffel                                                                                           ✓                                             
  Elisp                                                                                            ✓                                             
  Fortran                                                                                          ✓ ^[(1)](https://fedorahosted.org/sssd#a1)^   ✓
  Haskell                                                                                          ✓                                             ✓
  Genshi                                                                                                                                         ✓
  HTML                                               ✓                                             ✓                                             ✓
  IDL                                                                                              ✓                                             
  INI                                                                                                                                            ✓
  Javascript                                         ✓                                             ✓                                             ✓
  Lua                                                                                                                                            ✓
  m4                                                                                               ✓                                             
  Makefile                                                                                         ✓                                             ✓
  Mako                                                                                                                                           ✓
  Matlab ^[(3)](https://fedorahosted.org/sssd#a3)^                                                 ✓                                             ✓
  Mygthy                                                                                                                                         ✓
  Objective-C                                                                                      ✓                                             ✓
  OCaml                                                                                                                                          ✓
  Pascal                                                                                           ✓                                             ✓
  Perl                                               ✓                                             ✓                                             ✓
  PHP                                                ✓                                                                                           ✓
  PSP                                                ✓                                                                                           
  Pyrex                                                                                            ✓                                             
  Python                                             ✓                                             ✓                                             ✓
  Ruby                                               ✓                                             ✓ ^[(1)](https://fedorahosted.org/sssd#a1)^   ✓
  Scheme                                                                                           ✓                                             ✓
  Shell                                                                                            ✓                                             ✓
  Smarty                                                                                                                                         ✓
  SQL                                                ✓                                             ✓                                             ✓
  Troff                                                                                            ✓                                             ✓
  TCL                                                                                              ✓                                             
  Tex                                                                                              ✓                                             ✓
  Verilog                                            ✓ ^[(2)](https://fedorahosted.org/sssd#a2)^   ✓                                             
  VHDL                                                                                             ✓                                             
  Visual Basic                                                                                     ✓                                             ✓
  VRML                                                                                             ✓                                             
  XML                                                ✓                                                                                           ✓
  -------------------------------------------------- --------------------------------------------- --------------------------------------------- ----------

*[(1)]{#a1 .wikianchor} Not included in the Enscript distribution.
Additional highlighting rules can be obtained for
[[​]{.icon}Ruby](http://neugierig.org/software/ruby/){.ext-link},
[[​]{.icon}C\#](http://wiki.hasno.info/index.php/Csharp.st){.ext-link},
[[​]{.icon}Fortran
90x/2003](http://wiki.hasno.info/index.php/F90.st){.ext-link}*

*[(2)]{#a2 .wikianchor} since Silvercity 0.9.7 released on 2006-11-23*

*[(3)]{#a3 .wikianchor} By default `.m` files are considered Objective-C
files. In order to treat `.m` files as MATLAB files, add "text/matlab:m"
to the "mime\_map" setting in the [\[mimeviewer\] section of
trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#mimeviewer-section){.wiki}.*

Extra Software {#ExtraSoftware}
--------------

-   GNU Enscript —
    [[​]{.icon}http://directory.fsf.org/GNU/enscript.html](http://directory.fsf.org/GNU/enscript.html){.ext-link}
-   GNU Enscript for Windows —
    [[​]{.icon}http://gnuwin32.sourceforge.net/packages/enscript.htm](http://gnuwin32.sourceforge.net/packages/enscript.htm){.ext-link}
-   SilverCity —
    [[​]{.icon}http://silvercity.sf.net/](http://silvercity.sf.net/){.ext-link}
-   **Pygments —
    [[​]{.icon}http://pygments.org/](http://pygments.org/){.ext-link}**

------------------------------------------------------------------------

See also:
[WikiProcessors](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki},
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki},
[TracWiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki},
[TracBrowser](https://docs.pagure.org/sssd-test2/TracBrowser.html){.wiki}