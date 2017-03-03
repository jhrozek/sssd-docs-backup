Trac Ticket Queries
===================

.. raw:: html

   <div class="system-message">

**Error: Macro TracGuideToc(None) failed**
::

    'NoneType' object has no attribute 'find'

.. raw:: html

   </div>

In addition to
`reports <https://docs.pagure.org/sssd-test2/TracReports.html>`__, Trac
provides support for *custom ticket queries*, used to display lists of
tickets meeting a specified set of criteria.

To configure and execute a custom query, switch to the *View Tickets*
module from the navigation bar, and select the *Custom Query* link.

Filters
-------

When you first go to the query page the default filter will display
tickets relevant to you:

-  If logged in then all open tickets it will display open tickets
   assigned to you.
-  If not logged in but you have specified a name or email address in
   the preferences then it will display all open tickets where your
   email (or name if email not defined) is in the CC list.
-  If not logged and no name/email defined in the preferences then all
   open issues are displayed.

Current filters can be removed by clicking the button to the left with
the minus sign on the label. New filters are added from the pulldown
lists at the bottom corners of the filters box ('And' conditions on the
left, 'Or' conditions on the right). Filters with either a text box or a
pulldown menu of options can be added multiple times to perform an *or*
of the criteria.

You can use the fields just below the filters box to group the results
based on a field, or display the full description for each ticket.

Once you've edited your filters click the *Update* button to refresh
your results.

Navigating Tickets
------------------

Clicking on one of the query results will take you to that ticket. You
can navigate through the results by clicking the *Next Ticket* or
*Previous Ticket* links just below the main menu bar, or click the *Back
to Query* link to return to the query page.

You can safely edit any of the tickets and continue to navigate through
the results using the *Next/Previous/Back to Query* links after saving
your results. When you return to the query *any tickets which were
edited* will be displayed with italicized text. If one of the tickets
was edited such that it no longer matches the query criteria the text
will also be greyed. Lastly, if **a new ticket matching the query
criteria has been created**, it will be shown in bold.

The query results can be refreshed and cleared of these status
indicators by clicking the *Update* button again.

Saving Queries
--------------

Trac allows you to save the query as a named query accessible from the
reports module. To save a query ensure that you have *Updated* the view
and then click the *Save query* button displayed beneath the results.
You can also save references to queries in Wiki content, as described
below.

*Note:* one way to easily build queries like the ones below, you can
build and test the queries in the Custom report module and when ready -
click *Save query*. This will build the query string for you. All you
need to do is remove the extra line breaks.

*Note:* you must have the **REPORT\_CREATE** permission in order to save
queries to the list of default reports. The *Save query* button will
only appear if you are logged in as a user that has been granted this
permission. If your account does not have permission to create reports,
you can still use the methods below to save a query.

Using `TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You may want to save some queries so that you can come back to them
later. You can do this by making a link to the query from any Wiki page.

.. code:: wiki

    [query:status=new|assigned|reopened&version=1.0 Active tickets against 1.0]

Which is displayed as:

    `Active tickets against
    1.0 <https://fedorahosted.org/sssd/query?status=new&status=assigned&status=reopened&version=1.0&order=priority>`__

This uses a very simple query language to specify the criteria (see
`Query
Language <https://docs.pagure.org/sssd-test2/TracQuery.html#QueryLanguage>`__).

Alternatively, you can copy the query string of a query and paste that
into the Wiki link, including the leading ``?`` character:

.. code:: wiki

    [query:?status=new&status=assigned&status=reopened&group=owner Assigned tickets by owner]

Which is displayed as:

    `Assigned tickets by
    owner <https://fedorahosted.org/sssd/query?status=new&status=assigned&status=reopened&group=owner>`__

Using the ``[[TicketQuery]]`` Macro
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The `​TicketQuery <http://trac.edgewall.org/intertrac/TicketQuery>`__
macro lets you display lists of tickets matching certain criteria
anywhere you can use
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__.

Example:

.. code:: wiki

    [[TicketQuery(version=0.6|0.7&resolution=duplicate)]]

This is displayed as:

    No results

Just like the `query: wiki
links <https://docs.pagure.org/sssd-test2/TracQuery.html#UsingTracLinks>`__,
the parameter of this macro expects a query string formatted according
to the rules of the simple `ticket query
language <https://docs.pagure.org/sssd-test2/TracQuery.html#QueryLanguage>`__.
This also allows displaying the link and description of a single ticket:

.. code:: wiki

    [[TicketQuery(id=123)]]

This is displayed as:

    .. raw:: html

       <div>

    `#123 </sssd/ticket/123>`__
        SSSD requirement on gettext 0.17 breaks RHEL5 build (and is
        unnecessary)

    .. raw:: html

       </div>

A more compact representation without the ticket summaries is also
available:

.. code:: wiki

    [[TicketQuery(version=0.6|0.7&resolution=duplicate, compact)]]

This is displayed as:

    No results

Finally, if you wish to receive only the number of defects that match
the query, use the ````\ count\ ```` parameter.

.. code:: wiki

    [[TicketQuery(version=0.6|0.7&resolution=duplicate, count)]]

This is displayed as:

    0

Customizing the *table* format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can also customize the columns displayed in the table format
(*format=table*) by using *col=<field>* - you can specify multiple
fields and what order they are displayed by placing pipes (``|``)
between the columns like below:

.. code:: wiki

    [[TicketQuery(max=3,status=closed,order=id,desc=1,format=table,col=resolution|summary|owner|reporter)]]

This is displayed as:

.. raw:: html

   <div xmlns="http://www.w3.org/1999/xhtml">

.. rubric:: Results (1 - 3 of 2745)
   :name: results-1---3-of-2745
   :class: report-result

.. raw:: html

   <div class="paging">

 1
`2 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`3 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=3&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`4 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=4&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`5 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=5&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`6 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=6&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`7 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=7&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`8 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=8&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`9 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=9&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`10 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=10&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`11 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=11&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`→ </sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__

.. raw:: html

   </div>

+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| `Ticket <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=id>`__   | `Resolution <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=resolution>`__   | `Summary <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=summary>`__   | `Owner <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=owner>`__   | `Reporter <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=reporter>`__   |
+==========================================================================================================================================+======================================================================================================================================================+================================================================================================================================================+============================================================================================================================================+==================================================================================================================================================+
| `#3309 </sssd/ticket/3309>`__                                                                                                            | fixed                                                                                                                                                | `Coverity warns about an unused value in IPA sudo code </sssd/ticket/3309>`__                                                                  | pcech                                                                                                                                      | jhrozek                                                                                                                                          |
+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| `#3301 </sssd/ticket/3301>`__                                                                                                            | fixed                                                                                                                                                | `storing a sudo rule with sudoRule attribute values that only differ by case fails </sssd/ticket/3301>`__                                      | somebody                                                                                                                                   | jhrozek                                                                                                                                          |
+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| `#3299 </sssd/ticket/3299>`__                                                                                                            | fixed                                                                                                                                                | `SSSD does not start if using only the local provider and services line is empty </sssd/ticket/3299>`__                                        | fidencio                                                                                                                                   | fidencio                                                                                                                                         |
+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

.. raw:: html

   <div class="paging">

 1
`2 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`3 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=3&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`4 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=4&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`5 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=5&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`6 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=6&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`7 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=7&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`8 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=8&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`9 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=9&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`10 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=10&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`11 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=11&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__
`→ </sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__

.. raw:: html

   </div>

.. raw:: html

   </div>

Full rows
^^^^^^^^^

In *table* format you can also have full rows by using *rows=<field>*
like below:

.. code:: wiki

    [[TicketQuery(max=3,status=closed,order=id,desc=1,format=table,col=resolution|summary|owner|reporter,rows=description)]]

This is displayed as:

.. raw:: html

   <div xmlns="http://www.w3.org/1999/xhtml">

.. rubric:: Results (1 - 3 of 2745)
   :name: results-1---3-of-2745-1
   :class: report-result

.. raw:: html

   <div class="paging">

 1
`2 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`3 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=3&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`4 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=4&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`5 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=5&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`6 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=6&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`7 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=7&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`8 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=8&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`9 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=9&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`10 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=10&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`11 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=11&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`→ </sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__

.. raw:: html

   </div>

`Ticket <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=id&row=description>`__
`Resolution <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=resolution&row=description>`__
`Summary <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=summary&row=description>`__
`Owner <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=owner&row=description>`__
`Reporter <https://fedorahosted.org/sssd/query?status=closed&max=3&col=id&col=resolution&col=summary&col=owner&col=reporter&order=reporter&row=description>`__
`#3309 </sssd/ticket/3309>`__
fixed
`Coverity warns about an unused value in IPA sudo
code </sssd/ticket/3309>`__
pcech
jhrozek
Description
.. code:: wiki

     943    for (i = 0; table[i].ipa != NULL; i++) {
        value_overwrite: Overwriting previous write to ret with value from sysdb_attrs_get_string_array(rule->attrs, table[i].ipa, tmp_ctx, &values).
     944        ret = sysdb_attrs_get_string_array(rule->attrs, table[i].ipa,
     945                                           tmp_ctx, &values);
     946        if (ret == ENOENT) {
     947            continue;
     948        } else if (ret != EOK) {
     949            DEBUG(SSSDBG_CRIT_FAILURE, "Unable to read attribute "
     950                  "%s [%d]: %s\n", table[i].ipa, ret, sss_strerror(ret));
     951            goto done;
     952        }
     953
     954        for (j = 0; values[j] != NULL; j++) {
     955            if (table[i].conv_fn != NULL) {
     956                value = table[i].conv_fn(tmp_ctx, conv, values[j], &skip_entry);
     957                if (value == NULL) {
     958                    if (skip_entry) {
        CID 14791 (#1 of 1): Unused value (UNUSED_VALUE)assigned_value: Assigning value 2 to ret here, but that stored value is overwritten before it can be used.
     959                        ret = ENOENT;
     960                        continue;
     961                    } else {
        value_overwrite: Overwriting previous write to ret with value 12.
     962                        ret = ENOMEM;
     963                        goto done;
     964                    }
     965                }
     966            } else {
     967                value = values[j];
     968            }
     969
        value_overwrite: Overwriting previous write to ret with value from sysdb_attrs_add_string_safe(attrs, table[i].sudo, value).

`#3301 </sssd/ticket/3301>`__
fixed
`storing a sudo rule with sudoRule attribute values that only differ by
case fails </sssd/ticket/3301>`__
somebody
jhrozek
Description
Consider the following sudo rule where two values of the sudoUser
attribute only differ by case:

.. code:: wiki

    # catrule, sudoers, win.trust.test
    dn: CN=catrule,OU=sudoers,DC=win,DC=trust,DC=test
    objectClass: top
    objectClass: sudoRole
    cn: catrule
    distinguishedName: CN=catrule,OU=sudoers,DC=win,DC=trust,DC=test
    instanceType: 4
    whenCreated: 20161114214917.0Z
    whenChanged: 20170205101639.0Z
    uSNCreated: 69688
    uSNChanged: 595722
    name: catrule
    objectGUID:: 2ZFRxbVBW0GtLR10+u5Pgg==
    objectCategory: CN=sudoRole,CN=Schema,CN=Configuration,DC=win,DC=trust,DC=test
    dSCorePropagationData: 16010101000000.0Z
    sudoHost: ALL
    sudoUser: tuser
    sudoUser: TUSER
    sudoCommand: /usr/bin/cat

With the current master, storing the rule fails with EEXIST. We should
gracefully store the rule, adding the lowercase attribute value only
once.

`#3299 </sssd/ticket/3299>`__
fixed
`SSSD does not start if using only the local provider and services line
is empty </sssd/ticket/3299>`__
fidencio
fidencio
Description
SSSD hits a timeout while being started in case the only configured
domain is the local one and the services' line is empty.

sssd.conf:

.. code:: wiki

    [sssd]
    domains = LOCAL
    config_file_version = 2

    [nss]
    filter_groups = root
    filter_users = root

    [domain/LOCAL]
    id_provider = local
    auth_provider = local
    access_provider = permit

.. raw:: html

   <div class="paging">

 1
`2 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`3 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=3&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`4 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=4&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`5 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=5&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`6 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=6&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`7 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=7&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`8 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=8&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`9 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=9&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`10 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=10&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`11 <https://fedorahosted.org/sssd/query?status=closed&max=3&page=11&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id&row=description>`__
`→ </sssd/query?status=closed&max=3&page=2&col=id&col=resolution&col=summary&col=owner&col=reporter&desc=1&order=id>`__

.. raw:: html

   </div>

.. raw:: html

   </div>

Query Language
~~~~~~~~~~~~~~

``query:``
`TracLinks <https://docs.pagure.org/sssd-test2/TracLinks.html>`__ and
the ``[[TicketQuery]]`` macro both use a mini “query language” for
specifying query filters. Basically, the filters are separated by
ampersands (``&``). Each filter then consists of the ticket field name,
an operator, and one or more values. More than one value are separated
by a pipe (``|``), meaning that the filter matches any of the values. To
include a literal ``&`` or ``|`` in a value, escape the character with a
backslash (``\``).

The available operators are:

+--------------+--------------------------------------------------------+
| **``=``**    | the field content exactly matches one of the values    |
+--------------+--------------------------------------------------------+
| **``~=``**   | the field content contains one or more of the values   |
+--------------+--------------------------------------------------------+
| **``^=``**   | the field content starts with one of the values        |
+--------------+--------------------------------------------------------+
| **``$=``**   | the field content ends with one of the values          |
+--------------+--------------------------------------------------------+

All of these operators can also be negated:

+---------------+-----------------------------------------------------------+
| **``!=``**    | the field content matches none of the values              |
+---------------+-----------------------------------------------------------+
| **``!~=``**   | the field content does not contain any of the values      |
+---------------+-----------------------------------------------------------+
| **``!^=``**   | the field content does not start with any of the values   |
+---------------+-----------------------------------------------------------+
| **``!$=``**   | the field content does not end with any of the values     |
+---------------+-----------------------------------------------------------+

The date fields ``created`` and ``modified`` can be constrained by using
the ``=`` operator and specifying a value containing two dates separated
by two dots (``..``). Either end of the date range can be left empty,
meaning that the corresponding end of the range is open. The date parser
understands a few natural date specifications like "3 weeks ago", "last
month" and "now", as well as Bugzilla-style date specifications like
"1d", "2w", "3m" or "4y" for 1 day, 2 weeks, 3 months and 4 years,
respectively. Spaces in date specifications can be left out to avoid
having to quote the query string.

+------------------------------------------+--------------------------------------------------------------+
| **``created=2007-01-01..2008-01-01``**   | query tickets created in 2007                                |
+------------------------------------------+--------------------------------------------------------------+
| **``created=lastmonth..thismonth``**     | query tickets created during the previous month              |
+------------------------------------------+--------------------------------------------------------------+
| **``modified=1weekago..``**              | query tickets that have been modified in the last week       |
+------------------------------------------+--------------------------------------------------------------+
| **``modified=..30daysago``**             | query tickets that have been inactive for the last 30 days   |
+------------------------------------------+--------------------------------------------------------------+

--------------

See also:
`TracTickets <https://docs.pagure.org/sssd-test2/TracTickets.html>`__,
`TracReports <https://docs.pagure.org/sssd-test2/TracReports.html>`__,
`TracGuide <https://docs.pagure.org/sssd-test2/TracGuide.html>`__
