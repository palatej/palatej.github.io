---
layout: left-menu
title: Leap year
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Leap year and length of period variables
order: 30
category: variables
---
# {{page.description}}

This regression variable is defined for regular domain, with a periodicity lower or equal to one month and higher or equal to one year.

### Leap year

The leap year variable is defined as follows:

- $v(t)=0.75$ if the period $t$ contains February and if the corresponding year is a leap year 
- $v(t)=-0.25$ if the period $t$ contains February and if the corresponding year is not a leap year 
- $v(t)=0$ otherwise.

### Length of period

The length of period variable is defined as follows:

We suppose that $f$ is the annual frequency of the series.

- $v(t)=D-m$ where $D$ is the number of days in the period $t$ and $m=365.25/f$ is the average number of days in one period.

### Implementation

This variable is implemented in the class ```demetra.modelling.regression.LengthOfPeriodVariable ``` 