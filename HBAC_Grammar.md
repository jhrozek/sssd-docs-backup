<div class="wiki-toc">

1.  1.  [Time Rules](#TimeRules)
        1.  [Related Attributes](#RelatedAttributes)
        2.  [Grammar Definition](#GrammarDefinition)
        3.  [Terminology](#Terminology)
        4.  [Examples](#Examples)
            1.  [Standard shift](#Standardshift)
            2.  [Second Shift](#SecondShift)
            3.  [Regularly Scheduled Maintenance
                Window](#RegularlyScheduledMaintenanceWindow)
            4.  [The last Saturday of the
                month](#ThelastSaturdayofthemonth)
            5.  [One-time Maintenance
                Window](#One-timeMaintenanceWindow)

</div>

Time Rules {#TimeRules}
----------

### Related Attributes {#RelatedAttributes}

accessTime
:   Grammar describing time that a user is allowed (or denied) access
    startTime: Date and time after which the HBAC rule will be valid
    endTime: Date and time after which the HBAC rule will no longer be
    valid

### Grammar Definition {#GrammarDefinition}

This grammar describes the time period for which the HBAC rule will be
valid

``` {.wiki}
timerange = Absolute / Periodic

Absolute = "absolute" WSP generalizedTime WSP "~" WSP generalizedTime 

generalizedTime as defined in RFC 4517 section 3.3.13 but without time zone at the end.

Periodic = "periodic" WSP Yearly / Monthly / Weekly / Daily

Yearly = "yearly" WSP Y-specifier WSP range-specified

Monthly = "monthly" WSP M-specifier WSP range-specifier

Weekly = "weekly" WSP W-specifier WSP range-specifier

Daily = "daily" WSP range-specifier

Y-specifier = Y-month / Y-week / Y-day

Y-month = "month" WSP month-number WSP M-specifier

Y-week = "week" WSP week-of-the-year WSP W-specifier

Y-day = "day" WSP day-of-the-year

M-specifier = M-on / M-day

M-on = "on" WSP day-of-the-week WSP day-of-the-month-range

M-day = "day" WSP interval day-of-the-month

W-specifier = "day" WSP day-of-the-week

month-number = interval 1-12

week-of-the-year = interval 1-52

day-of-the-month-range = "between" WSP day-of-the-month WSP "and" WSP day-of-the-month

day-of-the-month = "-31" to "-1" or "0" to "31"

day-of-the-week = interval 1-7 (or Mon-Sun)

range-specifier = "at" WSP HHMM WSP "+" WSP duration-specifier

duration-specifier = DDHHMM

DD = "00" to "31"

HH = "00" to "23"

MM = "00" to "59"


interval XX-YY = a comma-separated list of items from XX to YY, or dash-separated ranges.
range = dash-separated range

For example, (interval 1-31) 3-7,10,12,15,25-31 with no spaces inside.
```

### Terminology {#Terminology}

WSP
:   Whitespace - one or more whitespace characters

day-of-the-month
:   Positive numbers refer to exact days, negative one (-1) starts at
    the end of the month and counts back. Day 31 == Day -1 for a 31-day
    month

### Examples {#Examples}

#### Standard shift {#Standardshift}

Monday through Friday, 09:00 until 17:00 each day.

``` {.wiki}
accessTime = periodic weekly day 1-5 at 0900 + 000800
```

#### Second Shift {#SecondShift}

Monday Evening through Saturday Morning, 17:00 until 01:00 the following
day

``` {.wiki}
accessTime = periodic weekly day 1-5 at 1700 + 000800
```

#### Regularly Scheduled Maintenance Window {#RegularlyScheduledMaintenanceWindow}

The second Tuesday of every month, all day

``` {.wiki}
accessTime = periodic monthly on Tue between 8 and 14 at 0000 + 010000
```

#### The last Saturday of the month {#ThelastSaturdayofthemonth}

The last Saturday of the month, all day

``` {.wiki}
accessTime = periodic monthly on Sat between -7 and -1 at 0000 + 010000
```

#### One-time Maintenance Window {#One-timeMaintenanceWindow}

Saturday, Nov 20 2010 from 02:00 until 06:00

``` {.wiki}
accessTime = absolute 20101120200000 ~ 20101120060000
```
