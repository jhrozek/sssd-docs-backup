Installing Trac as CGI {#InstallingTracasCGI}
======================

<div class="important">

> *Please note that using Trac via CGI is the slowest deployment method
> available. It is slower than
> [mod\_python](https://docs.pagure.org/sssd-test2/TracModPython.html){.wiki},
> [FastCGI](https://docs.pagure.org/sssd-test2/TracFastCgi.html){.wiki}
> and even
> [[​]{.icon}IIS/AJP](http://trac.edgewall.org/intertrac/TracOnWindowsIisAjp "TracOnWindowsIisAjp in Trac project trac"){.ext-link}
> on Windows.*

</div>

CGI script is the entrypoint that web-server calls when a web-request to
an application is made. To generate the `trac.cgi` script run:

``` {.wiki}
trac-admin /path/to/env deploy /path/to/www/trac
```

`trac.cgi` will be in the `cgi-bin` folder inside the given path. *Make
sure it is executable by your web server*. This command also copies
`static resource` files to a `htdocs` directory of a given destination.

Apache web-server configuration {#Apacheweb-serverconfiguration}
-------------------------------

In [[​]{.icon}Apache](http://httpd.apache.org/){.ext-link} there are two
ways to run Trac as CGI:

1.  Use a `ScriptAlias` directive that maps an URL to the `trac.cgi`
    script (recommended)
2.  Copy the `trac.cgi` file into the directory for CGI executables used
    by your web server (commonly named `cgi-bin`). You can also create a
    symbolic link, but in that case make sure that the `FollowSymLinks`
    option is enabled for the `cgi-bin` directory.

To make Trac available at `http://yourhost.example.org/trac` add
`ScriptAlias` directive to Apache configuration file, changing
`trac.cgi` path to match your installation:

``` {.wiki}
ScriptAlias /trac /path/to/www/trac/cgi-bin/trac.cgi
```

> *Note that this directive requires enabled `mod_alias` module.*

If you're using Trac with a single project you need to set its location
using the `TRAC_ENV` environment variable:

``` {.wiki}
<Location "/trac">
  SetEnv TRAC_ENV "/path/to/projectenv"
</Location>
```

Or to use multiple projects you can specify their common parent
directory using the `TRAC_ENV_PARENT_DIR` variable:

``` {.wiki}
<Location "/trac">
  SetEnv TRAC_ENV_PARENT_DIR "/path/to/project/parent/dir"
</Location>
```

> *Note that the `SetEnv` directive requires enabled `mod_env` module.
> It is also possible to set TRAC\_ENV in trac.cgi. Just add the
> following code between "try:" and "from trac.web ...":*

``` {.wiki}
    import os
    os.environ['TRAC_ENV'] = "/path/to/projectenv"
```

> *Or for TRAC\_ENV\_PARENT\_DIR:*

``` {.wiki}
    import os
    os.environ['TRAC_ENV_PARENT_DIR'] = "/path/to/project/parent/dir"
```

If you are using the [[​]{.icon}Apache
suEXEC](http://httpd.apache.org/docs/suexec.html){.ext-link} feature
please see
[[​]{.icon}http://trac.edgewall.org/wiki/ApacheSuexec](http://trac.edgewall.org/wiki/ApacheSuexec){.ext-link}.

On some systems, you *may* need to edit the shebang line in the
`trac.cgi` file to point to your real Python installation path. On a
Windows system you may need to configure Windows to know how to execute
a .cgi file (Explorer -&gt; Tools -&gt; Folder Options -&gt; File Types
-&gt; CGI).

### Using WSGI {#UsingWSGI}

You can run a [[​]{.icon}WSGI
handler](http://henry.precheur.org/python/how_to_serve_cgi){.ext-link}
[[​]{.icon}under
CGI](http://pythonweb.org/projects/webmodules/doc/0.5.3/html_multipage/lib/example-webserver-web-wsgi-simple-cgi.html){.ext-link}.
You can [write your own application
function](https://docs.pagure.org/sssd-test2/TracModWSGI.html#Thetrac.wsgiscript){.wiki},
or use the deployed trac.wsgi's application.

Mapping Static Resources {#MappingStaticResources}
------------------------

See
[TracInstall\#MappingStaticResources](https://docs.pagure.org/sssd-test2/TracInstall.html#MappingStaticResources){.wiki}.

Adding Authentication {#AddingAuthentication}
---------------------

See
[TracInstall\#ConfiguringAuthentication](https://docs.pagure.org/sssd-test2/TracInstall.html#ConfiguringAuthentication){.wiki}.

------------------------------------------------------------------------

See also:
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[TracInstall](https://docs.pagure.org/sssd-test2/TracInstall.html){.wiki},
[TracModWSGI](https://docs.pagure.org/sssd-test2/TracModWSGI.html){.wiki},
[TracFastCgi](https://docs.pagure.org/sssd-test2/TracFastCgi.html){.wiki},
[TracModPython](https://docs.pagure.org/sssd-test2/TracModPython.html){.wiki}
