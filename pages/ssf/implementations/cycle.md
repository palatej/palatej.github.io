---
layout: left-menu
title: Cycle
tagline: JD+. State space models
description: Cycle component
category: STS
order: 3050
---
# {{page.description}}

#### Introduction

A Cycle component is a special case of an AR2 component, which contains two complex conjugate roots. 

More precisely, it is defined by a period $\lambda$ and a dumping factor $\rho$. If $\gamma = \frac{2\pi}{\lambda}$, we have that

$$   \begin{pmatrix} y_{t+1} \\ y^*_{t+1}\end {pmatrix} = \begin{pmatrix} \rho \cos{\gamma} &&   \rho \sin{\gamma}\\  -\rho \sin{\gamma}  && \rho \cos{\gamma}\end {pmatrix}\begin{pmatrix} y_t \\ y_t^*\end {pmatrix}+\begin{pmatrix} \epsilon_t \\ \epsilon_t^*\end {pmatrix} $$

Using those notations, the state-space model can be written as follows :

##### State vector: 

$$ \alpha_t= \begin{pmatrix} y_t \\ y_t^* \end{pmatrix}$$  


##### Dynamics

$$ T_t = \begin{pmatrix} \rho \cos{\gamma} &&   \rho \sin{\gamma}\\  -\rho \sin{\gamma}  && \rho \cos{\gamma}\end {pmatrix}$$

$$ S_t = \sigma_c \begin{pmatrix} 1 && 0\\  0  && 1\end {pmatrix} $$  

$$ V_t = \sigma_c^2\begin{pmatrix} 1 && 0\\  0  && 1\end {pmatrix} $$

##### Measurement

$$ Z_t = \begin{pmatrix} 1 & 0 \end{pmatrix}$$

$$ h_t = 0 $$

##### Initialization 

$$ \alpha_{-1} = \begin{pmatrix}0 \\ 0 \end{pmatrix} $$  

$$ P_{*} =  \sigma_c^2\begin{pmatrix} \frac{1}{1-\rho^2} && 0\\  0  && \frac{1}{1-\rho^2}\end {pmatrix} $$


<hr>

##### Implementation

Cycle models are implemented in the class `jdplus.ssf.CyclicalComponent`

##### Bibliograhpy

Durbin J. and Koopman S.J [2012], Time Series Analysis by State Space Methods, second edition, Oxford University Press, §3.2.4  

