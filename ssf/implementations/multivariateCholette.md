## Multivariate Cholette

### Introduction

Given a set of initial time series $\left\lbrace z_{i,t}\right\rbrace_{i \in I}$ we have to find the corresponding  $\left\lbrace x_{i,t}\right\rbrace_{i \in I}$ that respect temporal aggregation constraints, represented by $\mathbf{x_{i,T}}=\sum_{t \in T}x_{i,t}$ and contemporaneous constraints given by $q_{k,t}=\sum_{j \in J_k}{w_{k,j}x_{j,t}}$ or, in matrix form $q_{k,t} = w_k x_t$

The Cholette's method consists in minimizing a quadratic penalty function that can take different forms. We consider in this paper the usual form:

$$ \sum_{i,t}{\left( \left( \frac{x_{i,t}-z_{i,t}}{|z_{i,t}|^\lambda} \right)-\rho \left( \frac{x_{i,t-1}-z_{i,t-1}}{|z_{i,t-1}|^\lambda} \right) \right)^2} $$


### State vector

The state space representation of the multi-variate benchmarking model is obtained by juxtaposing the different matrices of the univariate models (one for each series involved in the model) and by adding, for each linear constraint, the corresponding "measurement" equation.

More precisely, the state vector is

$$ \alpha_t = \begin{pmatrix} \left( \delta_{0,t} \gamma_{0,t}\right)^{\underline C} \\ \delta_{0,t} \\ \vdots \\ \left( \delta_{m,t} \gamma_{m,t}\right)^{\underline C} \\ \delta_{m,t} \end{pmatrix} $$


After that the constraints have been adapted to correspond to differences in comparison with the actual data, the vector of "observations" becomes
υ_t=(■(■(⋮@q ̃_0t@⋮)@q ̃_kt@■(⋮@δ_0s^C@■(⋮@δ_ns^C@⋮))))
and the measurement matrix is
Z ̅_t={█((■(■(1&γ_0t )&0&0@0&⋱&0@0&0&■(1&γ_nt )))  "if " t=c*T-1@(■(⋯&■(0&w_0 γ_it )&⋯&⋯@⋯&⋯&⋯&⋯@⋯&⋯&w_k γ_jt&⋯))" otherwise" )┤

In other words, the vector of the "observations" is composed of a sequence of contemporaneous constraints (for each t that doesn't correspond to the end of an aggregation period) and of temporal constraints  (for each t that corresponds to the end of an aggregation period); the matrices of the measurement equation are defined accordingly.
As mentioned above, the other matrices of the system are just the juxtaposition of the matrices defined in the univariate case. 
By construction, the smoothed states contain MMSE estimates of the δ_it that respect all the constraints of the model.
