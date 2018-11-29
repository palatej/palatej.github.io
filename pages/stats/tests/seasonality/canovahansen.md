---
layout: left-menu
title: Canova-Hansen test
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Canova-Hansen test
category: Seasonality tests
order: 2040
---

# {{page.description}}

### Method 1 (Gretl)


### Method 2 (Proietti)

We consider the following least squares problem:

$$ y = X \beta + \epsilon$$

For $f \neq \pi$, $X$ takes the form

$$  \begin{cases} X_{0,j}=1 \\ X_{1,j}=\cos(jf) \\ X_{2,j}=\sin(j f) \\ \left[ X_{3,j}=j \right] \\ \left[X_{4,j}=j \cos(jf)\right]  \\ \left[X_{5,j}=j \sin(j f)\right] \end{cases}$$

In most case, we don't take into account the linear trend (column 3) and the seasonal trends (columns 4,5)
If $f=\pi$, we have to suppress the columns 2 and 5. 

We compute the residuals $e=y-X\hat \beta$ of the least squares problem.

A robust estimator of the variance of the residuals is computed by means of the Newey-West algorithm:

$$\sigma_r^2 = \sum_{-l}^{l} w_l \text{acf}_e(l) $$

When the truncation lag $l$ is 0, the robust estimator is the usual estimator of the variance.

By default, the weighting function is the Bartlett's window $\left(w_i=1-\mid i \mid/\left(l+1\right)\right)$, but any other one could be choosen.

We define the matrix Z as follows

$$\begin{cases}Z_{0,j}=\sum_{k=0}^j e_k \cos k f \\ \left[Z_{1,j}=\sum_{k=0}^j e_k \sin k f \right] \end{cases}$$

The Canova-Hansen statistics is than defined by

$$\begin{cases}\left(\sum_{k=0}^{k \lt n} Z_{0,k}^2 \right)/\left(n^2 \sigma_r^2 \right) & f = \pi \\ 2\left( \sum_{k=0}^{k \lt n} \left(Z_{0,k}^2 + Z_{1,k}^2 \right)\right)/\left(n^2 \sigma_r^2 \right) & f \neq \pi \end{cases}  $$