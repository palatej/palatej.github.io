---
layout: left-menu
title: Diffuse initialization
tagline: JD+. State space models
description: Diffuse initialization (Durbin Koopman)
category: Initialization
order: 200
---
# {{page.description}}

We describe below the diffuse initialization of Durbin-Koopman and a variant that we call "partial square root initialization"

When $y_t$ is observed, we compute the following recursions 

$$ F_{*t} = Z_t P_{*t} Z_T' $$

$$ C_{*t} = T_t P_{*t} Z_T' $$

$$ F_{\infty t} = Z_t P_{\infty t} Z_T' $$

$$ C_{\infty t} = T_t P_{\infty t} Z_T' $$

$$ v_t = y_t - Z_t a_t $$

if $F_{\infty t}=0$

$$ a_{t+1} = T_t a_t + v_t F_{* t}^{-1} C_{* t} $$

$$ P_{\infty t+1} = T_t P_{\infty t} T_t'$$

$$ P_{* t+1} = T_t P_{*t} T_t' - C_{*t}  F_{*t}^{-1} C_{* t}'  + V_t$$

if $F_{\infty t}$ is invertible

$$ a_{t+1} = T_t a_t + v_t F_{\infty t}^{-1} C_{\infty t} $$

$$ P_{\infty t+1} = T_t P_{* t} T_t' - C_{\infty t} F_{\infty t}^{-1}  C_{\infty t}'$$

$$ P_{* t+1} = T_t P_{\infty t} T_t' - C_{\infty t} F_{\infty t}^{-1} F_{*t} F_{\infty t}^{-1} C_{\infty t}' - < C_{* t} F_{\infty t}^{-1} C_{\infty t}'> + V_t$$

where $\lt A \gt$ stands for $A+A'$



### Partial square root form

The partial square root form is trivially derived from the Durbin-Koopman equations, taking into account that $P_{\infty t}=B_t B_t'$.  

When $y_t$ is observed, we compute the following recursions 

$$ F_{*t} = Z_t P_{*t} Z_T' $$

$$ C_{*t} = T_t P_{*t} Z_T' $$

$$ F_{\infty t} = \left(Z_t B_t \right) \left(Z_t B_t \right)' $$

$$ C_{\infty t} = \left(T_t B_t \right) \left(Z_t B_t \right)' $$

$$ v_t = y_t - Z_t a_t $$

if $Z_t B_t=0$

$$ a_{t+1} = T_t a_t + v_t F_{* t}^{-1} C_{* t} $$

$$ B_{t+1} = T_t B_t$$

$$ P_{* t+1} = T_t P_{* t} T_t' - C_{*t}  F_{*t}^{-1} C_{*t}'  + V_t$$


if $Z_t B_t \neq 0$

$$ a_{t+1} = T_t a_t + v_t F_{\infty t}^{-1} C_{\infty t} $$

$$ P_{\infty t+1} = T_t P_{* t} T_t' - C_{\infty t} F_{\infty t}^{-1}  C_{\infty t}'$$

$$ P_{* t+1} = T_t P_{\infty t} T_t' - C_{\infty t} F_{\infty t}^{-1} F_{*t} F_{\infty t}^{-1} C_{\infty t}' - < C_{* t} F_{\infty t}^{-1} C_{\infty t}'> + V_t$$

$B_{t+1}$ is computed as follows:

* Choose an orthogonal transformation that transforms $Z_t B_t$ in $\begin{pmatrix}L_t &0&\cdots&0 \end{pmatrix}$; by default, JD+ takes Householder reflection(s)
* Apply that transformation on $T_t B_t$
* The first column(s) of the transformed $T_t B_t$ corresponds to $C_{\infty t} F_{\infty t}^{-1/2}$ and the remaining to $B_{t+1}$

That can be shown using the same arguments as in an array algorithm, applied on the transformations:

$$\begin{pmatrix} 0 \\ B_t \end{pmatrix} \rightarrow \begin{pmatrix} Z_t B_t \\ T_t B_t \end{pmatrix} \rightarrow \begin{pmatrix} F_{\infty t}^{1/2} & 0 \\ C_{\infty t} F_{\infty t}^{-1/2} & B_{t+1} \end{pmatrix}$$

Contrary to the usual array algorithm, we don’t compute a complete triangularization: processing the first rows, which correspond to the measurement equations, is indeed sufficient. So, in the case of a univariate series, we just have to use a single householder reflection to compute the next $B_{t+1}$. 
To be noted that that formulation shows in an obvious way that the rank of $B_t$ will decrease by $rank(F_{\infty t})$ at each step. That implies that, after every iteration, the matrix $B_t$ becomes smaller and the computations less expensive.

### Implementation

The Diffuse initialization is implemented in several classes

* The "Durbin Koopman" initialization of the filter is provided by the class `demetra.ssf.dk.DurbinKoopmanInitializer` 
* The corresponding "Durbin Koopman" smoother is provided by the class `demetra.ssf.dk.DiffuseSmoother` 
* The "Partial square root" initialization of the filter is provided by the class  `demetra.ssf.dk.sqrt.DiffuseSquareRootInitializer`
* The corresponding diffuse square root smoother is provided by the class  `demetra.ssf.dk.sqrt.DiffuseSquareRootSmoother`.