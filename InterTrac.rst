`InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__ Links
=======================================================================

Trac supports a convenient way to refer to resources of other Trac
servers, from within the Wiki markup, since version 0.10.

Definitions
-----------

An `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
link can be seen as a scoped
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__. It is
used for referring to a Trac resource (Wiki page, changeset, ticket,
...) located in another Trac environment.

List of Active `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__ Prefixes
-----------------------------------------------------------------------------------------

.. raw:: html

   <div class="system-message">

**Error: Macro InterTrac(None) failed**
::

    'unicode' object does not support item assignment

.. raw:: html

   </div>

Link Syntax
-----------

Simply use the name of the other Trac environment as a prefix, followed
by a colon, ending with the resource located in the other environment.

.. code:: wiki

    <target_environment>:<TracLinks>

The other resource is specified using a regular
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__, of
any flavor.

That target environment name is either the real name of the environment,
or an alias for it. The aliases are defined in ``trac.ini`` (see below).
The prefix is case insensitive.

If the `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
link is enclosed in square brackets (like ``[th:WikiExtrasPlugin]``),
the `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
prefix is removed in the displayed link, like a normal link resolver
would be (i.e. the above would be displayed as ``WikiExtrasPlugin``).

For convenience, there's also some alternative short-hand form, where
one can use an alias as an immediate prefix for the identifier of a
ticket, changeset or report: (e.g. ``#T234``, ``[T1508]``,
``[trac 1508]``, ...)

Examples
--------

It is necessary to setup a configuration for the
`InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
facility. This configuration has to be done in the
`TracIni <https://docs.pagure.org/sssd-test2/TracIni.html>`__ file,
``[intertrac]`` section.

Example configuration:

.. code:: wiki

    ...
    [intertrac]
    # -- Example of setting up an alias:
    t = trac

    # -- Link to an external Trac:
    trac.title = Edgewall's Trac for Trac
    trac.url = http://trac.edgewall.org

The ``.url`` is mandatory and is used for locating the other Trac. This
can be a relative URL in case that Trac environment is located on the
same server.

The ``.title`` information will be used for providing an useful tooltip
when moving the cursor over an
`InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__ links.

Finally, the ``.compat`` option can be used to activate or disable a
*compatibility* mode:

-  If the targeted Trac is running a version below
   `​0.10 <http://trac.edgewall.org/intertrac/milestone%3A0.10>`__
   (`​r3526 <http://trac.edgewall.org/intertrac/r3526>`__ to be
   precise), then it doesn't know how to dispatch an
   `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
   link, and it's up to the local Trac to prepare the correct link. Not
   all links will work that way, but the most common do. This is called
   the compatibility mode, and is ``true`` by default.
-  If you know that the remote Trac knows how to dispatch
   `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
   links, you can explicitly disable this compatibility mode and then
   *any*
   `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__ can
   become an
   `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
   link.

Now, given the above configuration, one could create the following
links:

-  to this
   `InterTrac <https://docs.pagure.org/sssd-test2/InterTrac.html>`__
   page:

   -  ``trac:wiki:InterTrac``
      `​trac:wiki:InterTrac <http://trac.edgewall.org/intertrac/wiki%3AInterTrac>`__
   -  ``t:wiki:InterTrac`` t:wiki:InterTrac
   -  Keys are case insensitive: ``T:wiki:InterTrac`` T:wiki:InterTrac

-  to the ticket `#234 <https://fedorahosted.org/sssd/ticket/234>`__:

   -  ``trac:ticket:234``
      `​trac:ticket:234 <http://trac.edgewall.org/intertrac/ticket%3A234>`__
   -  ``trac:#234``
      `​trac:#234 <http://trac.edgewall.org/intertrac/%23234>`__
   -  ``#T234`` #T234

-  to the changeset [1912]:

   -  ``trac:changeset:1912``
      `​trac:changeset:1912 <http://trac.edgewall.org/intertrac/changeset%3A1912>`__
   -  ``[T1912]`` [T1912]

-  to the log range
   `[3300:3330] <https://fedorahosted.org/sssd/log/?revs=3300-3330>`__:
   **(Note: the following ones need ``trac.compat=false``)**

   -  ``trac:log:@3300:3330``
      `​trac:log:@3300:3330 <http://trac.edgewall.org/intertrac/log%3A%403300%3A3330>`__
   -  ``[trac 3300:3330]`` `​[trac
      3300:3330] <http://trac.edgewall.org/intertrac/log%3A/%403300%3A3330>`__

-  finally, to link to the start page of a remote trac, simply use its
   prefix followed by ':', inside an explicit link. Example:
   ``[th: Trac Hacks]`` (*since 0.11; note that the* remote *Trac has to
   run 0.11 for this to work*)

The generic form ``intertrac_prefix:module:id`` is translated to the
corresponding URL ``<remote>/module/id``, shorthand links are specific
to some modules (e.g. #T234 is processed by the ticket module) and for
the rest (``intertrac_prefix:something``), we rely on the
`TracSearch#quickjump <https://docs.pagure.org/sssd-test2/TracSearch.html#quickjump>`__
facility of the remote Trac.

--------------

See also:
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__,
`InterWiki <https://docs.pagure.org/sssd-test2/InterWiki.html>`__
