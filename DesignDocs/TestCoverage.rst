SSSD Test Suite Coverage
------------------------

This document describes the plan on improving the test coverage of the
SSSD using the cmocka unit test library. The plan might be implemented
through Fedora's participation in Gnome outreach for women.

High Level Strategy
~~~~~~~~~~~~~~~~~~~

The contributor should, on a high level, follow these steps:

#. familiarize herself with SSSD from user point of view

   -  what is it good for?
   -  how do I install it?
   -  how do I configure it?
   -  Useful links:

      -  `docs on this wiki, includes
         presentations <https://docs.pagure.org/sssd-test2/Documentation.html>`__
      -  `​lwn.net article on SSSD <http://lwn.net/Articles/457415/>`__
      -  `​RHEL documentation on
         SSSD <https://access.redhat.com/knowledge/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/SSSD-Introduction.html>`__

#. investigate how the SSSD can be built from source

   -  clone the git repository
   -  configure and make the sources
   -  make check

#. learn about the current unit tests being used in the SSSD project

   -  currently used tests are stored in ``src/tests`` subdirectory and
      mostly use the check unit test suite
   -  newer tests have started to use the cmocka library to leverage the
      mocking framework

#. get familiar with the cmocka unit test library

   -  `​http://cmocka.cryptomilk.org/ <http://cmocka.cryptomilk.org/>`__

#. implement a new unit test for the SSSD as a proof-of-concept

   -  this first unit test would make the contributor familiar with how
      a unit test can be written
   -  does not have to cover any important piece of the SSSD, but rather
      one that is self-contained

#. gradually start learning about the architecture of the SSSD

   -  this step requires coordination with the SSSD developers
   -  work with the SSSD developers on understanding the architecture
   -  blog posts on the SSSD are mostly welcome!

#. propose a couple of unit tests to the SSSD upstream

   -  the most important tier would contain tests such as "does identity
      work" or "does authentication work"

#. cover the most important parts of the SSSD with unit tests

   -  as some of the unit tests might share the same boilerplate code,
      the contributor might also need to implement convenient functions
      reusable by different tests

Schedule
~~~~~~~~

The complete OPFW schedule is
`​here <https://wiki.gnome.org/OutreachProgramForWomen/2013/DecemberMarch>`__.
