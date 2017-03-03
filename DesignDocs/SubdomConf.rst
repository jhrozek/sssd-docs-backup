Subdomain configuration
=======================

Related ticket(s):

-  `​https://fedorahosted.org/sssd/ticket/2599 <https://fedorahosted.org/sssd/ticket/2599>`__

Problem statement
~~~~~~~~~~~~~~~~~

When SSSD is joined to a FreeIPA/Active Directory domain, Administrator
can easily configure/tweak the domain settings in ``sssd.conf``.
However, when SSSD is joined to a FreeIPA domain that is in a trust
relationship with other domain (Active Directory), Administrator can
only tweak the main (FreeIPA) domain, but cannot tweak the trusted
(Active Directory) domain as it does not have a proper domain section in
``sssd.conf``. While we introduced ``subdomain_inherit`` option which
worked for some use cases, it does not help if the subdomain needs
parameters different from the main domain.

This design page describes new feature that allows admins to configure
subdomain parameters in standard SSSD configuration files in similar way
as the main domain's parameters.

Use cases
~~~~~~~~~

Use Case 1: filtering inactive users in trusted AD domain
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As an Administrator, I want to set a different search base for users and
groups in the trusted AD domain, to filter out users from inactive
organizational units, so that only active users and groups are visible
to the system.

Use Case 2: restricting FreeIPA/SSSD only to selected AD servers and/or sites
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As an Administrator, I want to disable autodiscovery of AD servers and
sites in the trusted AD domain and instead list servers and/or sites
manually, so that I can limit the list of Active Directories SSSD
communicates with and for example avoid reaching out to sites that are
not accessible.

Overview of the solution
~~~~~~~~~~~~~~~~~~~~~~~~

A new section in SSSD configuration will be added where the subdomain
options can be set.

This section name will be the same as the main domain section with
"/<subdomain name>" suffix, where the ``<subdomain name>`` is the
trusted domain's name. For example if the main domain's (FreeIPA) name
is ``ipadomain.test`` and the trusted (Active Directory) domain's name
is ``addomain.test``, then the configuration sections will look like
this

.. code:: wiki

    [domain/ipadomain.test]
    # this is the main domain section

    [domain/ipadomain.test/addomain.test]
    # this is the trusted domain section

Note that **not all options available for the main domain will also be
available in the new subdomain section**. Here are some options that
will be supported (the list is not exhaustive):

-  ldap\_search\_base
-  ldap\_user\_search\_base
-  ldap\_group\_search\_base
-  ad\_server
-  ad\_backup\_server
-  ad\_site

Implementation details
~~~~~~~~~~~~~~~~~~~~~~

TBD

How To Test
~~~~~~~~~~~

-  Configure FreeIPA server and set it in a Trust relationship with
   respective Active Directory domain
-  In ``sssd.conf`` on the FreeIPA server, add trusted domain section
   and redefine some of the supported options for this section (for
   example ``ldap_user_search_base`` for `Use Case
   1 <https://fedorahosted.org/sssd#Use%20Case%201:%20filtering%20inactive%20users%20in%20trusted%20AD%20domain>`__
   or ``ad_server``/``ad_site`` for `Use Case
   2 <https://fedorahosted.org/sssd#Use%20Case%202:%20restricting%20FreeIPA/SSSD%20only%20to%20selected%20AD%20servers%20and/or%20sites>`__)
-  Restart SSSD
-  Join FreeIPA domain with another client (with ``ipa-client-install``
   for example), see if the set option is used correctly

How To Debug
~~~~~~~~~~~~

TBD

Authors
~~~~~~~

Michal Židek `​mzidek@redhat.com <mailto:mzidek@redhat.com>`__
