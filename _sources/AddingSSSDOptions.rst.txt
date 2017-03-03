Adding a new SSSD option
------------------------

-  This wiki page should help developers understand which places need to
   be touched when a new option should be added. This process is quite
   manual at the moment and this page is meant as a stopgap until a
   better solution is developed.

sssd.conf and confdb
~~~~~~~~~~~~~~~~~~~~

-  SSSD configuration is normally placed in ``/etc/sssd/sssd.conf`` and
   optionally in include directories. The format is a Windows-style INI
   format. However, SSSD doesn't read from the file directly, it reads
   configuration from a config database, or confdb for short. When the
   main sssd process starts, it reads the plaintext config files and
   dumps the resulting config into confdb.

-  Thes confdb file can be inspected manually with

   .. code:: wiki

       ldbsearch -H /var/lib/sss/db/config.ldb

Two kinds of SSSD options
~~~~~~~~~~~~~~~~~~~~~~~~~

-  SSSD has two basic kinds of options - raw config database options and
   data provider options. The former are used in the main sssd process
   and the responders, the latter in providers. The raw options are read
   directly from the database using calls like ``confdb_get_string``.
   The data provider options are an abstraction over that where the
   programmer describes the option in a ``dp_option`` structure and the
   provider fills the option value into the ``dp_option`` structure
   field on startup.

Adding the option
~~~~~~~~~~~~~~~~~

-  This section describes what files must be touched in order for the
   new option to be added.

-  **Man pages**

   -  ``src/man/sssd.conf.5.xml`` (Raw)
   -  ``src/man/sssd-<provider>.5.xml`` (Data Provider)

-  **Python config API**

   -  ``src/config/SSSDConfig/__init__.py.in``
   -  ``src/config/SSSDConfigTest.py``
   -  ``src/config/etc/sssd.api.conf`` (Raw)
   -  ``src/config/etc/sssd.api.d/sssd-<provider>.conf`` (Data Provider)

-  **Confdb** (Raw)

   -  ``src/confdb/confdb.h``

-  **dp\_option Structure** (Data provider)

   -  ``src/providers/<provider>/<provider>_opts.c``

-  **Config Checking schema**

   -  ``src/config/cfg_rules.ini``

The man pages
^^^^^^^^^^^^^

-  The man page files are in XML format inside the ``src/man/``
   directory identifying the manual section number in the filename. XML
   elements must have matching opening and closing tags and options will
   normally be defined between opening ``<varlistentry>`` and closing
   ``</varlistentry>`` tags. Man page descriptions should be
   informational enough for end-users to understand and explicitly state
   the Default value when the option is not added.

-  Data provider options will be included in the associated data
   provider man page ``sssd-<provider>.5.xml`` while raw options will be
   added to the ``sssd.conf.5.xml``

The python config API
^^^^^^^^^^^^^^^^^^^^^

-  The option name and a concise description will be added under the
   correct option [section] in ``src/config/SSSDConfig/__init__.py.in``

-  The option name also will be added in the appropriate list in
   ``src/config/SSSDConfigTest.py``

-  Modification to the config validation file
   ``src/config/etc/sssd.api.conf`` will be done to include raw options
   in the format *option = type, subtype, mandatory[, default]* under
   the correct [section]. Data provider options will be added to the
   file ``src/config/etc/sssd.api.d/sssd-<provider>.conf``. These files
   get copied into ``/usr/share/sssd/`` on the SSSD-installed system.

confdb.h
^^^^^^^^

-  Only for raw options, a macro will be created in the format in the
   header file ``src/confdb/confdb.h`` to add the option into the confDB

   .. code:: wiki

       #define CONFDB_SECTION_OPTION_NAME "option_name"  

dp\_option structure
^^^^^^^^^^^^^^^^^^^^

only for data provider options

config checking schema
^^^^^^^^^^^^^^^^^^^^^^

-  The option will be added to the appropriate section in
   ``src/config/cfg_rules.ini`` for config file validation(new in 1.14)

Retrieving the option
^^^^^^^^^^^^^^^^^^^^^

-  The option needs to be retrieved either by using the confdb\_get\*
   functions or accessing the dp\_option fields

    ``confdb_get_string`` example to retrieve the ``id_provider`` option
    from the confdb domain section:

.. code:: wiki

            ret = confdb_get_string(cdb, tmp_ctx, conf_path,
                                    CONFDB_DOMAIN_ID_PROVIDER, NULL, &id_provider);
            if (ret == EOK) {
                if (id_provider == NULL) {
                    DEBUG(SSSDBG_OP_FAILURE, "id_provider is not set for "
                          "domain [%s], trying next domain.\n", domain_names[c]);
                    continue;
                }

Examples
~~~~~~~~

-  `​Raw option
   'certificate\_verification' <https://git.fedorahosted.org/cgit/sssd.git/commit/?id=544a20de7667f05c1a406c4dea0706b0ab507430>`__
-  `​Data provider option
   'ad\_enabled\_domains' <https://git.fedorahosted.org/cgit/sssd.git/commit/?id=d6342c92c226becbdd254f90a0005b8c00c300dc>`__
