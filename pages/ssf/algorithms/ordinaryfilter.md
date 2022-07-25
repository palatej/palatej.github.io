---
layout: left-menu
title: Ordinary filter
tagline: JD+. State space models
description: State space model. Ordinary Kalman filter
category: Default
order: 10
---

# Ordinary filter

With the usual [notations](./index.md), we define the ordinary filter as follows:

#### Univariate model

##### Update step t

$$ e_t = y_t - Z_t a_t $$   

$$ C_t = P_t Z_t' $$  

$$ f_t= Z_t P_t Z_t' +h_t = C_tZ_t' + h_t $$  

$$ a_{t|t} = a_t + C_t f_t^{-1}e_t $$  

$$ P_{t|t}= P_t - C_t f_t^{-1} C_t' $$  


##### Forecast step t

$$ a_{t+1} = T_t a_{t|t} $$   

$$ P_{t+1} = T_t P_{t|t} T_t' + V_t $$   


##### Compact form

The two steps can be easily combined to give a more compact formulation.

$$ e_t = y_t - Z_t a_t $$   

$$ f_t= Z_t P_t Z_t' + h_t$$  

$$ K_t = T_t P_t Z_t' f_t^{-1} $$  

$$ a_{t+1} = T_t a_t + K_t e_t $$   

$$ P_{t+1} = T_t P_t T_t' - K_t f_t K_t' + V_t $$   

However, the current implementation uses explicitly the two steps form.

#### Multivariate model


In the multi-variate case, we use a slightly different (but strictly equivalent) implementation:

##### Update step t	

$$ e_t = y_t - Z_t a_t $$  

$$ F_t = Z_t P_t Z_t' + H_t = R_t R_t' \quad(Cholesky)$$  

$$ \tilde{K_t} = P_t Z_t' {R_t'}^{-1} \Leftrightarrow \tilde{K_t} R_t' = P_t Z_t'$$  

$$ u_t = R_t^{-1} e_t \Leftrightarrow R_t u_t = e_t $$  

$$ a_{t|t} = a_t + \tilde{K_t} u_t $$

$$ P_{t|t}= P_t - \tilde{K_t}\tilde{K_t}' $$  

##### Forecast step t

$$ a_{t+1} = T_t a_{t|t} $$   

$$ P_{t+1} = T_t P_{t|t} T_t' + V_t $$   

##### Special cases

This implementation is robust (the covariance matrices are symmetric by construction) and makes the computation of the likelihood easy. It also provides a straightforward solution for singular covariance matrices and for missing values.

When some observations are missing, we just remove from $Z_t$ the corresponding equations.

When the covariance matrix $F_t$ is singular, some columns of $R_t$ are equal to 0. Those columns correspond to "redundant" equations. The corresponding errors $u_t$  and the corresponding columns in the gain matrix are undefined (set to 0). The over-determined system $R_t u_t = e_t$ imposes some restrictions on the observations, which can be easily checked (the system must be solvable).

When the measurement errors are diagonal, it should be noted that the solution based on the Cholesky decomposition is identical to the so-called univariate treatment of multi-variate models.


### Implementation

The ordinary filter is implemented in the classes `demetra.ssf.univariate.OrdinaryFilter` and `demetra.ssf.multivariate.MultivariateOrdinaryFilter`.