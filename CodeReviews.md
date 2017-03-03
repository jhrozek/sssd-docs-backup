<div class="wiki-toc">

1.  1.  [Code Reviews](#CodeReviews)
        1.  [Configuring a development
            tree](#Configuringadevelopmenttree)
        2.  [Creating a code-review: The Automated
            Way](#Creatingacode-review:TheAutomatedWay)
            1.  [Troubleshooting](#Troubleshooting)
        3.  [Creating a code-review: The Manual
            Way](#Creatingacode-review:TheManualWay)
    2.  [Performing Reviews](#PerformingReviews)
        1.  [First Steps](#FirstSteps)
        2.  [Performing a review](#Performingareview)

</div>

Code Reviews {#CodeReviews}
------------

Code reviews in the SSSD are managed through the Fedora Hosted
[[​]{.icon}ReviewBoard](https://fedorahosted.org/reviewboard){.ext-link}
instance. To submit a code review, you will need a Fedora Account System
user account. This is the same account that you use for the SSSD wiki
and ticket tracker. If you do not yet have an account, please sign up
for one at
[[​]{.icon}FAS](https://fedorahosted.org/accounts){.ext-link}.

### Configuring a development tree {#Configuringadevelopmenttree}

1.  Check out the source repository, if you haven't already done so.

    ``` {.wiki}
    git clone https://pagure.io/SSSD/sssd.git
    ```

2.  In the SSSD source checkout, run the following command to set the
    location of the ReviewBoard server:

    ``` {.wiki}
    git config reviewboard.url https://fedorahosted.org/reviewboard/
    ```

### Creating a code-review: The Automated Way {#Creatingacode-review:TheAutomatedWay}

1.  Create a new git branch, based off of the head of the upstream
    master (or branch). For purposes of illustration, I will assume this
    branch will be named 'review', and that the upstream repository is
    'origin'

    ``` {.wiki}
    git checkout -b review origin/master
    ```

2.  On this new branch, use `git cherry-pick` or `git am` to apply the
    series of one or more patches you want to submit for review. Fix any
    merge conflicts.
3.  Verify with `git log` that you have the correct set of patches
    applied.
4.  From the root of the SSSD source checkout (or the root \$builddir if
    you are building in a parallel tree), run this command:

    ``` {.wiki}
    make review
    ```

5.  You may be prompted for your username and password. This is your
    Fedora Account System name and password, the same as you would use
    for filing bugs in Trac.
6.  Generating the review may take some time (for large patches or many
    patches, this may even be minutes).
7.  The tool will output several HTTP links, one per review that has
    been created. You should go to the ReviewBoard server and verify
    that the patches were submitted properly, and then publish the
    review for all to see.
    1.  Log into the ReviewBoard web interface at
        [[​]{.icon}https://fedorahosted.org/sssd/](https://fedorahosted.org/sssd/){.ext-link}
    2.  Click on `All My Requests`
    3.  Review each patch marked "Draft" in that list. Make sure to
        check `View Diff`.
    4.  The `Summary`, `Description` and `Reviewers` should be
        automatically set.
    5.  If you would prefer to have a particular reviewer, add them to
        the list.
    6.  If the change is related to one or more tickets in Trac, enter
        the number(s) into the `Bugs` field. ReviewBoard will
        automatically convert that to a link.
    7.  If the change is intended for a branch instead of master,
        specify it in the `Branch` field.
    8.  Publish the review (or discard it if something went wrong)

#### Troubleshooting {#Troubleshooting}

-   If you see:

    ``` {.wiki}
    The repository path "sgallagh@fedorapeople.org:public_git/sssd.git" is not in the
    list of known repositories on the server.
    ```

This means you did not properly create the branch to generate the review
requests from. This branch must be based off of the upstream master (or
branch). Chances are, the branch you're trying to commit is based off of
a private git repo branch like Fedora People.

-   If you see:

    ``` {.wiki}
    'The repository path "https://pagure.io/SSSD/sssd.git" is not in the list of known repositories on the server.'
    ```

This means you have your remote repo configured to use the alias for the
SSSD repo instead of the proper full path. You will want to do edit your
.git/config file and edit the URL for this repo to be
`https://pagure.io/SSSD/sssd.git`

### Creating a code-review: The Manual Way {#Creatingacode-review:TheManualWay}

*Note: These instructions apply only to single-patch changes. For
multiple patch sets, it is VASTLY easier to follow `The Automated Way`.
The post-review tool included in the contrib/ directory handles the
necessary magic to produce parent diffs in ReviewBoard*

1.  Generate the patch to be submitted using the following command:

    ``` {.wiki}
    git format-patch --full-index -1
    ```

2.  Log into the ReviewBoard web interface at
    [[​]{.icon}https://fedorahosted.org/reviewboard/](https://fedorahosted.org/reviewboard/){.ext-link}
3.  Click on `New Review Request` in the navigation bar.
4.  In the `Repository` drop-down menu, select `sssd`
5.  `Browse...` to your patch
6.  Click `Create Review Request`
7.  Enter the `Summary` and `Description` fields and click "OK"
8.  If you would prefer to have a particular reviewer, add them to the
    list.
9.  If the change is related to one or more tickets in Trac, enter the
    number(s) into the `Bugs` field. ReviewBoard will automatically
    convert that to a link.
10. If the change is intended for a branch instead of master, specify it
    in the `Branch` field.
11. Publish the review (or discard it if something went wrong)

Performing Reviews {#PerformingReviews}
------------------

### First Steps {#FirstSteps}

1.  Add yourself to the SSSD Review Group.
    1.  Click on `My account` in the upper-right corner.
    2.  Check the box labeled `SSSD Review Group`
    3.  Click `Save Preferences`

### Performing a review {#Performingareview}

1.  Log into the ReviewBoard instance at
    [[​]{.icon}https://fedorahosted.org/reviewboard/](https://fedorahosted.org/reviewboard/){.ext-link}
2.  Click on `sssd` under `Incoming Reviews` in the dashboard. This will
    show you the list of pending reviews for the SSSD.
3.  Click on a pending review to see its details.
4.  Click on `View Diff` tab to see a side-by-side diff.
5.  You can click on any line number in the diff to make a comment, or
    drag-select to make a comment on multiple lines at once.
6.  Comments are not published when you click 'OK', they are queued and
    published all at once when you click on `Publish`
7.  To make a comment on the patch as a whole, or to approve the chance,
    click on the `Review` tab. Making comments here behaves like making
    comments on lines.
8.  Clicking "Ship It" marks your approval for this patch. (Similar to
    sending "Ack" to the email list)

