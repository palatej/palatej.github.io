---
layout: left-menu
title: Ljung-Box
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Ljung-Box test
order: 100
---
# {{page.description}}

#### Overview

The Ljung-Box test checks the "overall" randomnes of a time series using a given number of [autocorrelations](../../descriptive.md).   
It tests wether any of a group of autocorrelations of a time series are significantly different from 0.

#### Algorithm

We consider the autocorrelations
$$ \hat\gamma_l, \cdots, \hat\gamma_{l\cdot k}$$

The value of the test is defined by
$$ lb=n \left(n+2\right)\sum_{i=1}^k\frac{\hat\gamma_{i \cdot l}^2}{n-i \cdot l}$$

It is asymptotically distributed as a 
$$\chi \left(k\right)$$


#### Implementation

This test is implemented in the class `demetra.stats.tests.LjungBoxTest`

#### Example

```java
    int N=100;
    DataBlock X=DataBlock.make(N);
    Random rnd=new Random();
    X.set(rnd::nextDouble);
    OrderedSampleWithZeroMean sample=OrderedSampleWithZeroMean.of(X);
    LjungBoxTest lb=new LjungBoxTest(sample);
    StatisticalTest test = lb.lag(3).autoCorrelationsCount(10).build();
```
