---
layout: left-menu
title: Approximate forecasts
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Forecasts of ARIMA models (X12 implementation)
category: Forecasts
order: 2010
---

# {{page.description}}

Using the definition of an [ARMA model](../index.md), we can compute recursively the ARMA forecasts of the series $\lbrace y_t\rbrace_{0 \lt t \le n}$ by the formula:

$$ y_{n+k}=-\phi_1 y_{n+k-1} - \cdots - \phi_p y_{n+k-p} + \theta_1 \hat \epsilon_{n+k-1} + \cdots +\theta_q \hat \epsilon_{n+k-q} $$

where $\hat \epsilon_t=0$ if $t \gt n$ or has been estimated otherwise.

A simple approximate solution consists in estimating by maximum likelihood the residuals corresponding to the pure moving average model obtained after applying the auto-regressive filter. This is exactly what is done in the method developed for the [X12 original program](./estimation/x12.md).

Such forecasts are optimal solution when the original ARIMA model doesn't contain any auto-regressive part. In the other case, they corresponds to the forecasts conditional to the first p observations and not to the full data set. 

A similar reasoning applies to non-stationary models.

#### Implementation

This solution is implemented in the class `demetra.arima.internal.FastArimaForecasts`