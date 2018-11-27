---
layout: left-menu
title: Estimation
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Fractional airline model
category: Canonical decomposition
order: 40
---

# {{page.description}}

Suppose that the period of the series $y_t$ is $p$, which might be non integer.

The fractional airline model of the series is defined by 

$$\left(1-B\right)\left(1- \left( 1-\alpha \right) B^q - \alpha B^{q+1}\right)y_t= \left(1-\theta B\right)\left(1-\theta_s \left( 1-\alpha \right) B^q - \theta_s \alpha B^{q+1}\right) \epsilon_t$$

where $q$ and $\alpha$ are respectively the integer and the fractional parts of $p$.

The auto-regressive polynomials of the decomposition are defined by $\left( 1-B\right)^2$ for the trend and $1+B+\cdots +B^{q-1}+ \alpha B^q$ for the seasonal component.

