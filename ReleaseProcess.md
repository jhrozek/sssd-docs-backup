<div class="wiki-toc">

1.  1.  [Release Process for SSSD](#ReleaseProcessforSSSD)
        1.  [Pre-requisites](#Pre-requisites)
        2.  [Prepare the sources](#Preparethesources)
            1.  [Special Beta or Pre-release
                rules](#SpecialBetaorPre-releaserules)
        3.  [Tag and sign the release](#Tagandsigntherelease)
            1.  [Special Beta or Pre-release
                rules](#SpecialBetaorPre-releaserules1)
        4.  [Generate HTML manpages](#GenerateHTMLmanpages)
        5.  [Create a release tarball](#Createareleasetarball)
            1.  [Special Beta or Pre-release
                rules](#SpecialBetaorPre-releaserules2)
        6.  [Prepare the branch for the next
            version](#Preparethebranchforthenextversion)
            1.  [Special-case: branching off master to track the next
                major
                version](#Special-case:branchingoffmastertotrackthenextmajorversion)
        7.  [Upload the tarball to
            Fedorahosted.org](#UploadthetarballtoFedorahosted.org)
        8.  [Update the SSSD Release Page](#UpdatetheSSSDReleasePage)
            1.  [Special-case: final release after multiple preview
                releases](#Special-case:finalreleaseaftermultiplepreviewreleases)
        9.  [Update the Trac milestones and
            versions](#UpdatetheTracmilestonesandversions)
        10. [Schedule review of the SSSD's wiki pages for the next
            release](#SchedulereviewoftheSSSDswikipagesforthenextrelease)
        11. [Update the SSSD Front Page](#UpdatetheSSSDFrontPage)
        12. [Announce the release to the
            world!](#Announcethereleasetotheworld)

</div>

Release Process for SSSD {#ReleaseProcessforSSSD}
------------------------

> We will use SSSD 1.3.0 as an example. Substitute with the appropriate
> version where needed.

### Pre-requisites {#Pre-requisites}

-   Commit access to the SSSD upstream repository
-   A GPG key signed by at least two other members of the SSSD team.
-   Access to the fedorahosted.org fileserver
-   WIKI\_ADMIN privilege for the SSSD Trac instance
-   Maintainer privileges on the SSSD Zanata Instance. Follow the
    [[​]{.icon}zanata
    guide](http://zanata.org/help/cli/cli-configuration/){.ext-link} to
    set up the zanata-cli tool
-   A fresh clone of the SSSD upstream repository to work from
-   Ensure that all tickets that were closed in this release are marked
    with the appropriate resolution.
-   Perform a scratch build on all supported architectures.

### Prepare the sources {#Preparethesources}

1.  Ensure that you have the latest version of the upstream sources.
2.  Update the translation files.
    1.  In the root of SSSD checkout, pull new translations from zanata
        with

        ``` {.wiki}
        zanata-cli pull -s . -t .
        ```

    2.  If new translations have been added to the main translations
        (`po/*.po`), add the new language to `po/LINGUAS`. Please keep
        them in English alphabetical order.
    3.  If new translations have been added to the manpage translations
        (`src/man/po/*.po`), add the new language to
        `src/man/po/po4a.cfg`. Please keep them in English alphabetical
        order.
    4.  Run
        `autoreconf -if && ./configure && make update-po && make distcheck`
        from the root
    5.  Check `git status` for changes to `*.po` or `*.pot` files.

3.  Commit the new `.po[t]` files.
4.  Push the changes.

#### Special Beta or Pre-release rules {#SpecialBetaorPre-releaserules}

1.  For the benefit of translators, push any new strings up to Zanata
    whenever we make a pre-release tarball

    ``` {.wiki}
    zanata-cli push -s .
    ```

2.  If this is is the last pre-release (e.g. final beta before
    bugfix-only phase) String Freeze should be announced on the
    sssd-devel list and the Zanata site.

### Tag and sign the release {#Tagandsigntherelease}

1.  Tag the release and sign it with your GPG key

    ``` {.wiki}
    git tag -s sssd-1_3_0
    ```

2.  Push the tag. Pus the tag explictly instead of using --tags so that
    you do not push extraneous tags by mistake.

    ``` {.wiki}
    git push origin sssd-1_3_0
    ```

#### Special Beta or Pre-release rules {#SpecialBetaorPre-releaserules1}

When tagging a beta or release candidate, the sources should be tagged
twice. Once for the pure numeric value and once for the human-friendly
value. So for example, if we are tagging SSSD 1.9.0 beta 2, we should
do:

``` {.wiki}
git tag -s sssd-1_8_92
git tag -s sssd-1_9_0_beta2
```

Followed by

``` {.wiki}
git push --tags
```

### Generate HTML manpages {#GenerateHTMLmanpages}

-   Use the attached perl script to produce XHTML-formatted manpages.

    ``` {.wiki}
    perl make-xhtml.pl /path/to/xml /path/to/output
    ```

-   Upload these manpages to public space (for example, FedoraPeople
    space)
-   Link to these files when creating the release page entry.

### Create a release tarball {#Createareleasetarball}

1.  Run `scripts/release.sh` from the root directory of the source
    checkout
    -   This will create two files, `sssd-1.3.0.tar.gz` and
        `sssd-1.3.0.tar.gz.asc`
2.  Create an md5sum and a sha1sum of the tarball

    ``` {.wiki}
    md5sum sssd-1.3.0.tar.gz > sssd-1.3.0.tar.gz.md5sum
    sha1sum sssd-1.3.0.tar.gz > sssd-1.3.0.tar.gz.sha1sum
    ```

#### Special Beta or Pre-release rules {#SpecialBetaorPre-releaserules2}

When creating a tarball for a beta or a release candidate, the resulting
tarball should be renamed appropriately. To use the 1.9.0 beta 2
example:

``` {.wiki}
mv sssd-1.8.92.tar.gz sssd-1.9.0beta2.tar.gz
mv sssd-1.8.92.tar.gz.asc sssd-1.9.0beta2.tar.gz.asc
```

### Prepare the branch for the next version {#Preparethebranchforthenextversion}

1.  Update the version in version.m4 to the next point release (e.g.
    1.3.1)
    -   Only update the version to a final release (like 1.9.0) right
        before releasing the final version. Bumping the version to final
        sooner would prevent us from being able to release another
        pre-release..
2.  Push this new version

    ``` {.wiki}
    git push
    ```

#### Special-case: branching off master to track the next major version {#Special-case:branchingoffmastertotrackthenextmajorversion}

1.  As an example, we will branch off `sssd-1-3` and let master track
    the development of sssd 1.4
2.  Create a stable branch from master

    ``` {.wiki}
        git checkout -b sssd-1-3
        git push -n origin sssd-1-3
        # verify everything looks sane
        git push origin sssd-1-3
    ```

3.  Switch back to the master branch
4.  On master, update the version in version.m4 to the next point
    release (e.g. `1.3.90`)
5.  Push this new version

    ``` {.wiki}
        git push -n origin master
        # verify everything looks sane
        git push origin master
    ```

### Upload the tarball to Fedorahosted.org {#UploadthetarballtoFedorahosted.org}

1.  `scp sssd-1.3.0.tar.gz fedorahosted.org:sssd`
2.  `scp sssd-1.3.0.tar.gz.asc fedorahosted.org:sssd`

### Update the [SSSD Release Page](https://docs.pagure.org/sssd-test2/Releases.html){.wiki} {#UpdatetheSSSDReleasePage}

1.  Add a line at the top of the
    [Releases](https://docs.pagure.org/sssd-test2/Releases.html){.wiki}
    page with links to
    `https://fedorahosted.org/released/sssd/sssd-1.3.0.tar.gz` and
    `https://fedorahosted.org/released/sssd/sssd-1.3.0.tar.gz.asc`
2.  Add the md5sum and sha1sum calculated above
3.  Create a release notes page (e.g.
    [Releases/Notes-1.3.0](https://docs.pagure.org/sssd-test2/Releases/Notes-1.3.0.html){.wiki}).
    This page should be marked read-only (so only WIKI\_ADMINS can
    modify it). To generate the detailed changelog:

    ``` {.wiki}
    git shortlog previoustag..newtag
    ```

4.  For each release, if any changes have occurred in packaging (a new
    directory, a new provider plugin, etc.), the release notes page
    should include a section notifying potential packagers of these
    changes. In general, this can be determined by doing (from the root
    of the git checkout):

    ``` {.wiki}
     git diff previoustag..newtag -- contrib/sssd.spec.in
    ```

5.  For each release, if any changes have occured in documentation, such
    as new options, options changing default values, the release notes
    should include a section that summarizes there changes.

    ``` {.wiki}
     git diff previoustag..newtag -- src/man
    ```

6.  Update
    [Documentation](https://docs.pagure.org/sssd-test2/Documentation.html){.wiki}
    with links to the latest manual pages and/or Deployment Guides
7.  Update
    [SecuritySensitiveOptions](https://docs.pagure.org/sssd-test2/SecuritySensitiveOptions.html){.wiki}
    if any new security-sensitive options were added

#### Special-case: final release after multiple preview releases {#Special-case:finalreleaseaftermultiplepreviewreleases}

When releasing a final version (such as 1.9.0) after multiple preview
releases, the release notes page for that final release should contain
all of the changes from the various preview release note pages. This
way, potential packagers and users do not need to examine all of the
prerelease notes.

### Update the Trac milestones and versions {#UpdatetheTracmilestonesandversions}

Actions to take in the Trac Admin pages:

1.  Mark the milestone as complete
2.  Create a new milestone for the next minor version (even if one isn't
    planned)
3.  Create a new version
4.  If this new version is the highest available (i.e. not a maintenance
    release on an older branch or a beta release) change the default
    version to it
5.  Make sure all tickets that affect user experience are documented
    using the Release Notes field in Trac

### Schedule review of the SSSD's wiki pages for the next release {#SchedulereviewoftheSSSDswikipagesforthenextrelease}

1.  Add new ticket with the title 'Review and update SSSD's wiki pages
    for X.Y.Z release'. Example ticket:
    [[​]{.icon}https://fedorahosted.org/sssd/ticket/2779](https://fedorahosted.org/sssd/ticket/2779){.ext-link})

### Update the [SSSD Front Page](https://docs.pagure.org/sssd-test2/WikiStart.html){.wiki} {#UpdatetheSSSDFrontPage}

1.  Replace the latest release listed on the front page with the line
    you just created on the
    [Releases](https://docs.pagure.org/sssd-test2/Releases.html){.wiki}
    page.

### Announce the release to the world! {#Announcethereleasetotheworld}

1.  Send an email to `sssd-devel@lists.fedorahosted.org`,
    `sssd-users@lists.fedorahosted.org`,
    `freeipa-users@lists.fedorahosted.org` and
    `freeipa-interest@redhat.com` announcing the availability of the new
    version.
2.  Announce the release on social networks

