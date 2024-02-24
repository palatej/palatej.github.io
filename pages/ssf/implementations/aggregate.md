---
layout: left-menu
title: Aggregate
tagline: JD+. State space models
description: Aggregation of state space models
category: Generic
order: 1050
---
{{page.description}}

## Introduction

We consider the aggregation of $n$ state space blocks such that the innovations of the transition equations are independent.   

## State block

The state vector is defined as the stack of the state vectors of the different models

$$ \alpha_t = \begin{pmatrix} \alpha_{1t} \\ \vdots \\ \alpha_{nt} \end{pmatrix}$$

#### Dynamics and initialization

$$ T_t = \begin{pmatrix} T_{1t} & 0 & \cdots & 0 
\\ 0 & T_{2t} & 0 & \vdots \\ \vdots & \ddots & \ddots & \vdots\\ 0 & \cdots & 0 & T_{nt} \end{pmatrix} $$

The other matrices of the transition equation and of the initialization are defined in a similar way.

#### Measurement

$$ Z_t = \begin{pmatrix} Z_{1t} & \cdots & Z_{nt} \end{pmatrix} $$

$$ H_t = H_{1t} $$ 

<hr>

#### Implementation

Aggregate models are implemented in the classes `demetra.ssf.implementations.CompositeSsf` and  `demetra.ssf.implementations.MultivariateCompositeSsf`


