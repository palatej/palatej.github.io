---
layout: left-menu
title: Wiener-Kolmogorv estimators
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Wiener-Kolmogorov estimators
category: Seats
order: 100
---
## {{page.description}}


The estimator of the signal is obtained as

$$ \hat{s}_t = k_s \frac{\Psi_s(B)\Psi_s(F)}{\Psi(B)\Psi(F)}y_t=\nu(B, F)y_t$$

where $\Psi_i(x)=\frac{\theta_i(x)}{\phi_i(x)\Delta_i(x)}$ and $k_i=\frac{\sigma_i^2}{\sigma^2}$

$\nu(B, F)$ is the Wiener-Kolmogorv filter