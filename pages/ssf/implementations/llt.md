---
layout: left-menu
title: Local linear trend
tagline: JD+. State space models
description: Local linear trend
category: SSF Block
order: 120
---
# {{page.description}}

#### Description

The local linear trend block describes the following trend component:

$$ l_{t+1} = l_t + n_t +  \epsilon_t $$
$$ n_{t+1} = n_t + \mu_t $$
$$ \epsilon_t \sim N(0, \sigma^2_l)$$
$$ \mu_t \sim N(0, \sigma^2_n)$$



#### State block

The state block is 

$$\alpha_t=\begin{pmatrix} l_t \\ n_t  \end{pmatrix}$$

#### Diffuse initialization 

$$ a_0 = 0$$

$$ P_*=  0 $$

$$ B= \begin{pmatrix} 1 && 0 \\ 0 && 1 \end{pmatrix} $$


$$ P_{\infty}= \begin{pmatrix} 1 && 0 \\ 0 && 1 \end{pmatrix} $$

#### Dynamics

$$ T_t = \begin{pmatrix} 1 && 1 \\ 0 && 1 \end{pmatrix} $$

$$ V_t = \begin{pmatrix} \sigma^2_l && 0 \\ 0 && \sigma^2_n \end{pmatrix} $$

$$ S_t = \begin{pmatrix} \sigma_l && 0 \\ 0 && \sigma_n \end{pmatrix} $$

#### Default measurement

$$ Z_t= \begin{pmatrix} 1 && 0 \end{pmatrix} $$

#### Parameters

$$ \sigma^2_l \ge 0,\quad \sigma^2_n \ge 0 $$

The block is represented by 

$$ \text{llt}(\sigma^2_l,\sigma^2_n) $$

#### Remarks

On occasion, the local linear trend can be split into two components:

* A smooth trend $=\text{llt}(0, \sigma^2_n)$
* A short-term component $=\text{ll}_0(\sigma^2_l)$