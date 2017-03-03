Trac Backup
===========

.. raw:: html

   <div class="system-message">

**Error: Macro TracGuideToc(None) failed**
::

    'NoneType' object has no attribute 'find'

.. raw:: html

   </div>

Since Trac uses a database backend, some extra care is required to
safely create a backup of a `project
environment <https://docs.pagure.org/sssd-test2/TracEnvironment.html>`__.
Luckily,
`trac-admin <https://docs.pagure.org/sssd-test2/TracAdmin.html>`__ has a
command to make backups easier: ``hotcopy``.

    *Note: Trac uses the ``hotcopy`` nomenclature to match that of
    `​Subversion <http://subversion.tigris.org/>`__, to make it easier
    to remember when managing both Trac and Subversion servers.*

Creating a Backup
-----------------

To create a backup of a live
`TracEnvironment <https://docs.pagure.org/sssd-test2/TracEnvironment.html>`__,
simply run:

.. code:: wiki

      $ trac-admin /path/to/projenv hotcopy /path/to/backupdir

`trac-admin <https://docs.pagure.org/sssd-test2/TracAdmin.html>`__ will
lock the database while copying. **

The resulting backup directory is safe to handle using standard
file-based backup tools like ``tar`` or ``dump``/``restore``.

Please, note, that hotcopy command does not overwrite target directory
and when such exists, hotcopy ends with error:
``Command failed: [Errno 17] File exists:`` This is discussed in
`​#3198 <http://trac.edgewall.org/intertrac/ticket%3A3198>`__.

Restoring a Backup
~~~~~~~~~~~~~~~~~~

Backups are simply a copied snapshot of the entire `project
environment <https://docs.pagure.org/sssd-test2/TracEnvironment.html>`__
directory, including the SQLite database.

To restore an environment from a backup, stop the process running Trac
(i.e. the Web server or
`tracd <https://docs.pagure.org/sssd-test2/TracStandalone.html>`__),
restore the contents of your backup (path/to/backupdir) to your `project
environment <https://docs.pagure.org/sssd-test2/TracEnvironment.html>`__
directory and restart the service.

    *Note: Automatic backup of environments that don't use SQLite as
    database backend is not supported at this time. As a workaround, we
    recommend that you stop the server, copy the environment directory,
    and make a backup of the database using whatever mechanism is
    provided by the database system.*

--------------

See also:
`TracAdmin <https://docs.pagure.org/sssd-test2/TracAdmin.html>`__,
`TracEnvironment <https://docs.pagure.org/sssd-test2/TracEnvironment.html>`__,
`TracGuide <https://docs.pagure.org/sssd-test2/TracGuide.html>`__,
`​TracMigrate <http://trac.edgewall.org/intertrac/TracMigrate>`__
