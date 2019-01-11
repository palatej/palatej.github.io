---
layout: left-menu
title: AR(p) 
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space representation of an AR model
category: "Arima"
order: 2011
---

# {{page.description}}

#### Introduction

The AR process is defined by

$$\Phi\left(B\right)y_t=\epsilon_t $$ 

where:  

$$\Phi\left(B\right)=1+\varphi_1 B + \cdots + \varphi_p B^p $$   

is an auto-regressive polynomial. 

Let $\gamma_i$ be the autocovariances of the model.

Using those notations, the state-space model can be written as follows :

##### State vector: 

$$ \alpha_t= \begin{pmatrix} y_t \\ y_{t-1} \\ \vdots \\ y_{t-p+1} \end{pmatrix}$$  


##### Dynamics

$$ T_t = \begin{pmatrix}-\varphi_1 & \cdots & \cdots  & -\varphi_p  \\
                        1          & \cdots &  \cdots &  0          \\ 
						\vdots     & \ddots &  \ddots & \vdots\\ 
						0          &   0    &  1      & 0  \end{pmatrix}$$

$$ S_t = \begin{pmatrix} \sigma_{ar} \\ 0 \\ \vdots\\ 0 \end{pmatrix} $$  

$$ V_t = S S' $$

#### Measurement

$$ Z_t = \begin{pmatrix} 1 & 0 & \cdots & 0\end{pmatrix}$$

$$ h_t = 0 $$

#### Initialization 

$$ \alpha_{-1} = \begin{pmatrix}1 \\ 0 \\ \vdots\\ 0 \end{pmatrix} $$  

$$ P_{*} = \Omega $$

$\Omega$ is the unconditional covariance of the state array; it can be easily derived using the MA representation. We have:

$$ \Omega\left(i,0\right) = \gamma_i $$  

$$ \Omega\left(i,j\right) = \Omega\left(i-1,j-1\right)-\psi_i \psi_j $$  

<hr>

#### Implementation

AR models are implemented in the class `demetra.arima.ssf.SsfArima`

