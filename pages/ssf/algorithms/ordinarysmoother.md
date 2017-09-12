---
layout: left-menu
title: Ordinary smoother
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space model. Ordinary Kalman smoother
order: 100
---

# Ordinary smoother (univariate)

#### Notations

$a_t, P_t, C_t \left(=P_t Z_t' \right), f_t, e_t$ are quantities obtained in the [filtering process](./ordinaryfilter.md). $r_t, r_{0t}, r_{1t}$ are auxiliary row-matrices, while $N_t,N_{0t},N_{1t}, N_{2t}$
are auxiliary square matrices.
Except $r_{0t},N_{0t}$ which are initialised with the last values of $r_t,N_t$, those objects are set to 0 at the beginning of the process.

The following notations are used: 

$$ \tilde a_t=E\left(\alpha_{t} \vert y_0 \cdots y_{n}\right)$$  

$$ \tilde P_t=var\left(\alpha_{t} \vert y_0 \cdots y_{n}\right)$$  

$$ \tilde e_t=E\left(\epsilon_{t} \vert y_0 \cdots y_{n}\right)$$ 


#### Normal recursions

##### Observed t

$$ K_t = T_t C_t / f_t $$  

$$ \tilde e_t = v_t / f_t - r_t K_t  $$  

$$ \left[var \tilde e_t = 1/f_t + K_t' N_t K_t \right]$$  

$$ r_{t-1} = \tilde e_t Z_t + r_t T_t $$  

$$ \left[L_t = T_t - K_t Z_t \right]$$  

$$ \left[N_{t-1} = Z_t' Z_t / f_t + L_t' N_t L_t \right]$$  

##### Missing t   

$$ r_{t-1} = r_t T_t $$  

$$ \left[N_{t-1} = T_t' N_t T_t \right]$$  

##### Smoothed states 

$$ \tilde a_t' = a_t' + r_t P_t $$  

$$ \left[\tilde P_t = P_t + P_t N_t P_t \right] $$  

##### Smoothed disturbances

$$ \tilde u_t = r_t S_t $$   

$$ \left[var\left(\tilde u_t \right) = V_t-S_t' N_t S_t \right] $$ 	


#### Implementation details

The ordinary smoother for univariate models is implemented in the class ___demetra.ssf.univariate.OrdinarySmoother___ of the library _demetra-ssf_  

The current implementation computes successively the following quantities (observed case; operations marked with an asterisk don't imply actual matrix computations; they use functional forms):  

$$ x = r_t T_t \quad *$$

$$ \tilde e_t =\left( v_t-x C_t\right)/f_t $$

$$ r_{t-1} = x + \tilde e_t Z_t \quad *$$

$$ A = xl(xl(N_t)') $$

##### xl operator
The operator $xl(y) = y(T_t - K_t Z_t)$ is computed as follows

$$ q = y T_t \quad *$$

$$ w = q C_t $$

$$ xl(y) = q - w/f_t Z_t \quad *$$

It can be applied on each row of a matrix 

### Implementation

The ordinary smoother is implemented in the classes `demetra.ssf.univariate.OrdinarySmoother` and `demetra.ssf.multivariate.MultivariateOrdinarySmoother`.