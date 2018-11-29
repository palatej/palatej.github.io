---
layout: left-menu
title: Local level
tagline: JD+. State space models
description: Local level (= random walk)
category: SSF Block
order: 100
---
# {{page.description}}

#### Description

The local level block describes a random walk component. When the innovation variance is set to 0, it also describes a constant term (known when the initialization is specified, estimated otherwise)

$$ l_{t+1} = l_t + \epsilon_t $$

$$ \epsilon_t \sim N(0, \sigma^2_l)$$

#### State block

The state block is $\alpha_t=\begin{pmatrix} l_t  \end{pmatrix}$ 

#### Diffuse initialization 

$$ a_0 = 0$$

$$ P_*=  0 $$

$$ B= 1 $$


$$ P_\infty= 1 $$

#### Dynamics

$$ T_t = 1 $$

$$ V_t = \sigma^2_l $$

$$ S_t = \sigma_l $$

#### Default measurement

$$ Z_t = 1$$

#### Parameters

$$ \sigma^2_l \ge 0 $$

The block is represented by $\text{ll}(\sigma^2_l)$ or $\text{ll}_0(\sigma^2_l)$ in case of 0-initialization
