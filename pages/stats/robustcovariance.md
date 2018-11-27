---
layout: left-menu
title: Robust covariance
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Robust covariance
category: Descriptive statistics
order: 1000
---
# {{page.description}}

The robust covariance of the series $\lbrace x_t, y_t\rbrace_{0 \le t \lt N}$ is computed as follows:

$$cov(x,y)=1/N \sum_{k=-M}^M {\omega_k} \sum_{i}x_{i}y_{i+k} $$

