SSSD github workflow
--------------------

This page describes how to submit, review and push pull requests from
github.

A quick overwiew
~~~~~~~~~~~~~~~~

Github pull requests are the preferred way of handling code submissions
to SSSD. If, for some reason you prefer to not use github, you can also
e-mail your patch as an attachment to the
`​sssd-devel <https://lists.fedorahosted.org/archives/list/sssd-devel%40lists.fedorahosted.org/>`__
mailing list.

However, we still keep our code in the fedorahosted repository and we
never merge pull requests, but push them directly to the fedorahosted
repo in order to keep our history linear. The fedorahosted repo is
automatically mirrored to github after every push using a
fedorahosted.org plugin.

All pull request activity also generates an e-mail notification to the
sssd-devel mailing list so that we keep the development history outside
github.

Tip: the ``hub`` command-line tool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The `​hub <https://github.com/github/hub>`__ tool provides a nice way of
interacting with github from the command line. You can even alias
``hub`` as ``git`` and use the same commands locally and against github.

Submitting a pull-request
~~~~~~~~~~~~~~~~~~~~~~~~~

To submit a pull request, create a fork of the `​sssd
repository <https://github.com/SSSD/sssd>`__ on github. Once you have
that, add your repository as a remote locally:

.. code:: wiki

        git remote add myfork git@github.com:$github_username/sssd.git

It's a good idea to add the SSSD github repo as a remote, especially if
you plan on using ``hub``:

.. code:: wiki

        git remote add github https://github.com/SSSD/sssd.git

Using ``https://`` will ensure you don't push to sssd's github repo by
mistake.

Once you're done working on your patches, push them to a feature branch
on github:

.. code:: wiki

        git push myfork mybranch

You can then open a pull request either from the `​web
ui <https://help.github.com/articles/creating-a-pull-request/>`__ or
using the hub tool:

.. code:: wiki

        hub pull-request

Reviewing a pull requests
~~~~~~~~~~~~~~~~~~~~~~~~~

The list of open pull requests can be found at
`​https://github.com/SSSD/sssd/pulls <https://github.com/SSSD/sssd/pulls>`__.
If you want to formally review a pull request, please assign the pull
request to yourself. This indicates that you'll be working with the
submitter on pushing their pull requests upstream. You don't need to
assign the pull request if you just want to add a one-time comment. The
pull-request assignee(s) will be added as ``Reviewed-By`` tags when
pushing to the ``fedorahosted.org`` repository.

To comment on the code, you can use either add a comment to the github
text field, or click on the individual commit links and add comments
inline to the diff.

If there is an issue in the code that you feel warrants a patch respin,
add the ``nack`` label to the pull request.

Once you agree with the pull request, add the ``ack`` label to the pull
request. One of the gatekeepers will then push the pull request to the
sssd repository manually.

If a pull-request is submitted by someone from outside the core team,
the CI tests won't run to make sure some potentially malicious code is
not ran on the CI nodes. To allow the code to be tested, one of the core
developers must add:

.. code:: wiki

        ok to test

as a comment to the pull request. An example of one such pull request
can be found `​here <https://github.com/SSSD/sssd/pull/35>`__.

Any github user can comment on an open github issue. However, only
collaboratos can self-assign the pull requests and add labels. If you
would like to be added as a collaborator, please send a mail to
`​sssd-devel <https://lists.fedorahosted.org/archives/list/sssd-devel%40lists.fedorahosted.org/>`__
and ask to be added.

**Pro-tips:**

-  Pressing ``l`` on the gihub request allows to set labels without
   reaching for the mouse. You can also set assignee by pressing ``a``.
-  You can add pull requests as refs and add check them out as branches
   locally. To do that, add another ``fetch`` directive to your github
   remote definition using ``git config``.

   .. code:: wiki

           GITHUB_REMOTE="github"
           git config --add remote.$GITHUB_REMOTE.fetch "+refs/pull/*/head:refs/remotes/$GITHUB_REMOTE/pull/*"

Then you can fetch and checkout the pull requests with git:

.. code:: wiki

        git fetch github
        git checkout -b pr7review --track github/pull/7

Pushing a pull request
~~~~~~~~~~~~~~~~~~~~~~

Only pull requests with an ``ack`` label can be pushed.

To push a patch, first apply it, for example:

.. code:: wiki

        hub am https://github.com/SSSD/sssd/pull/5

Don't forget to add the ``Reviewed-By`` tags, based on the pull request
assignee. It's recommended to use the pre-push hook from
``contrib/git/pre-push`` that rejects any pushes without a
``Reviewed-By`` tag.

Then check again what patches would be pushed:

.. code:: wiki

        git push -n origin master

And if the hashes look OK, finally push the patches:

.. code:: wiki

        git push origin master

Finally, add the commit hashes to the pull request page, add the label
``pushed`` and close the pull request.
