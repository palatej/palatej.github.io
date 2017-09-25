---
layout: left-menu
title: Ramp
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Ramp
order: 100
category: variables
---
{{page.description}}

A ramp $r$ is defined by its starting date $t_0$ and its ending date $t_1$

$$ r(t)=\begin{cases} -1 & for \quad t\le t_0 \\ \left(t-t_0\right)/\left(t_1-t_0\right)-1 & for \quad t_0\lt t \lt t_1 \\  0 & for \quad t\ge t_1\end{cases}$$

{: .alert .alert-danger role="alert"}
Different from 2.2. Return to the definition used in 2.1

In the case of regular time series (defined by the contiguous periods $\lbrace p_i \rbrace_{0 \le i \lt n}$), we adapt the definition as follows;

- $i_0$ is the period that contains $t_0$
- $i_1$ is the period that contains $t_1$

We then replace $t,t_0, t_1$ by $i,i_0, i_1$ in the definition of the ramp.

_For instance, the monthly ramp defined for the period 1-Jan-2017 : 30-Sep-2017 is -1 up to Jan-2017 inclusive and 0 after Sep-2017 inclusive._

<hr>

#### Implementation

Ramps are implemented in the class `demetra.timeseries.regression.Ramp`