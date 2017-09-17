---
layout: left-menu
title: Likelihood evaluation
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Likelihood evaluation
order: 20
---

# {{page.description}}

### Stationary models

When the initial state of the model is completely specified (no diffuse elements), the Kalman filter provides the exact likelihood in a trivial way, using the prediction error decomposition:

$$ p(y_1, \ldots, y_n) = p(y_1) p(y_2\vert y_1) \ldots p(y_n\vert y_1 \ldots, y_{n-1})$$  

So, by concentrating the scaling factor $\sigma^2$ out of the likelihood, we get, using the notations defined for the [ordinary filter](./ordinaryfilter.md):

univariate case:

$$\log l_c(\theta \vert y)=-1/2\left(n \log(2 \pi) + n  + n\log \frac{1}{n}\sum_{i=1}^n e_i^2/f_i + \sum_{i=1}^n {\log \vert f_i \vert }\right)$$


multi-variate case:

$$\log l_c(\theta \vert y)=-1/2\left(n \log(2 \pi) + n  + n\log \frac{1}{n}\sum_{i=1}^n u_i' u_i + 2\sum_{i=1}^n {\log \vert R_i \vert }\right)$$

### Diffuse models

We define the diffuse likelihood as 

$$l(y\vert \theta, \sigma^2) = \lim_{k \rightarrow \infty} \left(l(y \vert k, \theta,\sigma^2)  (2 \pi \sigma^2 k)^{d/2}\right)$$

This is similar to Francke et al.(2010), (equation 14).
Apart from the scaling factor, it also identical to the approach of Ansley and Kohn (1985) (theorem 5.1). 

The expression of the log-likelihood for stationary model as to be corrected by the term

$$ -1/2 \sum_{i=1}^d {\log \vert F_{\infty, i} \vert }$$

to get the diffuse likelihood by means of the approach of [Durbin and Koopman](dk/md). To simplify the notations, we considered above that the diffuse initialization is performed with the first $d$ observations. See DK for the general case. 

 #### Bibliography
ANSLEY F. C. and KOHN R. (1985), “Estimating, filtering and smoothing in state space models with incompletely specified initial conditions”, The annals of statistics, vol. 13, n°4, 1286-1316.  

DURBIN J. AND KOOPMAN S.J. (2012): "Time Series Analysis by State Space Methods", second edition. Oxford University Press.

FRANCKE, M. K., KOOPMAN, S. J. and DE VOS, A. F. (2010), “Likelihood functions for state space models with diffuse initial conditions”, Journal of Time Series Analysis, 31, 6.


 #### Implementation

 The diffuse likelihood is implemented in the class `demetra.ssf.dk.DkLikelihood`. The likelihood of stationary models is handled by the same class.
 The computation of the diffuse likelihood is generate by the method `likelihoodComputer` of the class `demetra.ssf.dk.DkToolkit` or by one of its variants.