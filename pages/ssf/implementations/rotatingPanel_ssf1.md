---
layout: left-menu
title: Bias
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space of a rotating panels error structure
category: "Rotating Panel"
order: 2011
---

# {{page.description}}

#### [Error Specification in a Rotating Panel](../implementations/rotatingPanel_ssf0.html)

The error term $$e^{(i)}_{t}$$ has a particular structure
that is given by the rotating survey design:

$$
\begin{eqnarray}
e^{(i)}_{t} = \underbrace{ \color{red} b^{(i)}_{t}}_{\color{red} bias} + \underbrace{\varepsilon^{(i)}_{t}}_{autocorrelation}
\end{eqnarray}
$$

Here, we describe the $$\color{red} bias$$ component, which follows a random walk process. The sum of the bias terms accross waves is equal to zero:

$$ b^{(i)}_{t} = b^{(i)}_{t-1} + w^{(i)}_{t} $$, 

where $$w^{(i)}_{t} \sim N\left(0, \sigma^2_{i} \right)$$ and $$ b^{(1)}_{t} = -\sum_{i=2}^{W} b^{(i)}_{t} $$





##### State vectors: 

The block in the state vector corresponding to the bias component takes the following form

$$ \alpha_t= \begin{pmatrix} b^{(2)}_t \\ b^{(3)}_t\\ \vdots\\ b^{(W)}_t \end{pmatrix}$$  

[should I simply refer to the local level model?]

##### Dynamics

The identity matrix of size $$W$$ defines the motion equation of the bias component of each wave:

$$ T_t = \begin{pmatrix} 1 & 0 & \cdots & 0  \\  0 & 1 & \cdots & 0\\   \vdots & \vdots & \ddots & \vdots\\   0 & 0 & \cdots & 1 \end{pmatrix} $$


$$ S_t = \begin{pmatrix} \sigma_{1} & 0 & \cdots & 0  \\  0 & \sigma_{2} & \cdots & 0\\   \vdots & \vdots & \ddots & \vdots\\   0 & 0 & \cdots & \sigma_{W} \end{pmatrix} $$

$$ V_t = S S' $$

#### Diffuse initialization 

$$ a_0 =  \mathrm{0_{W \times 1}}$$

$$ P_*=   \mathrm{0_{W \times W}} $$

$$ B=  \mathrm{I_{W \times W}} $$

$$ P_\infty= \mathrm{I_{W \times W}} $$


 
#### Measurement

The measurement equation for each one of the $W$ waves incorporates the restriction that the bias component in the first wave 
plus the sum of the remaining ones equals zero, i.e. $$b^{(1)}_{t} = -\sum_{i=2}^{W} b^{(i)}_{t} $$. The resulting  $W \times (W-1)$ matrix
takes the following form:

$$ Z_t = \begin{pmatrix} -1 & -1 & \cdots & -1    \\  1 & 0 & \cdots & 0 \\   \vdots & \vdots & \ddots & \vdots\\   0 & 0 & \cdots & 1 \end{pmatrix} $$

$$ H_t = 0 $$



<br/>

#### Implementation

[check this]
ARMA models are implemented in the class `demetra.arima.ssf.SsfArima`

