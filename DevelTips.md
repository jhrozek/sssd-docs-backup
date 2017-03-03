<div class="wiki-toc">

1.  [SSSD Devel page](#SSSDDevelpage)
    1.  [Are there any introductory tutorials
        available?](#Arethereanyintroductorytutorialsavailable)
        1.  [Talloc](#Talloc)
        2.  [Tevent and tevent\_req](#Teventandtevent_req)
    2.  [When I debug an SSSD process in a debugger, it always gets
        killed with
        …](#WhenIdebuganSSSDprocessinadebuggeritalwaysgetskilledwithSIGTERMorreceivesSIGRTperiodically)
        1.  [Until and including sssd-1.13](#Untilandincludingsssd-1.13)
        2.  [sssd-1.14 or later](#sssd-1.14orlater)
    3.  [Using valgrind to identify memory access
        problems](#Usingvalgrindtoidentifymemoryaccessproblems)
    4.  [Using strace to track the SSSD
        processes](#UsingstracetotracktheSSSDprocesses)
    5.  [How do I track work-in-progress of other
        developers?](#HowdoItrackwork-in-progressofotherdevelopers)
    6.  [Why does make check take so long?](#Whydoesmakechecktakesolong)
    7.  [Using clang to perform static analysis of source
        code](#Usingclangtoperformstaticanalysisofsourcecode)
    8.  [When I compile the SSSD from source there is an error that says
        …](#WhenIcompiletheSSSDfromsourcethereisanerrorthatsaysusrlibldbmemberof.la:invalidELFheader)
    9.  [When I try to debug tests using [​]{.icon}gdb I
        …](#WhenItrytodebugtestsusinggdbIgetmessagesimilartohomeusersssd.sysdb-tests:notinexecutableformat:Fileformatnotrecognized)

</div>

SSSD Devel page {#SSSDDevelpage}
===============

This wiki page contains a collection of tips that might be useful for
SSSD developers and contributors. If you use a trick that is not
mentioned here, tell us on the [[​]{.icon}SSSD development
list](https://fedorahosted.org/mailman/listinfo/sssd-devel){.ext-link}
or the [[​]{.icon}IRC](irc://irc.freenode.net/sssd){.ext-link}

Are there any introductory tutorials available? {#Arethereanyintroductorytutorialsavailable}
-----------------------------------------------

### Talloc {#Talloc}

SSSD relies on the talloc memory allocator that originated in the Samba
project.

SSSD developer Pavel Březina wrote a very detailed tutorial on its
design, use and best practices. This is a must-read for anyone
interested in contributing to SSSD.

-   [[​]{.icon}Talloc
    Tutorial](http://talloc.samba.org/talloc/doc/html/libtalloc__tutorial.html){.ext-link}

Other resources:

-   [[​]{.icon}Why you should use talloc for your next
    project](http://sgallagh.wordpress.com/2010/03/17/why-you-should-use-talloc-for-your-next-project/){.ext-link}

### Tevent and tevent\_req {#Teventandtevent_req}

-   [[​]{.icon}Tevent
    Tutorial](https://tevent.samba.org/tevent_tutorial.html){.ext-link}

When I debug an SSSD process in a debugger, it always gets killed with `SIGTERM` or receives `SIGRT` periodically {#WhenIdebuganSSSDprocessinadebuggeritalwaysgetskilledwithSIGTERMorreceivesSIGRTperiodically}
-----------------------------------------------------------------------------------------------------------------

The behaviour here depends a bit on your SSSD version.

### Until and including sssd-1.13 {#Untilandincludingsssd-1.13}

The main SSSD process (the monitor) sends "heartbeat" checks called
pings to the other SSSD services, both responders and providers. If the
service does not respond in a specified time interval, the monitor sends
the `SIGTERM` signal to the service in an attempt to terminate a non
responding instance and start a new one.

However, in the case a service is being traced in a debugger, it is
quite common to examine the process for long enough that the monitor
would consider the service hung and send SIGTERM. The SSSD has an option
simply called `timeout` that specifies the interval between the pings
the monitor sends to the services. Currently the monitor sends three
pings before sending the terminating signals, each ping is sent after 10
seconds by default.

To change the monitor settings to send pings after one hour:

``` {.wiki}
    timeout = 3600
```

An alternate approach while debugging is to send SIGSTOP to the 'sssd'
process, which will halt the monitor process. However, you must remember
to send SIGCONT when you're done debugging, or your monitor will be
unable to manage the other processes or shut down gracefully.

### sssd-1.14 or later {#sssd-1.14orlater}

In order to support socket-activated services better, we removed the
watchdog ping-pong in 1.14 and replaces it with a "watchdog" in the
services themselves. The services send themselves a `SIGRT` signal and
increase a counter each time `SIGRT` is delivered. There is also a timer
event using the SSSD event loop that periodically re-sets the counter to
signal the service is still processing event loop events and thus can be
considered alive. Once the counter reaches a threshold (3 by default),
the service exits and the monitor restarts the service upon receiving a
`SIGCHLD` signal.

To change the period of `SIGRT` signals and therefore to change how
often is the counter increased, change the `timeout` parameter in the
service section, for example to be increased only once per hour:

``` {.wiki}
    timeout = 3600
```

Alternatively, you can disable the function that stops the watchdog
completely:

``` {.wiki}
    p teardown_watchdog()
```

You can place this command to a `.gdbinit` file so that it gets executed
once you attach gdb to a sssd process.

Using valgrind to identify memory access problems {#Usingvalgrindtoidentifymemoryaccessproblems}
-------------------------------------------------

[[​]{.icon}valgrind](http://valgrind.org){.ext-link} is an immensely
useful tool that is able to check a wide range of memory access problems
- from memory leaks to use-after-free bugs.

When debugging the main SSSD program, one can just run the program as a
positional valgrind parameter:

``` {.wiki}
    valgrind /usr/sbin/sssd
```

The situation is somewhat complex when the developer needs to debug one
of the services that the SSSD monitor spawns. The best solution is to
use the special (undocumented) parameter called `command`. By default,
the "command" defaults to `${libexec}/sssd_${service`} which expands to
absolute path pointing to `/usr/libexec/sssd/sssd_${service`} on Fedora.

The general format is `valgrind <path-to-service>`. For example to debug
the `sss_nss` process, you need to specify the following in the `[nss]`
section of the sssd.conf file:

``` {.wiki}
    command = valgrind --leak-check=full /usr/libexec/sssd/sssd_nss
```

Some of the SSSD processes, notable the sssd\_be processes that
represent the `[domain/]` sections of `sssd.conf`, require command line
parameters in order to function correctly. The easiest way to check how
exactly the SSSD spawns the worker processes is to simply check with the
`ps(1)` utility:

``` {.wiki}
    ps -axu | grep sss
```

The following example illustrates using valgrind to debug an SSSD domain
called "default", which is the name authconfig uses:

``` {.wiki}
    command = valgrind --leak-check=full --log-file=/tmp/valgrind.%p.log /usr/libexec/sssd/sssd_be --domain default
```

This will log valgrind findings to a file in /tmp named with the process
ID.

Using strace to track the SSSD processes {#UsingstracetotracktheSSSDprocesses}
----------------------------------------

Sometimes, the DEBUG messages are not enough in telling you what went
wrong. A typical example, found in the wild was that `libkrb5`
initialization was failing in krb5\_child process:

``` {.wiki}
(Thu Feb 19 15:58:12 2015) [[sssd[krb5_child[54101]]]] [become_user] (0x0200): Trying to become user [9922][14].
(Thu Feb 19 15:58:12 2015) [[sssd[krb5_child[54101]]]] [create_ccache] (0x0020): 575: [13][Permission denied]
```

So krb5\_child couldn't access a resource, but how do we tell which one?
It's best to start the back end under strace. This has to be done
similarly to how we start `sssd_be` under `valgrind`, by adding the
`command` option to the `[domain]` section. For SSSD 1.13+ the `command`
can be specified as:

``` {.wiki}
command = strace -ff -o /tmp/sssd_be_strace /usr/libexec/sssd/sssd_be --debug-level=10 --domain ipa.example.com --uid=0 --gid=0
```

SSSD version 1.12 and lower require a slightly modified `command`
option:

``` {.wiki}
command = strace -ff -o /tmp/sssd_be_strace /usr/libexec/sssd/sssd_be --debug-level=10 --domain ipa.example.com
```

The `-ff` options are significant for debugging the child processes
`sssd_be` spawns. When the `sssd_be` process execs a subprocess, strace
would also track the child process by creating one file per process and
appending a numeric PID after the base filename `/tmp/sssd_be_strace`.

Then restart SSSD and run the sequence of commands that triggered the
bug.

Please make sure SELinux should be set to Permissive, otherwise sssd\_be
might not be able to execute child programs through strace. After that,
you should see several files under `/tmp/` matching the base filename:

``` {.wiki}
$ ls /tmp/sssd_be_strace*
/tmp/sssd_be_strace.27067  /tmp/sssd_be_strace.27071  /tmp/sssd_be_strace.27079
```

If you're looking for a file from a specific subprocess, it's best to
just grep the strace log file for the binary name of the subprocess:

``` {.wiki}
$ grep krb5_child /tmp/sssd_be_strace*
/tmp/sssd_be_strace.27079:execve("/usr/libexec/sssd/krb5_child", ["/usr/libexec/sssd/krb5_child"], [/* 24 vars */]) = 0
/tmp/sssd_be_strace.27079:write(2, "krb5_child started.\n", 20)   = 20
```

How do I track work-in-progress of other developers? {#HowdoItrackwork-in-progressofotherdevelopers}
----------------------------------------------------

Most of the core SSSD developers publish their work in progress patches
in topic branches of git repositories on
[[​]{.icon}http://fedorapeople.org](http://fedorapeople.org){.ext-link}

The web interface for the git repositories are available at

``` {.wiki}
    http://fedorapeople.org/gitweb?p=USERNAME/public_git/REPO_NAME
```

where USERNAME is the FAS user name of the developer and in the
particular case of REPO\_NAME is usually sssd.git

To add the repository as a git remote, issue the following:

``` {.wiki}
    git remote add REMOTE_NAME git://fedorapeople.org/home/fedora/USERNAME/public_git/REPO_NAME.git
    git fetch REMOTE_NAME
```

You can then see all the branches you are tracking with:

``` {.wiki}
    git branch -a
```

Or for a particular remote:

``` {.wiki}
    git branch -a | grep remotes/REMOTE_NAME
```

If you'd like to publish your work in the fedorapeople.org repo, follow
[[​]{.icon}the
guide](https://fedoraproject.org/wiki/Infrastructure/fedorapeople.org#BETA_git_hosting_support){.ext-link}
on the Fedora Project wiki -

Why does make check take so long? {#Whydoesmakechecktakesolong}
---------------------------------

By default, the SSSD tests are performed in the build directory. Some of
the unit tests, in particular the sysdb test generate a lot of disk
activity and the test runs might take a long time if executed on local
disk.

One solution is to use the `--with-test-dir` parameter which specifies
where the tests are creating their temporary files. Configuring the test
dir to use the in memory tmpfs filesystem located in `/dev/shm` will
mitigate the disk activity and improve the execution time.

``` {.wiki}
    ./configure --with-test-dir=/dev/shm
    make check
```

Using clang to perform static analysis of source code {#Usingclangtoperformstaticanalysisofsourcecode}
-----------------------------------------------------

The LLVM compiler suite contains a static analyzer that can help you
find bugs that are otherwise hard to notice. The analysis is run by
overriding the `$(CC)` Makefile variable to point to the `ccc-analyzer`
binary and then compiling the project. The clang suite contains a handy
Perl script `scan-build` that sets all the right variables for you. To
run the analysis, on Fedora, make sure to have the `clang-analyzer`
package installed. Then reconfigure and rebuild the SSSD using the
`scan-build` script:

``` {.wiki}
    scan-build ./configure
    scan-build make
```

You should see individual functions being analyzed during the build
process:

``` {.wiki}
    ANALYZE: src/db/sysdb_ops.c sysdb_mod_netgroup_member
    ANALYZE: src/db/sysdb_ops.c sysdb_remove_attrs
```

The default output is one HTML page per defect that can be viewed using
a special `scan-view` helper:

``` {.wiki}
    scan-build: 20 bugs found.
    scan-build: Run 'scan-view /tmp/scan-build-2012-05-09-2' to examine bug reports.
```

See the [[​]{.icon}official
documentation](http://clang-analyzer.llvm.org/scan-build.html){.ext-link}
for more info.

When I compile the SSSD from source there is an error that says `/usr/lib/ldb/memberof.la: invalid ELF header` {#WhenIcompiletheSSSDfromsourcethereisanerrorthatsaysusrlibldbmemberof.la:invalidELFheader}
--------------------------------------------------------------------------------------------------------------

You can safely ignore this warning or remove the `.la` file completely.

The .la file is a libtool archive and is a relic of how we generate the
module. They are only necessary for enabling `make uninstall` to work
properly, but if you are packaging an RPM or DEB file, the removal would
be handled by the packaging tools.

When I try to debug tests using [[​]{.icon}gdb](https://www.gnu.org/software/gdb/){.ext-link} I get message similar to `"/home/user/sssd/./sysdb-tests": not in executable format: File format not recognized` {#WhenItrytodebugtestsusinggdbIgetmessagesimilartohomeusersssd.sysdb-tests:notinexecutableformat:Fileformatnotrecognized}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The test you are trying to run is actually libtool script. To run for
example the sysdb-tests, use the following command to run the actual
binary file with gdb:

``` {.wiki}
libtool --mode=execute gdb ./sysdb-tests
```

instead of just

``` {.wiki}
gdb ./sysdb-tests
```
