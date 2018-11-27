---
layout: left-menu
title: Smoothed periodogram
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Smoothed periodogram
order: 30
category: analysis
---
# {{page.description}}

### Description 

The smoothed periodogram of the time series $y_t$ is defined by the following procedure:

- Remove the mean
- Apply a taper, if any

In formulae, we apply:

- $y_{1t}=y_t-\bar y_t$
- $\left[y_{2t}=taper(y_{1t})\right]$



### 