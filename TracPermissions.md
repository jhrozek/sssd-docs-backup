Trac Permissions {#TracPermissions}
================

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

Trac uses a simple, case sensitive, permission system to control what
users can and can't access.

Permission privileges are managed using the
[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki}
tool or (new in version 0.11) the *General / Permissions* panel in the
*Admin* tab of the web interface.

In addition to the default permission policy described in this page, it
is possible to activate additional permission policies by enabling
plugins and listing them in the `[trac] permission_policies`
configuration entry in the
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki}. See
[TracFineGrainedPermissions](https://docs.pagure.org/sssd-test2/TracFineGrainedPermissions.html){.wiki}
for more details.

Non-authenticated users accessing the system are assigned the name
"anonymous". Assign permissions to the "anonymous" user to set
privileges for anonymous/guest users. The parts of Trac that a user does
not have the privileges for will not be displayed in the navigation. In
addition to these privileges, users can be granted additional individual
rights in effect when authenticated and logged into the system. All
logged in users belong to the virtual group "authenticated", which
inherits permissions from "anonymous".

Graphical Admin Tab {#GraphicalAdminTab}
-------------------

*This feature is new in version 0.11.*

To access this tab, a user must have one of the following permissions:
`TRAC_ADMIN`, `PERMISSION_ADMIN`, `PERMISSION_ADD`, `PERMISSION_REMOVE`.
The permissions can granted using the `trac-admin` command (more on
`trac-admin` below):

``` {.wiki}
  $ trac-admin /path/to/projenv permission add bob TRAC_ADMIN
```

Then, the user `bob` will be able to see the Admin tab, and can then
access the permissions menu. This menu will allow you to perform all the
following actions, but from the browser without requiring root access to
the server (just the correct permissions for your user account). **Use
at least one lowercase character in user names, as all-uppercase names
are reserved for permissions.**

1.  [![admin.png](https://fedorahosted.org/sssd/chrome/site/../common/guide/admin.png "admin.png")](https://fedorahosted.org/sssd/chrome/site/../common/guide/admin.png)
2.  [![admin-permissions.png](https://fedorahosted.org/sssd/chrome/site/../common/guide/admin-permissions.png "admin-permissions.png")](https://fedorahosted.org/sssd/chrome/site/../common/guide/admin-permissions.png)
3.  [![admin-permissions-TICKET\_ADMIN.png](https://fedorahosted.org/sssd/chrome/site/../common/guide/admin-permissions-TICKET_ADMIN.png "admin-permissions-TICKET_ADMIN.png")](https://fedorahosted.org/sssd/chrome/site/../common/guide/admin-permissions-TICKET_ADMIN.png)

An easy way to quickly secure a new Trac install is to run the above
command on the anonymous user, install the
[[​]{.icon}AccountManagerPlugin](http://trac-hacks.org/wiki/AccountManagerPlugin){.ext-link},
create a new admin account graphically and then remove the TRAC\_ADMIN
permission from the anonymous user.

Available Privileges {#AvailablePrivileges}
--------------------

To enable all privileges for a user, use the `TRAC_ADMIN` permission.
Having `TRAC_ADMIN` is like being `root` on a \*NIX system: it will
allow you to perform any operation.

Otherwise, individual privileges can be assigned to users for the
various different functional areas of Trac (**note that the privilege
names are case-sensitive**):

### Repository Browser {#RepositoryBrowser}

  ------------------ -------------------------------------------------------------------------------------------------------------------------------------
  `BROWSER_VIEW`     View directory listings in the [repository browser](https://docs.pagure.org/sssd-test2/TracBrowser.html){.wiki}
  `LOG_VIEW`         View revision logs of files and directories in the [repository browser](https://docs.pagure.org/sssd-test2/TracBrowser.html){.wiki}
  `FILE_VIEW`        View files in the [repository browser](https://docs.pagure.org/sssd-test2/TracBrowser.html){.wiki}
  `CHANGESET_VIEW`   View [repository check-ins](https://docs.pagure.org/sssd-test2/TracChangeset.html){.wiki}
  ------------------ -------------------------------------------------------------------------------------------------------------------------------------

### Ticket System {#TicketSystem}

  --------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `TICKET_VIEW`               View existing [tickets](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki} and perform [ticket queries](https://docs.pagure.org/sssd-test2/TracQuery.html){.wiki}
  `TICKET_CREATE`             Create new [tickets](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki}
  `TICKET_APPEND`             Add comments or attachments to [tickets](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki}
  `TICKET_CHGPROP`            Modify [ticket](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki} properties (priority, assignment, keywords, etc.) with the following exceptions: edit description field, add/remove other users from cc field when logged in, and set email to pref
  `TICKET_MODIFY`             Includes both `TICKET_APPEND` and `TICKET_CHGPROP`, and in addition allows resolving [tickets](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki}. Tickets can be assigned to users through a [drop-down list](https://docs.pagure.org/sssd-test2/TracTickets.html#Assign-toasDrop-DownList){.wiki} when the list of possible owners has been restricted.
  `TICKET_EDIT_CC`            Full modify cc field
  `TICKET_EDIT_DESCRIPTION`   Modify description field
  `TICKET_EDIT_COMMENT`       Modify comments
  `TICKET_ADMIN`              All `TICKET_*` permissions, plus the deletion of ticket attachments and modification of the reporter and description fields. It also allows managing ticket properties in the [WebAdmin?](https://docs.pagure.org/sssd-test2/WebAdmin.html){.missing .wiki} panel.
  --------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Attention: the "view tickets" button appears with the `REPORT_VIEW`
permission.

### Roadmap {#Roadmap}

  -------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `MILESTONE_VIEW`     View milestones and assign tickets to milestones.
  `MILESTONE_CREATE`   Create a new milestone
  `MILESTONE_MODIFY`   Modify existing milestones
  `MILESTONE_DELETE`   Delete milestones
  `MILESTONE_ADMIN`    All `MILESTONE_*` permissions
  `ROADMAP_VIEW`       View the [roadmap](https://docs.pagure.org/sssd-test2/TracRoadmap.html){.wiki} page, is not (yet) the same as MILESTONE\_VIEW, see [[​]{.icon}\#4292](http://trac.edgewall.org/intertrac/%234292 "#4292 in Trac project trac"){.ext-link}
  `ROADMAP_ADMIN`      to be removed with [[​]{.icon}\#3022](http://trac.edgewall.org/intertrac/%233022 "#3022 in Trac project trac"){.ext-link}, replaced by MILESTONE\_ADMIN
  -------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Reports {#Reports}

  ------------------- -----------------------------------------------------------------------------------------------------------
  `REPORT_VIEW`       View [reports](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki}, i.e. the "view tickets" link.
  `REPORT_SQL_VIEW`   View the underlying SQL query of a [report](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki}
  `REPORT_CREATE`     Create new [reports](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki}
  `REPORT_MODIFY`     Modify existing [reports](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki}
  `REPORT_DELETE`     Delete [reports](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki}
  `REPORT_ADMIN`      All `REPORT_*` permissions
  ------------------- -----------------------------------------------------------------------------------------------------------

### Wiki System {#WikiSystem}

  --------------- ----------------------------------------------------------------------------------------------
  `WIKI_VIEW`     View existing [wiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki} pages
  `WIKI_CREATE`   Create new [wiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki} pages
  `WIKI_MODIFY`   Change [wiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki} pages
  `WIKI_RENAME`   Rename [wiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki} pages
  `WIKI_DELETE`   Delete [wiki](https://docs.pagure.org/sssd-test2/TracWiki.html){.wiki} pages and attachments
  `WIKI_ADMIN`    All `WIKI_*` permissions, plus the management of *readonly* pages.
  --------------- ----------------------------------------------------------------------------------------------

### Permissions {#Permissions}

  --------------------- --------------------------------
  `PERMISSION_GRANT`    add/grant a permission
  `PERMISSION_REVOKE`   remove/revoke a permission
  `PERMISSION_ADMIN`    All `PERMISSION_*` permissions
  --------------------- --------------------------------

### Others {#Others}

  ----------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  `TIMELINE_VIEW`   View the [timeline](https://docs.pagure.org/sssd-test2/TracTimeline.html){.wiki} page
  `SEARCH_VIEW`     View and execute [search](https://docs.pagure.org/sssd-test2/TracSearch.html){.wiki} queries
  `CONFIG_VIEW`     Enables additional pages on *About Trac* that show the current configuration or the list of installed plugins
  `EMAIL_VIEW`      Shows email addresses even if [trac show\_email\_addresses](https://docs.pagure.org/sssd-test2/TracIni.html#trac-section){.wiki} configuration option is false
  ----------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------

Creating New Privileges {#CreatingNewPrivileges}
-----------------------

To create custom permissions, for example to be used in a custom
workflow, enable the optional
[[​]{.icon}tracopt.perm.config\_perm\_provider.ExtraPermissionsProvider](http://trac.edgewall.org/intertrac/ExtraPermissionsProvider "ExtraPermissionsProvider in Trac project trac"){.ext-link}
component in the "Plugins" admin panel, and add the desired permissions
to the `[extra-permissions]` section in your
[trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#extra-permissions-section){.wiki}.
For more information, please refer to the documentation of the component
in the admin panel.

Granting Privileges {#GrantingPrivileges}
-------------------

You grant privileges to users using
[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki}.
The current set of privileges can be listed with the following command:

``` {.wiki}
  $ trac-admin /path/to/projenv permission list
```

This command will allow the user *bob* to delete reports:

``` {.wiki}
  $ trac-admin /path/to/projenv permission add bob REPORT_DELETE
```

The `permission add` command also accepts multiple privilege names:

``` {.wiki}
  $ trac-admin /path/to/projenv permission add bob REPORT_DELETE WIKI_CREATE
```

Or add all privileges:

``` {.wiki}
  $ trac-admin /path/to/projenv permission add bob TRAC_ADMIN
```

Permission Groups {#PermissionGroups}
-----------------

There are two built-in groups, "authenticated" and "anonymous". Any user
who has not logged in is automatically in the "anonymous" group. Any
user who has logged in is also in the "authenticated" group. The
"authenticated" group inherits permissions from the "anonymous" group.
For example, if the "anonymous" group has permission WIKI\_MODIFY, it is
not necessary to add the WIKI\_MODIFY permission to the "authenticated"
group as well.

Custom groups may be defined that inherit permissions from the two
built-in groups.

Permissions can be grouped together to form roles such as *developer*,
*admin*, etc.

``` {.wiki}
  $ trac-admin /path/to/projenv permission add developer WIKI_ADMIN
  $ trac-admin /path/to/projenv permission add developer REPORT_ADMIN
  $ trac-admin /path/to/projenv permission add developer TICKET_MODIFY
  $ trac-admin /path/to/projenv permission add bob developer
  $ trac-admin /path/to/projenv permission add john developer
```

Group membership can be checked by doing a `permission list` with no
further arguments; the resulting output will include group memberships.
**Use at least one lowercase character in group names, as all-uppercase
names are reserved for permissions**.

Adding a New Group and Permissions {#AddingaNewGroupandPermissions}
----------------------------------

Permission groups can be created by assigning a user to a group you wish
to create, then assign permissions to that group.

The following will add *bob* to the new group called *beta\_testers* and
then will assign WIKI\_ADMIN permissions to that group. (Thus, *bob*
will inherit the WIKI\_ADMIN permission)

``` {.wiki}
   $ trac-admin /path/to/projenv permission add bob beta_testers
   $ trac-admin /path/to/projenv permission add beta_testers WIKI_ADMIN
```

Removing Permissions {#RemovingPermissions}
--------------------

Permissions can be removed using the 'remove' command. For example:

This command will prevent the user *bob* from deleting reports:

``` {.wiki}
  $ trac-admin /path/to/projenv permission remove bob REPORT_DELETE
```

Just like `permission add`, this command accepts multiple privilege
names.

You can also remove all privileges for a specific user:

``` {.wiki}
  $ trac-admin /path/to/projenv permission remove bob '*'
```

Or one privilege for all users:

``` {.wiki}
  $ trac-admin /path/to/projenv permission remove '*' REPORT_ADMIN
```

Default Permissions {#DefaultPermissions}
-------------------

By default on a new Trac installation, the `anonymous` user will have
*view* access to everything in Trac, but will not be able to create or
modify anything. On the other hand, the `authenticated` users will have
the permissions to *create and modify tickets and wiki pages*.

**anonymous**

``` {.wiki}
 BROWSER_VIEW 
 CHANGESET_VIEW 
 FILE_VIEW 
 LOG_VIEW 
 MILESTONE_VIEW 
 REPORT_SQL_VIEW 
 REPORT_VIEW 
 ROADMAP_VIEW 
 SEARCH_VIEW 
 TICKET_VIEW 
 TIMELINE_VIEW
 WIKI_VIEW
```

**authenticated**

``` {.wiki}
 TICKET_CREATE 
 TICKET_MODIFY 
 WIKI_CREATE 
 WIKI_MODIFY  
```

------------------------------------------------------------------------

See also:
[TracAdmin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki},
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki}
and
[TracFineGrainedPermissions](https://docs.pagure.org/sssd-test2/TracFineGrainedPermissions.html){.wiki}
