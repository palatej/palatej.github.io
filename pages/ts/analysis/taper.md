---
layout: left-menu
title: Taper
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Taper
order: 50
category: analysis
---
# {{page.description}}

### Description 

Tapering consists of altering the ends of the (mean-adjusted) series so that they taper gradually down to zero.

An example of tapering is the TUKEY-HANNING Taper: the series is modified at the beginning at the end by means of a cosine transformation.

More exactly, if $\alpha$ is the proportion of the data being tapered, we have (using $l=\alpha n/2$):

$$x_i^{taper}=\begin{cases}0.5 x_i (1-\cos{ \pi i/l}) & i \lt l \\ 0.5 x_i (1-\cos{ \pi (n-i)/l}) & i \gt n-l \\ x_i & otherwise\end{cases}$$

### Implementation

The generic interface for tapers is ```demetra.data.ITaper```

The TUKEY-HANNING Taper is implemeted in ```demetra.data.TukeyHanningTaper```

```java
        double[] x=new double[60];
        DataBlock X=DataBlock.ofInternal(x);
        Random rnd=new Random();
        X.set(rnd::nextGaussian);
        TukeyHanningTaper taper=new TukeyHanningTaper(.5);
        System.out.println(X);
        taper.process(x);
        System.out.println(X);

```
![OverviewTags](/assets/img/tapering.png)

