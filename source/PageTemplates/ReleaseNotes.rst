Highlights
----------

-  Manually cherry-picked important commits

Packaging Changes
-----------------

.. code:: wiki

    git diff previoustag..newtag -- contrib/sssd.spec.in

Documentation Changes
---------------------

.. code:: wiki

    git diff previoustag..newtag -- src/man

Tickets Fixed
-------------

.. code:: wiki

    [[TicketQuery(milestone=$MILESTONE&resolution=fixed)]]

Detailed Changelog
------------------

.. code:: wiki

    git shortlog previoustag..newtag
