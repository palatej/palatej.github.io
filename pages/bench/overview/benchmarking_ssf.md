---
layout: left-menu
title: Generic SSF
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Generic state space form
order: 10
---

# Generic state space form


We write

$$y^C_t=\sum_{k=t-t \textsf{ mod }c}^t{y_k}$$

It represents the cumulator variable, from the beginning of each benchmarking period to the current period (included).

So, $y^C_t=\mathbf{y}_{t/c}$  when $t+1$ is a multiple of $c$ and is unobserved otherwise.


We consider that the unobserved disaggregated series has a state space form (SSF) identified by the state $\tilde\alpha_t$ and the system matrices $\left[ \tilde Z_t,\tilde H_t,\tilde T_t,\tilde V_t, \tilde S_t, \tilde a_{-1}, \tilde P_*,\tilde B,\tilde P_\infty \right]$ (see [Ssf model](../model.md) ).

The benchmarking SSF is the original SSF extended by the cumulator variable


### State vector

The state is $\alpha_t=\begin{pmatrix}y_t^{\underline C} \\ \tilde\alpha_t \end{pmatrix}$ 

### Initialization

$$ a_{-1} = \begin{pmatrix} 0 & \tilde a_{-1}\end{pmatrix}$$

<br>

$$ B = \begin{pmatrix} 0 \\ \tilde B\end{pmatrix}$$

<br>

$$ P_*= \begin{pmatrix} 0 & 0 \\ 0 &\tilde P_*\end{pmatrix} $$

<br>

$$ P_\infty= \begin{pmatrix} 0 & 0 \\ 0 &\tilde P_\infty\end{pmatrix} $$

### Dynamics

$$ T_t =\begin{cases}  \begin{pmatrix} 0 & 0 \\ 0 &\tilde T_t\end{pmatrix} & if\; {t+1} \textsf{ mod } c = 0 \\\begin{pmatrix} 0 & \tilde Z_t \\ 0 &\tilde T_t\end{pmatrix} & if\; t \textsf{ mod } c = 0 \\\begin{pmatrix} 1 & \tilde Z_t \\ 0 &\tilde T_t\end{pmatrix} &  otherwise \end{cases} $$

<br>

$$ V_t= \begin{pmatrix} 0 & 0 \\ 0 &\tilde V_t\end{pmatrix} $$

<br>

$$ S_t = \begin{pmatrix} 0 \\ \tilde S_t\end{pmatrix}$$


### Measurement

$$ Z_t = \begin{cases} \begin{pmatrix} 0 & \tilde Z_t \end{pmatrix} & if \; t \textsf{ mod } c = 0 \\ \begin{pmatrix} 1 & \tilde Z_t \end{pmatrix} & if \; t \textsf{ mod } c \neq 0\end{cases}$$


### Regression model

The regression model is now built on the cumulated series $y_t^C = X_t^C \beta+\mu_t^C$.

The problem is then a simple problem of missing observations, which can be easily computed by means of the Kalman smoother. 
