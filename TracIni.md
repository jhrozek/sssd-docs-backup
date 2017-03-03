The Trac Configuration File {#TheTracConfigurationFile}
===========================

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

<div class="wiki-toc">

1.  [The Trac Configuration File](#TheTracConfigurationFile)
    1.  [Global Configuration](#GlobalConfiguration)
    2.  [Reference for settings](#Referenceforsettings)
    3.  [Reference for special sections](#Referenceforspecialsections)
        1.  [\[components\]](#components-section)
        2.  [\[extra-permissions\]](#extra-permissions-section)
        3.  [\[milestone-groups\]](#milestone-groups-section)
        4.  [\[repositories\]](#repositories-section)
        5.  [\[svn:externals\]](#svn:externals-section)
        6.  [\[ticket-custom\]](#ticket-custom-section)
        7.  [\[ticket-workflow\]](#ticket-workflow-section)

</div>

Trac configuration is done by editing the **`trac.ini`** config file,
located in `<projectenv>/conf/trac.ini`. Changes to the configuration
are usually reflected immediately, though changes to the `[components]`
or `[logging]` sections will require restarting the web server. You may
also need to restart the web server after creating a global
configuration file when none was previously present.

The `trac.ini` configuration file and its parent directory should be
writable by the web server, as Trac currently relies on the possibility
to trigger a complete environment reload to flush its caches.

Global Configuration {#GlobalConfiguration}
--------------------

In versions prior to 0.11, the global configuration was by default
located in `$prefix/share/trac/conf/trac.ini` or /etc/trac/trac.ini,
depending on the distribution. If you're upgrading, you may want to
specify that file to inherit from. Literally, when you're upgrading to
0.11, you have to add an `[inherit]` section to your project's
`trac.ini` file. Additionally, you have to move your customized
templates and common images from `$prefix/share/trac/...` to the new
location.

Global options will be merged with the environment-specific options,
where local options override global options. The options file is
specified as follows:

``` {.wiki}
[inherit]
file = /path/to/global/trac.ini
```

Multiple files can be specified using a comma-separated list.

Note that you can also specify a global option file when creating a new
project, by adding the option `--inherit=/path/to/global/trac.ini` to
[trac-admin](https://docs.pagure.org/sssd-test2/TracAdmin.html#initenv){.wiki}'s
`initenv` command. If you do not do this but nevertheless intend to use
a global option file with your new environment, you will have to go
through the newly generated `conf/trac.ini` file and delete the entries
that will otherwise override those set in the global file.

There are two more entries in the
[\[inherit\]](https://fedorahosted.org/sssd#inherit-section) section,
`templates_dir` for sharing global templates and `plugins_dir`, for
sharing plugins. Those entries can themselves be specified in the shared
configuration file, and in fact, configuration files can even be chained
if you specify another `[inherit] file` there.

Note that the templates found in the `templates/` directory of the
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
have precedence over those found in `[inherit] templates_dir`. In turn,
the latter have precedence over the installed templates, so be careful
about what you put there, notably if you override a default template be
sure to refresh your modifications when you upgrade to a new version of
Trac (the preferred way to perform
[TracInterfaceCustomization](https://docs.pagure.org/sssd-test2/TracInterfaceCustomization.html){.wiki}
being still to write a custom plugin doing an appropriate
`ITemplateStreamFilter` transformation).

Reference for settings {#Referenceforsettings}
----------------------

This is a brief reference of available configuration options, and their
default settings.

<div class="tracini">

### `[attachment]` {#attachment-section}

  ------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `max_size`                Maximum allowed file size (in bytes) for ticket and wiki attachments.
  `render_unsafe_content`   Whether attachments should be rendered in the browser, or only made downloadable. Pretty much any file may be interpreted as HTML by the browser, which allows a malicious user to attach a file containing cross-site scripting attacks. For public sites where anonymous users can create attachments it is recommended to leave this option disabled (which is the default).
  ------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[batchmod]` {#batchmod-section}

  ------------------------- ----------------------------------------------------------
  `fields_as_list`          field names modified as a value list(separated by ',')
  `list_connector_string`   Connector string for 'list' fields. Defaults to a space.
  `list_separator_regex`    separator regex used for 'list' fields
  ------------------------- ----------------------------------------------------------

### `[browser]` {#browser-section}

  ------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `color_scale`             Enable colorization of the *age* column. This uses the same color scale as the source code annotation: blue is older, red is newer. (*since 0.11*)
  `downloadable_paths`      List of repository paths that can be downloaded. Leave the option empty if you want to disable all downloads, otherwise set it to a comma-separated list of authorized paths (those paths are glob patterns, i.e. "\*" can be used as a wild card) (*since 0.10*)
  `hide_properties`         Comma-separated list of version control properties to hide from the repository browser. (*since 0.9*)
  `intermediate_color`      (r,g,b) color triple to use for the color corresponding to the intermediate color, if two linear interpolations are used for the color scale (see `intermediate_point`). If not set, the intermediate color between `oldest_color` and `newest_color` will be used. (*since 0.11*)
  `intermediate_point`      If set to a value between 0 and 1 (exclusive), this will be the point chosen to set the `intermediate_color` for interpolating the color value. (*since 0.11*)
  `newest_color`            (r,g,b) color triple to use for the color corresponding to the newest color, for the color scale used in *blame* or the browser *age* column if `color_scale` is enabled. (*since 0.11*)
  `oldest_color`            (r,g,b) color triple to use for the color corresponding to the oldest color, for the color scale used in *blame* or the browser *age* column if `color_scale` is enabled. (*since 0.11*)
  `oneliner_properties`     Comma-separated list of version control properties to render as oneliner wiki content in the repository browser. (*since 0.11*)
  `render_unsafe_content`   Whether raw files should be rendered in the browser, or only made downloadable. Pretty much any file may be interpreted as HTML by the browser, which allows a malicious user to create a file containing cross-site scripting attacks. For open repositories where anyone can check-in a file, it is recommended to leave this option disabled (which is the default).
  `wiki_properties`         Comma-separated list of version control properties to render as wiki content in the repository browser. (*since 0.11*)
  ------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[cgit]` {#cgit-section}

  ----------------- -----------------------------------------------------------------------------
  `cgit_redirect`   Redirect to cgit project page when true, embed in trac interface when false
  `cgit_url`        URL to cgit project page. Example: /cgit/projectName
  ----------------- -----------------------------------------------------------------------------

### `[changeset]` {#changeset-section}

  ------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `max_diff_bytes`         Maximum total size in bytes of the modified files (their old size plus their new size) for which the changeset view will attempt to show the diffs inlined (*since 0.10*).
  `max_diff_files`         Maximum number of modified files for which the changeset view will attempt to show the diffs inlined (*since 0.10*).
  `wiki_format_messages`   Whether wiki formatting should be applied to changeset messages. If this option is disabled, changeset messages will be rendered as pre-formatted text.
  ------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[fedmsg]` {#fedmsg-section}

  ----------------- -----------------------------------------------------------
  `banned_fields`   A comma separated list of fields not to be sent to fedmsg
  ----------------- -----------------------------------------------------------

### `[git]` {#git-section}

  ---------------------- -------------------------------------------------------------------------------------------------------------
  `cached_repository`    wrap `GitRepository` in `CachedRepository`
  `git_bin`              path to git executable (relative to trac project folder!)
  `git_fs_encoding`      define charset encoding of paths within git repository
  `persistent_cache`     enable persistent caching of commit tree
  `shortrev_len`         length rev sha sums should be tried to be abbreviated to (must be &gt;= 4 and &lt;= 40)
  `trac_user_rlookup`    enable reverse mapping of git email addresses to trac user ids
  `use_committer_id`     use git-committer id instead of git-author id as changeset owner
  `use_committer_time`   use git-committer-author timestamp instead of git-author timestamp as changeset timestamp
  `wiki_shortrev_len`    minimum length of hex-string for which auto-detection as sha id is performed (must be &gt;= 4 and &lt;= 40)
  ---------------------- -------------------------------------------------------------------------------------------------------------

### `[header_logo]` {#header_logo-section}

  ---------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `alt`      Alternative text for the header logo.
  `height`   Height of the header logo image in pixels.
  `link`     URL to link to, from the header logo.
  `src`      URL of the image to use as header logo. It can be absolute, server relative or relative. If relative, it is relative to one of the `/chrome` locations: `site/your-logo.png` if `your-logo.png` is located in the `htdocs` folder within your [TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}; `common/your-logo.png` if `your-logo.png` is located in the folder mapped to the [htdocs\_location](https://fedorahosted.org/sssd#trac-section) URL. Only specifying `your-logo.png` is equivalent to the latter.
  `width`    Width of the header logo image in pixels.
  ---------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[inherit]` {#inherit-section}

  ----------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `plugins_dir`     Path to the *shared plugins directory*. Plugins in that directory are loaded in addition to those in the directory of the environment `plugins`, with this one taking precedence. (*since 0.11*)
  `templates_dir`   Path to the *shared templates directory*. Templates in that directory are loaded in addition to those in the environments `templates` directory, but the latter take precedence. (*since 0.11*)
  ----------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[iniadmin]` {#iniadmin-section}

  ------------- --------------------------------------------------------------------------------------
  `excludes`    Excludes this options. Comma separated list as `section:name`.
  `passwords`   Show input-type as password instead of text. Comma separated list as `section:name`.
  ------------- --------------------------------------------------------------------------------------

### `[logging]` {#logging-section}

  -------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `log_file`     If `log_type` is `file`, this should be a path to the log-file. Relative paths are resolved relative to the `log` directory of the environment.
  `log_format`   Custom logging format. If nothing is set, the following will be used: Trac\[\$(module)s\] \$(levelname)s: \$(message)s In addition to regular key names supported by the Python logger library (see [[​]{.icon}http://docs.python.org/library/logging.html](http://docs.python.org/library/logging.html){.ext-link}), one could use: - \$(path)s the path for the current environment - \$(basename)s the last path component of the current environment - \$(project)s the project name Note the usage of `$(...)s` instead of `%(...)s` as the latter form would be interpreted by the [ConfigParser?](https://docs.pagure.org/sssd-test2/ConfigParser.html){.missing .wiki} itself. Example: `($(thread)d) Trac[$(basename)s:$(module)s] $(levelname)s: $(message)s` *(since 0.10.5)*
  `log_level`    Level of verbosity in log. Should be one of (`CRITICAL`, `ERROR`, `WARN`, `INFO`, `DEBUG`).
  `log_type`     Logging facility to use. Should be one of (`none`, `file`, `stderr`, `syslog`, `winlog`).
  -------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[milestone]` {#milestone-section}

  ------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------
  `stats_provider`   Name of the component implementing `ITicketGroupStatsProvider`, which is used to collect statistics on groups of tickets for display in the milestone views.
  ------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[mimeviewer]` {#mimeviewer-section}

  -------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `max_preview_size`         Maximum file size for HTML preview. (*since 0.9*)
  `mime_map`                 List of additional MIME types and keyword mappings. Mappings are comma-separated, and for each MIME type, there's a colon (":") separated list of associated keywords or file extensions. (*since 0.10*)
  `pygments_default_style`   The default style to use for Pygments syntax highlighting.
  `pygments_modes`           List of additional MIME types known by Pygments. For each, a tuple `mimetype:mode:quality` has to be specified, where `mimetype` is the MIME type, `mode` is the corresponding Pygments mode to be used for the conversion and `quality` is the quality ratio associated to this conversion. That can also be used to override the default quality ratio used by the Pygments render.
  `tab_width`                Displayed tab width in file preview. (*since 0.9*)
  `treat_as_binary`          Comma-separated list of MIME types that should be treated as binary data. (*since 0.11.5*)
  -------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[notification]` {#notification-section}

  --------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `admit_domains`             Comma-separated list of domains that should be considered as valid for email addresses (such as localdomain).
  `always_notify_owner`       Always send notifications to the ticket owner (*since 0.9*).
  `always_notify_reporter`    Always send notifications to any address in the *reporter* field.
  `always_notify_updater`     Always send notifications to the person who causes the ticket property change and to any previous updater of that ticket.
  `ambiguous_char_width`      Which width of ambiguous characters (e.g. 'single' or 'double') should be used in the table of notification mail. If 'single', the same width as characters in US-ASCII. This is expected by most users. If 'double', twice the width of US-ASCII characters. This is expected by CJK users. *(since 0.12.2)*
  `email_sender`              Name of the component implementing `IEmailSender`. This component is used by the notification system to send emails. Trac currently provides `SmtpEmailSender` for connecting to an SMTP server, and `SendmailEmailSender` for running a `sendmail`-compatible executable. (*since 0.12*)
  `ignore_domains`            Comma-separated list of domains that should not be considered part of email addresses (for usernames with Kerberos domains).
  `mime_encoding`             Specifies the MIME encoding scheme for emails. Valid options are 'base64' for Base64 encoding, 'qp' for Quoted-Printable, and 'none' for no encoding, in which case mails will be sent as 7bit if the content is all ASCII, or 8bit otherwise. (*since 0.10*)
  `sendmail_path`             Path to the sendmail executable. The sendmail program must accept the `-i` and `-f` options. (*since 0.12*)
  `smtp_always_bcc`           Email address(es) to always send notifications to, addresses do not appear publicly (Bcc:). (*since 0.10*).
  `smtp_always_cc`            Email address(es) to always send notifications to, addresses can be seen by all recipients (Cc:).
  `smtp_default_domain`       Default host/domain to append to address that do not specify one.
  `smtp_enabled`              Enable email notification.
  `smtp_from`                 Sender address to use in notification emails.
  `smtp_from_name`            Sender name to use in notification emails.
  `smtp_password`             Password for SMTP server. (*since 0.9*)
  `smtp_port`                 SMTP server port to use for email notification.
  `smtp_replyto`              Reply-To address to use in notification emails.
  `smtp_server`               SMTP server hostname to use for email notifications.
  `smtp_subject_prefix`       Text to prepend to subject line of notification emails. If the setting is not defined, then the \[\$project\_name\] prefix. If no prefix is desired, then specifying an empty option will disable it. (*since 0.10.1*).
  `smtp_user`                 Username for SMTP server. (*since 0.9*)
  `ticket_subject_template`   A Genshi text template snippet used to get the notification subject. By default, the subject template is `$prefix #$ticket.id: $summary`. `$prefix` being the value of the `smtp_subject_prefix` option. *(since 0.11)*
  `use_public_cc`             Recipients can see email addresses of other CC'ed recipients. If this option is disabled (the default), recipients are put on BCC. (*since 0.10*)
  `use_short_addr`            Permit email address without a host/domain (i.e. username only). The SMTP server should accept those addresses, and either append a FQDN or use local delivery. (*since 0.10*)
  `use_tls`                   Use SSL/TLS to send notifications over SMTP. (*since 0.10*)
  --------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[openid]` {#openid-section}

  ---------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `absolute_trust_root`        Whether we should use absolute trust root or by project.
  `black_list`                 Comma separated list of denied [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} addresses.
  `check_list`                 JSON service for openid check.
  `check_list_key`             Key for openid Service.
  `check_list_username`        Username for openid Service.
  `combined_username`          Username will be written as username\_in\_remote\_system &lt;openid\_url&gt;.
  `custom_provider_image`      Custom [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} provider image.
  `custom_provider_label`      Custom [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} provider label.
  `custom_provider_name`       Custom [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} provider name.
  `custom_provider_size`       Custom [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} provider image size (small or large).
  `custom_provider_url`        Custom [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} provider URL. E.g.: [[​]{.icon}http://claimid.com/{username](http://claimid.com/%7Busername){.ext-link}}
  `default_openid`             Default OpenID provider for directed identity.
  `email_white_list`           Comma separated list of allowed users, using the resolved SREG/AX email address. Use in combination with trusted identity patterns in white\_list.
  `groups_to_request`          Which 'team names' to request via the OpenIDTeams extension. To use this option you must have python-openid-teams installed.
  `lowercase_authname`         Whether authnames should always be lower-cased. Setting this to false generally makes more sense, however this is backwards-incompatible if you already have user sessions which you would like to preserve.
  `pape_method`                Default PAPE method to request from OpenID provider.
  `providers`                  Explicit set of provider names to display. E.g: google, yahoo, …
  `signup`                     Signup link
  `sreg_required`              Whether SREG data should be required or optional.
  `strip_protocol`             Instead of using username beginning with [[​]{.icon}http://](http://){.ext-link} or [[​]{.icon}https://](https://){.ext-link} you can strip the beginning.
  `strip_trailing_slash`       In case your OpenID is some sub-domain address [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} library adds trailing slash. This option strips it.
  `take_default_login`         Set to true if /login should be handled by openid.
  `timeout`                    Specify if expiration time should act as timeout. If set, cookie lifetime will be extended to auth\_cookie\_lifetime on each authenticated access.
  `trust_authname`             WARNING: Only enable this if you know what this mean! This could make identity theft very easy if you do not control the OpenID provider! Enabling this option makes the retrieved authname from the OpenID provider authorative, i.e. it trusts the authname to be the unique username of the user. Enabling this disables the collission checking, so two different OpenID urls may suddenly get the same username if they have the same authname
  `use_nickname_as_authname`   Whether the nickname as retrieved by SReg is used as username
  `whatis`                     What is [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} link.
  `white_list`                 Comma separated list of allowed [OpenId?](https://docs.pagure.org/sssd-test2/OpenId.html){.missing .wiki} addresses.
  ---------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[privatetickets]` {#privatetickets-section}

  ------------------- --------------------------------------------------------
  `group_blacklist`   Groups that do not affect the common membership check.
  ------------------- --------------------------------------------------------

### `[project]` {#project-section}

  ------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `admin`            E-Mail address of the project's administrator.
  `admin_trac_url`   Base URL of a Trac instance where errors in this Trac should be reported. This can be an absolute or relative URL, or '.' to reference this Trac instance. An empty value will disable the reporting buttons. (*since 0.11.3*)
  `descr`            Short description of the project.
  `footer`           Page footer text (right-aligned).
  `icon`             URL of the icon of the project.
  `name`             Name of the project.
  `url`              URL of the main project web site, usually the website in which the `base_url` resides. This is used in notification e-mails.
  ------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[query]` {#query-section}

  --------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `default_anonymous_query`   The default query for anonymous users. The query is either in [query language](https://docs.pagure.org/sssd-test2/TracQuery.html#QueryLanguage){.wiki} syntax, or a URL query string starting with `?` as used in `query:` [Trac links](https://docs.pagure.org/sssd-test2/TracQuery.html#UsingTracLinks){.wiki}. (*since 0.11.2*)
  `default_query`             The default query for authenticated users. The query is either in [query language](https://docs.pagure.org/sssd-test2/TracQuery.html#QueryLanguage){.wiki} syntax, or a URL query string starting with `?` as used in `query:` [Trac links](https://docs.pagure.org/sssd-test2/TracQuery.html#UsingTracLinks){.wiki}. (*since 0.11.2*)
  `items_per_page`            Number of tickets displayed per page in ticket queries, by default (*since 0.11*)
  `ticketlink_query`          The base query to be used when linkifying values of ticket fields. The query is a URL query string starting with `?` as used in `query:` [Trac links](https://docs.pagure.org/sssd-test2/TracQuery.html#UsingTracLinks){.wiki}. (*since 0.12*)
  --------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[report]` {#report-section}

  ---------------------- -----------------------------------------------------------------------------------
  `items_per_page`       Number of tickets displayed per page in ticket reports, by default (*since 0.11*)
  `items_per_page_rss`   Number of tickets displayed in the rss feeds for reports (*since 0.11*)
  ---------------------- -----------------------------------------------------------------------------------

### `[revisionlog]` {#revisionlog-section}

  --------------------- -----------------------------------------------------------------------------------------------------------------------------------------------
  `default_log_limit`   Default value for the limit argument in the [TracRevisionLog](https://docs.pagure.org/sssd-test2/TracRevisionLog.html){.wiki} (*since 0.11*).
  --------------------- -----------------------------------------------------------------------------------------------------------------------------------------------

### `[roadmap]` {#roadmap-section}

  ------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------
  `stats_provider`   Name of the component implementing `ITicketGroupStatsProvider`, which is used to collect statistics on groups of tickets for display in the roadmap views.
  ------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[search]` {#search-section}

  ---------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `default_disabled_filters`   Specifies which search filters should be disabled by default on the search page. This will also restrict the filters for the quick search function. The filter names defined by default components are: `wiki`, `ticket`, `milestone` and `changeset`. For plugins, look for their implementation of the ISearchSource interface, in the `get_search_filters()` method, the first member of returned tuple. Once disabled, search filters can still be manually enabled by the user on the search page. (since 0.12)
  `min_query_length`           Minimum length of query string allowed when performing a search.
  ---------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[sensitivetickets]` {#sensitivetickets-section}

  --------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `allow_cc`            Whether users listed in the cc field of a sensitive ticket should have access to that ticket even if they do not have SENSITIVE\_VIEW privileges
  `allow_owner`         Whether the owner of a sensitive ticket should have access to that ticket even if they do not have SENSITIVE\_VIEW privileges
  `allow_reporter`      Whether the reporter of a sensitive ticket should have access to that ticket even if they do not have SENSITIVE\_VIEW privileges
  `limit_sensitivity`   With limit\_sensitivity set to true, users cannot set the sensitivity checkbox on a ticket unless they are authenticated and would otherwise be permitted to deal with the ticket if it were marked sensitive. This prevents users from marking the tickets of other users as "sensitive".
  --------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[sqlite]` {#sqlite-section}

  -------------- --------------------------------------------------------------------------------------------------
  `extensions`   Paths to sqlite extensions, relative to Trac environment's directory or absolute. (*since 0.12*)
  -------------- --------------------------------------------------------------------------------------------------

### `[svn]` {#svn-section}

  ------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `branches`   Comma separated list of paths categorized as branches. If a path ends with '\*', then all the directory entries found below that path will be included. Example: `/trunk, /branches/*, /projectAlpha/trunk, /sandbox/*`
  `tags`       Comma separated list of paths categorized as tags. If a path ends with '\*', then all the directory entries found below that path will be included. Example: `/tags/*, /projectAlpha/tags/A-1.0, /projectAlpha/tags/A-v1.1`
  ------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[ticket]` {#ticket-section}

  ------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `default_cc`             Default cc: list for newly created tickets.
  `default_component`      Default component for newly created tickets.
  `default_description`    Default description for newly created tickets.
  `default_keywords`       Default keywords for newly created tickets.
  `default_milestone`      Default milestone for newly created tickets.
  `default_owner`          Default owner for newly created tickets.
  `default_priority`       Default priority for newly created tickets.
  `default_resolution`     Default resolution for resolving (closing) tickets (*since 0.11*).
  `default_severity`       Default severity for newly created tickets.
  `default_summary`        Default summary (title) for newly created tickets.
  `default_type`           Default type for newly created tickets (*since 0.9*).
  `default_version`        Default version for newly created tickets.
  `max_comment_size`       Don't accept tickets with a too big comment. (*since 0.11.2*)
  `max_description_size`   Don't accept tickets with a too big description. (*since 0.11*).
  `preserve_newlines`      Whether Wiki formatter should respect the new lines present in the Wiki text. If set to 'default', this is equivalent to 'yes' for new environments but keeps the old behavior for upgraded environments (i.e. 'no'). (*since 0.11*).
  `restrict_owner`         Make the owner field of tickets use a drop-down menu. Be sure to understand the performance implications before activating this option. See [Assign-to as Drop-Down List](https://docs.pagure.org/sssd-test2/TracTickets.html#Assign-toasDrop-DownList){.wiki}. Please note that e-mail addresses are **not** obfuscated in the resulting drop-down menu, so this option should not be used if e-mail addresses must remain protected. (*since 0.9*)
  `workflow`               Ordered list of workflow controllers to use for ticket actions (*since 0.11*).
  ------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[timeline]` {#timeline-section}

  ----------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `abbreviated_messages`        Whether wiki-formatted event messages should be truncated or not. This only affects the default rendering, and can be overriden by specific event providers, see their own documentation. (*Since 0.11*)
  `changeset_collapse_events`   Whether consecutive changesets from the same author having exactly the same message should be presented as one event. That event will link to the range of changesets in the log view. (*since 0.11*)
  `changeset_long_messages`     Whether wiki-formatted changeset messages should be multiline or not. If this option is not specified or is false and `wiki_format_messages` is set to true, changeset messages will be single line only, losing some formatting (bullet points, etc).
  `changeset_show_files`        Number of files to show (`-1` for unlimited, `0` to disable). This can also be `location`, for showing the common prefix for the changed files. (since 0.11).
  `default_daysback`            Default number of days displayed in the Timeline, in days. (*since 0.9.*)
  `max_daysback`                Maximum number of days (-1 for unlimited) displayable in the Timeline. (*since 0.11*)
  `newticket_formatter`         Which formatter flavor (e.g. 'html' or 'oneliner') should be used when presenting the description for new tickets. If 'oneliner', the \[timeline\] abbreviated\_messages option applies. (*since 0.11*).
  `ticket_show_details`         Enable the display of all ticket changes in the timeline, not only open / close operations (*since 0.9*).
  ----------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[trac]` {#trac-section}

  ------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `authz_file`                    The path to the Subversion [[​]{.icon}authorization (authz) file](http://svnbook.red-bean.com/en/1.5/svn.serverconfig.pathbasedauthz.html){.ext-link}. To enable authz permission checking, the `AuthzSourcePolicy` permission policy must be added to `[trac] permission_policies`.
  `authz_module_name`             The module prefix used in the `authz_file` for the default repository. If left empty, the global section is used.
  `auto_preview_timeout`          Inactivity timeout in seconds after which the automatic wiki preview triggers an update. This option can contain floating-point values. The lower the setting, the more requests will be made to the server. Set this to 0 to disable automatic preview. The default is 2.0 seconds. (*since 0.12*)
  `auto_reload`                   Automatically reload template files after modification.
  `backup_dir`                    Database backup location
  `base_url`                      Reference URL for the Trac deployment. This is the base URL that will be used when producing documents that will be used outside of the web browsing context, like for example when inserting URLs pointing to Trac resources in notification e-mails.
  `check_auth_ip_mask`            What mask should be applied to user address.
  `database`                      Database connection [string](https://docs.pagure.org/sssd-test2/TracEnvironment.html#DatabaseConnectionStrings){.wiki} for this project
  `debug_sql`                     Show the SQL queries in the Trac log, at DEBUG level. *(Since 0.11.5)*
  `default_charset`               Charset to be used when in doubt.
  `default_handler`               Name of the component that handles requests to the base URL. Options include `TimelineModule`, `RoadmapModule`, `BrowserModule`, `QueryModule`, `ReportModule`, `TicketModule` and `WikiModule`. The default is `WikiModule`. (*since 0.9*)
  `default_language`              The preferred language to use if no user preference has been set. (*since 0.12.1*)
  `default_timezone`              The default timezone to use
  `genshi_cache_size`             The maximum number of templates that the template loader will cache in memory. The default value is 128. You may want to choose a higher value if your site uses a larger number of templates, and you have enough memory to spare, or you can reduce it if you are short on memory.
  `htdocs_location`               Base URL for serving the core static resources below `/chrome/common/`. It can be left empty, and Trac will simply serve those resources itself. Advanced users can use this together with [trac-admin ... deploy &lt;deploydir&gt;](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki} to allow serving the static resources for Trac directly from the web server. Note however that this only applies to the `<deploydir>/htdocs/common` directory, the other deployed resources (i.e. those from plugins) will not be made available this way and additional rewrite rules will be needed in the web server.
  `mainnav`                       Order of the items to display in the `mainnav` navigation bar, listed by IDs. See also [TracNavigation](https://docs.pagure.org/sssd-test2/TracNavigation.html){.wiki}.
  `metanav`                       Order of the items to display in the `metanav` navigation bar, listed by IDs. See also [TracNavigation](https://docs.pagure.org/sssd-test2/TracNavigation.html){.wiki}.
  `mysqldump_path`                Location of mysqldump for MySQL database backups
  `never_obfuscate_mailto`        Never obfuscate `mailto:` links explicitly written in the wiki, even if `show_email_addresses` is false or the user has not the EMAIL\_VIEW permission (*since 0.11.6*).
  `permission_policies`           List of components implementing `IPermissionPolicy`, in the order in which they will be applied. These components manage fine-grained access control to Trac resources. Defaults to the [DefaultPermissionPolicy?](https://docs.pagure.org/sssd-test2/DefaultPermissionPolicy.html){.missing .wiki} (pre-0.11 behavior) and [LegacyAttachmentPolicy?](https://docs.pagure.org/sssd-test2/LegacyAttachmentPolicy.html){.missing .wiki} (map ATTACHMENT\_\* permissions to realm specific ones)
  `permission_store`              Name of the component implementing `IPermissionStore`, which is used for managing user and group permissions.
  `pg_dump_path`                  Location of pg\_dump for Postgres database backups
  `repository_dir`                Path to the default repository. This can also be a relative path (*since 0.11*). This option is deprecated, and repositories should be defined in the [repositories](https://docs.pagure.org/sssd-test2/TracIni.html#repositories-section){.wiki} section, or using the "Repositories" admin panel. (*since 0.12*)
  `repository_sync_per_request`   List of repositories that should be synchronized on every page request. Leave this option empty if you have set up post-commit hooks calling `trac-admin $ENV changeset added` on all your repositories (recommended). Otherwise, set it to a comma-separated list of repository names. Note that this will negatively affect performance, and will prevent changeset listeners from receiving events from the repositories specified here. The default is to synchronize the default repository, for backward compatibility. (*since 0.12*)
  `repository_type`               Default repository connector type. (*since 0.10*) This is also used as the default repository type for repositories defined in [TracIni\#repositories-section repositories](https://docs.pagure.org/sssd-test2/TracIni.html#repositories-section%20repositories){.wiki} or using the "Repositories" admin panel. (*since 0.12*)
  `request_filters`               Ordered list of filters to apply to all requests (*since 0.10*).
  `resizable_textareas`           Make `<textarea>` fields resizable. Requires JavaScript. (*since 0.12*)
  `secure_cookies`                Restrict cookies to HTTPS connections. When true, set the `secure` flag on all cookies so that they are only sent to the server on HTTPS connections. Use this if your Trac instance is only accessible through HTTPS. (*since 0.11.2*)
  `show_email_addresses`          Show email addresses instead of usernames. If false, we obfuscate email addresses. (*since 0.11*)
  `show_ip_addresses`             Show IP addresses for resource edits (e.g. wiki). (*since 0.11.3*)
  `timeout`                       Timeout value for database connection, in seconds. Use '0' to specify *no timeout*. *(Since 0.11)*
  `use_base_url_for_redirect`     Optionally use `[trac] base_url` for redirects. In some configurations, usually involving running Trac behind a HTTP proxy, Trac can't automatically reconstruct the URL that is used to access it. You may need to use this option to force Trac to use the `base_url` setting also for redirects. This introduces the obvious limitation that this environment will only be usable when accessible from that URL, as redirects are frequently used. *(since 0.10.5)*
  ------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[tracbzr]` {#tracbzr-section}

  ---------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `include_sideline_changes`   Include sideline changes in the list of changes. This option controls whether sideline changes (i.e. changes with dotted revision numbers only) are included in the list of changes as reported by the timeline view. Note that there might be other plugins using that information as well, so there might be other components beside the timeline view that get affected by this setting. Defaults to True.
  `primary_branches`           Ordered list of primary branches. These will be listed first in the Branches macro. When viewing the timeline, each changeset will be associated with the first primary branch that contains it. The value is a comma separated list of globs, as used by the fnmatch module. An empty list element can be used to denote the branch at the root of the repository. Defaults to 'trunk'.
  ---------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[versioncontrol]` {#versioncontrol-section}

  ----------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `allowed_repository_dir_prefixes`   Comma-separated list of allowed prefixes for repository directories when adding and editing repositories in the repository admin panel. If the list is empty, all repository directories are allowed. (*since 0.12.1*)
  ----------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### `[watchlist]` {#watchlist-section}

  ----------------- -------------------------------
  `notifications`   Enables notification features
  ----------------- -------------------------------

### `[wiki]` {#wiki-section}

  ------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `ignore_missing_pages`    Enable/disable highlighting [CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.wiki} links to missing pages (*since 0.9*).
  `max_size`                Maximum allowed wiki page size in bytes. (*since 0.11.2*)
  `render_unsafe_content`   Enable/disable the use of unsafe HTML tags such as `<script>` or `<embed>` with the HTML [WikiProcessor](https://docs.pagure.org/sssd-test2/WikiProcessors.html){.wiki} (*since 0.10.4*). For public sites where anonymous users can edit the wiki it is recommended to leave this option disabled (which is the default).
  `safe_schemes`            List of URI schemes considered "safe", that will be rendered as external links even if `[wiki] render_unsafe_content` is `false`. (*since 0.11.8*)
  `split_page_names`        Enable/disable splitting the [WikiPageNames](https://docs.pagure.org/sssd-test2/WikiPageNames.html){.wiki} with space characters (*since 0.10*).
  ------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

Reference for special sections {#Referenceforspecialsections}
------------------------------

1.  [\[components\]](#components-section)
2.  [\[extra-permissions\]](#extra-permissions-section)
3.  [\[milestone-groups\]](#milestone-groups-section)
4.  [\[repositories\]](#repositories-section)
5.  [\[svn:externals\]](#svn:externals-section)
6.  [\[ticket-custom\]](#ticket-custom-section)
7.  [\[ticket-workflow\]](#ticket-workflow-section)

### \[components\] {#components-section}

This section is used to enable or disable components provided by
plugins, as well as by Trac itself. The component to enable/disable is
specified via the name of the option. Whether its enabled is determined
by the option value; setting the value to `enabled` or `on` will enable
the component, any other value (typically `disabled` or `off`) will
disable the component.

The option name is either the fully qualified name of the components or
the module/package prefix of the component. The former enables/disables
a specific component, while the latter enables/disables any component in
the specified package/module.

Consider the following configuration snippet:

``` {.wiki}
[components]
trac.ticket.report.ReportModule = disabled
webadmin.* = enabled
```

The first option tells Trac to disable the [report
module](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki}. The
second option instructs Trac to enable all components in the `webadmin`
package. Note that the trailing wildcard is required for module/package
matching.

See the *Plugins* page on *About Trac* to get the list of active
components (requires `CONFIG_VIEW`
[permissions](https://docs.pagure.org/sssd-test2/TracPermissions.html){.wiki}.)

See also:
[TracPlugins](https://docs.pagure.org/sssd-test2/TracPlugins.html){.wiki}

### \[extra-permissions\] {#extra-permissions-section}

*(since 0.12)*

Custom additional permissions can be defined in this section when
[ExtraPermissionsProvider?](https://docs.pagure.org/sssd-test2/ExtraPermissionsProvider.html){.missing
.wiki} is enabled.

### \[milestone-groups\] {#milestone-groups-section}

*(since 0.11)*

As the workflow for tickets is now configurable, there can be many
ticket states, and simply displaying closed tickets vs. all the others
is maybe not appropriate in all cases. This section enables one to
easily create *groups* of states that will be shown in different colors
in the milestone progress bar.

Example configuration (the default only has closed and active):

``` {.wiki}
closed = closed
# sequence number in the progress bar
closed.order = 0
# optional extra param for the query (two additional columns: created and modified and sort on created)
closed.query_args = group=resolution,order=time,col=id,col=summary,col=owner,col=type,col=priority,col=component,col=severity,col=time,col=changetime
# indicates groups that count for overall completion percentage
closed.overall_completion = true

new = new
new.order = 1
new.css_class = new
new.label = new

# one catch-all group is allowed
active = *
active.order = 2
# CSS class for this interval
active.css_class = open
# Displayed label for this group
active.label = in progress
```

The definition consists in a comma-separated list of accepted status.
Also, '\*' means any status and could be used to associate all remaining
states to one catch-all group.

The CSS class can be one of: new (yellow), open (no color) or closed
(green). New styles can easily be added using the following selector:
`table.progress td.<class>`

### \[repositories\] {#repositories-section}

(*since 0.12* multirepos)

One of the alternatives for registering new repositories is to populate
the `[repositories]` section of the trac.ini.

This is especially suited for setting up convenience aliases,
short-lived repositories, or during the initial phases of an
installation.

See
[TracRepositoryAdmin](https://docs.pagure.org/sssd-test2/TracRepositoryAdmin.html#Intrac.ini){.wiki}
for details about the format adopted for this section and the rest of
that page for the other alternatives.

### \[svn:externals\] {#svn:externals-section}

*(since 0.11)*

The
[TracBrowser](https://docs.pagure.org/sssd-test2/TracBrowser.html){.wiki}
for Subversion can interpret the `svn:externals` property of folders. By
default, it only turns the URLs into links as Trac can't browse remote
repositories.

However, if you have another Trac instance (or an other repository
browser like [[​]{.icon}ViewVC](http://www.viewvc.org/){.ext-link})
configured to browse the target repository, then you can instruct Trac
which other repository browser to use for which external URL.

This mapping is done in the `[svn:externals]` section of the
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki}

Example:

``` {.wiki}
[svn:externals]
1 = svn://server/repos1                       http://trac/proj1/browser/$path?rev=$rev
2 = svn://server/repos2                       http://trac/proj2/browser/$path?rev=$rev
3 = http://theirserver.org/svn/eng-soft       http://ourserver/viewvc/svn/$path/?pathrev=25914
4 = svn://anotherserver.com/tools_repository  http://ourserver/tracs/tools/browser/$path?rev=$rev
```

With the above, the
`svn://anotherserver.com/tools_repository/tags/1.1/tools` external will
be mapped to `http://ourserver/tracs/tools/browser/tags/1.1/tools?rev=`
(and `rev` will be set to the appropriate revision number if the
external additionally specifies a revision, see the [[​]{.icon}SVN Book
on
externals](http://svnbook.red-bean.com/en/1.4/svn.advanced.externals.html){.ext-link}
for more details).

Note that the number used as a key in the above section is purely used
as a place holder, as the URLs themselves can't be used as a key due to
various limitations in the configuration file parser.

Finally, the relative URLs introduced in [[​]{.icon}Subversion
1.5](http://subversion.tigris.org/svn_1.5_releasenotes.html#externals){.ext-link}
are not yet supported.

### \[ticket-custom\] {#ticket-custom-section}

In this section, you can define additional fields for tickets. See
[TracTicketsCustomFields](https://docs.pagure.org/sssd-test2/TracTicketsCustomFields.html){.wiki}
for more details.

### \[ticket-workflow\] {#ticket-workflow-section}

*(since 0.11)*

The workflow for tickets is controlled by plugins. By default, there's
only a `ConfigurableTicketWorkflow` component in charge. That component
allows the workflow to be configured via this section in the trac.ini
file. See
[TracWorkflow](https://docs.pagure.org/sssd-test2/TracWorkflow.html){.wiki}
for more details.

------------------------------------------------------------------------

See also:
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[TracAdmin](https://docs.pagure.org/sssd-test2/TracAdmin.html){.wiki},
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
