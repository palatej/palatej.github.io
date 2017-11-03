---
layout: left-menu
title: Implementation
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Implementation of news analysis in JDemetra+ 
category: News
order: 60

---
# {{page.description}}

The weights associated to each piece of news are calculated as follows:

$$
\begin{equation}
\underbrace{\left[ w^{k,h}_{1}  \ldots w^{k,h}_{J}\right]}_{w} =  \underbrace{E[y_{k,t+h}\mathcal{I}^{'}]}_{A} \underbrace{E[\mathcal{I}\mathcal{I}^{'}]^{-1}}_{(LL')^{-1}} 
\end{equation}
$$

In order to calculate the weights, we use the Kalman smoother for the determination of the precision matrices, which are an essential part of the formula: 

- The covariance between the target variable and the news vector has the following form:

$$
\begin{equation}
 E[y_{k,t+h}\mathcal{I}^{'}]=\left[ \begin{array}{c}
\Lambda_{k} E \left[ \left( \mathrm{f_{t_{k}}}- E[\mathrm{f_{t_{k}}}|\mathcal{F}^{old}] \right)\left( \mathrm{f_{t_{1}}}- E[\mathrm{f_{t_{1}}}|\mathcal{F}^{old}]  \right) \right] \Lambda^{'}_{i_{1}}  \\
\Lambda_{k} E \left[ \left( \mathrm{f_{t_{k}}}- E[\mathrm{f_{t_{k}}}|\mathcal{F}^{old}] \right)\left( \mathrm{f_{t_{2}}}- E[\mathrm{f_{t_{2}}}|\mathcal{F}^{old}]  \right) \right] \Lambda^{'}_{i_{2}}  \\
\vdots \\
\Lambda_{k} E \left[ \left( \mathrm{f_{t_{k}}}- E[\mathrm{f_{t_{k}}}|\mathcal{F}^{old}] \right)\left( \mathrm{f_{t_{J}}}- E[\mathrm{f_{t_{J}}}|\mathcal{F}^{old}]  \right) \right] \Lambda^{'}_{i_{J}}    
\end{array} 
\right]
\end{equation}
$$

- The covariance of the news vector can be written as follows:

$$
\begin{equation}
 E[\mathcal{I}\mathcal{I}^{'}]_{j,l}=
\Lambda_{i_{j}} E \left[ \left( \mathrm{f_{t_{j}}}- E[\mathrm{f_{t_{j}}}|\mathcal{F}^{old}] \right)\left( \mathrm{f_{t_{l}}}- E[\mathrm{f_{t_{l}}}|\mathcal{F}^{old}]  \right) \right] \Lambda^{'}_{i_{l}} + E[\mathrm{e_{i_{j},t_{j}}}\mathrm{e_{i_{l},t_{l}}}]
\end{equation}
$$


Our implementation can be summarized in a few simple steps:

1. ```computeNewsCovariance()``` computes a lower-triangular matrix `lcov_`, which is the Choleski factor of $$ E[\mathcal{I}\mathcal{I}^{'}] $$

2. ```weights(int series, TsPeriod p)``` first stores  $$ E[y_{k,t+h}\mathcal{I}^{'}] $$ in a DataBlock `a`, and then it solves the system without the need to invert $$ E[\mathcal{I}\mathcal{I}^{'}] $$

3.   The  **weights**  are computed by solving two systems, which can be represented in matrix notation: 
		- First, calculate $$B=wL$$ by solving $$LB’ =A’$$ using the `rsolve` method contained in the class lower triangular 
		- Second, calculate $$w$$ by solving  $$wL=B$$  using the `lsolve` method 