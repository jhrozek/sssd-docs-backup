The Trac Roadmap
================

.. raw:: html

   <div class="system-message">

**Error: Macro TracGuideToc(None) failed**
::

    'NoneType' object has no attribute 'find'

.. raw:: html

   </div>

The roadmap provides a view on the `ticket
system <https://docs.pagure.org/sssd-test2/TracTickets.html>`__ that
helps planning and managing the future development of a project.

The Roadmap View
----------------

Basically, the roadmap is just a list of future milestones. You can add
a description to milestones (using
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__)
describing main objectives, for example. In addition, tickets targeted
for a milestone are aggregated, and the ratio between active and
resolved tickets is displayed as a milestone progress bar. It is
possible to further `​customise the ticket
grouping <http://trac.edgewall.org/intertrac/TracRoadmapCustomGroups>`__
and have multiple ticket statuses shown on the progress bar.

The roadmap can be filtered to show or hide *completed milestones* and
*milestones with no due date*. In the case that both *show completed
milestones* and *hide milestones with no due date* are selected,
*completed* milestones with no due date will be shown.

The Milestone View
------------------

You can add a description for each milestone (using
`WikiFormatting <https://docs.pagure.org/sssd-test2/WikiFormatting.html>`__)
describing main objectives, for example. In addition, tickets targeted
for a milestone are aggregated, and the ratio between active and
resolved tickets is displayed as a milestone progress bar. It is
possible to further `​customise the ticket
grouping <http://trac.edgewall.org/intertrac/TracRoadmapCustomGroups>`__
and have multiple ticket statuses shown on the progress bar.

It is possible to drill down into this simple statistic by viewing the
individual milestone pages. By default, the active/resolved ratio will
be grouped and displayed by component. You can also regroup the status
by other criteria, such as ticket owner or severity. Ticket numbers are
linked to `custom
queries <https://docs.pagure.org/sssd-test2/TracQuery.html>`__ listing
corresponding tickets.

Roadmap Administration
----------------------

With appropriate permissions it is possible to add, modify and remove
milestones using either the web interface (roadmap and milestone pages),
web administration interface or by using ``trac-admin``.

**Note:** Milestone descriptions can not currently be edited using
'trac-admin'.

iCalendar Support
-----------------

The Roadmap supports the
`​iCalendar <http://www.ietf.org/rfc/rfc2445.txt>`__ format to keep
track of planned milestones and related tickets from your favorite
calendar software. Many calendar applications support the iCalendar
specification including

-  `​Apple iCal <http://www.apple.com/ical/>`__ for Mac OS X
-  the cross-platform `​Mozilla
   Calendar <http://www.mozilla.org/projects/calendar/>`__
-  `​Chandler <http://chandlerproject.org>`__
-  `​Korganizer <http://kontact.kde.org/korganizer/>`__ (the calendar
   application of the `​KDE <http://www.kde.org/>`__ project)
-  `​Evolution <http://www.novell.com/de-de/products/desktop/features/evolution.html>`__
   also support iCalendar
-  `​Microsoft Outlook <http://office.microsoft.com/en-us/outlook/>`__
   can also read iCalendar files (it appears as a new static calendar in
   Outlook)
-  `​Google Calendar <https://www.google.com/calendar/>`__

To subscribe to the roadmap, copy the iCalendar link from the roadmap
(found at the bottom of the page) and choose the "Subscribe to remote
calendar" action (or similar) of your calendar application, and insert
the URL just copied.

**Note:** For tickets to be included in the calendar as tasks, you need
to be logged in when copying the link. You will only see tickets
assigned to yourself, and associated with a milestone.

**Note:** To include the milestones in Google Calendar you might need to
rewrite the URL.

.. code:: wiki

    RewriteEngine on
    RewriteRule ([^/.]+)/roadmap/([^/.]+)/ics /$1/roadmap?user=$2&format=ics

More information about iCalendar can be found at
`​Wikipedia <http://en.wikipedia.org/wiki/ICalendar>`__.

--------------

See also:
`TracTickets <https://docs.pagure.org/sssd-test2/TracTickets.html>`__,
`TracReports <https://docs.pagure.org/sssd-test2/TracReports.html>`__,
`TracQuery <https://docs.pagure.org/sssd-test2/TracQuery.html>`__,
`​TracRoadmapCustomGroups <http://trac.edgewall.org/intertrac/TracRoadmapCustomGroups>`__
