.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Code Reviews <#CodeReviews>`__

      #. `Configuring a development
         tree <#Configuringadevelopmenttree>`__
      #. `Creating a code-review: The Automated
         Way <#Creatingacode-review:TheAutomatedWay>`__

         #. `Troubleshooting <#Troubleshooting>`__

      #. `Creating a code-review: The Manual
         Way <#Creatingacode-review:TheManualWay>`__

   #. `Performing Reviews <#PerformingReviews>`__

      #. `First Steps <#FirstSteps>`__
      #. `Performing a review <#Performingareview>`__

.. raw:: html

   </div>

Code Reviews
------------

Code reviews in the SSSD are managed through the Fedora Hosted
`​ReviewBoard <https://fedorahosted.org/reviewboard>`__ instance. To
submit a code review, you will need a Fedora Account System user
account. This is the same account that you use for the SSSD wiki and
ticket tracker. If you do not yet have an account, please sign up for
one at `​FAS <https://fedorahosted.org/accounts>`__.

Configuring a development tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Check out the source repository, if you haven't already done so.

   .. code:: wiki

       git clone https://pagure.io/SSSD/sssd.git

#. In the SSSD source checkout, run the following command to set the
   location of the ReviewBoard server:

   .. code:: wiki

       git config reviewboard.url https://fedorahosted.org/reviewboard/

Creating a code-review: The Automated Way
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Create a new git branch, based off of the head of the upstream master
   (or branch). For purposes of illustration, I will assume this branch
   will be named 'review', and that the upstream repository is 'origin'

   .. code:: wiki

       git checkout -b review origin/master

#. On this new branch, use ``git cherry-pick`` or ``git am`` to apply
   the series of one or more patches you want to submit for review. Fix
   any merge conflicts.
#. Verify with ``git log`` that you have the correct set of patches
   applied.
#. From the root of the SSSD source checkout (or the root $builddir if
   you are building in a parallel tree), run this command:

   .. code:: wiki

       make review

#. You may be prompted for your username and password. This is your
   Fedora Account System name and password, the same as you would use
   for filing bugs in Trac.
#. Generating the review may take some time (for large patches or many
   patches, this may even be minutes).
#. The tool will output several HTTP links, one per review that has been
   created. You should go to the ReviewBoard server and verify that the
   patches were submitted properly, and then publish the review for all
   to see.

   #. Log into the ReviewBoard web interface at
      `​https://fedorahosted.org/sssd/ <https://fedorahosted.org/sssd/>`__
   #. Click on ``All My Requests``
   #. Review each patch marked "Draft" in that list. Make sure to check
      ``View Diff``.
   #. The ``Summary``, ``Description`` and ``Reviewers`` should be
      automatically set.
   #. If you would prefer to have a particular reviewer, add them to the
      list.
   #. If the change is related to one or more tickets in Trac, enter the
      number(s) into the ``Bugs`` field. ReviewBoard will automatically
      convert that to a link.
   #. If the change is intended for a branch instead of master, specify
      it in the ``Branch`` field.
   #. Publish the review (or discard it if something went wrong)

Troubleshooting
^^^^^^^^^^^^^^^

-  If you see:

   .. code:: wiki

       The repository path "sgallagh@fedorapeople.org:public_git/sssd.git" is not in the
       list of known repositories on the server.

This means you did not properly create the branch to generate the review
requests from. This branch must be based off of the upstream master (or
branch). Chances are, the branch you're trying to commit is based off of
a private git repo branch like Fedora People.

-  If you see:

   .. code:: wiki

       'The repository path "https://pagure.io/SSSD/sssd.git" is not in the list of known repositories on the server.'

This means you have your remote repo configured to use the alias for the
SSSD repo instead of the proper full path. You will want to do edit your
.git/config file and edit the URL for this repo to be
``https://pagure.io/SSSD/sssd.git``

Creating a code-review: The Manual Way
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Note: These instructions apply only to single-patch changes. For
multiple patch sets, it is VASTLY easier to follow
``The Automated Way``. The post-review tool included in the contrib/
directory handles the necessary magic to produce parent diffs in
ReviewBoard*

#. Generate the patch to be submitted using the following command:

   .. code:: wiki

       git format-patch --full-index -1

#. Log into the ReviewBoard web interface at
   `​https://fedorahosted.org/reviewboard/ <https://fedorahosted.org/reviewboard/>`__
#. Click on ``New Review Request`` in the navigation bar.
#. In the ``Repository`` drop-down menu, select ``sssd``
#. ``Browse...`` to your patch
#. Click ``Create Review Request``
#. Enter the ``Summary`` and ``Description`` fields and click "OK"
#. If you would prefer to have a particular reviewer, add them to the
   list.
#. If the change is related to one or more tickets in Trac, enter the
   number(s) into the ``Bugs`` field. ReviewBoard will automatically
   convert that to a link.
#. If the change is intended for a branch instead of master, specify it
   in the ``Branch`` field.
#. Publish the review (or discard it if something went wrong)

Performing Reviews
------------------

First Steps
~~~~~~~~~~~

#. Add yourself to the SSSD Review Group.

   #. Click on ``My account`` in the upper-right corner.
   #. Check the box labeled ``SSSD Review Group``
   #. Click ``Save Preferences``

Performing a review
~~~~~~~~~~~~~~~~~~~

#. Log into the ReviewBoard instance at
   `​https://fedorahosted.org/reviewboard/ <https://fedorahosted.org/reviewboard/>`__
#. Click on ``sssd`` under ``Incoming Reviews`` in the dashboard. This
   will show you the list of pending reviews for the SSSD.
#. Click on a pending review to see its details.
#. Click on ``View Diff`` tab to see a side-by-side diff.
#. You can click on any line number in the diff to make a comment, or
   drag-select to make a comment on multiple lines at once.
#. Comments are not published when you click 'OK', they are queued and
   published all at once when you click on ``Publish``
#. To make a comment on the patch as a whole, or to approve the chance,
   click on the ``Review`` tab. Making comments here behaves like making
   comments on lines.
#. Clicking "Ship It" marks your approval for this patch. (Similar to
   sending "Ack" to the email list)
