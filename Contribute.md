<div class="wiki-toc">

1.  [Contribute](#Contribute)
    1.  [Contribution Policy](#ContributionPolicy)
    2.  [Source Code Repository](#SourceCodeRepository)
    3.  [Tasks for newcomers](#Tasksfornewcomers)
        1.  [Getting the source](#Gettingthesource)
    4.  [Building SSSD](#BuildingSSSD)
        1.  [Useful Tips and information for
            developers](#UsefulTipsandinformationfordevelopers)
        2.  [COPR Repository](#COPRRepository)
    5.  [Sending patch to upstream](#Sendingpatchtoupstream)
        1.  [Coding Style](#CodingStyle)
        2.  [Submitting](#Submitting)
        3.  [Patch metadata](#Patchmetadata)
        4.  [Unit tests](#Unittests)
            1.  [Running integration tests
                (locally)](#Runningintegrationtestslocally)
        5.  [Localization and
            Internationalization](#LocalizationandInternationalization)
2.  [Latest Documentation and
    Presentations](#LatestDocumentationandPresentations)

</div>

Contribute {#Contribute}
==========

There are many ways you can contribute to the System Security Services
Daemon. This page should provide some basic pointers.

SSSD development discussions occur either on the [[​]{.icon}SSSD
development
list](https://fedorahosted.org/mailman/listinfo/sssd-devel){.ext-link}
or on the [[​]{.icon}\#sssd IRC
channel](irc://irc.freenode.net/sssd){.ext-link} on
[[​]{.icon}freenode](http://freenode.net/){.ext-link}. Keep in mind that
SSSD developers are spread across different time zones, which makes
mailing list preferred communication channel if you wish to reach the
entire team.

The SSSD originated as a sister-project to
[[​]{.icon}FreeIPA](http://www.freeipa.org){.ext-link}, so we share many
pieces. Contributing to FreeIPA may also help SSSD and vice versa.

If you want to file a bug or enhancement request, please log in with
your Fedora Account System credentials. If you do not have a Fedora
Account, you can register for one at
[[​]{.icon}https://admin.fedoraproject.org/accounts/](https://admin.fedoraproject.org/accounts/){.ext-link}.
There is dedicated page about [[​]{.icon}bug
reporting](https://docs.pagure.org/sssd-test2/Reporting_sssd_bugs.html){.ext-link}.

Contribution Policy {#ContributionPolicy}
-------------------

All source code committed to the SSSD is assumed to be made available
under the GPLv3+ license unless the submitter specifies another license
at that time. The upstream SSSD maintainers reserve the right to refuse
a submission if the license is deemed incompatible with the goals of the
project.

Source Code Repository {#SourceCodeRepository}
----------------------

For the SSSD project, we use the
[[​]{.icon}Git](http://www.kernel.org/pub/software/scm/git/docs/gittutorial.html){.ext-link}
source control system.

``` {.wiki}
https://pagure.io/SSSD/sssd.git
```

Tasks for newcomers {#Tasksfornewcomers}
-------------------

We try to mark tickets that don't require too much existing knowledge
with the `easyfix` keyword in Trac. We also prepared [[​]{.icon}a Trac
query](https://fedorahosted.org/sssd/report/34){.ext-link} that lists
the easy fixes. Before starting the work on any of these tickets, it
might be a good idea to contact the SSSD developers on the
[[​]{.icon}sssd-devel
list](https://lists.fedorahosted.org/archives/list/sssd-devel@lists.fedorahosted.org/){.ext-link}
and check if the ticket is still valid or ask for guidance in general.

### Getting the source {#Gettingthesource}

To check out the latest SSSD sources, install git on your system
(Instructions are for Fedora, you may need to use a platform-specific
installation mechanism for other OSes).

``` {.wiki}
sudo dnf -y install git
```

You can find an excellent
[[​]{.icon}tutorial](http://www.kernel.org/pub/software/scm/git/docs/gittutorial.html){.ext-link}
for using git.

The first time, you will want to configure git with your name and email
address for patch attribution:

``` {.wiki}
git config --global user.name "GIVENNAME SURNAME"
git config --global user.email "username@domain.com"
```

You can enable syntax highlighting at the console (for git commands such
as '`git status`' and '`git diff`') by setting:

``` {.wiki}
git config --global color.ui auto
```

And if you would like to have a graphical tool for resolving merge
conflicts, you can install and set up meld:

``` {.wiki}
sudo dnf -y install meld
```

``` {.wiki}
git config --global merge.tool meld
```

It can be invoked with

``` {.wiki}
git mergetool
```

You can also enable the commit template by:

``` {.wiki}
git config commit.template .git-commit-template
```

Once that's done, you can clone our upstream git repository with

``` {.wiki}
git clone https://pagure.io/SSSD/sssd.git
```

This will create a new subdirectory 'sssd' in the current directory
which will contain the current master sources. All development should be
done first against the master branch, then backported to one of the
stable branches if necessary.

Building SSSD {#BuildingSSSD}
-------------

Starting with SSSD 1.10 beta, we now include a set of helper aliases and
environment variables in SSSD to simplify building development versions
of SSSD on Fedora. To take advantage of them, use the following command:

``` {.wiki}
. /path/to/sssd-source/contrib/fedora/bashrc_sssd
```

To build SSSD from source, follow these steps:

1.  Install necessary tools

    ``` {.wiki}
    # when using yum
    sudo yum -y install rpm-build yum-utils libldb-devel

    # when using dnf
    sudo dnf -y install rpm-build dnf-plugins-core libldb-devel
    ```

<!-- -->

2.  Create source rpm (run from git root directory)

    ``` {.wiki}
    contrib/fedora/make_srpm.sh
    ```

<!-- -->

3.  Install SSSD dependencies

    ``` {.wiki}
    # when using yum
    sudo yum-builddep rpmbuild/SRPMS/sssd-*.src.rpm

    # when using dnf
    sudo dnf builddep rpmbuild/SRPMS/sssd-*.src.rpm
    ```

If you plan on working with the SSSD source often, you may want to add
the following to your `~/.bashrc` file:

``` {.wiki}
if [ -f /path/to/sssd-source/contrib/fedora/bashrc_sssd ]; then
    . /path/to/sssd-source/contrib/fedora/bashrc_sssd
fi
```

You can now produce a Debug build of SSSD by running:

``` {.wiki}
cd /path/to/sssd-source
reconfig && chmake
```

The `reconfig` alias will run `autoreconf -if`, create a parallel build
directory named after your CPU architecture (e.g. x86\_64) and then run
the configure script with the appropriate options for installing on a
Fedora system with all experimental features enabled.

The `chmake` alias will then perform the build (with build messages
suppressed except on warning or error) as well as build and run tests.

Finally, assuming you have sudo privilege, you can run the `sssinstall`
alias to install this debug build onto the build machine.

``` {.wiki}
sssinstall && echo build install successful
```

You can also directly build **rpm packages** for Fedora or CentOS using
make target *rpms* or *prerelease-rpms*. The second version will create
rpm packages with date and git hash in package release.

``` {.wiki}
make rpms
#snip
Wrote: /dev/shm/gcc/rpmbuild/RPMS/x86_64/sssd-libwbclient-1.13.90-0.fc23.x86_64.rpm
Wrote: /dev/shm/gcc/rpmbuild/RPMS/x86_64/sssd-libwbclient-devel-1.13.90-0.fc23.x86_64.rpm
Wrote: /dev/shm/gcc/rpmbuild/RPMS/x86_64/sssd-debuginfo-1.13.90-0.fc23.x86_64.rpm
Executing(%clean): /bin/sh -e /var/tmp/rpm-tmp.jeWpr7
+ umask 022
+ cd /dev/shm/gcc/rpmbuild/BUILD
+ cd sssd-1.13.90
+ rm -rf /dev/shm/gcc/rpmbuild/BUILDROOT/sssd-1.13.90-0.fc23.x86_64
+ exit 0
```

To install SSSD on other distributions, you can run the usual Autotools
combo:

``` {.wiki}
autoreconf -i -f && \
./configure --enable-nsslibdir=/lib64 --enable-pammoddir=/lib64/security && \
make
sudo make install
```

To build and install the code. Please note that by default, the
Autotools install prefix is `/usr/local`. Also, if you are building and
installing on a 32bit machine, you should use `/lib/` instead of
`/lib64` for `nsslibdir` and `pammoddir`. Please note that even if you
are installing to `/usr/local`, the NSS and PAM libraries must be
installed to system library directories as that's where NSS and PAM
would be looking for them.

### Useful Tips and information for developers {#UsefulTipsandinformationfordevelopers}

There is a [dedicated
page](https://docs.pagure.org/sssd-test2/DevelTips.html){.wiki} that
contains a collection of tips that are useful for developers. The
[[​]{.icon}SSSD Internals
page](https://docs.pagure.org/sssd-test2/InternalsDocs.html){.ext-link}
is useful to become more familiar with SSSD terminology, components, and
flow between processes.

### COPR Repository {#COPRRepository}

You can download development packages from
[[​]{.icon}COPR](https://copr.fedoraproject.org/coprs/){.ext-link} repo:

-   [[​]{.icon}https://copr.fedorainfracloud.org/groups/g/sssd/coprs/](https://copr.fedorainfracloud.org/groups/g/sssd/coprs/){.ext-link}

Sending patch to upstream {#Sendingpatchtoupstream}
-------------------------

### Coding Style {#CodingStyle}

We have adopted the code style and formatting specification used by the
FreeIPA project to describe our
[[​]{.icon}Python](http://www.freeipa.org/page/Python_Coding_Style){.ext-link}
coding style. For C language we also used [[​]{.icon}FreeIPA C
style](http://www.freeipa.org/page/Coding_Style){.ext-link} but this
style is currently outdated and a [new updated C style
guide](http://fedorahosted.org/sssd/wiki/CodingStyle) was written for
SSSD.

### Submitting {#Submitting}

Make your changes and then add any new or modified files to a change-set
with the command:

``` {.wiki}
git add <path_to_file1> <path_to_file2> ...
git commit
```

Before submitting a patch, always make sure it [[​]{.icon}doesn't break
SSSD
tests](https://docs.pagure.org/sssd-test2/Contribute.html#Runningintegrationtestslocally){.ext-link}
and applies to the latest upstream master branch. You will want to
rebase to this branch and fix any merge conflicts (in case someone else
changed the same code).

``` {.wiki}
git remote update
git rebase -i origin/master
```

If this rebase has a merge conflict, you will need to resolve the
conflict before you continue. If you get stuck or make a mistake, you
can use

``` {.wiki}
git rebase --abort
```

This will put you right back where you started.

Patches should be split so that every logical change in the large
patchset is contained in its own patch. An example of this is
[[​]{.icon}SSSD Ticket
\#2789](https://fedorahosted.org/sssd/ticket/2789){.ext-link} where one
patch makes the resolv\_is\_address() function public with tests and the
other adds the function in the SSSD providers.

Once your changes are ready for submission, submit it via a
[[​]{.icon}github pull
request](https://docs.pagure.org/sssd-test2/GithubWorkflow.html){.ext-link}.

If a patch isn't accepted on the first review, you will need to modify
it and resubmit it. When this happens, you will want to amend your
changes to the existing patch with

``` {.wiki}
git add <files>
git commit --amend
```

If you need to make changes to earlier patches in your tree, you can use

``` {.wiki}
git rebase -i origin/master
```

and follow the directions in the interactive rebase to modify specific
patches.

Then just re-push the patches to github, the pull request will be
refreshed automatically.

### Patch metadata {#Patchmetadata}

The description associated with the patch is an important piece of
information that allows other developers or users to see what the change
was about, what bug did the commit fix or what feature did the commit
implement. To structure the information many SSSD developers use the
following format:

-   one-line short description
-   blank line
-   ticket or bugzilla URL (if available)
-   blank line
-   One or more paragraphs that describe the change if it can't be
    described fully in the one-line description

These best practices are loosely based on the [[​]{.icon}kernel patch
submission
recommendation](http://www.kernel.org/doc/Documentation/SubmittingPatches){.ext-link}.

An example of a patch formatted according to the above guidelines is
commit
[cbee11e912bb391ba254b0bac8c1159c1f634533](https://fedorahosted.org/sssd/changeset/cbee11e912bb391ba254b0bac8c1159c1f634533/ "sssctl: Flags for command initialization

Allow passing flags for command ..."){.changeset}:

``` {.wiki}
sssctl: Flags for command initialization

Allow passing flags for command specific initialization. Currently
only one flag is available to skip the confdb initialization which is
required to improve config-check command.

Resolves:
https://fedorahosted.org/sssd/ticket/3209
```

### Unit tests {#Unittests}

It is preferred if a patch comes together with a unit test. SSSD uses
the [[​]{.icon}cmocka](http://cmocka.org/){.ext-link} library for
developing unit tests, although some older tests still use the
[[​]{.icon}check framework](http://check.sourceforge.net/){.ext-link}.
For an introduction to cmocka, see either the examples in the
`src/tests/cmocka` directory or read the [[​]{.icon}lwn article on
cmocka](https://lwn.net/Articles/558106/){.ext-link}.

#### Running integration tests (locally) {#Runningintegrationtestslocally}

The easiest way to run the integration tests is by running:

``` {.wiki}
make intgcheck
```

Running the complete suite of tests may be overkill for debugging.
Running individual tests from the suite can be done according to the
following examples:

``` {.wiki}
INTGCHECK_PYTEST_ARGS="-k test_netgroup.py" make intgcheck-run
INTGCHECK_PYTEST_ARGS="test_netgroup.py -k test_add_empty_netgroup" make intgcheck-run
```

The INTGCHECK\_PYTEST\_ARGS format can be checked in the
[[​]{.icon}PyTest official
documentation](http://doc.pytest.org/en/latest/contents.html){.ext-link}.

### Localization and Internationalization {#LocalizationandInternationalization}

Our development policy for the SSSD requires that any code that
generates a user-facing message should be wrapped by GNU `gettext`
macros so that they can eventually be translated. We use
[[​]{.icon}zanata](http://zanata.org/){.ext-link} for translating.

Latest Documentation and Presentations {#LatestDocumentationandPresentations}
======================================

There is a dedicated page where we keep our documentation.

-   [Documentation](https://docs.pagure.org/sssd-test2/Documentation.html){.wiki}

