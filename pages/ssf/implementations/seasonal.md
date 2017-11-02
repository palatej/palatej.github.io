---
layout: left-menu
title: Seasonal
tagline: JD+. State space models
description: Seasonal component
category: STS
order: 3100
---
{{page.description}}

The seasonal component provided in JD+ is based on Proietti[2000]

We consider that it is composed of latent variables corresponding to each period, which follow a multivariate random walk. We also impose that the sum of the latent variables is 0 at each point time.

For a periodicity of $s$, we define the state space form of the seasonal component as follows (West-Harrison form):

#### State vector

We consider first the state vector $\tilde \gamma_t$ such that $\tilde \gamma_{it}$ is the (unobserved) seasonal component of season $i$ observed at time $t$.

Using that definition would imply a time varying measurement error. To avoid it, we use the state vector $\gamma_t$ which is a rotation of $\tilde \gamma_t$ such that the first component corresponds to the current period. More precisely, $\gamma_{it} =\tilde\gamma_{\left( \left(t-i\right) \mod s \right), t}$.

Moreover, the constraint that the sum of the latent variables is 0 allows us to consider only $s-1$ periods (the missing one being the opposite of the sum of all the other periods).

#### Dynamics

$$ T_t = \begin{pmatrix} 0 & 1 & \cdots & 0 \\ \vdots & \ddots & \ddots & \vdots \\ 0 &  \cdots & 0 & 1  \\ -1 & -1 & \cdots & -1\end{pmatrix}$$

The 

#### Measurement

$$ Z_t = \begin{pmatrix} 1 & 0 & \cdots & 0\end{pmatrix}$$

#### Bibliography

Proietti T. (2000), "Comparing seasonal components for structural time series models", International Journal of Forecasting, 16, 2, 247-260.