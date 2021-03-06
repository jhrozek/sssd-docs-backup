.. raw:: html

   <div class="wiki-toc">

#. `How to file a useful SSSD bug
   report <#HowtofileausefulSSSDbugreport>`__

   #. `Where to file the bugs? <#Wheretofilethebugs>`__
   #. `Help us reproduce the bug <#Helpusreproducethebug>`__
   #. `Include necessary debugging
      data <#Includenecessarydebuggingdata>`__

      #. `Providing SSSD crash data <#ProvidingSSSDcrashdata>`__
      #. `Mind your privacy <#Mindyourprivacy>`__

   #. `Always test the latest available
      version <#Alwaystestthelatestavailableversion>`__
   #. `Consider if the bug has security
      consequences <#Considerifthebughassecurityconsequences>`__

.. raw:: html

   </div>

How to file a useful SSSD bug report
====================================

Unfortunately, SSSD is not perfect and sometimes, you might encounter a
bug. This document describes how to file an SSSD bug report or an
enhancement request. Providing accurate and well formed information
might help us find the bug and ultimately fix it. As a bug reporter, you
should work with us on pinpointing the bug - we should then work with
you on fixing the bug.

Where to file the bugs?
-----------------------

You'll need a `​Fedora Account
System <https://admin.fedoraproject.org/accounts/>`__ login to file a
bug. When you have one, navigate to `​the new ticket
form <https://fedorahosted.org/sssd/newticket>`__.

Some bugs will be automatically cloned from distribution bug-trackers,
such as ​\ `​http://bugzilla.redhat.com <http://bugzilla.redhat.com>`__.
People working with upstream code should file bugs directly in Trac.

Help us reproduce the bug
-------------------------

The easier for us is to see the flaw in our environment, the easier it
is to fix the bug. If we can't conclusively see the bug exist, it might
even be closed as NOTABUG. If the bug can't be reproduced easily,
describe your environment in detail and allow us more time to analyze
your problem.

Include necessary debugging data
--------------------------------

For both bug reports and feature requests, select the type of the ticket
to indicate if it's a bug report or an enhancement.

Always include the following data in a bug report:

-  One bug report per ticket. If you think you found multiple problems,
   file each one in a separate ticket
-  Search the ticket database for possible duplicates. If you find a
   duplicate, please add a comment saying that you encountered the
   problem as well.
-  Is this a defect or an enhancement? (Tasks should be reserved for
   internal development tasks, such as creating unit tests.)
-  Short summary. Good example is: "The LDAP provider segfaults when an
   invalid TLS certificate is specified".
-  Component. Please select the SSSD component most accurate for your
   issue. This will ensure that the default assignee is set correctly.
-  CC (optional). If there are other parties interested in a particular
   bug, please include their Fedora usernames here.
-  What platform are you on? Please provide operating system version and
   architecture.
-  The SSSD version. On an RPM-based system, you can just run
   ``rpm -q sssd``. (If the bug is in the current working tree, select
   the most recent released version.)
-  The SSSD config file. Typically this would be located at
   ``/etc/sssd/sssd.conf``
-  The SSSD log files with a high debug level Please see the
   `troubleshooting
   page <https://docs.pagure.org/sssd-test2/Troubleshooting.html>`__ on
   information on how to gather them and other required information.
   When submitting the logs, it's very helpful to remove the existing
   log files before running the test case. This ensures the logs only
   capture the problem and developers don't need to weed out gigabytes
   of info.
-  The steps to reproduce the bug. It's very useful to log the times of
   the commands that reproduce the bug as you execute them. For
   instance, if two ``id`` commands run in sequence would give different
   information for the admin user, please run them like this:

   .. code:: wiki

           $ date; id admin; date; id admin; date

   This would help us cross-link your actions with the log files.

-  Describe your network topology and the server types and versions.
   This is especially important in complex setups with trusted IPA or
   Active Directory domains.
-  What are the results you expect? What were the results you see
   instead? Please be specific. A bad example is "My logins are slow". A
   much better example is "When a user who is a member of 100 groups
   logs in, his login takes 50 seconds even though a ``kinit`` and
   ``id -G`` for the same user are fast."

Some data in the SSSD tickets are handled by the SSSD team members.
Please leave Priority, Milestone, Keywords and Assignee to their
defaults.

Providing SSSD crash data
~~~~~~~~~~~~~~~~~~~~~~~~~

In addition to the data described above, please also provide the
coredump and backtrace along with the bug report.

If you are on a Fedora or RHEL system, abrt is a great tool for
gathering crash info. If abrt is not available, you can retrieve the
core file and backtrace manually. First, find out which sssd process is
crashing. Please always make sure you have the exact matching debuginfo
package version on your system. On Fedora and RHEL, you can easily
install the debuginfo packages with ``debuginfo-install sssd``. Then,
connect to the faulty process with gdb and resume it:

.. code:: wiki

        # gdb program $(pidof sssd_be)
        (gdb) continue

When the program crashes, save the core file and backtrace:

.. code:: wiki

        (gdb) generate-core-file
        Saved corefile core.7336
        (gdb) bt full
        # lots of output, copy and paste to the bug report

Then attach the core file and the backtrace.

Mind your privacy
~~~~~~~~~~~~~~~~~

Both the SSSD log files and the coredumps might include confidential
information. If you don't like them to be exposed in the SSSD Trac
instance, please contact some of the SSSD developers on the ``#sssd``
channel on FreeNode or on the
`​sssd-users <https://lists.fedorahosted.org/mailman/listinfo/sssd-users>`__
mailing list.

Always test the latest available version
----------------------------------------

SSSD moves at a rapid pace. It's not useful to file a bug report against
an old version, please upgrade to the latest release in the branch
you're running, if the branch is still active. You can find the tarballs
on our `releases
page <https://docs.pagure.org/sssd-test2/Releases.html>`__. If you're
running an Enterprise or Long-Term-Maintenance distribution and can't
update to a newer version, consider filing a bug report in your
distribution bug tracker instead.

Alternatively, ask on the ``#sssd`` channel on FreeNode. Several SSSD or
FreeIPA developers maintain private repositories with custom builds for
stable platforms.

Consider if the bug has security consequences
---------------------------------------------

If you think you found a bug that has security impact (allows an
unprivileged user to take down SSSD or elevate privileges for instance),
**don't** file the bug in a public bug tracker. Instead, e-mail any of
the SSSD developers instead.
