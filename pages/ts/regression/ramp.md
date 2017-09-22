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

In the case of regular time series (defined by the contiguous periods $\lbrace p_i \rbrace_{0 \le i \lt n}$), we adapt the definition as follows;

- $i_0$ is the last period that starts strictly before $t_0$
- $i_1$ is the first period that finishes strictly after $t_1$

    _For instance, the monthly period corresponding to the starting date 1/1/2010 (or 31/12/2009) is December 2009 while the monthly period corresponding to 2/1/2010 is January 2010; the monthly period corresponding to the ending date 31/12/2010 (or 1/1/2011) is January 2011 while the monthly period corresponding to 30/12/2011 is December 2010. So, we suppose that only complete months are "included" in the ramp._ 



We then replace $t,t_0, t_1$ by $i,i_0, i_1$ in the definition of the ramp.