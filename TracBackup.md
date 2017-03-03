Trac Backup {#TracBackup}
===========

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

Since Trac uses a database backend, some extra care is required to
safely create a backup of a [project
environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}.
Luckily,
[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki}
has a command to make backups easier: `hotcopy`.

> *Note: Trac uses the `hotcopy` nomenclature to match that of
> [[​]{.icon}Subversion](http://subversion.tigris.org/){.ext-link}, to
> make it easier to remember when managing both Trac and Subversion
> servers.*

Creating a Backup {#CreatingaBackup}
-----------------

To create a backup of a live
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki},
simply run:

``` {.wiki}
  $ trac-admin /path/to/projenv hotcopy /path/to/backupdir
```

[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki}
will lock the database while copying. **

The resulting backup directory is safe to handle using standard
file-based backup tools like `tar` or `dump`/`restore`.

Please, note, that hotcopy command does not overwrite target directory
and when such exists, hotcopy ends with error:
`Command failed: [Errno 17] File exists:` This is discussed in
[[​]{.icon}\#3198](http://trac.edgewall.org/intertrac/ticket%3A3198 "ticket:3198 in Trac project trac"){.ext-link}.

### Restoring a Backup {#RestoringaBackup}

Backups are simply a copied snapshot of the entire [project
environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
directory, including the SQLite database.

To restore an environment from a backup, stop the process running Trac
(i.e. the Web server or
[tracd](https://docs.pagure.org/sssd-test2/TracStandalone.html){.wiki}),
restore the contents of your backup (path/to/backupdir) to your [project
environment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
directory and restart the service.

> *Note: Automatic backup of environments that don't use SQLite as
> database backend is not supported at this time. As a workaround, we
> recommend that you stop the server, copy the environment directory,
> and make a backup of the database using whatever mechanism is provided
> by the database system.*

------------------------------------------------------------------------

See also:
[TracAdmin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki},
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki},
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[[​]{.icon}TracMigrate](http://trac.edgewall.org/intertrac/TracMigrate "TracMigrate in Trac project trac"){.ext-link}
