.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Release Process for SSSD <#ReleaseProcessforSSSD>`__

      #. `Pre-requisites <#Pre-requisites>`__
      #. `Prepare the sources <#Preparethesources>`__

         #. `Special Beta or Pre-release
            rules <#SpecialBetaorPre-releaserules>`__

      #. `Tag and sign the release <#Tagandsigntherelease>`__

         #. `Special Beta or Pre-release
            rules <#SpecialBetaorPre-releaserules1>`__

      #. `Generate HTML manpages <#GenerateHTMLmanpages>`__
      #. `Create a release tarball <#Createareleasetarball>`__

         #. `Special Beta or Pre-release
            rules <#SpecialBetaorPre-releaserules2>`__

      #. `Prepare the branch for the next
         version <#Preparethebranchforthenextversion>`__

         #. `Special-case: branching off master to track the next major
            version <#Special-case:branchingoffmastertotrackthenextmajorversion>`__

      #. `Upload the tarball to
         Fedorahosted.org <#UploadthetarballtoFedorahosted.org>`__
      #. `Update the SSSD Release Page <#UpdatetheSSSDReleasePage>`__

         #. `Special-case: final release after multiple preview
            releases <#Special-case:finalreleaseaftermultiplepreviewreleases>`__

      #. `Update the Trac milestones and
         versions <#UpdatetheTracmilestonesandversions>`__
      #. `Schedule review of the SSSD's wiki pages for the next
         release <#SchedulereviewoftheSSSDswikipagesforthenextrelease>`__
      #. `Update the SSSD Front Page <#UpdatetheSSSDFrontPage>`__
      #. `Announce the release to the
         world! <#Announcethereleasetotheworld>`__

.. raw:: html

   </div>

Release Process for SSSD
------------------------

    We will use SSSD 1.3.0 as an example. Substitute with the
    appropriate version where needed.

Pre-requisites
~~~~~~~~~~~~~~

-  Commit access to the SSSD upstream repository
-  A GPG key signed by at least two other members of the SSSD team.
-  Access to the fedorahosted.org fileserver
-  WIKI\_ADMIN privilege for the SSSD Trac instance
-  Maintainer privileges on the SSSD Zanata Instance. Follow the
   `​zanata guide <http://zanata.org/help/cli/cli-configuration/>`__ to
   set up the zanata-cli tool
-  A fresh clone of the SSSD upstream repository to work from
-  Ensure that all tickets that were closed in this release are marked
   with the appropriate resolution.
-  Perform a scratch build on all supported architectures.

Prepare the sources
~~~~~~~~~~~~~~~~~~~

#. Ensure that you have the latest version of the upstream sources.
#. Update the translation files.

   #. In the root of SSSD checkout, pull new translations from zanata
      with

      .. code:: wiki

          zanata-cli pull -s . -t .

   #. If new translations have been added to the main translations
      (``po/*.po``), add the new language to ``po/LINGUAS``. Please keep
      them in English alphabetical order.
   #. If new translations have been added to the manpage translations
      (``src/man/po/*.po``), add the new language to
      ``src/man/po/po4a.cfg``. Please keep them in English alphabetical
      order.
   #. Run
      ``autoreconf -if && ./configure && make update-po && make distcheck``
      from the root
   #. Check ``git status`` for changes to ``*.po`` or ``*.pot`` files.

#. Commit the new ``.po[t]`` files.
#. Push the changes.

Special Beta or Pre-release rules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. For the benefit of translators, push any new strings up to Zanata
   whenever we make a pre-release tarball

   .. code:: wiki

       zanata-cli push -s .

#. If this is is the last pre-release (e.g. final beta before
   bugfix-only phase) String Freeze should be announced on the
   sssd-devel list and the Zanata site.

Tag and sign the release
~~~~~~~~~~~~~~~~~~~~~~~~

#. Tag the release and sign it with your GPG key

   .. code:: wiki

       git tag -s sssd-1_3_0

#. Push the tag. Pus the tag explictly instead of using --tags so that
   you do not push extraneous tags by mistake.

   .. code:: wiki

       git push origin sssd-1_3_0

Special Beta or Pre-release rules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When tagging a beta or release candidate, the sources should be tagged
twice. Once for the pure numeric value and once for the human-friendly
value. So for example, if we are tagging SSSD 1.9.0 beta 2, we should
do:

.. code:: wiki

    git tag -s sssd-1_8_92
    git tag -s sssd-1_9_0_beta2

Followed by

.. code:: wiki

    git push --tags

Generate HTML manpages
~~~~~~~~~~~~~~~~~~~~~~

-  Use the attached perl script to produce XHTML-formatted manpages.

   .. code:: wiki

       perl make-xhtml.pl /path/to/xml /path/to/output

-  Upload these manpages to public space (for example, FedoraPeople
   space)
-  Link to these files when creating the release page entry.

Create a release tarball
~~~~~~~~~~~~~~~~~~~~~~~~

#. Run ``scripts/release.sh`` from the root directory of the source
   checkout

   -  This will create two files, ``sssd-1.3.0.tar.gz`` and
      ``sssd-1.3.0.tar.gz.asc``

#. Create an md5sum and a sha1sum of the tarball

   .. code:: wiki

       md5sum sssd-1.3.0.tar.gz > sssd-1.3.0.tar.gz.md5sum
       sha1sum sssd-1.3.0.tar.gz > sssd-1.3.0.tar.gz.sha1sum

Special Beta or Pre-release rules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When creating a tarball for a beta or a release candidate, the resulting
tarball should be renamed appropriately. To use the 1.9.0 beta 2
example:

.. code:: wiki

    mv sssd-1.8.92.tar.gz sssd-1.9.0beta2.tar.gz
    mv sssd-1.8.92.tar.gz.asc sssd-1.9.0beta2.tar.gz.asc

Prepare the branch for the next version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Update the version in version.m4 to the next point release (e.g.
   1.3.1)

   -  Only update the version to a final release (like 1.9.0) right
      before releasing the final version. Bumping the version to final
      sooner would prevent us from being able to release another
      pre-release..

#. Push this new version

   .. code:: wiki

       git push

Special-case: branching off master to track the next major version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. As an example, we will branch off ``sssd-1-3`` and let master track
   the development of sssd 1.4
#. Create a stable branch from master

   .. code:: wiki

           git checkout -b sssd-1-3
           git push -n origin sssd-1-3
           # verify everything looks sane
           git push origin sssd-1-3

#. Switch back to the master branch
#. On master, update the version in version.m4 to the next point release
   (e.g. ``1.3.90``)
#. Push this new version

   .. code:: wiki

           git push -n origin master
           # verify everything looks sane
           git push origin master

Upload the tarball to Fedorahosted.org
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. ``scp sssd-1.3.0.tar.gz fedorahosted.org:sssd``
#. ``scp sssd-1.3.0.tar.gz.asc fedorahosted.org:sssd``

Update the `SSSD Release Page <https://docs.pagure.org/sssd-test2/Releases.html>`__
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Add a line at the top of the
   `Releases <https://docs.pagure.org/sssd-test2/Releases.html>`__ page
   with links to
   ``https://fedorahosted.org/released/sssd/sssd-1.3.0.tar.gz`` and
   ``https://fedorahosted.org/released/sssd/sssd-1.3.0.tar.gz.asc``
#. Add the md5sum and sha1sum calculated above
#. Create a release notes page (e.g.
   `Releases/Notes-1.3.0 <https://docs.pagure.org/sssd-test2/Releases/Notes-1.3.0.html>`__).
   This page should be marked read-only (so only WIKI\_ADMINS can modify
   it). To generate the detailed changelog:

   .. code:: wiki

       git shortlog previoustag..newtag

#. For each release, if any changes have occurred in packaging (a new
   directory, a new provider plugin, etc.), the release notes page
   should include a section notifying potential packagers of these
   changes. In general, this can be determined by doing (from the root
   of the git checkout):

   .. code:: wiki

        git diff previoustag..newtag -- contrib/sssd.spec.in

#. For each release, if any changes have occured in documentation, such
   as new options, options changing default values, the release notes
   should include a section that summarizes there changes.

   .. code:: wiki

        git diff previoustag..newtag -- src/man

#. Update
   `Documentation <https://docs.pagure.org/sssd-test2/Documentation.html>`__
   with links to the latest manual pages and/or Deployment Guides
#. Update
   `SecuritySensitiveOptions <https://docs.pagure.org/sssd-test2/SecuritySensitiveOptions.html>`__
   if any new security-sensitive options were added

Special-case: final release after multiple preview releases
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When releasing a final version (such as 1.9.0) after multiple preview
releases, the release notes page for that final release should contain
all of the changes from the various preview release note pages. This
way, potential packagers and users do not need to examine all of the
prerelease notes.

Update the Trac milestones and versions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Actions to take in the Trac Admin pages:

#. Mark the milestone as complete
#. Create a new milestone for the next minor version (even if one isn't
   planned)
#. Create a new version
#. If this new version is the highest available (i.e. not a maintenance
   release on an older branch or a beta release) change the default
   version to it
#. Make sure all tickets that affect user experience are documented
   using the Release Notes field in Trac

Schedule review of the SSSD's wiki pages for the next release
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Add new ticket with the title 'Review and update SSSD's wiki pages
   for X.Y.Z release'. Example ticket:
   `​https://fedorahosted.org/sssd/ticket/2779 <https://fedorahosted.org/sssd/ticket/2779>`__)

Update the `SSSD Front Page <https://docs.pagure.org/sssd-test2/WikiStart.html>`__
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Replace the latest release listed on the front page with the line you
   just created on the
   `Releases <https://docs.pagure.org/sssd-test2/Releases.html>`__ page.

Announce the release to the world!
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Send an email to ``sssd-devel@lists.fedorahosted.org``,
   ``sssd-users@lists.fedorahosted.org``,
   ``freeipa-users@lists.fedorahosted.org`` and
   ``freeipa-interest@redhat.com`` announcing the availability of the
   new version.
#. Announce the release on social networks
