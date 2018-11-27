---
layout: left-menu
title: HC, HAC
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Heteroskedasiticy [and Autocorrelation] Consistent estimators 
category: Linear model
order: 1020
---
# {{page.description}}

### Background

We consider the regression model

$$ y = X \beta + \mu $$

The OLS estimator of $\beta$ is 

$$ \hat\beta= \left(X'X\right)^{-1}X'y $$

and the estimator of the residuals is

$$ \hat \mu= y- X \hat \beta = \left(I - X \left(X'X\right)^{-1}X'\right) y $$

If the covariance matrix of $\mu$ is $\Sigma$, the covariance matrix of $\hat\beta$ becomes

$$\left(X'X\right)^{-1}X'\Sigma X\left(X'X\right)^{-1}$$

If we write $B=\left(\frac{1}{n}X'X\right)^{-1}$ and $M=\frac{1}{n}\left(X'\Sigma X\right)$, we get $var\left(\hat\beta\right)=\frac{1}{n} BMB$ (sandwich estimator).

#### HC

The HC estimator is provided for $M=\sum_t {X_t'X_t \omega_t}$

Typical weighting functions $\omega$ are:

- HC0: $\omega_t=\hat{u}_t^2$
- HC1: $\omega_t=\frac{n}{n-k}\hat{u}_t^2$
- ...

#### HAC

If we write $\hat V_t=X_t \hat u_t$,

$$M=\frac{1}{n} \sum_{k=-l}^{k \le l} \left(w_k \sum_t{ V_t}'{V_{t+k}}\right)$$

Typically, we will use the Barlett's window function

$$ w_k = 1 - \frac{\mid k \mid}{l+1} $$ 


### Implementation

The routines for computing HC and HAC estimates are provided by the class `demetra.linearmodel.RobustCovarianceEstimators`

The computation of the M ("meat") matrices, which are estimates of the covariance matrix of $X \hat\mu$, are included in the class `demetra.stats.RobustCovarianceComputer`