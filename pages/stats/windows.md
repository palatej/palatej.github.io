---
layout: left-menu
title: Window functions
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Window functions
category: Descriptive statistics
order: 1000
---
# {{page.description}}

### Definitions

The window functions are defined on the interval [-1, 1].

- Bartlett: $w(x)=\mid 1-x\mid$
- Hamming: $w(x)=0.54+0.46 \cos \pi x$
- Parzen: $w(x)=\begin{cases} 1-6x^2+6x^3 & x \le .5 \\ 2 \left(1-x \right)^3 & x> 0.5\end{cases}$
- Square: $w(x)=1$
- Tukey: $w(x)=0.5 \times\left(1+\cos \pi x\right)$
- Welch: $w(x)=1-x^2$

### Implementation

Usual window functions are defined in the class `demetra.data.windowFunction`