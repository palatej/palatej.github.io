---
layout: left-menu
title: State-Space form
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space form of the dynamic factor model
category: Estimation
order: 40
---
# {{page.description}}

### Description of the model

The model contains $m$ factors $F_t = \begin{pmatrix}f_{1,t}\\ \cdots \\ f_{m, t}\end{pmatrix}$. The dynamic of the factors is defined by a VAR with $p$ lags.

$$ F_t = A_1 F_{t-1} + \cdots + A_p F_{t-p} + \mu_t$$

### State array

The state array is a stack composed of all the lags of each factor.
The number of lags introduced in the state array ($q$) must be sufficent to deal with the dynamics of the model ($\ge p$), to deal with the different measurement equations and - eventually - to deal with the needs of a news analysis.
More formally, it is defined as:


$$ \alpha_t = \begin{pmatrix} f_{1,t} \\ \vdots \\ f_{1,t-q} \\ \vdots \\ f_{m,t} \\ \vdots \\ f_{m,t-q}\end{pmatrix}  $$