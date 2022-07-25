---
layout: left-menu
title: General Model
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space model
order: 0
---

# {{page.description}}

The `general linear gaussian` state-space model can be written in many different ways. The form considered in JD+ 3.0 is presented below.

$$ y_t = Z_t \alpha_t + \epsilon_t,\quad \epsilon_t \sim N\left(0, \sigma^2 H_t\right),\quad t \gt 0 $$

$$ \alpha_{t+1} = T_t \alpha_t + \mu_t, \quad \mu_t \sim N \left(0, \sigma^2 V_t \right),\quad t \ge 0 $$

$y_t$  is the observation at period t, $\alpha_t$  is the state vector.
$\epsilon_t, \mu_t$ are assumed to be serially independent at all leads and lags and independent from each other.  
In the case of multi-variate models, $y_t$ is a vector of observations. However, in most cases, we will use the univariate approach by considering the observations one by one (univariate handling of multi-variate models). 

The innovations of the state equation will be modelled as 

$$ \mu_t = S_t \xi_t, \quad \xi_t \sim N\left( 0, \sigma^2 I\right) $$

In other words, $V_t=S_t S_t'$

The initial ($\equiv t=0$) conditions of the filter are defined as follows:

$$ \alpha_{0} = a_{0} + B\delta + \mu_{0}, \quad \delta \sim N\left(0, \kappa I \right),\: \mu_{0} \sim N\left(0, P_*\right)$$

where  $\kappa$ is arbitrary large. $P_*$ is the variance of the stationary part of the initial state vector and $BB'=P_\infty$
models the diffuse part. 

The definition used in JD+ is quasi-identical to that of Durbin and Koopman[1].

In summary, the model is completely defined by the following quantities (possible default values are indicated in brackets):

$$ \mathbf{Z_t}, \mathbf{H_t} [=0] $$

$$ \mathbf{T_t}, \mathbf{V_t} [=S_t S_t'], \mathbf{S_t} [=Cholesky(V)] $$ 

$$ \mathbf{a_{0}}[=0], \mathbf{P_*} [=0], \mathbf{B} [=0], \mathbf{P_\infty} [=BB'] $$

 
---

### Implementation details

#### Functional forms

State space forms and the related algorithms focus on the state vectors and their (conditional) distribution, and on the relationships between those vectors at different time points. For instance, using obvious notations, we will consider:

| Operations | Formulae |
|--|--|
| Initialization | $a_0$ |
| Prediction | $a_{t \vert t}\rightarrow a_{t+1 \vert t}$ |
| Update | $a_{t-1 \vert t}\rightarrow a_{t \vert t}$ |
| Prediction error | $e_t=y_t- \hat y_{t \vert t-1}$ |
| Smoothing | $a_{t \vert n} \rightarrow a_{t-1\vert n}$ |
| … | ... |

The relationships considered above are usually expressed under the form of matrices.  All things considered, matrices are only a convenient way for describing linear transformations. By replacing matrix computations (at least the most frequent and/or the most expansive ones) with equivalent functions, it is possible to achieve substantial performance gain. 

This is the basic principle of the JD+ state space framework: every type of model will have to provide a set of functions that allows an efficient computation of the different algorithms considered in the framework.

We shall clarify that point by an example. The prediction step is defined by the equations:

$$ a_{t+1 \vert t}=T_t a_{t \vert t}, \quad P_{t+1 \vert t}=T_t P_{t \vert t} T_t'+V_t=T_t \left(T_t P_{t \vert t} \right)'+V_t $$

 The transformation $f_{T_t} (x)$ of an array (and by extension, of a matrix) by means of the matrix $T_t$ plays thus a central role in the forecasting step:

*  Apply $f_{T_t}$ on $a$
*  Apply $f_{T_t}$ on each column of $P$ ; we get $Q$
* Apply $f_{T_t}$ on each row of $Q$ ; we get $O$
* Add $V_t$ to $O$

In the case of (partially) time invariant systems, we will usually omit in the documentation of the framework the subscript $_t$ of the different arrays/matrices/functions.

Using matrix computation, the transformation $f_{T_t}$ needs $r \times r$ multiplications, where $r$  is the length of the state array. In many cases, the functional form will involve at most $r$ multiplications and much less memory traffic.

For instance, in some SSF forms of ARIMA models (see Gomez-Maravall, 1994), the function $y=f_T(x)$ is defined by

$$ y_i = \begin{cases} x_{i+1} & 1 \le i \lt r  \\ -\sum_{k=1}^p {\varphi_k x_{r-k} } & i =r\end{cases} $$
 
which involved only $p$  (order of the autoregressive polynomial) multiplications.

As soon as direct matrix computations are avoided, the matrices of the system themselves don’t usually need to be created. That leads to another substantial gain in time and in memory space, especially in the case of time dependent systems.

#### Structure of a model

Each model is defined by three components:

- Initialization (defined in **jdplus.ssf.ISsfInitialization**)
- Dynamics (defined in **jdplus.ssf.ISsfDynamics**)
- Measurement(s) (defined in **jdplus.ssf.univariate.ISsfMeasurement** and in **jdplus.ssf.multivariate.ISsfMeasurements**)

The first two components are independent of the structure of the observations and constitute what is called in JD+ a "state component" (**jdplus.ssf.StateComponent**)

Generic models are defined in the class **jdplus.ssf.univariate.Ssf**, which is the default implementation of the interface **jdplus.ssf.univariate.ISsf** or **jdplus.ssf.multivariate.Ssf**, which is the default implementation of the interface **jdplus.ssf.multivariate.IMultivariateSsf**. 
To be noted that the modelled series is not attached to the definition of the state space form.

JD+ provides numerous atomic models/building blocks that can be combined to define more complex models. We list below the most important ones. See the corresponding documents for more information

- State components
    - ARMA, ARIMA (**jdplus.ssf.arima.SsfArima**), UCARIMA (**jdplus.ssf.arima.SsfUcarima**)
    - Structural time series
        - Local level:  **jdplus.ssf.sts.LocalLevel**
        - Local linear trend: **jdplus.ssf.sts.LocalLinearTrend**
        - Seasonal component: **jdplus.ssf.sts.SeasonalComponent**
        - Noise: **jdplus.ssf.sts.Noise**
        - Cyclical component: **jdplus.ssf.sts.CyclicalComponent**
        - Periodic harmonics: **jdplus.ssf.sts.PeriodicComponent**

    - Time varying coefficients, modelled by (multi-variate) random walks (**jdplus.ssf.basic.Coefficients** )


#### Algorithms

##### Generalities

The two basic algorithms related to state space models are filtering (computation of $a_{t|t-1}$) and (fixed interval) smoothing (computation of $a_{t|T}$).

JD+ provides several implementations of those algorithms and of variants of them. They are designed to solve the complications linked to diffuse (non stationary) models and/or to provide faster or more robust solutions. 

Those algorithms will often make use of slightly different representations of the state array anf of its covariance matrix. Moreover, following the objective (likelihood evaluation, outliers detection, smoothing, simulation...), more or less output should be stored.

Beside the algorithms themselves and their related state representations, the framework offers several output storages to improve the general performances of the processing.  

##### Ordinary filters

##### Handling of diffuse models

##### CKMS filters

##### Array filters

##### Others

##### State representations

##### Output
     
---

#### Bibliography

[1] _ANDERSON, B. D. O. and MOORE, J. B._ (1979), “Optimal Filtering”, Prentice Hall.

[2] _DE JONG P._ (1991): "Stable Algorithms For the State Space Model", Journal of Time Series Analysis, 12, 2, 143-157.

[3] _DURBIN J. AND KOOPMAN S.J._ (2012): "Time Series Analysis by State Space Methods", second edition. Oxford University Press.

[4] _GOMEZ, V. AND A. MARAVALL_ (1994): "Estimation, Prediction, and Interpolation for Nonstationary Series with the Kalman Filter", Journal of the American Statistical Association, 89(426), 611-624.

[5] _HARVEY, A.C._ (1989): "Forecasting, Structural Time Series Models and the Kalman Filter", Cambridge University Press.
