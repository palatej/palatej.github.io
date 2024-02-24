---
layout: left-menu
title: Array filter
tagline: JD+. State space models
description: Array filter
category: "Others"
order: 1030
---
# {{page.description}}

We shall use the following notations:

$$ P_t = L_t L_T'$$ 

$$ F_t = Z_t P_t Z_t' + H_t = Z_t P_t Z_t' + G_t G_t' = R_t R_t' $$

$$ K_t = T_t P_t Z_t' {R_t^{-1}}' $$

where $L_t$ and $R_t$ are lower triangular matrices.

The array form of the Kalman filter is described by the following sequence:

$$\begin{pmatrix}R_{t-1} & 0 & 0 \\ K_{t-1} & L_t & 0\end{pmatrix} \rightarrow \begin{pmatrix}G_t & Z_t L_t & 0 \\ 0 & T_t L_t & S_t\end{pmatrix} \rightarrow \begin{pmatrix}R_t & 0 & 0 \\ K_t & L_{t+1} & 0\end{pmatrix}$$

Given $L_t$, we can easily form the "pre-array" matrix defined in the second step. That matrix is then triangularized by means of usual orthogonal transformations. JD+ uses Givens rotations when the pre-array form is quasi-triangular and Householder reflections in the other cases.

The result of the triangularization corresponds necessarily to the matrices of the third step.

Indeed, we have that

$$ \begin{pmatrix}G_t & Z_t L_t & 0 \\ 0 & T_t L_t & S_t\end{pmatrix}\begin{pmatrix}G_t & Z_t L_t & 0 \\ 0 & T_t L_t & S_t\end{pmatrix}'=\begin{pmatrix}F_t & R_t K_t' \\ K_t R_t' & T_t P_t T_t' +V_t\end{pmatrix}$$  
  

$$=\begin{pmatrix}A & 0 & 0\\ B & C & 0\end{pmatrix}\begin{pmatrix}A & 0 & 0\\ B & C & 0\end{pmatrix}'=\begin{pmatrix}AA' & AB' \\ BA' & BB' + CC'\end{pmatrix}\Leftrightarrow \begin{cases}A=R_t \\B=K_t \\ C = L_{t+1} \end{cases}$$

The last equality comes from: $P_{t+1}=T_t P_t T_t' -K_t K_t' + V_t  \Leftrightarrow T_t P_t T_t'  + V_t = K_t K_t' + P_{t+1}$ 

The other quantities are computed as usual:

$$ u_t = R_t^{-1} e_t $$

$$ a_{t+1} = T_t a_{t} + K_t u_t  $$

---

### Implementation

The array filter is implemented in the classes `jdplus.ssf.array.ArrayFilter` and `jdplus.ssf.array.MultivariateArrayFilter`.

Those filters will use a modified representation of the state, which contains the Cholesky factor of its covariance matrix (see ``jdplus.ssf.array.LState``