---
layout: left-menu
title: Regression
tagline: JD+. State space models
description: Regression variables
category: Generic
order: 1100
---
{{page.description}}

Regression variables $X_1, \cdots,X_k$ can be added to any state space model by extending the state with the regression coefficients ($\gamma = \gamma_1, \cdots,\gamma_k$).
We consider that the initial model has a state space form (SSF) identified by the state $\tilde\alpha_t$ and the system matrices $\left[ \tilde Z_t,\tilde H_t,\tilde T_t,\tilde V_t, \tilde S_t, \tilde a_{-1}, \tilde P_*,\tilde B,\tilde P_\infty \right]$ (see [Ssf model](../model.md) ).

The vectors and the matrices of the extended model are defined in a straightforward way. We consider below fixed and variable coefficients.

### State vector

The state is $\alpha_t=\begin{pmatrix}\tilde\alpha_t \\ \gamma_t \end{pmatrix}$ 

### Initialization

$$ a_{0} = \begin{pmatrix} \tilde a_{0} \\ 0 \end{pmatrix}$$

$$ B = \begin{pmatrix} \tilde B\ & 0 \\ 0 & I \end{pmatrix}$$

$$ P_*= \begin{pmatrix} \tilde P_* & 0 \\ 0 & 0 \end{pmatrix} $$

$$ P_\infty= \begin{pmatrix} \tilde P_\infty & 0 \\ 0 & I  \end{pmatrix} $$

### Dynamics

$$ T_t =\begin{pmatrix} \tilde T_t & 0 \\ 0 & I\end{pmatrix}  $$

Fixed (case 1) or variable (case 2) coefficients are defined by means of the innovations of the transition equation 

$$ V_t= \begin{cases}\begin{pmatrix} \tilde V_t & 0 \\ 0 & 0\end{pmatrix} \\ \begin{pmatrix} \tilde V_t & 0 \\ 0 & \Gamma_t\end{pmatrix}\end{cases}$$

<br>

$$ S_t= \begin{cases}\begin{pmatrix} \tilde S_t & 0 \\ 0 & 0\end{pmatrix} \\ \begin{pmatrix} \tilde S_t & 0 \\ 0 & _t\end{pmatrix}\end{cases}$$

### Measurement

$$ Z_t = \begin{cases} \begin{pmatrix} 0 & \tilde Z_t \end{pmatrix} if \; t \mod c = 0 \\ \begin{pmatrix} 1 & \tilde Z_t \end{pmatrix} if \; t \mod c \neq 0\end{cases}$$

