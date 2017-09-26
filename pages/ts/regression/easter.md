---
layout: left-menu
title: Easter
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Easter holiday
order: 20
category: variables
---
# {{page.description}}

The Easter variable defines a time period before Easter. The Easter effect is defined by the relative number of days that occurs in the different months (February, March, April and May for the JulianEaster) or quarters (first or second quarter). 
To avoid seasonal effects, the variable is corrected using long term mean corrections. Tramo uses a very simple correction: we remove 0.5 from March and from April (independently of the duration); X13 uses a more sophisticated solution. JD+ provides both solutions, with a correction based on the approximate theoretical distribution of Easter in the calendar.

For instance, using a duration of 10 and considering that the end day is Easter (see below), we have:

{: .table .table-bordered .table-striped}
| Year | Easter | #Days in March | #Days in April | Effect in March (not corrected) | Effect in April (not corrected) | March (Tramo) | April (Tramo) |
|2014|5 April|5|5|0.5|0.5|0|0|
|2015|27 March|10|0|1|0|0.5|-0.5|
|2017|16 April|0|10|0|1|-0.5|0.5|
|2018|1 April |9|1|.9|.1|0.4|-0.4|

Note that the Easter variable may be 0 in some years.
See below the specific features of Tramo-Seats and of X13 concerning Easter.

EASTER IN TRAMO
The Easter period in Tramo is defined by the daily period [end – duration, end] where end may be Easter -1 (legacy solution), Easter (default) or Easter Monday.
As mentioned above, the long term mean correction is always -.5 for March and for April.

EASTER IN X13
The Easter period in X13 is defined by the daily period [end – duration, end] where end is Easter-1.
The long term mean corrections have been computed on a long period, for all possible durations.

<hr>

#### Implementation

The computation of Easter is given by the class `demetra.timeseries.calendars.Easter`. The regression variable for Easter is given by  the class `demetra.timeseries.regression.EasterVariable`. The Easter variable is only computed for monthly and quarterly series.