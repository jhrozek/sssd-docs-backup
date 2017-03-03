SSSD performance improvements for the 1.15 release
==================================================

Related ticket(s):

-  `​https://fedorahosted.org/sssd/ticket/XYZ <https://fedorahosted.org/sssd/ticket/XYZ>`__

Problem statement
~~~~~~~~~~~~~~~~~

We introduced the timestamp cache in 1.14 to help improve performance.
But more work is needed to make SSSD work better in large environment.

Use cases
~~~~~~~~~

#. As a user of a machine that contains a directory with a large number
   of files, each owned by a large group, I want commands like ``ls -l``
   to resolve those large groups noticeably and measurably quicker than
   the previous version
#. As an operator who is a member of several large domain groups, I want
   a log in to a machine to be noticeably and measurably faster than the
   previous version

Overview of the solution
~~~~~~~~~~~~~~~~~~~~~~~~

The most work is still needed in the LDAP provider. There we can:

-  refactor the ``sdap_async_groups.c`` module. Currently it iterates
   over all attribute values several times, which is really costly with
   a large number of attributes
-  refactor the nested group processing to make sure expensive lookups
   (such as lookups of all members of the group, there can potentially
   be thousands of these) are only performed once and intermediate
   results are stored in-memory.
-  attempt to shortcut parsing the attributes of the entry returned from
   LDAP sooner. The idea behind this is that if the modifyTimestamp did
   not change, we can reuse the entry we already cached.
-  Looking up an entry in sysdb\_attrs is slow. We might want to
   implement a smarter way (sorted entries? Tree?)

A separate effort with performance impact is:

-  implement a generic way to pass around intermediate results between
   requests in memory. Currently when transitioning between IPA and AD
   requests, we must write the intermediate results to the disk, which
   is a full transaction.

Implementation details
~~~~~~~~~~~~~~~~~~~~~~

A more technical extension of the previous section. Might include
low-level details, such as C structures, function synopsis etc. In case
of very trivial features (e.g a new option), this section can be merged
with the previous one.

Configuration changes
~~~~~~~~~~~~~~~~~~~~~

Does your feature involve changes to configuration, like new options or
options changing values? Summarize them here. There's no need to go into
too many details, that's what man pages are for.

How To Test
~~~~~~~~~~~

This section should explain to a person with admin-level of SSSD
understanding how this change affects run time behaviour of SSSD and how
can an SSSD user test this change. If the feature is internal-only,
please list what areas of SSSD are affected so that testers know where
to focus.

How To Debug
~~~~~~~~~~~~

Explain how to debug this feature if something goes wrong. This section
might include examples of additional commands the user might run (such
as keytab or certificate sanity checks) or explain what message to look
for.

Authors
~~~~~~~

Give credit to authors of the design in this section.
