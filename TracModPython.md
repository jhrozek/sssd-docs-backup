Trac and mod\_python {#Tracandmod_python}
====================

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

Trac supports
[[​]{.icon}mod\_python](http://www.modpython.org/){.ext-link}, which
speeds up Trac's response times considerably, especially compared to
[CGI](https://docs.pagure.org/sssd-test2/TracCgi.html){.wiki}, and
permits use of many Apache features not possible with
[tracd](https://docs.pagure.org/sssd-test2/TracStandalone.html){.wiki}/mod\_proxy.

<div class="important">

**A Word of Warning**

As of 16^th^ June 2010, the mod\_python project is officially dead. If
you are considering using mod\_python for a new installation, **please
don't**! There are known issues which will not be fixed and there are
now better alternatives. Check out the main
[TracInstall](https://docs.pagure.org/sssd-test2/TracInstall.html){.wiki}
pages for your target version for more information.

</div>

These instructions are for Apache 2; if you are still using Apache 1.3,
you may have some luck with
[[​]{.icon}TracModPython2.7](http://trac.edgewall.org/intertrac/wiki%3ATracModPython2.7 "wiki:TracModPython2.7 in Trac project trac"){.ext-link},
but you'll be totally on your own.

#### Overview

1.  [Simple configuration: single project](#Simpleconfiguration)
    1.  [Python Egg Cache](#PythonEggCache)
    2.  [Configuring Authentication](#ConfiguringAuthentication)
2.  [Advanced Configuration](#AdvancedConfiguration)
    1.  [Setting the Python Egg Cache](#SettingthePythonEggCache)
    2.  [Setting the PythonPath](#SettingthePythonPath)
    3.  [Setting up multiple projects](#Settingupmultipleprojects)
    4.  [Virtual Host Configuration](#VirtualHostConfiguration)
3.  [Troubleshooting](#Troubleshooting)
    1.  [Login Not Working](#LoginNotWorking)
    2.  [Expat-related segmentation faults](#expat)
    3.  [Form submission problems](#Formsubmissionproblems)
    4.  [Problem with virtual host
        configuration](#Problemwithvirtualhostconfiguration)
    5.  [Problem with zipped egg](#Problemwithzippedegg)
    6.  [Using .htaccess](#Using.htaccess)
    7.  [Additional .htaccess help](#Additional.htaccesshelp)
    8.  [Platform specific issues](#Platformspecificissues)
    9.  [Subversion issues](#Subversionissues)
    10. [Page layout issues](#Pagelayoutissues)
    11. [HTTPS issues](#HTTPSissues)
    12. [Segmentation fault with php5-mhash or other php5
        modules](#Segmentationfaultwithphp5-mhashorotherphp5modules)

Simple configuration: single project {#Simpleconfiguration}
------------------------------------

If you just installed mod\_python, you may have to add a line to load
the module in the Apache configuration:

``` {.wiki}
LoadModule python_module modules/mod_python.so
```

*Note: The exact path to the module depends on how the HTTPD
installation is laid out.*

On Debian using apt-get

``` {.wiki}
apt-get install libapache2-mod-python libapache2-mod-python-doc
```

(Still on Debian) after you have installed mod\_python, you must enable
the modules in apache2 (equivalent of the above Load Module directive):

``` {.wiki}
a2enmod python
```

On Fedora use, using yum:

``` {.wiki}
yum install mod_python
```

You can test your mod\_python installation by adding the following to
your httpd.conf. You should remove this when you are done testing for
security reasons. Note: mod\_python.testhandler is only available in
mod\_python 3.2+.

<div class="code">

    <Location /mpinfo>
       SetHandler mod_python
       PythonInterpreter main_interpreter
       PythonHandler mod_python.testhandler
       Order allow,deny
       Allow from all
    </Location>

</div>

A simple setup of Trac on mod\_python looks like this:

<div class="code">

    <Location /projects/myproject>
       SetHandler mod_python
       PythonInterpreter main_interpreter
       PythonHandler trac.web.modpython_frontend 
       PythonOption TracEnv /var/trac/myproject
       PythonOption TracUriRoot /projects/myproject
       Order allow,deny
       Allow from all
    </Location>

</div>

The option **`TracUriRoot`** may or may not be necessary in your setup.
Try your configuration without it; if the URLs produced by Trac look
wrong, if Trac does not seem to recognize URLs correctly, or you get an
odd "No handler matched request to..." error, add the **`TracUriRoot`**
option. You will notice that the `Location` and **`TracUriRoot`** have
the same path.

The options available are

``` {.wiki}
    # For a single project
    PythonOption TracEnv /var/trac/myproject

    # For multiple projects
    PythonOption TracEnvParentDir /var/trac/myprojects

    # For the index of multiple projects
    PythonOption TracEnvIndexTemplate /srv/www/htdocs/trac/project_list_template.html

    # A space delimitted list, with a "," between key and value pairs.
    PythonOption TracTemplateVars key1,val1 key2,val2

    # Useful to get the date in the wanted order
    PythonOption TracLocale en_GB.UTF8

    # See description above        
    PythonOption TracUriRoot /projects/myproject
```

### Python Egg Cache {#PythonEggCache}

Compressed python eggs like Genshi are normally extracted into a
directory named `.python-eggs` in the users home directory. Since
apache's home usually is not writable an alternate egg cache directory
can be specified like this:

``` {.wiki}
PythonOption PYTHON_EGG_CACHE /var/trac/myprojects/egg-cache
```

or you can uncompress the Genshi egg to resolve problems extracting from
it.

### Configuring Authentication {#ConfiguringAuthentication}

See corresponding section in the
[TracModWSGI](https://docs.pagure.org/sssd-test2/TracModWSGI.html#ConfiguringAuthentication){.wiki}
page.

Advanced Configuration {#AdvancedConfiguration}
----------------------

### Setting the Python Egg Cache {#SettingthePythonEggCache}

If the Egg Cache isn't writeable by your Web server, you'll either have
to change the permissions, or point Python to a location where Apache
can write. This can manifest itself as a *500 internal server error*
and/or a complaint in the syslog.

<div class="code">

    <Location /projects/myproject>
      ...
      PythonOption PYTHON_EGG_CACHE /tmp 
      ...
    </Location>

</div>

### Setting the PythonPath {#SettingthePythonPath}

If the Trac installation isn't installed in your Python path, you'll
have to tell Apache where to find the Trac mod\_python handler using the
`PythonPath` directive:

<div class="code">

    <Location /projects/myproject>
      ...
      PythonPath "sys.path + ['/path/to/trac']"
      ...
    </Location>

</div>

Be careful about using the PythonPath directive, and *not*
`SetEnv PYTHONPATH`, as the latter won't work.

### Setting up multiple projects {#Settingupmultipleprojects}

The Trac mod\_python handler supports a configuration option similar to
Subversion's `SvnParentPath`, called `TracEnvParentDir`:

<div class="code">

    <Location /projects>
      SetHandler mod_python
      PythonInterpreter main_interpreter
      PythonHandler trac.web.modpython_frontend 
      PythonOption TracEnvParentDir /var/trac
      PythonOption TracUriRoot /projects
    </Location>

</div>

When you request the `/projects` URL, you will get a listing of all
subdirectories of the directory you set as `TracEnvParentDir` that look
like Trac environment directories. Selecting any project in the list
will bring you to the corresponding Trac environment.

If you don't want to have the subdirectory listing as your projects home
page you can use a

<div class="code">

    <LocationMatch "/.+/">

</div>

This will instruct Apache to use mod\_python for all locations different
from root while having the possibility of placing a custom home page for
root in your DocumentRoot folder.

You can also use the same authentication realm for all of the projects
using a `<LocationMatch>` directive:

<div class="code">

    <LocationMatch "/projects/[^/]+/login">
      AuthType Basic
      AuthName "Trac"
      AuthUserFile /var/trac/.htpasswd
      Require valid-user
    </LocationMatch>

</div>

### Virtual Host Configuration {#VirtualHostConfiguration}

Below is the sample configuration required to set up your trac as a
virtual server (i.e. when you access it at the URLs like
http://trac.mycompany.com):

<div class="code">

    <VirtualHost * >
        DocumentRoot /var/www/myproject
        ServerName trac.mycompany.com
        <Location />
            SetHandler mod_python
            PythonInterpreter main_interpreter
            PythonHandler trac.web.modpython_frontend
            PythonOption TracEnv /var/trac/myproject
            PythonOption TracUriRoot /
        </Location>
        <Location /login>
            AuthType Basic
            AuthName "MyCompany Trac Server"
            AuthUserFile /var/trac/myproject/.htpasswd
            Require valid-user
        </Location>
    </VirtualHost>

</div>

This does not seem to work in all cases. What you can do if it does not:

-   Try using `<LocationMatch>` instead of `<Location>`
-   &lt;Location /&gt; may, in your server setup, refer to the complete
    host instead of simple the root of the server. This means that
    everything (including the login directory referenced below) will be
    sent to python and authentication does not work (i.e. you get the
    infamous Authentication information missing error). If this applies
    to you, try using a sub-directory for trac instead of the root (i.e.
    /web/ and /web/login instead of / and /login).
-   Depending on apache's `NameVirtualHost` configuration, you may need
    to use `<VirtualHost *:80>` instead of `<VirtualHost *>`.

For a virtual host that supports multiple projects replace "`TracEnv`"
/var/trac/myproject with "`TracEnvParentDir`" /var/trac/

Note: DocumentRoot should not point to your Trac project env. As Asmodai
wrote on \#trac: "suppose there's a webserver bug that allows disclosure
of DocumentRoot they could then leech the entire Trac environment".

Troubleshooting {#Troubleshooting}
---------------

In general, if you get server error pages, you can either check the
Apache error log, or enable the `PythonDebug` option:

<div class="code">

    <Location /projects/myproject>
      ...
      PythonDebug on
    </Location>

</div>

For multiple projects, try restarting the server as well.

### Login Not Working {#LoginNotWorking}

If you've used `<Location />` directive, it will override any other
directives, as well as `<Location /login>`. The workaround is to use
negation expression as follows (for multi project setups):

<div class="code">

    #this one for other pages
    <Location ~ "/*(?!login)">
       SetHandler mod_python
       PythonHandler trac.web.modpython_frontend
       PythonOption TracEnvParentDir /projects
       PythonOption TracUriRoot /

    </Location>
    #this one for login page
    <Location ~ "/[^/]+/login">
       SetHandler mod_python
       PythonHandler trac.web.modpython_frontend
       PythonOption TracEnvParentDir /projects
       PythonOption TracUriRoot /

       #remove these if you don't want to force SSL
       RewriteEngine On 
       RewriteCond %{HTTPS} off
       RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

       AuthType Basic
       AuthName "Trac"
       AuthUserFile /projects/.htpasswd
       Require valid-user
    </Location>

</div>

### Expat-related segmentation faults {#expat}

This problem will most certainly hit you on Unix when using Python 2.4.
In Python 2.4, some version of Expat (an XML parser library written in
C) is used, and if Apache is using another version, this results in
segmentation faults. As Trac 0.11 is using Genshi, which will indirectly
use Expat, that problem can now hit you even if everything was working
fine before with Trac 0.10.

See Graham Dumpleton's detailed [[​]{.icon}explanation and
workarounds](http://www.dscpl.com.au/wiki/ModPython/Articles/ExpatCausingApacheCrash){.ext-link}
for the issue.

### Form submission problems {#Formsubmissionproblems}

If you're experiencing problems submitting some of the forms in Trac (a
common problem is that you get redirected to the start page after
submission), check whether your `DocumentRoot` contains a folder or file
with the same path that you mapped the mod\_python handler to. For some
reason, mod\_python gets confused when it is mapped to a location that
also matches a static resource.

### Problem with virtual host configuration {#Problemwithvirtualhostconfiguration}

If the &lt;Location /&gt; directive is used, setting the `DocumentRoot`
may result in a *403 (Forbidden)* error. Either remove the
`DocumentRoot` directive, or make sure that accessing the directory it
points is allowed (in a corresponding `<Directory>` block).

Using &lt;Location /&gt; together with `SetHandler` resulted in having
everything handled by mod\_python, which leads to not being able
download any CSS or images/icons. I used &lt;Location /trac&gt;
`SetHandler None` &lt;/Location&gt; to circumvent the problem, though I
do not know if this is the most elegant solution.

### Problem with zipped egg {#Problemwithzippedegg}

It's possible that your version of mod\_python will not import modules
from zipped eggs. If you encounter an
`ImportError: No module named trac` in your Apache logs but you think
everything is where it should be, this might be your problem. Look in
your site-packages directory; if the Trac module appears as a *file*
rather than a *directory*, then this might be your problem. To rectify,
try installing Trac using the `--always-unzip` option, like this:

``` {.wiki}
easy_install --always-unzip Trac-0.12b1.zip
```

### Using .htaccess {#Using.htaccess}

Although it may seem trivial to rewrite the above configuration as a
directory in your document root with a `.htaccess` file, this does not
work. Apache will append a "/" to any Trac URLs, which interferes with
its correct operation.

It may be possible to work around this with mod\_rewrite, but I failed
to get this working. In all, it is more hassle than it is worth. Stick
to the provided instructions. :)

A success story: For me it worked out-of-box, with following trivial
config:

<div class="code">

    SetHandler mod_python
    PythonInterpreter main_interpreter
    PythonHandler trac.web.modpython_frontend 
    PythonOption TracEnv /system/path/to/this/directory
    PythonOption TracUriRoot /path/on/apache

    AuthType Basic
    AuthName "ProjectName"
    AuthUserFile /path/to/.htpasswd
    Require valid-user

</div>

The `TracUriRoot` is obviously the path you need to enter to the browser
to get to the trac (e.g. domain.tld/projects/trac)

### Additional .htaccess help {#Additional.htaccesshelp}

If you are using the .htaccess method you may have additional problems
if your trac directory is inheriting .htaccess directives from another.
This may also help to add to your .htaccess file:

``` {.wiki}
<IfModule mod_rewrite.c>
  RewriteEngine Off
</IfModule>
```

### Platform specific issues {#Platformspecificissues}

#### Win32 Issues {#Win32Issues}

If you run trac with mod\_python &lt; 3.2 on Windows, uploading
attachments will **not** work. This problem is resolved in mod\_python
3.1.4 or later, so please upgrade mod\_python to fix this.

#### OS X issues {#OSXissues}

When using mod\_python on OS X you will not be able to restart Apache
using `apachectl restart`. This is apparently fixed in mod\_python 3.2,
but there's also a patch available for earlier versions
[[​]{.icon}here](http://www.dscpl.com.au/projects/vampire/patches.html){.ext-link}.

#### SELinux issues {#SELinuxissues}

If Trac reports something like: *Cannot get shared lock on db.lock* The
security context on the repository may need to be set:

``` {.wiki}
chcon -R -h -t httpd_sys_content_t PATH_TO_REPOSITORY
```

See also
[[​]{.icon}http://subversion.tigris.org/faq.html\#reposperms](http://subversion.tigris.org/faq.html#reposperms){.ext-link}

#### FreeBSD issues {#FreeBSDissues}

Pay attention to the version of the installed mod\_python and sqlite
packages. Ports have both the new and old ones, but earlier versions of
pysqlite and mod\_python won't integrate as the former requires threaded
support in python, and the latter requires a threadless install.

If you compiled and installed apache2, apache wouldn´t support threads
(cause it doesn´t work very well on FreeBSD). You could force thread
support when running ./configure for apache, using --enable-threads, but
this isn´t recommendable. The best option [[​]{.icon}seems to
be](http://modpython.org/pipermail/mod_python/2006-September/021983.html){.ext-link}
adding to /usr/local/apache2/bin/ennvars the line

``` {.wiki}
export LD_PRELOAD=/usr/lib/libc_r.so
```

#### Fedora 7 Issues {#Fedora7Issues}

Make sure you install the 'python-sqlite2' package as it seems to be
required for
[TracModPython](https://docs.pagure.org/sssd-test2/TracModPython.html){.wiki}
but not for tracd

### Subversion issues {#Subversionissues}

If you get the following Trac Error
`Unsupported version control system "svn"` only under mod\_python,
though it works well on the command-line and even with
[TracStandalone](https://docs.pagure.org/sssd-test2/TracStandalone.html){.wiki},
chances are that you forgot to add the path to the Python bindings with
the
[PythonPath](https://docs.pagure.org/sssd-test2/TracModPython.html#ConfiguringPythonPath){.wiki}
directive. (The better way is to add a link to the bindings in the
Python `site-packages` directory, or create a `.pth` file in that
directory.)

If this is not the case, it's possible that you're using Subversion
libraries that are binary incompatible with the apache ones (an
incompatibility of the `apr` libraries is usually the cause). In that
case, you also won't be able to use the svn modules for Apache
(`mod_dav_svn`).

You also need a recent version of `mod_python` in order to avoid a
runtime error (`argument number 2: a 'apr_pool_t *' is expected`) due to
the default usage of multiple sub-interpreters. 3.2.8 *should* work,
though it's probably better to use the workaround described in
[[​]{.icon}\#3371](http://trac.edgewall.org/intertrac/%233371 "#3371 in Trac project trac"){.ext-link},
in order to force the use of the main interpreter:

``` {.wiki}
PythonInterpreter main_interpreter
```

This is anyway the recommended workaround for other well-known issues
seen when using the Python bindings for Subversion within mod\_python
([[​]{.icon}\#2611](http://trac.edgewall.org/intertrac/%232611 "#2611 in Trac project trac"){.ext-link},
[[​]{.icon}\#3455](http://trac.edgewall.org/intertrac/%233455 "#3455 in Trac project trac"){.ext-link}).
See in particular Graham Dumpleton's comment in
[[​]{.icon}\#3455](http://trac.edgewall.org/intertrac/comment%3A9%3Aticket%3A3455 "comment:9:ticket:3455 in Trac project trac"){.ext-link}
explaining the issue.

### Page layout issues {#Pagelayoutissues}

If the formatting of the Trac pages look weird chances are that the
style sheets governing the page layout are not handled properly by the
web server. Try adding the following lines to your apache configuration:

<div class="code">

    Alias /myproject/css "/usr/share/trac/htdocs/css"
    <Location /myproject/css>
        SetHandler None
    </Location>

</div>

Note: For the above configuration to have any effect it must be put
after the configuration of your project root location, i.e.
`<Location /myproject />`.

Also, setting `PythonOptimize On` seems to mess up the page headers and
footers, in addition to hiding the documentation for macros and plugins
(see \#Trac8956). Considering how little effect the option has, it is
probably a good idea to leave it `Off`.

### HTTPS issues {#HTTPSissues}

If you want to run Trac fully under https you might find that it tries
to redirect to plain http. In this case just add the following line to
your apache configuration:

<div class="code">

    <VirtualHost * >
        DocumentRoot /var/www/myproject
        ServerName trac.mycompany.com
        SetEnv HTTPS 1
        ....
    </VirtualHost>

</div>

### Segmentation fault with php5-mhash or other php5 modules {#Segmentationfaultwithphp5-mhashorotherphp5modules}

You may encounter segfaults (reported on debian etch) if php5-mhash
module is installed. Try to remove it to see if this solves the problem.
See debian bug report
[[​]{.icon}http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=411487](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=411487){.ext-link}

Some people also have troubles when using php5 compiled with its own 3rd
party libraries instead of system libraries. Check here
[[​]{.icon}http://www.djangoproject.com/documentation/modpython/\#if-you-get-a-segmentation-fault](http://www.djangoproject.com/documentation/modpython/#if-you-get-a-segmentation-fault){.ext-link}

------------------------------------------------------------------------

See also:
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[TracInstall](https://docs.pagure.org/sssd-test2/TracInstall.html){.wiki},
[ModWSGI](https://docs.pagure.org/sssd-test2/TracModWSGI.html){.wiki},
[FastCGI](https://docs.pagure.org/sssd-test2/TracFastCgi.html){.wiki},
[[​]{.icon}TracNginxRecipe](http://trac.edgewall.org/intertrac/TracNginxRecipe "TracNginxRecipe in Trac project trac"){.ext-link}