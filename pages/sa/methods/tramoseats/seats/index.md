---
layout: left-menu
title: Seats
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Canonical decomposition of ARIMA models
category: TramoSeats
order: 300
---

## {{page.description}}

We consider in the description of SEATS a simplified model with two components (the signal and the noise):

$$ y_t = s_t + n_t $$

$$ \phi(B) \Delta(B) y_t = \theta(B)\epsilon_t $$

$$ \phi_s(B) \Delta_s(B) s_t = \theta_s(B)\epsilon_{st} $$

$$ \phi_n(B) \Delta_n(B) n_t = \theta_n(B)\epsilon_{nt} $$

The variances of the innovations are respectively $\sigma^2$, $\sigma^2_s$ and $\sigma^2_n$

The aggregation constraint yields:

$$ \phi(B) = \phi_s(B)\phi_n(B) $$

$$ \Delta(B) = \Delta_s(B)\Delta_n(B) $$

$$ 
\sigma^2\theta(B)\theta(F)=\sigma^2_s\phi_n(B)\Delta_n(B)\theta_s(B)\phi_n(F)\Delta_n(F)\theta_s(F) $$
$$ +\sigma^2_n\phi_s(B)\Delta_s(B)\theta_n(B)\phi_s(F)\Delta_s(F)\theta_n(F) 
$$


The estimator of the signal is obtained as

$$ \hat{s}_t = k_s \frac{\Psi_s(B)\Psi_s(F)}{\Psi(B)\Psi(F)}y_t$$