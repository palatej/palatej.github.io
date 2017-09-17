---
layout: left-menu
title: Array filter
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space model. Array filter
categoy: Main algorithms
order: 30
---
# Array algorithm

Using the following notations:

$$ P_t = L_t L_T'$$ 

$$ F_t = Z_t P_t Z_t' + H_t = Z_t P_t Z_t' + G_t G_t' = R_t R_t' $$

$$ K_t = T_t P_t Z_t' {R_t^{-1}}' $$

A square root array algorithm is based on the following consideration. Suppose that we triangularize a matrix $A$ by means of an orthogonal transformation $\Omega$.
We have then that $AA'=A\Omega \Omega' A'=BB'$

the array form of the Kalman filter is described by the following sequence:

$$\begin{pmatrix}R_{t-1} & 0 & 0 \\ K_{t-1} & L_t & 0\end{pmatrix} \rightarrow \begin{pmatrix}G_t & Z_t L_t & 0 \\ 0 & T_t L_t & S_t\end{pmatrix} \rightarrow \begin{pmatrix}R_t & 0 & 0 \\ K_t & L_{t+1} & 0\end{pmatrix}$$

The second step is defined by the "pre-array" matrix, which is triangularized by means of usual orthogonal transformations. JD+ uses Givens rotations when the pre-array form is quasi-triangular and Householder reflections in the other cases.

Indeed, we have that

$$ \begin{pmatrix}G_t & Z_t L_t & 0 \\ 0 & T_t L_t & S_t\end{pmatrix}\begin{pmatrix}G_t & Z_t L_t & 0 \\ 0 & T_t L_t & S_t\end{pmatrix}'=\begin{pmatrix}F_t & R_t K_t' \\ K_t R_t' & T_t P_t T_t' +V_t\end{pmatrix}$$

<br>

$$=\begin{pmatrix}A & 0 \\ B & C\end{pmatrix}\begin{pmatrix}A & 0 \\ B & C\end{pmatrix}'=\begin{pmatrix}AA' & AB' \\ BA' & BB' + CC'\end{pmatrix}\Leftrightarrow \begin{cases}A=R_t \\B=K_t \\ C = L_{t+1} \end{cases}$$

The other quantities are computed as usual:

$$ u_t = R_t^{-1} e_t $$

$$ a_{t+1} = T_t a_{t} + K_t u_t  $$

### Implementation

The array filter is implemented in the classes `demetra.ssf.array.ArrayFilter` and `demetra.ssf.array.MultivariateArrayFilter`.