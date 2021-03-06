Importing ticket data
=====================

.. raw:: html

   <div class="wiki-toc">

#. `Importing ticket data <#Importingticketdata>`__

   #. `TicketImportPlugin <#TicketImportPlugin>`__
   #. `ExportImportXlsPlugin <#ExportImportXlsPlugin>`__
   #. `Bugzilla <#Bugzilla>`__
   #. `Jira <#Jira>`__
   #. `Mantis <#Mantis>`__
   #. `PlanetForge <#PlanetForge>`__
   #. `Scarab <#Scarab>`__
   #. `Sourceforge <#Sourceforge>`__
   #. `Other <#Other>`__

      #. `Comma delimited file - CSV <#Commadelimitedfile-CSV>`__

.. raw:: html

   </div>

By means of migrating from other issue-tracking systems, perform some
external actions over tickets or simply synchronize different data
bases, there are some available tools, plug-ins or scripts which lets
you import or up-date tickets into Trac.

Below, follows a collection of some of those.

TicketImportPlugin
------------------

`​TicketImportPlugin <http://trac-hacks.org/wiki/TicketImportPlugin>`__
    mainly, but not only, this plug-in lets you import or up-date into
    Trac a series of tickets from a **CSV file** or (if the `​xlrd
    library <http://pypi.python.org/pypi/xlrd>`__ is installed) from an
    **Excel file**.

ExportImportXlsPlugin
---------------------

`​ExportImportXlsPlugin <http://trac-hacks.org/wiki/ExportImportXlsPlugin>`__
    this plug-in add an admin panel for export and import tickets via
    **XLS file**.

    -  It depends on the python packages xlwt/rxld.

Bugzilla
--------

`​BugzillaIssueTrackingPlugin <http://trac-hacks.org/wiki/BugzillaIssueTrackingPlugin>`__
    integrates Bugzilla into Trac keeping
    `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__

Ticket data can be imported from Bugzilla using the
`​bugzilla2trac.py <http://trac.edgewall.org/browser/trunk/contrib/bugzilla2trac.py>`__
script, available in the contrib/ directory of the Trac distribution.

.. code:: wiki

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

Currently, the following data is imported from Bugzilla:

-  bugs
-  bug activity (field changes)
-  bug attachments
-  user names and passwords (put into a htpasswd file)

The script provides a number of features to ease the conversion, such
as:

-  PRODUCT\_KEYWORDS: Trac doesn't have the concept of products, so the
   script provides the ability to attach a ticket keyword instead.

-  IGNORE\_COMMENTS: Don't import Bugzilla comments that match a certain
   regexp.

-  STATUS\_KEYWORDS: Attach ticket keywords for the Bugzilla statuses
   not available in Trac. By default, the 'VERIFIED' and 'RELEASED'
   Bugzilla statuses are translated into Trac keywords.

For more details on the available options, see the configuration section
at the top of the script.

Jira
----

`​JiraToTracIntegration <http://trac-hacks.org/wiki/JiraToTracIntegration>`__
    provides tools to import Atlassian Jira backup files into Trac. The
    plug-in consists of a Python 3.1 commandline tool that:

    -  Parses the Jira backup XML file
    -  Sends the imported Jira data and attachments to Trac using the
       `​XmlRpcPlugin <http://trac-hacks.org/wiki/XmlRpcPlugin>`__
    -  Generates a htpasswd file containing the imported Jira users and
       their SHA-512 base64 encoded passwords

Mantis
------

`​MantisImportScript <http://trac-hacks.org/wiki/MantisImportScript>`__
    script to import from Mantis into Trac the following data:

    -  bugs
    -  bug comments
    -  bug activity (field changes)
    -  attachments (as long as the files live in the mantis db, not on
       the filesystem) .

PlanetForge
-----------

`​PlanetForgeImportExportPlugin <http://trac-hacks.org/wiki/PlanetForgeImportExportPlugin>`__
    this plugin exports Trac data (wiki, tickets, compoments,
    permissions, repositories, etc.) using the open format designed by
    the COCLICO project. It extends the webadmin panel and the 'trac
    admin ...' command. Still has no 'import' feature.

Scarab
------

`​ScarabToTracScript <http://trac-hacks.org/wiki/ScarabToTracScript>`__
    script that migrates Scarab issues to Trac tickets

    -  Requires
       `​XmlRpcPlugin <http://trac-hacks.org/wiki/XmlRpcPlugin>`__

Sourceforge
-----------

`​SfnToTracScript <http://trac-hacks.org/wiki/SfnToTracScript>`__
    importer of SourceForge's new backup file (originated from
    #Trac3521)

Also, ticket data can be imported from Sourceforge using the
`​sourceforge2trac.py <http://trac.edgewall.org/browser/trunk/contrib/sourceforge2trac.py>`__
script, available in the contrib/ directory of the Trac distribution.

Other
-----

Since trac uses a SQL database to store the data, you can import from
other systems by examining the database tables. Just go into
`​sqlite <http://www.sqlite.org/sqlite.html>`__ command line to look at
the tables and import into them from your application.

Comma delimited file - CSV
~~~~~~~~~~~~~~~~~~~~~~~~~~

See
`​csv2trac.2.py <http://trac.edgewall.org/attachment/wiki/TracSynchronize/csv2trac.2.py>`__
for details. This approach is particularly useful if one needs to enter
a large number of tickets by hand. (note that the ticket type type
field, (task etc...) is also needed for this script to work with more
recent Trac releases) Comments on script: The script has an error on
line 168, ('Ticket' needs to be 'ticket'). Also, the listed values for
severity and priority are swapped.

--------------

See also:

-  to import/export wiki pages:
   `TracAdmin <https://docs.pagure.org/sssd-test2/TracAdmin.html>`__,
-  to export tickets:
   `TracTickets <https://docs.pagure.org/sssd-test2/TracTickets.html>`__,
   `TracQuery <https://docs.pagure.org/sssd-test2/TracQuery.html>`__
