---
layout: left-menu
title: Moving trading days
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Trading days
order: 1000
category: variables
---
# {{page.description}}

$\alpha_i$ is the effect of day $i$, $\bar\alpha$ is the average of the TD effects,  $N_t=\sum_{i=1}^7 D_{it}$ is the number of days in the period $t$.

$$ \sum_{i=1}^7 \alpha_i D_{it}=\bar \alpha N_t + \sum_{i=1}^7 (\alpha_i - \bar \alpha) D_{it}$$

$$ {TD}_t=\sum_{i=1}^6 (\alpha_i - \bar \alpha)(D_{it}-D_{7t}) = \sum_{i=1}^6 \beta_i C_{it}$$


We introduce time varying trading days effect by supposing that the coefficients ($\alpha_i$ or $\beta_i$) follow a multivariate random walk.

#### Model I (Bell)

$\beta_{t+1} = \beta_t +\varepsilon_t$ where the covariance of the innovations is diagonal. Usually, we will use a single parameter (same variance for all the coefficients). 

In this model, the contrast day plays a special role. More specifically, the innovation of its coefficient is negatively correlated with all the other innovations and it has a larger variance (the sum of all the other variances).

#### Model II (Harvey)

$\alpha_{t+1} = \alpha_t +\varepsilon_t$ where the covariance of the innovations is diagonal. 

Using $\beta_{it}=\alpha_{it} - \bar \alpha_t$ we can easily derive the covariance of $\Delta \beta$. In the case of a single parameter (same variance for all coefficients, that we set to 1 to simplify), we get: 

$$cov(\Delta \beta) = \begin{pmatrix}6/7 & -1/7 & \cdots & -1/7 \\ -1/7 & 6/7  & -1/7 &\vdots \\ \vdots &\ddots & \ddots & -1/7 \\-1/7 & \cdots & -1/7 & 6/7 \end{pmatrix} $$

The generalization to different variances for each day is immediate.

In this model, all the days play the same role, which seems more attractive.

#### Other generalizations

This approach can be easily extended to other definitions of the trading days effects, obtained by putting the days in different groups and by defining the contrasts variables accordingly (see for instance the usual working days).

#### State space form

A linear regression component with time varying coefficients can be added in a straightforward way to any state space model. Using the usual notations, we have: 

State: $\tilde\alpha_t = \begin{pmatrix} \alpha_t \\ \beta_t\end{pmatrix}$

Measurement: $\tilde Z_t = \begin{pmatrix}Z_t && C_t\end{pmatrix}$, $\tilde H_t = H_t$

Transition: $\tilde T_t = \begin{pmatrix}T_t && 0 \\ 0 && I\end{pmatrix}$, $\tilde V_t = \begin{pmatrix}V_t && 0 \\ 0 && V_{\beta} \end{pmatrix}$

Initialization: $\tilde\alpha_0 = \begin{pmatrix} \alpha_0 \\ 0\end{pmatrix}$, $\tilde P_* = \begin{pmatrix}P_* && 0 \\ 0 && 0\end{pmatrix}$, $\tilde P_{\infty} = \begin{pmatrix}P_{\infty} && 0 \\ 0 && I\end{pmatrix}$

The model can be estimated using the usual algorithms (prediction error decomposition by means of the diffuse Kalman filter and smoothing of the results by the Kalman smoother).

#### Example

Estimation of time varying trading days for the Australian monthly retail trade (1982-2017)

For the results presented below, we appended the stochastic trading days to an airline model.

|Model| Log-likelihood | AIC | MA(1) | MA(12) | TD variance |
|-|-|-|-|-|-|
|Fixed|1087.6|-2171.2|-.65|-.69|0|
|Bell|1127.6|-2249.2|-.59|-.67|0.0002|
|Harvey|1125.1|-2244.3|-.59|-.66|0.0008|


