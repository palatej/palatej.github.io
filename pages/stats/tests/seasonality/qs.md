---
layout: left-menu
title: QS test
tagline: technical documentation for JDemetra+ using GitHub Pages
description: QS Test for seasonality
category: Seasonality tests
order: 2010
---
# {{page.description}}

The QS test is a variant of the [Ljung-Box](../wn/ljungbox.html) test computed on seasonal lags, where we only consider positive auto-correlations

More exactly,

$$ qs=n \left(n+2\right)\sum_{i=1}^k\frac{\left[ \max  \left(0, \hat\gamma_{i \cdot l}\right)\right]^2}{n-i \cdot l}$$

The current implementation still considers that the statistics is distributed as a 
$$\chi \left(k\right)$$
even if it is obvioulsly incorrect.

Example of how results are displayed:
![qs](https://palatej.github.io/pages/stats/tests/seasonality/images/qs.png)