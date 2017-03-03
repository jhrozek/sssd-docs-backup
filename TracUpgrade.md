Upgrade Instructions {#UpgradeInstructions}
====================

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

1.  [Instructions](#Instructions)
    1.  [1. Bring your server off-line](#a1.Bringyourserveroff-line)
    2.  [2. Update the Trac Code](#UpdatetheTracCode)
    3.  [3. Upgrade the Trac Environment](#UpgradetheTracEnvironment)
    4.  [4. Update the Trac Documentation](#UpdatetheTracDocumentation)
    5.  [5. Refresh static resources](#a5.Refreshstaticresources)
    6.  [6. Steps specific to a given Trac
        version](#a6.StepsspecifictoagivenTracversion)
    7.  [7. Restart the Web Server](#RestarttheWebServer)
2.  [Known Issues](#KnownIssues)
    1.  [Customized Templates](#CustomizedTemplates)
    2.  [ZipImportError](#ZipImportError)
    3.  [Wiki Upgrade](#WikiUpgrade)
    4.  [Trac database upgrade](#Tracdatabaseupgrade)
    5.  [parent dir](#parentdir)
3.  [Related topics](#Relatedtopics)
    1.  [Upgrading Python](#UpgradingPython)
    2.  [Changing Database Backend](#ChangingDatabaseBackend)
    3.  [Upgrading from older versions of Trac](#OlderVersions)

Instructions {#Instructions}
------------

Typically, there are seven steps involved in upgrading to a newer
version of Trac:

### 1. Bring your server off-line {#a1.Bringyourserveroff-line}

It is not a good idea to update a running server: the server processes
may have parts of the current packages cached in memory, and updating
the code will likely trigger [internal
errors](https://fedorahosted.org/sssd#ZipImportError).

### 2. Update the Trac Code {#UpdatetheTracCode}

Get the new version as described in
[TracInstall](https://docs.pagure.org/sssd-test2/TracInstall.html){.wiki},
or your operating system specific procedure.

If you already have a 0.11 version of Trac installed via `easy_install`,
it might be easiest to also use `easy_install` to upgrade your Trac
installation:

``` {.wiki}
# easy_install --upgrade Trac==0.12
```

If you do a manual (not operating system-specific) upgrade, you should
also stop any running Trac servers before the installation. Doing "hot"
upgrades is not advised, especially on Windows
([[​]{.icon}\#7265](http://trac.edgewall.org/intertrac/%237265 "#7265 in Trac project trac"){.ext-link}).

You may also want to remove the pre-existing Trac code by deleting the
`trac` directory from the Python `lib/site-packages` directory, or
remove Trac `.egg` files from former versions. The location of the
site-packages directory depends on the operating system and the location
in which Python was installed. However, the following locations are
typical:

-   on Linux: `/usr/lib/python2.X/site-packages`
-   on Windows: `C:\Python2.X\lib\site-packages`
-   on MacOSX: `/Library/Python/2.X/site-packages`

You may also want to remove the Trac `cgi-bin`, `htdocs`, `templates`
and `wiki-default` directories that are commonly found in a directory
called `share/trac`. (The exact location depends on your platform.)

This cleanup is not mandatory, but makes it easier to troubleshoot
issues later on, as you won't waste your time looking at code or
templates from a previous release that are not being used anymore... As
usual, make a backup before actually deleting things.

### 3. Upgrade the Trac Environment {#UpgradetheTracEnvironment}

Environment upgrades are not necessary for minor version releases unless
otherwise noted.

After restarting, Trac should show the instances which need a manual
upgrade via the automated upgrade scripts to ease the pain. These
scripts are run via
[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki}:

``` {.wiki}
trac-admin /path/to/projenv upgrade
```

This command will do nothing if the environment is already up-to-date.

Note that a backup of your database will be performed automatically
prior to the upgrade. This feature is relatively new for the PostgreSQL
or MySQL database backends, so if it fails, you will have to backup the
database manually. Then, to perform the actual upgrade, run:

``` {.wiki}
trac-admin /path/to/projenv upgrade --no-backup
```

### 4. Update the Trac Documentation {#UpdatetheTracDocumentation}

Every [Trac
environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
includes a copy of the Trac documentation for the installed version. As
you probably want to keep the included documentation in sync with the
installed version of Trac,
[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki}
provides a command to upgrade the documentation:

``` {.wiki}
trac-admin /path/to/projenv wiki upgrade
```

Note that this procedure will leave your `WikiStart` page intact.

### 5. Refresh static resources {#a5.Refreshstaticresources}

If you have set up a web server to give out static resources directly
(accessed using the `/chrome/` URL) then you will need to refresh them
using the same command:

``` {.wiki}
trac-admin /path/to/env deploy /deploy/path
```

this will extract static resources and CGI scripts (`trac.wsgi`, etc)
from new Trac version and its plugins into `/deploy/path`.

Some web browsers (IE, Opera) cache CSS and Javascript files
aggressively, so you may need to instruct your users to manually erase
the contents of their browser's cache, a forced refreshed (`<F5>`)
should be enough.

### 6. Steps specific to a given Trac version {#a6.StepsspecifictoagivenTracversion}

#### Upgrading from Trac 0.11 to Trac 0.12 {#UpgradingfromTrac0.11toTrac0.12}

##### Python 2.3 no longer supported {#Python2.3nolongersupported}

The minimum supported version of python is now 2.4

##### SQLite v3.x required {#SQLitev3.xrequired}

SQLite v2.x is no longer supported. If you still use a Trac database of
this format, you'll need to convert it to SQLite v3.x first. See
[[​]{.icon}PySqlite\#UpgradingSQLitefrom2.xto3.x](http://trac.edgewall.org/intertrac/PySqlite%23UpgradingSQLitefrom2.xto3.x "PySqlite#UpgradingSQLitefrom2.xto3.x in Trac project trac"){.ext-link}
for details.

##### [PySqlite?](https://docs.pagure.org/sssd-test2/PySqlite.html){.missing .wiki} 2 required {#PySqlite2required}

[PySqlite?](https://docs.pagure.org/sssd-test2/PySqlite.html){.missing
.wiki} 1.1.x is no longer supported. Please install 2.5.5 or later if
possible (see [Trac database
upgrade](https://fedorahosted.org/sssd#Tracdatabaseupgrade) below).

##### Multiple Repository Support {#MultipleRepositorySupport}

The latest version includes support for multiple repositories. If you
plan to add more repositories to your Trac instance, please refer to
[TracRepositoryAdmin\#Migration](https://docs.pagure.org/sssd-test2/TracRepositoryAdmin.html#Migration){.wiki}.

This may be of interest to users with only one repository, since there's
now a way to avoid the potentially costly resync check at every request.

##### Resynchronize the Trac Environment Against the Source Code Repository {#ResynchronizetheTracEnvironmentAgainsttheSourceCodeRepository}

Each [Trac
environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
must be resynchronized against the source code repository in order to
avoid errors such as "[[​]{.icon}No changeset ??? in the
repository](http://trac.edgewall.org/ticket/6120){.ext-link}" while
browsing the source through the Trac interface:

``` {.wiki}
trac-admin /path/to/projenv repository resync '*'
```

##### Improved repository synchronization {#Improvedrepositorysynchronization}

In addition to supporting multiple repositories, there is now a more
efficient method for synchronizing Trac and your repositories.

While you can keep the same synchronization as in 0.11 adding the
post-commit hook as outlined in
[TracRepositoryAdmin\#Synchronization](https://docs.pagure.org/sssd-test2/TracRepositoryAdmin.html#Synchronization){.wiki}
and
[TracRepositoryAdmin\#ExplicitSync](https://docs.pagure.org/sssd-test2/TracRepositoryAdmin.html#ExplicitSync){.wiki}
will allow more efficient synchronization and is more or less required
for multiple repositories.

Note that if you were using the `trac-post-commit-hook`, *you're
strongly advised to upgrade it* to the new hook documented in the above
references, as the old hook will not work with anything else than the
default repository and even for this case, it won't trigger the
appropriate notifications.

##### Authz permission checking {#Authzpermissionchecking}

The authz permission checking has been migrated to a fine-grained
permission policy. If you use authz permissions (aka `[trac] authz_file`
and `authz_module_name`), you must add `AuthzSourcePolicy` in front of
your permission policies in `[trac] permission_policies`. You must also
remove `BROWSER_VIEW`, `CHANGESET_VIEW`, `FILE_VIEW` and `LOG_VIEW` from
your global permissions (with `trac-admin $ENV permission remove` or the
"Permissions" admin panel).

##### Microsecond timestamps {#Microsecondtimestamps}

All timestamps in database tables (except the `session` table) have been
changed from "seconds since epoch" to "microseconds since epoch" values.
This change should be transparent to most users, except for custom
reports. If any of your reports use date/time columns in calculations
(e.g. to pass them to `datetime()`), you must divide the values
retrieved from the database by 1'000'000. Similarly, if a report
provides a calculated value to be displayed as a date/time (i.e. with a
column named "time", "datetime", "changetime", "date", "created" or
"modified"), you must provide a microsecond timestamp, that is, multiply
your previous calculation with 1'000'000.

#### Upgrading from Trac 0.10 to Trac 0.11 {#UpgradingfromTrac0.10toTrac0.11}

##### Site Templates and Styles {#SiteTemplatesandStyles}

The templating engine has changed in 0.11 to Genshi, please look at
[TracInterfaceCustomization](https://docs.pagure.org/sssd-test2/TracInterfaceCustomization.html){.wiki}
for more information.

If you are using custom CSS styles or modified templates in the
`templates` directory of the
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki},
you will need to convert them to the Genshi way of doing things. To
continue to use your style sheet, follow the instructions at
[TracInterfaceCustomization\#SiteAppearance](https://docs.pagure.org/sssd-test2/TracInterfaceCustomization.html#SiteAppearance){.wiki}.

##### Trac Macros, Plugins {#TracMacrosPlugins}

The Trac macros will need to be adapted, as the old-style wiki-macros
are not supported anymore (due to the drop of
[[​]{.icon}ClearSilver](http://trac.edgewall.org/intertrac/ClearSilver "ClearSilver in Trac project trac"){.ext-link}
and the HDF); they need to be converted to the new-style macros, see
[WikiMacros](https://docs.pagure.org/sssd-test2/WikiMacros.html){.wiki}.
When they are converted to the new style, they need to be placed into
the plugins directory instead and not wiki-macros, which is no longer
scanned for macros or plugins.

##### For FCGI/WSGI/CGI users {#ForFCGIWSGICGIusers}

For those who run Trac under the CGI environment, run this command in
order to obtain the trac.\*gi file:

``` {.wiki}
trac-admin /path/to/env deploy /deploy/directory/path
```

This will create a deploy directory with the following two
subdirectories: `cgi-bin` and `htdocs`. Then update your Apache
configuration file `httpd.conf` with this new `trac.cgi` location and
`htdocs` location.

##### Web Admin plugin integrated {#WebAdminpluginintegrated}

If you had the webadmin plugin installed, you can uninstall it as it is
part of the Trac code base since 0.11.

### 7. Restart the Web Server {#RestarttheWebServer}

If you are not running
[CGI](https://docs.pagure.org/sssd-test2/TracCgi.html){.wiki}, reload
the new Trac code by restarting your web server.

Known Issues {#KnownIssues}
------------

Things you should pay attention to, while upgrading.

### Customized Templates {#CustomizedTemplates}

Trac supports customization of its Genshi templates by placing copies of
the templates in the `<env>/templates` folder of your
[environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
or in a common location specified in the [\[inherit\]
templates\_dir](https://docs.pagure.org/sssd-test2/TracIni.html#GlobalConfiguration){.wiki}
configuration setting. If you choose to do so, be wary that you will
need to repeat your changes manually on a copy of the new templates when
you upgrade to a new release of Trac (even a minor one), as the
templates will likely evolve. So keep a diff around ;-)

The preferred way to perform
[TracInterfaceCustomization](https://docs.pagure.org/sssd-test2/TracInterfaceCustomization.html){.wiki}
is to write a custom plugin doing an appropriate `ITemplateStreamFilter`
transformation, as this is more robust in case of changes: we usually
won't modify element `id`s or change CSS `class`es, and if we have to do
so, this will be documented in the
[TracDev/ApiChanges?](https://docs.pagure.org/sssd-test2/TracDev/ApiChanges.html){.missing
.wiki} pages.

### ZipImportError {#ZipImportError}

Due to internal caching of zipped packages, whenever the content of the
packages change on disk, the in-memory zip index will no longer match
and you'll get irrecoverable ZipImportError errors. Better anticipate
and bring your server down for maintenance before upgrading. See
[[​]{.icon}\#7014](http://trac.edgewall.org/intertrac/%237014 "#7014 in Trac project trac"){.ext-link}
for details.

### Wiki Upgrade {#WikiUpgrade}

`trac-admin` will not delete or remove default wiki pages that were
present in a previous version but are no longer in the new version.

### Trac database upgrade {#Tracdatabaseupgrade}

A known issue in some versions of
[PySqlite?](https://docs.pagure.org/sssd-test2/PySqlite.html){.missing
.wiki} (2.5.2-2.5.4) prevents the trac-admin upgrade script from
successfully upgrading the database format. It is advised to use either
a newer or older version of the sqlite python bindings to avoid this
error. For more details see ticket
[[​]{.icon}\#9434](http://trac.edgewall.org/intertrac/%239434 "#9434 in Trac project trac"){.ext-link}.

### parent dir {#parentdir}

If you use a trac parent env configuration and one of the plugins in one
child does not work, none of the children work.

Related topics {#Relatedtopics}
--------------

### Upgrading Python {#UpgradingPython}

Upgrading Python to a newer version will require reinstallation of
Python packages: Trac of course; also
[[​]{.icon}easy\_install](http://pypi.python.org/pypi/setuptools){.ext-link},
if you've been using that. Assuming you're using Subversion, you'll also
need to upgrade the Python bindings for svn.

#### Windows and Python 2.6 {#WindowsandPython2.6}

If you've been using CollabNet's Subversion package, you may need to
uninstall that in favor of
[[​]{.icon}Alagazam](http://alagazam.net/){.ext-link}, which has the
Python bindings readily available (see
[TracSubversion?](https://docs.pagure.org/sssd-test2/TracSubversion.html){.missing
.wiki}). The good news is, that works with no tweaking.

### Changing Database Backend {#ChangingDatabaseBackend}

#### SQLite to PostgreSQL {#SQLitetoPostgreSQL}

The
[[​]{.icon}sqlite2pg](http://trac-hacks.org/wiki/SqliteToPgScript){.ext-link}
script on [[​]{.icon}trac-hacks.org](http://trac-hacks.org){.ext-link}
has been written to assist in migrating a SQLite database to a
PostgreSQL database

### Upgrading from older versions of Trac {#OlderVersions}

For upgrades from versions older than Trac 0.10, refer first to
[[​]{.icon}wiki:0.10/TracUpgrade\#SpecificVersions](http://trac.edgewall.org/intertrac/wiki%3A0.10/TracUpgrade%23SpecificVersions "wiki:0.10/TracUpgrade#SpecificVersions in Trac project trac"){.ext-link}.

------------------------------------------------------------------------

See also:
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[TracInstall](https://docs.pagure.org/sssd-test2/TracInstall.html){.wiki}