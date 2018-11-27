---
layout: left-menu
title: Periodogram
tagline: technical documentation for JDemetra+ using GitHub Pages
description:  Periodogram
order: 20
category: analysis
---
# {{page.description}}

The raw periodogram of the series $\lbrace y_t\rbrace_{0 \le t \lt N}$ is defined by 

$$ p_t= 1/N \lvert \sum_{t=0}^{t \lt N}{y_t e^{-i \omega t}} \rvert^2$$

It is usually computed at Fourier frequencies, defined by $\omega_k=2\pi k/N$

It should be noted that the series should be corrected for mean or trend effects

### Implementation

The periodogram is implemented in the class `demetra.data.Periodogram`

