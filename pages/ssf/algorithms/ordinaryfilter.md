---
layout: left-menu
title: Ordinary filter
tagline: JD+. State space models
description: State space model. Ordinary Kalman filter
category: Default
order: 10
---

# Ordinary filter

Using the usual [notations](./notations.md) we define the ordinary filter as follows:

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

#### Multivariate model


In the multi-variate case, we use a slightly different (but strictly equivalent) implementation:

##### Update step t	

$$ e_t = y_t - Z_t a_t $$  

$$ F_t= Z_t P_t Z_t' + H_t = R_t R_t' \quad(Cholesky)$$  

$$ K_t = P_t Z_t' {R_t'}^{-1} \Leftrightarrow K_t R_t' = P_t Z_t'$$  

$$ u_t = R_t^{-1} e_t \Leftrightarrow R_t u_t = e_t $$  

$$ a_{t|t} = a_t + K_t u_t $$

$$ P_{t|t}= P_t - K_t K_t' $$  

##### Forecast step t

$$ a_{t+1} = T_t a_{t|t} $$   

$$ P_{t+1} = T_t P_{t|t} T_t' + V_t $$   

This implementation is robust (the covariance matrices are symmetric by construction) and makes the computation of the likelihood easy. 
Missing observations are excluded from the computation by adapting the size of the different matrices and arrays accordingly. In that way, we don’t have any problem of underdetermined systems. 

### Implementation

The ordinary filter is implemented in the classes `demetra.ssf.univariate.OrdinaryFilter` and `demetra.ssf.multivariate.MultivariateOrdinaryFilter`.