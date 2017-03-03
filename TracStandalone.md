Tracd {#Tracd}
=====

Tracd is a lightweight standalone Trac web server. It can be used in a
variety of situations, from a test or development server to a
multiprocess setup behind another web server used as a load balancer.

Pros {#Pros}
----

-   Fewer dependencies: You don't need to install apache or any other
    web-server.
-   Fast: Should be almost as fast as the
    [mod\_python](https://docs.pagure.org/sssd-test2/TracModPython.html){.wiki}
    version (and much faster than the
    [CGI](https://docs.pagure.org/sssd-test2/TracCgi.html){.wiki}), even
    more so since version 0.12 where the HTTP/1.1 version of the
    protocol is enabled by default
-   Automatic reloading: For development, Tracd can be used in
    *auto\_reload* mode, which will automatically restart the server
    whenever you make a change to the code (in Trac itself or in a
    plugin).

Cons {#Cons}
----

-   Fewer features: Tracd implements a very simple web-server and is not
    as configurable or as scalable as Apache httpd.
-   No native HTTPS support:
    [[​]{.icon}sslwrap](http://www.rickk.com/sslwrap/){.ext-link} can be
    used instead, or [[​]{.icon}stunnel -- a tutorial on how to use
    stunnel with
    tracd](http://trac.edgewall.org/wiki/STunnelTracd){.ext-link} or
    Apache with mod\_proxy.

Usage examples {#Usageexamples}
--------------

A single project on port 8080.
([[​]{.icon}http://localhost:8080/](http://localhost:8080/){.ext-link})

``` {.wiki}
 $ tracd -p 8080 /path/to/project
```

Stricly speaking this will make your Trac accessible to everybody from
your network rather than *localhost only*. To truly limit it use
*--hostname* option.

``` {.wiki}
 $ tracd --hostname=localhost -p 8080 /path/to/project
```

With more than one project.
([[​]{.icon}http://localhost:8080/project1/](http://localhost:8080/project1/){.ext-link}
and
[[​]{.icon}http://localhost:8080/project2/](http://localhost:8080/project2/){.ext-link})

``` {.wiki}
 $ tracd -p 8080 /path/to/project1 /path/to/project2
```

You can't have the last portion of the path identical between the
projects since Trac uses that name to keep the URLs of the different
projects unique. So if you use `/project1/path/to` and
`/project2/path/to`, you will only see the second project.

An alternative way to serve multiple projects is to specify a parent
directory in which each subdirectory is a Trac project, using the `-e`
option. The example above could be rewritten:

``` {.wiki}
 $ tracd -p 8080 -e /path/to
```

To exit the server on Windows, be sure to use `CTRL-BREAK` -- using
`CTRL-C` will leave a Python process running in the background.

Installing as a Windows Service {#InstallingasaWindowsService}
-------------------------------

### Option 1 {#Option1}

To install as a Windows service, get the
[[​]{.icon}SRVANY](http://www.google.com/search?q=srvany.exe){.ext-link}
utility and run:

``` {.wiki}
 C:\path\to\instsrv.exe tracd C:\path\to\srvany.exe
 reg add HKLM\SYSTEM\CurrentControlSet\Services\tracd\Parameters /v Application /d "\"C:\path\to\python.exe\" \"C:\path\to\python\scripts\tracd-script.py\" <your tracd parameters>"
 net start tracd
```

**DO NOT** use `tracd.exe`. Instead register `python.exe` directly with
`tracd-script.py` as a parameter. If you use `tracd.exe`, it will spawn
the python process without SRVANY's knowledge. This python process will
survive a `net stop tracd`.

If you want tracd to start automatically when you boot Windows, do:

``` {.wiki}
 sc config tracd start= auto
```

The spacing here is important.

<div class="wikipage">

Once the service is installed, it might be simpler to run the Registry
Editor rather than use the `reg add` command documented above. Navigate
to:\
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\tracd\Parameters`

Three (string) parameters are provided:

  --------------- --------------------------------------
  AppDirectory    C:\\Python26\\
  Application     python.exe
  AppParameters   scripts\\tracd-script.py -p 8080 ...
  --------------- --------------------------------------

Note that, if the AppDirectory is set as above, the paths of the
executable *and* of the script name and parameter values are relative to
the directory. This makes updating Python a little simpler because the
change can be limited, here, to a single point. (This is true for the
path to the .htpasswd file, as well, despite the documentation calling
out the /full/path/to/htpasswd; however, you may not wish to store that
file under the Python directory.)

</div>

For Windows 7 User, srvany.exe may not be an option, so you can use
[[​]{.icon}WINSERV](http://www.google.com/search?q=winserv.exe){.ext-link}
utility and run:

``` {.wiki}
"C:\path\to\winserv.exe" install tracd -displayname "tracd" -start auto "C:\path\to\python.exe" c:\path\to\python\scripts\tracd-script.py <your tracd parameters>"

net start tracd
```

### Option 2 {#Option2}

Use
[[​]{.icon}WindowsServiceScript](http://trac-hacks.org/wiki/WindowsServiceScript){.ext-link},
available at [[​]{.icon}Trac Hacks](http://trac-hacks.org/){.ext-link}.
Installs, removes, starts, stops, etc. your Trac service.

### Option 3 {#Option3}

also cygwin's cygrunsrv.exe can be used:

``` {.wiki}
$ cygrunsrv --install tracd --path /cygdrive/c/Python27/Scripts/tracd.exe --args '--port 8000 --env-parent-dir E:\IssueTrackers\Trac\Projects'
$ net start tracd
```

Using Authentication {#UsingAuthentication}
--------------------

Tracd provides support for both Basic and Digest authentication. Digest
is considered more secure. The examples below use Digest; to use Basic
authentication, replace `--auth` with `--basic-auth` in the command
line.

The general format for using authentication is:

``` {.wiki}
 $ tracd -p port --auth="base_project_dir,password_file_path,realm" project_path
```

where:

-   **base\_project\_dir**: the base directory of the project specified
    as follows:
    -   when serving multiple projects: *relative* to the `project_path`
    -   when serving only a single project (`-s`): the name of the
        project directory

> Don't use an absolute path here as this won't work. *Note:* This
> parameter is case-sensitive even for environments on Windows.

-   **password\_file\_path**: path to the password file
-   **realm**: the realm name (can be anything)
-   **project\_path**: path of the project

<!-- -->

-   **`--auth`** in the above means use Digest authentication, replace
    `--auth` with `--basic-auth` if you want to use Basic auth. Although
    Basic authentication does not require a "realm", the command parser
    does, so the second comma is required, followed directly by the
    closing quote for an empty realm name.

Examples:

``` {.wiki}
 $ tracd -p 8080 \
   --auth="project1,/path/to/passwordfile,mycompany.com" /path/to/project1
```

Of course, the password file can be be shared so that it is used for
more than one project:

``` {.wiki}
 $ tracd -p 8080 \
   --auth="project1,/path/to/passwordfile,mycompany.com" \
   --auth="project2,/path/to/passwordfile,mycompany.com" \
   /path/to/project1 /path/to/project2
```

Another way to share the password file is to specify "\*" for the
project name:

``` {.wiki}
 $ tracd -p 8080 \
   --auth="*,/path/to/users.htdigest,mycompany.com" \
   /path/to/project1 /path/to/project2
```

### Basic Authorization: Using a htpasswd password file {#BasicAuthorization:Usingahtpasswdpasswordfile}

This section describes how to use `tracd` with Apache .htpasswd files.

> Note: It is necessary (at least with Python 2.6) to install the fcrypt
> package in order to decode the htpasswd format. Trac source code
> attempt an `import crypt` first, but there is no such package for
> Python 2.6.

To create a .htpasswd file use Apache's `htpasswd` command (see
[below](https://fedorahosted.org/sssd#GeneratingPasswordsWithoutApache)
for a method to create these files without using Apache):

``` {.wiki}
 $ sudo htpasswd -c /path/to/env/.htpasswd username
```

then for additional users:

``` {.wiki}
 $ sudo htpasswd /path/to/env/.htpasswd username2
```

Then to start `tracd` run something like this:

``` {.wiki}
 $ tracd -p 8080 --basic-auth="projectdirname,/fullpath/environmentname/.htpasswd,realmname" /fullpath/environmentname
```

For example:

``` {.wiki}
 $ tracd -p 8080 --basic-auth="testenv,/srv/tracenv/testenv/.htpasswd,My Test Env" /srv/tracenv/testenv
```

*Note:* You might need to pass "-m" as a parameter to htpasswd on some
platforms (OpenBSD).

### Digest authentication: Using a htdigest password file {#Digestauthentication:Usingahtdigestpasswordfile}

If you have Apache available, you can use the htdigest command to
generate the password file. Type 'htdigest' to get some usage
instructions, or read [[​]{.icon}this
page](http://httpd.apache.org/docs/2.0/programs/htdigest.html){.ext-link}
from the Apache manual to get precise instructions. You'll be prompted
for a password to enter for each user that you create. For the name of
the password file, you can use whatever you like, but if you use
something like `users.htdigest` it will remind you what the file
contains. As a suggestion, put it in your &lt;projectname&gt;/conf
folder along with the
[trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki} file.

Note that you can start tracd without the --auth argument, but if you
click on the *Login* link you will get an error.

### Generating Passwords Without Apache {#GeneratingPasswordsWithoutApache}

Basic Authorization can be accomplished via this [[​]{.icon}online HTTP
Password generator](http://aspirine.org/htpasswd_en.html){.ext-link}.
Copy the generated password-hash line to the .htpasswd file on your
system. Note that Windows Python lacks the "crypt" module that is the
default hash type for htpasswd ; Windows Python can grok MD5 password
hashes just fine and you should use MD5.

You can use this simple Python script to generate a **digest** password
file:

<div class="code">

    from optparse import OptionParser
    # The md5 module is deprecated in Python 2.5
    try:
        from hashlib import md5
    except ImportError:
        from md5 import md5
    realm = 'trac'

    # build the options
    usage = "usage: %prog [options]"
    parser = OptionParser(usage=usage)
    parser.add_option("-u", "--username",action="store", dest="username", type = "string",
                      help="the username for whom to generate a password")
    parser.add_option("-p", "--password",action="store", dest="password", type = "string",
                      help="the password to use")
    parser.add_option("-r", "--realm",action="store", dest="realm", type = "string",
                      help="the realm in which to create the digest")
    (options, args) = parser.parse_args()

    # check options
    if (options.username is None) or (options.password is None):
       parser.error("You must supply both the username and password")
    if (options.realm is not None):
       realm = options.realm
       
    # Generate the string to enter into the htdigest file
    kd = lambda x: md5(':'.join(x)).hexdigest()
    print ':'.join((options.username, realm, kd([options.username, realm, options.password])))

</div>

Note: If you use the above script you must set the realm in the `--auth`
argument to **`trac`**. Example usage (assuming you saved the script as
trac-digest.py):

``` {.wiki}
 $ python trac-digest.py -u username -p password >> c:\digest.txt
 $ tracd --port 8000 --auth=proj_name,c:\digest.txt,trac c:\path\to\proj_name
```

#### Using `md5sum` {#Usingmd5sum}

It is possible to use `md5sum` utility to generate digest-password file:

``` {.wiki}
user=
realm=
password=
path_to_file=
echo ${user}:${realm}:$(printf "${user}:${realm}:${password}" | md5sum - | sed -e 's/\s\+-//') > ${path_to_file}
```

Reference {#Reference}
---------

Here's the online help, as a reminder (`tracd --help`):

``` {.wiki}
Usage: tracd [options] [projenv] ...

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -a DIGESTAUTH, --auth=DIGESTAUTH
                        [projectdir],[htdigest_file],[realm]
  --basic-auth=BASICAUTH
                        [projectdir],[htpasswd_file],[realm]
  -p PORT, --port=PORT  the port number to bind to
  -b HOSTNAME, --hostname=HOSTNAME
                        the host name or IP address to bind to
  --protocol=PROTOCOL   http|scgi|ajp|fcgi
  -q, --unquote         unquote PATH_INFO (may be needed when using ajp)
  --http10              use HTTP/1.0 protocol version instead of HTTP/1.1
  --http11              use HTTP/1.1 protocol version (default)
  -e PARENTDIR, --env-parent-dir=PARENTDIR
                        parent directory of the project environments
  --base-path=BASE_PATH
                        the initial portion of the request URL's "path"
  -r, --auto-reload     restart automatically when sources are modified
  -s, --single-env      only serve a single project without the project list
  -d, --daemonize       run in the background as a daemon
  --pidfile=PIDFILE     When daemonizing, file to which to write pid
  --umask=MASK          When daemonizing, file mode creation mask to use, in
                        octal notation (default 022)
```

Use the -d option so that tracd doesn't hang if you close the terminal
window where tracd was started.

Tips {#Tips}
----

### Serving static content {#Servingstaticcontent}

If `tracd` is the only web server used for the project, it can also be
used to distribute static content (tarballs, Doxygen documentation,
etc.)

This static content should be put in the `$TRAC_ENV/htdocs` folder, and
is accessed by URLs like `<project_URL>/chrome/site/...`.

Example: given a `$TRAC_ENV/htdocs/software-0.1.tar.gz` file, the
corresponding relative URL would be
`/<project_name>/chrome/site/software-0.1.tar.gz`, which in turn can be
written as `htdocs:software-0.1.tar.gz`
([TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
syntax) or `[/<project_name>/chrome/site/software-0.1.tar.gz]` (relative
link syntax).

> *Support for `htdocs:`
> [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
> syntax was added in version 0.10*

### Using tracd behind a proxy {#Usingtracdbehindaproxy}

In some situations when you choose to use tracd behind Apache or another
web server.

In this situation, you might experience issues with redirects, like
being redirected to URLs with the wrong host or protocol. In this case
(and only in this case), setting the `[trac] use_base_url_for_redirect`
to `true` can help, as this will force Trac to use the value of
`[trac] base_url` for doing the redirects.

If you're using the AJP protocol to connect with `tracd` (which is
possible if you have flup installed), then you might experience problems
with double quoting. Consider adding the `--unquote` parameter.

See also
[[​]{.icon}TracOnWindowsIisAjp](http://trac.edgewall.org/intertrac/TracOnWindowsIisAjp "TracOnWindowsIisAjp in Trac project trac"){.ext-link},
[[​]{.icon}TracNginxRecipe](http://trac.edgewall.org/intertrac/TracNginxRecipe "TracNginxRecipe in Trac project trac"){.ext-link}.

### Authentication for tracd behind a proxy {#Authenticationfortracdbehindaproxy}

It is convenient to provide central external authentication to your
tracd instances, instead of using `--basic-auth`. There is some
discussion about this in [\#9206]{.missing .ticket}.

Below is example configuration based on Apache 2.2, mod\_proxy,
mod\_authnz\_ldap.

First we bring tracd into Apache's location namespace.

``` {.wiki}
<Location /project/proxified>
        Require ldap-group cn=somegroup, ou=Groups,dc=domain.com
        Require ldap-user somespecificusertoo
        ProxyPass http://localhost:8101/project/proxified/
        # Turns out we don't really need complicated RewriteRules here at all
        RequestHeader set REMOTE_USER %{REMOTE_USER}s
</Location>
```

Then we need a single file plugin to recognize HTTP\_REMOTE\_USER header
as valid authentication source. HTTP headers like **HTTP\_FOO\_BAR**
will get converted to **Foo-Bar** during processing. Name it something
like **remote-user-auth.py** and drop it into **proxified/plugins**
directory:

<div class="code">

    from trac.core import *
    from trac.config import BoolOption
    from trac.web.api import IAuthenticator

    class MyRemoteUserAuthenticator(Component):

        implements(IAuthenticator)

        obey_remote_user_header = BoolOption('trac', 'obey_remote_user_header', 'false', 
                   """Whether the 'Remote-User:' HTTP header is to be trusted for user logins 
                    (''since ??.??').""") 

        def authenticate(self, req):
            if self.obey_remote_user_header and req.get_header('Remote-User'): 
                return req.get_header('Remote-User') 
            return None

</div>

Add this new parameter to your
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki}:

``` {.wiki}
...
[trac]
...
obey_remote_user_header = true
...
```

Run tracd:

``` {.wiki}
tracd -p 8101 -r -s proxified --base-path=/project/proxified
```

### Serving a different base path than / {#Servingadifferentbasepaththan}

Tracd supports serving projects with different base urls than
/&lt;project&gt;. The parameter name to change this is

``` {.wiki}
 $ tracd --base-path=/some/path
```

------------------------------------------------------------------------

See also:
[TracInstall](https://docs.pagure.org/sssd-test2/TracInstall.html){.wiki},
[TracCgi](https://docs.pagure.org/sssd-test2/TracCgi.html){.wiki},
[TracModPython](https://docs.pagure.org/sssd-test2/TracModPython.html){.wiki},
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[[​]{.icon}Running tracd.exe as a Windows
service](http://trac.edgewall.org/intertrac/TracOnWindowsStandalone%23RunningTracdasservice "TracOnWindowsStandalone#RunningTracdasservice in Trac project trac"){.ext-link}
