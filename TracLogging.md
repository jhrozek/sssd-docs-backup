Trac Logging {#TracLogging}
============

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

Trac supports logging of system messages using the standard
[[​]{.icon}logging
module](http://docs.python.org/lib/module-logging.html){.ext-link} that
comes with Python.

Logging is configured in the `[logging]` section in
[trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#logging-section){.wiki}.

Supported Logging Methods {#SupportedLoggingMethods}
-------------------------

The log method is set using the `log_type` option in
[trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#logging-section){.wiki},
which takes any of the following values:

**none****
:   Suppress all log messages.

**file**
:   Log messages to a file, specified with the `log_file` option in
    [trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#logging-section){.wiki}.
    Relative paths in `log_file` are resolved relative to the `log`
    directory of the environment.

**stderr**
:   Output all log entries to console
    ([tracd](https://docs.pagure.org/sssd-test2/TracStandalone.html){.wiki}
    only).

**syslog**
:   (UNIX) Send all log messages to the local syslogd via named pipe
    `/dev/log`. By default, syslog will write them to the file
    /var/log/messages.

**eventlog**
:   (Windows) Use the system's NT Event Log for Trac logging.

Log Levels {#LogLevels}
----------

The verbosity level of logged messages can be set using the `log_level`
option in
[trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#logging-section){.wiki}.
The log level defines the minimum level of urgency required for a
message to be logged, and those levels are:

**CRITICAL**
:   Log only the most critical (typically fatal) errors.

**ERROR**
:   Log failures, bugs and errors.

**WARN**
:   Log warnings, non-interrupting events.

**INFO**
:   Diagnostic information, log information about all processing.

**DEBUG**
:   Trace messages, profiling, etc.

Note that starting with Trac 0.11.5 you can in addition enable logging
of SQL statements, at debug level. This is turned off by default, as
it's very verbose (set `[trac] debug_sql = yes` in
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki} to
activate).

Log Format {#LogFormat}
----------

Starting with Trac 0.10.4 (see
[[​]{.icon}\#2844](http://trac.edgewall.org/intertrac/%232844 "#2844 in Trac project trac"){.ext-link}),
it is possible to set the output format for log entries. This can be
done through the `log_format` option in
[trac.ini](https://docs.pagure.org/sssd-test2/TracIni.html#logging-section){.wiki}.
The format is a string which can contain any of the [[​]{.icon}Python
logging Formatter
variables](http://docs.python.org/lib/node422.html){.ext-link}.
Additonally, the following Trac-specific variables can be used:

**\$(basename)s**
:   The last path component of the current environment.

**\$(path)s**
:   The absolute path for the current environment.

**\$(project)s**
:   The originating project's name.

Note that variables are identified using a dollar sign (`$(...)s`)
instead of percent sign (`%(...)s`).

The default format is:

``` {.wiki}
log_format = Trac[$(module)s] $(levelname)s: $(message)s
```

In a multi-project environment where all logs are sent to the same place
(e.g. `syslog`), it makes sense to add the project name. In this example
we use `basename` since that can generally be used to identify a
project:

``` {.wiki}
log_format = Trac[$(basename)s:$(module)s] $(levelname)s: $(message)s
```

------------------------------------------------------------------------

See also:
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki},
[TracGuide](https://docs.pagure.org/sssd-test2/TracGuide.html){.wiki},
[TracEnvironment](https://docs.pagure.org/sssd-test2/TracEnvironment.html){.wiki}
