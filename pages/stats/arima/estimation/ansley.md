---
layout: left-menu
title: Ansley
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Ansley algorithm
category: Arima estimation
order: 520
---
## Ansley algorithm

### Short description

We consider the following stationary ARMA model of order $(p, q)$ 

$$ 
\Phi \left(B \right) y_t = \Theta \left(B \right) \epsilon_t 
$$

Consider the transformation 

$$
\begin{equation}
z_t=
\begin{cases}
y_t & (t=0, \cdots, p-1)
\\ 
w_t=\Phi(B)y_t & (t=p, \cdots, n)
\end{cases}

\end{equation}
$$



The covariance matrix $\Omega_z^2$ of $z_t$ is a band matrix with maximum bandwith $m= \max(p, q+1)$. More explicitly:

$$
\Omega_z^2 =
\begin{pmatrix}
\Omega_{y,p}^2 & cov(y, w)_{p \times (m-p)} & 0  \\
cov(w,y)_{(m-p) \times p} & \Omega_{w, m-p}^2 & 0 \\
0 & 0 & \Omega_{w, n-m}^2 
\end{pmatrix}
$$

where $\Omega_{y,k}^2, \Omega_{w,k}^2$  are the covariances of $y, w$ for $k$ observations. 

Using the Wold representation of $y$, it is easy to see that 

$$
cov(y_t,w_t+i)=
\begin{cases}
\sum_{j=i}^{j \le q}{\theta_j \psi_{j-i}} & (1\le i \le q) \\
0 & i \gt q
\end{cases}
$$ 

There exist efficient algorithms to compute the (banded) Cholesky factor $L$ of $\Omega_z^2$

$L^{-1}y$ can then be computed recursively and the determinant of $\Omega_z^2$ can be trivially retrieved from $L$


### Implementation

The algorithm is implemented in the class `internal.toolkit.base.core.arima.AnsleyFilter`

It should be noted that our implementation slightly differ from the original paper (which contains some typos/mistakes), but that it follows its main ideas.


### Bibliography

[1] ___Ansley C.F.___ (1979), "An algorithm for the exact likelihood of a mixed autoregressinve-moving average process", Biometrika, 66, 1, 59-65.