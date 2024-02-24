---
layout: left-menu
title: Implementation
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Estimation of dynamic factor models in JDemetra+ 
category: Estimation
order: 45
---
# {{page.description}}

### Expectations-Maximization (EM) algorithm (`DfmEM`)

Remember the modeling framework: 

$$ 
\begin{align*}
y_{t} =&\Lambda f_{t} + \psi_{t}&, \text{with  }  \psi_{t}\sim N(0,R_{\psi}) \\
f_{t} =&A_{1} f_{t-1}  + \ldots + A_{p} f_{t-p} +  u_{t}&,\text{with  } u_{t} \sim  N(0,Q)  
\end{align*} 
$$ 
where $\psi_{t}$ represents the measurement error, which is assumed to be independent from the factor innovations $u_{t}$. 

The EM algorithm can be used to obtain initial values that will be fed into the numerical optimization procedures described below.
The algorithm works by iterating two steps. The  `EStep()` (**expectation step**)  
runs the Kalman filter recursions and compute the likelihood, while the `MStep()` (**maximization**
step), new parameter values are computed. The new parameter values obtained at each maximization step are calculated 
by solving the first order conditions for  $\Lambda$, $R$, $A$ and $Q$  with 
respect to the joint log likelihood of the data and the 
factors ([resource](https://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf)). 

$$ 
\begin{align*}
log \quad \ell(f_{-p+1},\ldots, f_{0}, f_{1}, \ldots,  f_{T}, y_{1},\ldots,  y_{T}|\theta)= \nonumber \\
- \frac{1}{2} log \left|\bar{Q}_{0}\right| - \frac{1}{2} \bar{f}^{'}_{0}\bar{Q}^{-1}_{0} \bar{f}_{0} -  \frac{T}{2}log \left|Q\right|  
- \frac{1}{2}\mathrm{tr}\left[ Q^{-1}\sum^{T}_{t=1} (f_{t}-A \bar{f}_{t-1})(f_{t}-A \bar{f}_{t-1})^{'}\right]   \nonumber \\
- \frac{T}{2} log \left|R_{\psi}\right| - \frac{1}{2}\mathrm{tr}\left[ R_{\psi}^{-1}\sum^{T}_{t=1} (y_{t}-\Lambda f_{t})(y_{t}-\Lambda f_{t})^{'}\right]   
\end{align*}
$$ 

where $\bar{f}_{t}$  is a vector containing the first $p$ lags of $f_{t}$ with a parameters vector $\theta=\bar{f}_{0},\bar{Q}_{0},Q,A, R_{\psi},\Lambda$. Note that
$A=[A_{1}\ldots A_{p}]$ and it is therefore different from the transition matrix of the state-space representation of the model.

The equations resulting from the M-step at each iteration $i$ follow. Note that they are calculated under 
the assumption that the initial conditions are given ( i.e.  $ \bar{f}_{0},\bar{Q}_{0}$  are fixed):


$$ 
\begin{align*}
A^{(i)} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t}\bar{f}^{'}_{t-1}|\Omega_{T}]\right)  \left(\sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[\bar{f}_{t-1}\bar{f}^{'}_{t-1} | \Omega_{T}]\right)^{-1}  \\
\Lambda^{(i)} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[y_{t}f^{'}_{t}|\Omega_{T}]\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t}f^{'}_{t}|\Omega_{T}]\right)^{-1} \\
Q^{(i)} &=& \left( \frac{1}{T} \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t}f^{'}_{t}|\Omega_{T}]- A^{i} \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t-1}f^{'}_{t}|\Omega_{T}] \right)  \\
R^{(i)}_{\psi} &=& diag \left( \frac{1}{T} \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[y_{t}y^{'}_{t}|\Omega_{T}]- \Lambda^{i} \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t}y^{'}_{t}|\Omega_{T}] \right)
\end{align*}
$$ 

#### Missing Values

In the presence of missing values, the loadings matrix $\Lambda^{(i)}$ and $R^{(i)}$  are 
calculated **for each variable** by using only the periods of time for which data is available. That means that if a variable does not exist for a given 
period $t$, **both** components of the formula for $\Lambda^{(i)}$  will not be used for that period. 
 
#### Restrictions in the parameters


- The loadings for quarterly variables, for example, load on a weighted average of the factors. For those variables, the formula is almost the same as above 
with only one difference: the above expectations containing montly factors are replaced by an equivalent expression where the factors are quarterly. That is:
$$ 
f^{Q}_{t}={\frac{1}{3} f_{t}} +\frac{2}{3}{f_{t-1}} + {f_{t-2}} +\frac{2}{3}{f_{t-3}} +\frac{1}{3}{f_{t-4}}
$$ 

- When a model has a lower triangular matrix for the transition matrix, equating to zero the derivative of expression (\ref{like}) with respect to the 
lower triangular part yields a similar outcome as expression (6):

$$ 
\begin{align*}
A^{(i)} = lowerTriang \left\{ \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t}\bar{f}^{'}_{t-1}|\Omega_{T}]\right)  \left(\sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[\bar{f}_{t-1}\bar{f}^{'}_{t-1} | \Omega_{T}]\right)^{-1}  \right\} 
\end{align*}
$$ 


#### Restrictions related to the use of variables that represent expectations (not implemented)

- When the model contains a block of variables $y^{e}_{t}$  that reflect expectations about the future, 
($ y^{e}_{t} =[y^{e}_{u,t}\: y^{e}_{\pi,t} ]^{'}$), where $y^{e}_{u,t}$ and $y^{e}_{\pi,t}$ represent  $h$ months ahead forecasts for unemployment ($u_{t+h|t}$) and inflation ($\pi_{t+h|t}$), respectively.  This means the likelihood formula (\ref{like}) is modified as follows
$$ 
\begin{align*}
log &\quad & \ell(f_{0}, f_{1}, \ldots,  f_{T}, y_{1},\ldots,  y_{T}|\theta)= \nonumber \\
&-& \frac{1}{2} log \left|Q_{0}\right| - \frac{1}{2} f^{'}_{0}Q^{-1}_{0} f_{0} -  \frac{T}{2} log \left|Q\right|  - \frac{1}{2}\mathrm{tr}\left[ Q^{-1}\sum^{T}_{t=1} (f_{t}-A \bar{f}_{t-1})(f_{t}-A \bar{f}_{t-1})^{'}\right]   \nonumber \\
&-& \frac{T}{2} log \left|R_{\psi}\right| - \frac{1}{2}\mathrm{tr}\left[ R_{\psi}^{-1}\sum^{T}_{t=1} (y_{t}-{\color{blue}\Lambda^{*}} f_{t})(y_{t}-{\color{blue} \Lambda^{*}} f_{t})^{'}\right]   
\label{like2}
\end{align*}
$where the factor loadings corresponding to 

$$ y_{t} =\left( 
\begin{array}{l}
y_{u,t}  \\
y_{\pi,t}  \\
y^{e}_{u,t}  \\
y^{e}_{\pi,t} 
\end{array}\right)
$$
are equal to
$$ {\color{blue} \Lambda^{*}}=\left[
\begin{array}{l}
\Lambda_{u} \\
\Lambda_{\pi} \\
\Lambda_{u}{\color{red} A^{h}} \\
\Lambda_{\pi}{\color{red} A^{h}} \\
\end{array}\right]
$$ 


- By noticing that  $\color{red} A^{h}$ enters the factor loadings for variables reflecting **expectations**, the derivative of the likelihood 
with respect to $A$ will be more complex. Note 
that 

$$
\frac{\partial \text{trace}(f_{t}A^{h}) }{\partial A} = \sum^{h-1}_{r=0}(A^{r}f_{t}A^{h-4-1})'
$$ 

, so we can obtain a new formula where solving the first order condition for $A$ would become
much more complex whenever $$h>2$$. Thus,  we propose to replace this step by a directly numerically maximizating the likelihood 
with respect to $$A$$, keeping the remaining
parameters fixed to the values resulting from the previous iteration. Although 
we do not compute this formula, the EM algorithm remains valid. As opposed to the standard case, 
this modification in the M-step, allows us to exploit extra information contained in the likelihood function to improve the estimation of $$A$$. This affects the persistence of the variables, which is key for understanding the dynamics of the variables. In the case of inflation
for example, the persistence is a key parameter that monetary policy makers look at. 

- But $$ A$$  also appears multiplying the loadings in the likelihood function, so the M-step for the loadings in the measurement equations needs to be modified. Consider for
example inflation. The loadings associated to a variable that we think it is related to inflation expectations could be defined as
follows: 
$$ 
\begin{eqnarray}
\text{case 1}: \Lambda^{(i)}_{\pi^{e}} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[y^{e}_{\pi,t}f^{'}_{t}A^{h'}|\Omega_{T}]\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[Af_{t}f^{'}_{t}A^{h}|\Omega_{T}]\right)^{-1}  
\end{eqnarray}
$$ 
Again, in the presence of missing values, the loadings matrix $$ \Lambda^{(i)} $$ at each iteration 
$$i$$ is  calculated **for each variable** by using only the periods of time for which data is available.

- However, the equation above does not take into account the restriction that the loadings corresponding to 
the inflation time series ($$\Lambda_{\pi}$$) are related to those of inflation 
expectations ($$\Lambda_{\pi}A^{h}$$). This restriction, which helps to achieve parsimony, determines
a small change in the M-step: 
$$ 
\begin{eqnarray}
\definecolor{energy}{RGB}{251,0,29}
\text{case 2}: \Lambda^{(i)}_{\pi} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[y_{\pi,t} f^{'}_{t}|\Omega_{T}]+ {\color{blue}\sum^{T}_{k=1} \mathbb{E}_{\theta_{(i-1)}}[y^{e}_{\pi,k} f^{'}_{k} A^{h'}|\Omega_{T}]}\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{(i-1)}}[f_{t}f^{'}_{t}|\Omega_{T}]+ {\color{blue} \sum^{T}_{k=1} \mathbb{E}_{\theta_{(i-1)}}[Af_{k}f^{'}_{k}A^{h}|\Omega_{T}]}\right)^{-1} 
\label{newM}
\end{eqnarray}
$$ 
where $y_{\pi,t}$ stands for inflation and $y^{e}_{\pi,k}$ represents inflation expectations $h$ periods ahead. We use 
different time indices $t$ and $k$ as a way to underline the possibility that $y_{\pi,t}$ and $y^{e}_{\pi,k}$ are not
necessarily observable for the same periods.  As one can observe by looking at the second element inside each parenthesis 
of equation  (\ref{newM}), having few observables for the expectations data does not prevent us from obtaining 
estimates of $\Lambda^{(i)}_{\pi}$. The reason is that the data points corresponding to the actual inflation data
are informative about the loadings. Interestingly, the larger the number of data points for the expectations data, 
the larger its weight in the estimation of $\Lambda^{(i)}_{\pi}$.

### Numerical optimization methods

