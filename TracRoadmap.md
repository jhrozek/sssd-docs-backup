The Trac Roadmap {#TheTracRoadmap}
================

<div class="system-message">

**Error: Macro TracGuideToc(None) failed**
    'NoneType' object has no attribute 'find'

</div>

The roadmap provides a view on the [ticket
system](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki} that
helps planning and managing the future development of a project.

The Roadmap View {#TheRoadmapView}
----------------

Basically, the roadmap is just a list of future milestones. You can add
a description to milestones (using
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki})
describing main objectives, for example. In addition, tickets targeted
for a milestone are aggregated, and the ratio between active and
resolved tickets is displayed as a milestone progress bar. It is
possible to further [[​]{.icon}customise the ticket
grouping](http://trac.edgewall.org/intertrac/TracRoadmapCustomGroups "TracRoadmapCustomGroups in Trac project trac"){.ext-link}
and have multiple ticket statuses shown on the progress bar.

The roadmap can be filtered to show or hide *completed milestones* and
*milestones with no due date*. In the case that both *show completed
milestones* and *hide milestones with no due date* are selected,
*completed* milestones with no due date [will]{.underline} be shown.

The Milestone View {#TheMilestoneView}
------------------

You can add a description for each milestone (using
[WikiFormatting](https://docs.pagure.org/sssd-test2/WikiFormatting.html){.wiki})
describing main objectives, for example. In addition, tickets targeted
for a milestone are aggregated, and the ratio between active and
resolved tickets is displayed as a milestone progress bar. It is
possible to further [[​]{.icon}customise the ticket
grouping](http://trac.edgewall.org/intertrac/TracRoadmapCustomGroups "TracRoadmapCustomGroups in Trac project trac"){.ext-link}
and have multiple ticket statuses shown on the progress bar.

It is possible to drill down into this simple statistic by viewing the
individual milestone pages. By default, the active/resolved ratio will
be grouped and displayed by component. You can also regroup the status
by other criteria, such as ticket owner or severity. Ticket numbers are
linked to [custom
queries](https://docs.pagure.org/sssd-test2/TracQuery.html){.wiki}
listing corresponding tickets.

Roadmap Administration {#RoadmapAdministration}
----------------------

With appropriate permissions it is possible to add, modify and remove
milestones using either the web interface (roadmap and milestone pages),
web administration interface or by using `trac-admin`.

**Note:** Milestone descriptions can not currently be edited using
'trac-admin'.

iCalendar Support {#iCalendarSupport}
-----------------

The Roadmap supports the
[[​]{.icon}iCalendar](http://www.ietf.org/rfc/rfc2445.txt){.ext-link}
format to keep track of planned milestones and related tickets from your
favorite calendar software. Many calendar applications support the
iCalendar specification including

-   [[​]{.icon}Apple iCal](http://www.apple.com/ical/){.ext-link} for
    Mac OS X
-   the cross-platform [[​]{.icon}Mozilla
    Calendar](http://www.mozilla.org/projects/calendar/){.ext-link}
-   [[​]{.icon}Chandler](http://chandlerproject.org){.ext-link}
-   [[​]{.icon}Korganizer](http://kontact.kde.org/korganizer/){.ext-link}
    (the calendar application of the
    [[​]{.icon}KDE](http://www.kde.org/){.ext-link} project)
-   [[​]{.icon}Evolution](http://www.novell.com/de-de/products/desktop/features/evolution.html){.ext-link}
    also support iCalendar
-   [[​]{.icon}Microsoft
    Outlook](http://office.microsoft.com/en-us/outlook/){.ext-link} can
    also read iCalendar files (it appears as a new static calendar in
    Outlook)
-   [[​]{.icon}Google
    Calendar](https://www.google.com/calendar/){.ext-link}

To subscribe to the roadmap, copy the iCalendar link from the roadmap
(found at the bottom of the page) and choose the "Subscribe to remote
calendar" action (or similar) of your calendar application, and insert
the URL just copied.

**Note:** For tickets to be included in the calendar as tasks, you need
to be logged in when copying the link. You will only see tickets
assigned to yourself, and associated with a milestone.

**Note:** To include the milestones in Google Calendar you might need to
rewrite the URL.

``` {.wiki}
RewriteEngine on
RewriteRule ([^/.]+)/roadmap/([^/.]+)/ics /$1/roadmap?user=$2&format=ics
```

More information about iCalendar can be found at
[[​]{.icon}Wikipedia](http://en.wikipedia.org/wiki/ICalendar){.ext-link}.

------------------------------------------------------------------------

See also:
[TracTickets](https://docs.pagure.org/sssd-test2/TracTickets.html){.wiki},
[TracReports](https://docs.pagure.org/sssd-test2/TracReports.html){.wiki},
[TracQuery](https://docs.pagure.org/sssd-test2/TracQuery.html){.wiki},
[[​]{.icon}TracRoadmapCustomGroups](http://trac.edgewall.org/intertrac/TracRoadmapCustomGroups "TracRoadmapCustomGroups in Trac project trac"){.ext-link}
