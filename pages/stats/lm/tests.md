---
layout: left-menu
title: Tests
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Tests on linear model
category: Linear model
order: 1020
---
# {{page.description}}

### Description

We consider the regression model $y = X \beta + \varepsilon$ with $\varepsilon \sim N(0, \sigma^2\Omega)$

The GLS estimator of $\beta$ is $\hat\beta=(X'\Omega^{-1}X)^{-1}X'\Omega^{-1}y$ and its covariance matrix is $\sigma^2(X'\Omega^{-1}X)^{-1}=\sigma^2 W$

The BLUE of $\sigma^2$ is $s^2=\hat\varepsilon \Omega^{-1} \hat\varepsilon/(n-k)=RSS/(n-k)$, where $\hat\varepsilon=y-X\hat\beta=(I-X(X'\Omega^{-1}X)^{-1}X'\Omega^{-1})y$

### Test on a single coefficient

$H_0: \beta_i=\alpha$, $H_1: \beta_i \neq \alpha$

$$t=\frac{\hat\beta_i-\alpha}{\sqrt{s^2 w_{ii}}} \; t \sim T(n-k)$$

### Test on multiple coefficients

$H_0: R\beta=\alpha$, $H_1: R\beta \neq \alpha$, $R \sim m\times k$

$$f=(R\hat\beta-\alpha)'(s^2 R W R')^{-1}(R\hat\beta-\alpha)/m=\frac{(R\hat\beta-\alpha)'(R W R')^{-1}(R\hat\beta-\alpha)/m}{RSS/(n-k)}, \; f\sim F(m, n-k)$$

