.. raw:: html

   <div class="wiki-toc">

#. `Contribute <#Contribute>`__

   #. `Contribution Policy <#ContributionPolicy>`__
   #. `Source Code Repository <#SourceCodeRepository>`__
   #. `Tasks for newcomers <#Tasksfornewcomers>`__

      #. `Getting the source <#Gettingthesource>`__

   #. `Building SSSD <#BuildingSSSD>`__

      #. `Useful Tips and information for
         developers <#UsefulTipsandinformationfordevelopers>`__
      #. `COPR Repository <#COPRRepository>`__

   #. `Sending patch to upstream <#Sendingpatchtoupstream>`__

      #. `Coding Style <#CodingStyle>`__
      #. `Submitting <#Submitting>`__
      #. `Patch metadata <#Patchmetadata>`__
      #. `Unit tests <#Unittests>`__

         #. `Running integration tests
            (locally) <#Runningintegrationtestslocally>`__

      #. `Localization and
         Internationalization <#LocalizationandInternationalization>`__

#. `Latest Documentation and
   Presentations <#LatestDocumentationandPresentations>`__

.. raw:: html

   </div>

Contribute
==========

There are many ways you can contribute to the System Security Services
Daemon. This page should provide some basic pointers.

SSSD development discussions occur either on the `​SSSD development
list <https://fedorahosted.org/mailman/listinfo/sssd-devel>`__ or on the
`​#sssd IRC channel <irc://irc.freenode.net/sssd>`__ on
`​freenode <http://freenode.net/>`__. Keep in mind that SSSD developers
are spread across different time zones, which makes mailing list
preferred communication channel if you wish to reach the entire team.

The SSSD originated as a sister-project to
`​FreeIPA <http://www.freeipa.org>`__, so we share many pieces.
Contributing to FreeIPA may also help SSSD and vice versa.

If you want to file a bug or enhancement request, please log in with
your Fedora Account System credentials. If you do not have a Fedora
Account, you can register for one at
`​https://admin.fedoraproject.org/accounts/ <https://admin.fedoraproject.org/accounts/>`__.
There is dedicated page about `​bug
reporting <https://docs.pagure.org/sssd-test2/Reporting_sssd_bugs.html>`__.

Contribution Policy
-------------------

All source code committed to the SSSD is assumed to be made available
under the GPLv3+ license unless the submitter specifies another license
at that time. The upstream SSSD maintainers reserve the right to refuse
a submission if the license is deemed incompatible with the goals of the
project.

Source Code Repository
----------------------

For the SSSD project, we use the
`​Git <http://www.kernel.org/pub/software/scm/git/docs/gittutorial.html>`__
source control system.

.. code:: wiki

    https://pagure.io/SSSD/sssd.git

Tasks for newcomers
-------------------

We try to mark tickets that don't require too much existing knowledge
with the ``easyfix`` keyword in Trac. We also prepared `​a Trac
query <https://fedorahosted.org/sssd/report/34>`__ that lists the easy
fixes. Before starting the work on any of these tickets, it might be a
good idea to contact the SSSD developers on the `​sssd-devel
list <https://lists.fedorahosted.org/archives/list/sssd-devel@lists.fedorahosted.org/>`__
and check if the ticket is still valid or ask for guidance in general.

Getting the source
~~~~~~~~~~~~~~~~~~

To check out the latest SSSD sources, install git on your system
(Instructions are for Fedora, you may need to use a platform-specific
installation mechanism for other OSes).

.. code:: wiki

    sudo dnf -y install git

You can find an excellent
`​tutorial <http://www.kernel.org/pub/software/scm/git/docs/gittutorial.html>`__
for using git.

The first time, you will want to configure git with your name and email
address for patch attribution:

.. code:: wiki

    git config --global user.name "GIVENNAME SURNAME"
    git config --global user.email "username@domain.com"

You can enable syntax highlighting at the console (for git commands such
as '``git status``' and '``git diff``') by setting:

.. code:: wiki

    git config --global color.ui auto

And if you would like to have a graphical tool for resolving merge
conflicts, you can install and set up meld:

.. code:: wiki

    sudo dnf -y install meld

.. code:: wiki

    git config --global merge.tool meld

It can be invoked with

.. code:: wiki

    git mergetool

You can also enable the commit template by:

.. code:: wiki

    git config commit.template .git-commit-template

Once that's done, you can clone our upstream git repository with

.. code:: wiki

    git clone https://pagure.io/SSSD/sssd.git

This will create a new subdirectory 'sssd' in the current directory
which will contain the current master sources. All development should be
done first against the master branch, then backported to one of the
stable branches if necessary.

Building SSSD
-------------

Starting with SSSD 1.10 beta, we now include a set of helper aliases and
environment variables in SSSD to simplify building development versions
of SSSD on Fedora. To take advantage of them, use the following command:

.. code:: wiki

    . /path/to/sssd-source/contrib/fedora/bashrc_sssd

To build SSSD from source, follow these steps:

#. Install necessary tools

   .. code:: wiki

       # when using yum
       sudo yum -y install rpm-build yum-utils libldb-devel

       # when using dnf
       sudo dnf -y install rpm-build dnf-plugins-core libldb-devel

2. Create source rpm (run from git root directory)

   .. code:: wiki

       contrib/fedora/make_srpm.sh

3. Install SSSD dependencies

   .. code:: wiki

       # when using yum
       sudo yum-builddep rpmbuild/SRPMS/sssd-*.src.rpm

       # when using dnf
       sudo dnf builddep rpmbuild/SRPMS/sssd-*.src.rpm

If you plan on working with the SSSD source often, you may want to add
the following to your ``~/.bashrc`` file:

.. code:: wiki

    if [ -f /path/to/sssd-source/contrib/fedora/bashrc_sssd ]; then
        . /path/to/sssd-source/contrib/fedora/bashrc_sssd
    fi

You can now produce a Debug build of SSSD by running:

.. code:: wiki

    cd /path/to/sssd-source
    reconfig && chmake

The ``reconfig`` alias will run ``autoreconf -if``, create a parallel
build directory named after your CPU architecture (e.g. x86\_64) and
then run the configure script with the appropriate options for
installing on a Fedora system with all experimental features enabled.

The ``chmake`` alias will then perform the build (with build messages
suppressed except on warning or error) as well as build and run tests.

Finally, assuming you have sudo privilege, you can run the
``sssinstall`` alias to install this debug build onto the build machine.

.. code:: wiki

    sssinstall && echo build install successful

You can also directly build **rpm packages** for Fedora or CentOS using
make target *rpms* or *prerelease-rpms*. The second version will create
rpm packages with date and git hash in package release.

.. code:: wiki

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

To install SSSD on other distributions, you can run the usual Autotools
combo:

.. code:: wiki

    autoreconf -i -f && \
    ./configure --enable-nsslibdir=/lib64 --enable-pammoddir=/lib64/security && \
    make
    sudo make install

To build and install the code. Please note that by default, the
Autotools install prefix is ``/usr/local``. Also, if you are building
and installing on a 32bit machine, you should use ``/lib/`` instead of
``/lib64`` for ``nsslibdir`` and ``pammoddir``. Please note that even if
you are installing to ``/usr/local``, the NSS and PAM libraries must be
installed to system library directories as that's where NSS and PAM
would be looking for them.

Useful Tips and information for developers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There is a `dedicated
page <https://docs.pagure.org/sssd-test2/DevelTips.html>`__ that
contains a collection of tips that are useful for developers. The `​SSSD
Internals
page <https://docs.pagure.org/sssd-test2/InternalsDocs.html>`__ is
useful to become more familiar with SSSD terminology, components, and
flow between processes.

COPR Repository
~~~~~~~~~~~~~~~

You can download development packages from
`​COPR <https://copr.fedoraproject.org/coprs/>`__ repo:

-  `​https://copr.fedorainfracloud.org/groups/g/sssd/coprs/ <https://copr.fedorainfracloud.org/groups/g/sssd/coprs/>`__

Sending patch to upstream
-------------------------

Coding Style
~~~~~~~~~~~~

We have adopted the code style and formatting specification used by the
FreeIPA project to describe our
`​Python <http://www.freeipa.org/page/Python_Coding_Style>`__ coding
style. For C language we also used `​FreeIPA C
style <http://www.freeipa.org/page/Coding_Style>`__ but this style is
currently outdated and a `new updated C style
guide <http://fedorahosted.org/sssd/wiki/CodingStyle>`__ was written for
SSSD.

Submitting
~~~~~~~~~~

Make your changes and then add any new or modified files to a change-set
with the command:

.. code:: wiki

    git add <path_to_file1> <path_to_file2> ...
    git commit

Before submitting a patch, always make sure it `​doesn't break SSSD
tests <https://docs.pagure.org/sssd-test2/Contribute.html#Runningintegrationtestslocally>`__
and applies to the latest upstream master branch. You will want to
rebase to this branch and fix any merge conflicts (in case someone else
changed the same code).

.. code:: wiki

    git remote update
    git rebase -i origin/master

If this rebase has a merge conflict, you will need to resolve the
conflict before you continue. If you get stuck or make a mistake, you
can use

.. code:: wiki

    git rebase --abort

This will put you right back where you started.

Patches should be split so that every logical change in the large
patchset is contained in its own patch. An example of this is `​SSSD
Ticket #2789 <https://fedorahosted.org/sssd/ticket/2789>`__ where one
patch makes the resolv\_is\_address() function public with tests and the
other adds the function in the SSSD providers.

Once your changes are ready for submission, submit it via a `​github
pull
request <https://docs.pagure.org/sssd-test2/GithubWorkflow.html>`__.

If a patch isn't accepted on the first review, you will need to modify
it and resubmit it. When this happens, you will want to amend your
changes to the existing patch with

.. code:: wiki

    git add <files>
    git commit --amend

If you need to make changes to earlier patches in your tree, you can use

.. code:: wiki

    git rebase -i origin/master

and follow the directions in the interactive rebase to modify specific
patches.

Then just re-push the patches to github, the pull request will be
refreshed automatically.

Patch metadata
~~~~~~~~~~~~~~

The description associated with the patch is an important piece of
information that allows other developers or users to see what the change
was about, what bug did the commit fix or what feature did the commit
implement. To structure the information many SSSD developers use the
following format:

-  one-line short description
-  blank line
-  ticket or bugzilla URL (if available)
-  blank line
-  One or more paragraphs that describe the change if it can't be
   described fully in the one-line description

These best practices are loosely based on the `​kernel patch submission
recommendation <http://www.kernel.org/doc/Documentation/SubmittingPatches>`__.

An example of a patch formatted according to the above guidelines is
commit
`cbee11e912bb391ba254b0bac8c1159c1f634533 <https://fedorahosted.org/sssd/changeset/cbee11e912bb391ba254b0bac8c1159c1f634533/>`__:

.. code:: wiki

    sssctl: Flags for command initialization

    Allow passing flags for command specific initialization. Currently
    only one flag is available to skip the confdb initialization which is
    required to improve config-check command.

    Resolves:
    https://fedorahosted.org/sssd/ticket/3209

Unit tests
~~~~~~~~~~

It is preferred if a patch comes together with a unit test. SSSD uses
the `​cmocka <http://cmocka.org/>`__ library for developing unit tests,
although some older tests still use the `​check
framework <http://check.sourceforge.net/>`__. For an introduction to
cmocka, see either the examples in the ``src/tests/cmocka`` directory or
read the `​lwn article on cmocka <https://lwn.net/Articles/558106/>`__.

Running integration tests (locally)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The easiest way to run the integration tests is by running:

.. code:: wiki

    make intgcheck

Running the complete suite of tests may be overkill for debugging.
Running individual tests from the suite can be done according to the
following examples:

.. code:: wiki

    INTGCHECK_PYTEST_ARGS="-k test_netgroup.py" make intgcheck-run
    INTGCHECK_PYTEST_ARGS="test_netgroup.py -k test_add_empty_netgroup" make intgcheck-run

The INTGCHECK\_PYTEST\_ARGS format can be checked in the `​PyTest
official
documentation <http://doc.pytest.org/en/latest/contents.html>`__.

Localization and Internationalization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Our development policy for the SSSD requires that any code that
generates a user-facing message should be wrapped by GNU ``gettext``
macros so that they can eventually be translated. We use
`​zanata <http://zanata.org/>`__ for translating.

Latest Documentation and Presentations
======================================

There is a dedicated page where we keep our documentation.

-  `Documentation <https://docs.pagure.org/sssd-test2/Documentation.html>`__
