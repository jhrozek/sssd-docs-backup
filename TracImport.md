Importing ticket data {#Importingticketdata}
=====================

<div class="wiki-toc">

1.  [Importing ticket data](#Importingticketdata)
    1.  [TicketImportPlugin](#TicketImportPlugin)
    2.  [ExportImportXlsPlugin](#ExportImportXlsPlugin)
    3.  [Bugzilla](#Bugzilla)
    4.  [Jira](#Jira)
    5.  [Mantis](#Mantis)
    6.  [PlanetForge](#PlanetForge)
    7.  [Scarab](#Scarab)
    8.  [Sourceforge](#Sourceforge)
    9.  [Other](#Other)
        1.  [Comma delimited file - CSV](#Commadelimitedfile-CSV)

</div>

By means of migrating from other issue-tracking systems, perform some
external actions over tickets or simply synchronize different data
bases, there are some available tools, plug-ins or scripts which lets
you import or up-date tickets into Trac.

Below, follows a collection of some of those.

TicketImportPlugin {#TicketImportPlugin}
------------------

[[​]{.icon}TicketImportPlugin](http://trac-hacks.org/wiki/TicketImportPlugin){.ext-link}
:   mainly, but not only, this plug-in lets you import or up-date into
    Trac a series of tickets from a **CSV file** or (if the
    [[​]{.icon}xlrd
    library](http://pypi.python.org/pypi/xlrd){.ext-link} is installed)
    from an **Excel file**.

ExportImportXlsPlugin {#ExportImportXlsPlugin}
---------------------

[[​]{.icon}ExportImportXlsPlugin](http://trac-hacks.org/wiki/ExportImportXlsPlugin){.ext-link}
:   this plug-in add an admin panel for export and import tickets via
    **XLS file**.
    -   It depends on the python packages xlwt/rxld.

Bugzilla {#Bugzilla}
--------

[[​]{.icon}BugzillaIssueTrackingPlugin](http://trac-hacks.org/wiki/BugzillaIssueTrackingPlugin){.ext-link}
:   integrates Bugzilla into Trac keeping
    [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}

Ticket data can be imported from Bugzilla using the
[[​]{.icon}bugzilla2trac.py](http://trac.edgewall.org/browser/trunk/contrib/bugzilla2trac.py){.ext-link}
script, available in the contrib/ directory of the Trac distribution.

``` {.wiki}
$ bugzilla2trac.py
bugzilla2trac - Imports a bug database from Bugzilla into Trac.

Usage: bugzilla2trac.py [options]

Available Options:
  --db <MySQL dbname>              - Bugzilla's database
  --tracenv /path/to/trac/env      - full path to Trac db environment
  -h | --host <MySQL hostname>     - Bugzilla's DNS host name
  -u | --user <MySQL username>     - effective Bugzilla's database user
  -p | --passwd <MySQL password>   - Bugzilla's user password
  -c | --clean                     - remove current Trac tickets before importing
  --help | help                    - this help info

Additional configuration options can be defined directly in the script.
```

Currently, the following data is imported from Bugzilla:

-   bugs
-   bug activity (field changes)
-   bug attachments
-   user names and passwords (put into a htpasswd file)

The script provides a number of features to ease the conversion, such
as:

-   PRODUCT\_KEYWORDS: Trac doesn't have the concept of products, so the
    script provides the ability to attach a ticket keyword instead.

<!-- -->

-   IGNORE\_COMMENTS: Don't import Bugzilla comments that match a
    certain regexp.

<!-- -->

-   STATUS\_KEYWORDS: Attach ticket keywords for the Bugzilla statuses
    not available in Trac. By default, the 'VERIFIED' and 'RELEASED'
    Bugzilla statuses are translated into Trac keywords.

For more details on the available options, see the configuration section
at the top of the script.

Jira {#Jira}
----

[[​]{.icon}JiraToTracIntegration](http://trac-hacks.org/wiki/JiraToTracIntegration){.ext-link}
:   provides tools to import Atlassian Jira backup files into Trac. The
    plug-in consists of a Python 3.1 commandline tool that:
    -   Parses the Jira backup XML file
    -   Sends the imported Jira data and attachments to Trac using the
        [[​]{.icon}XmlRpcPlugin](http://trac-hacks.org/wiki/XmlRpcPlugin){.ext-link}
    -   Generates a htpasswd file containing the imported Jira users and
        their SHA-512 base64 encoded passwords

Mantis {#Mantis}
------

[[​]{.icon}MantisImportScript](http://trac-hacks.org/wiki/MantisImportScript){.ext-link}
:   script to import from Mantis into Trac the following data:
    -   bugs
    -   bug comments
    -   bug activity (field changes)
    -   attachments (as long as the files live in the mantis db, not on
        the filesystem) .

PlanetForge {#PlanetForge}
-----------

[[​]{.icon}PlanetForgeImportExportPlugin](http://trac-hacks.org/wiki/PlanetForgeImportExportPlugin){.ext-link}
:   this plugin exports Trac data (wiki, tickets, compoments,
    permissions, repositories, etc.) using the open format designed by
    the COCLICO project. It extends the webadmin panel and the 'trac
    admin ...' command. Still has no 'import' feature.

Scarab {#Scarab}
------

[[​]{.icon}ScarabToTracScript](http://trac-hacks.org/wiki/ScarabToTracScript){.ext-link}
:   script that migrates Scarab issues to Trac tickets
    -   Requires
        [[​]{.icon}XmlRpcPlugin](http://trac-hacks.org/wiki/XmlRpcPlugin){.ext-link}

Sourceforge {#Sourceforge}
-----------

[[​]{.icon}SfnToTracScript](http://trac-hacks.org/wiki/SfnToTracScript){.ext-link}
:   importer of SourceForge's new backup file (originated from
    \#Trac3521)

Also, ticket data can be imported from Sourceforge using the
[[​]{.icon}sourceforge2trac.py](http://trac.edgewall.org/browser/trunk/contrib/sourceforge2trac.py){.ext-link}
script, available in the contrib/ directory of the Trac distribution.

Other {#Other}
-----

Since trac uses a SQL database to store the data, you can import from
other systems by examining the database tables. Just go into
[[​]{.icon}sqlite](http://www.sqlite.org/sqlite.html){.ext-link} command
line to look at the tables and import into them from your application.

### Comma delimited file - CSV {#Commadelimitedfile-CSV}

See
[[​]{.icon}csv2trac.2.py](http://trac.edgewall.org/attachment/wiki/TracSynchronize/csv2trac.2.py){.ext-link}
for details. This approach is particularly useful if one needs to enter
a large number of tickets by hand. (note that the ticket type type
field, (task etc...) is also needed for this script to work with more
recent Trac releases) Comments on script: The script has an error on
line 168, ('Ticket' needs to be 'ticket'). Also, the listed values for
severity and priority are swapped.

------------------------------------------------------------------------

See also:

-   to import/export wiki pages:
    [TracAdmin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki},
-   to export tickets:
    [TracTickets](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki},
    [TracQuery](https://docs.pagure.org/sssd-test2/TracQuery.html){.wiki}

