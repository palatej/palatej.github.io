---
layout: left-menu
title: Implementation
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Estimation of dynamic factor models in JDemetra+ 
category: Estimation
order: 45
---
# {{page.description}}

### Expectations-Maximization (EM) algorithm (`DfmEM2`)

Remember the modeling framework: 

$$ 
\begin{eqnarray}
y_{t}&=& \Lambda f_{t} + \psi_{t}, \text{with  }  \psi_{t}\sim N(0,R_{\psi}) \\
f_{t} &=& A_{1} f_{t-1}  + \ldots + A_{p} f_{t-p} +  u_{t},\text{with  } u_{t} \sim  N(0,Q)  
\end{eqnarray}
$$ 
where $$ \psi_{t} $$ represents the measurement error, which is assumed to be independent from the factor innovations $$ u_{t} $$. 

The EM algorithm can be used to obtain initial values that will be fed into the numerical optimization procedures described below.
The algorithm works by iterating two steps. The  `EStep()` (**expectation step**)  runs the Kalman filter recursions and compute the likelihood, while the `MStep()` (**maximization**
step), new parameter values are computed. The new parameter values obtained at each maximization step are calculated by solving the first order conditions for  $$ \Lambda $$, 
$$ R$$, $$ A$$ and $$ Q$$  with respect to the joint log likelihood of the data and the factors ([resource](https://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf
)). 

$$ 
\begin{eqnarray}
log &\quad & \ell(f_{0}, f_{1}, \ldots,  f_{T}, y_{1},\ldots,  y_{T}|\theta)= \nonumber \\
&-& \frac{1}{2} log \left|Q_{0}\right| - \frac{1}{2} f^{'}_{0}Q^{-1}_{0} f_{0} -  \frac{T}{2}log \left|Q\right|  
- \frac{1}{2}\mathrm{tr}\left[ Q^{-1}\sum^{T}_{t=1} (f_{t}-A \bar{f}_{t-1})(f_{t}-A \bar{f}_{t-1})^{-1}\right]   \nonumber \\
&-& \frac{T}{2} log \left|R_{\psi}\right| - \frac{1}{2}\mathrm{tr}\left[ R_{\psi}^{-1}\sum^{T}_{t=1} (y_{t}-\Lambda f_{t})(y_{t}-\Lambda f_{t})^{-1}\right]   
\label{like}
\end{eqnarray}
$$ 

where $$ \bar{f}_{t} $$  is a vector containing the first first $$ p $$ lags of $$f_{t} $$ with a parameters vector $$\theta=Q_{0},Q,A, R_{\psi},\Lambda$$. Note that
$$A=[A_{1}\ldots A_{p}]$$ and it is therefore different from the transition matrix of the state-space representation of the model.

The equations resulting from the M-step at each iteration $$i$$ follow. Note that they are calculated under 
the assumption that the initial conditions are given ( i.e.  $$ f_{0},Q_{0}$$  are fixed):


$$ 
\begin{eqnarray}
A^{i} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[f_{t}\bar{f}^{'}_{t-1}|\Omega_{T}]\right)  \left(\sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[\bar{f}_{t-1}\bar{f}^{'}_{t-1} | \Omega_{T}]\right)^{-1}  \\
\Lambda^{i} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[y_{t}f^{'}_{t}|\Omega_{T}]\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[f_{t}f^{'}_{t}|\Omega_{T}]\right)^{-1} \\
Q^{i} &=& \left( \frac{1}{T} \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[f_{t}f^{'}_{t}|\Omega_{T}]- A^{i} \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[f_{t-1}f^{'}_{t}|\Omega_{T}] \right)  \\
R^{i}_{\psi} &=& diag \left( \frac{1}{T} \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[y_{t}y^{'}_{t}|\Omega_{T}]- \Lambda^{i} \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[f_{t}y^{'}_{t}|\Omega_{T}] \right)
\end{eqnarray}
$$ 

#### Missing Values

In the presence of missing values, the loadings matrix $$ \Lambda^{i} $$ and $$ R^{i} $$  are 
calculated **for each variable** by using only the periods of time for which data is available. That means that if a variable does not exist for a given 
period $$t$$, **both** components of the formula for $$ \Lambda^{i}$$  will not be used for that period. 
 
#### Restrictions in the parameters


- The loadings for quarterly variables, for example, load on a weighted average of the factors. For those variables, the formula is almost the same as above 
with only one difference: we above expectations containing montly factors are replaced by an equivalent expression where the factors are quarterly. That is:
$$ 
f^{Q}_{t}={\frac{1}{3} f_{t}} +\frac{2}{3}{f_{t-1}} + {f_{t-2}} +\frac{2}{3}{f_{t-3}} +\frac{1}{3}{f_{t-4}}
$$ 

- When a model has a lower triangular matrix for the transition matrix, the derivative of expression (\ref{like}) with respect to the 
lower triangular part yields a similar outcome as expression (5)

$$ 
\begin{eqnarray}
A^{i} = lowerTriang \left( \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[f_{t}\bar{f}^{'}_{t-1}|\Omega_{T}]\right)  \left(\sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[\bar{f}_{t-1}\bar{f}^{'}_{t-1} | \Omega_{T}]\right)^{-1}  \right) 
\end{eqnarray}
$$ 

- When the model contains a variable $$ S_{t} $$  that reflects expectations regarding another variable that already exists in the 
model  e.g. $$ h $$  periods ahead, $$ y_{t+h}$$.  This means the likelihood formula (\ref{like}) is modified as follows

$$ 
{\begin{eqnarray}
log &\quad & \ell(f_{0}, f_{1}, \ldots,  f_{T}, y_{1},\ldots,  y_{T}|\theta)= \nonumber \\
&-& \frac{1}{2} log \left|Q_{0}\right| - \frac{1}{2} f^{'}_{0}Q^{-1}_{0} f_{0} -  \frac{T}{2}log \left|Q\right|  
- \frac{1}{2}\mathrm{tr}\left[ Q^{-1}\sum^{T}_{t=1} (f_{t}-A f_{t-1})(f_{t}-A f_{t-1})^{-1}\right]   \nonumber \\
&-& \frac{T}{2} log \left|R_{\psi}\right| - \frac{1}{2}\mathrm{tr}\left[ R_{\psi}^{-1}\sum^{T}_{t=1} (y_{t}-\Lambda A^{h} f_{t})(y_{t}-\Lambda A^{h} f_{t})^{-1}\right]   
\label{like2}
\end{eqnarray}}
$$ 
Of course, this likelihood function has been written as if all observables  $$y $$ would represent expectations $$h $$ periods ahead. However, each row of 
the observation vector may mix standard data with variables that represent all kinds of expectations, e.g. y_{t}=[y^{\pi}_{t}, [y^{\pi}_{t+h}].

- By noticing that  $$A^{h} $$ now **also** appears in the last part of equation , and 
that  $$ \frac{\partial \text{trace}(f_{t}A^{h}) }{\partial A} = \sum^{h-1}_{r=0}(A^{r}f_{t}A^{h-4-1})'$$, we obtain a new formula where solving the first order condition for $$A $$ would become
much more complex whenever $$h>2$$, so we propose to replace this step by a directly numerically maximizating the likelihood with respect to $$A$$, keeping the remaining
parameters fixed to the values resulting from the previous iteration. Although we do not compute this formula, the EM algorithm remains valid. As opposed to the standard case, 
this modification in the M-step, allows us to exploit extra information contained in the likelihood function to improve the estimation of $$A$$. This affects the persistence of the variables, which is key for understanding the dynamics of the variables. In the case of inflation
for example, the persistance is a key parameter that monetaricy policy makers look at. 

- But $$ A$$  also appers multiplying the loadings in the likelihood function, so it enters now the measurement equations as follows:

$$ 
\begin{eqnarray}
\text{case 1}: \Lambda^{i} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[y_{t}f^{'}_{t}A^{h'}|\Omega_{T}]\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[Af_{t}f^{'}_{t}A^{h}|\Omega_{T}]\right)^{-1} \\ 
\text{case 2}: \Lambda^{i} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[y^{\pi}_{t} f^{'}_{t}|\Omega_{T}]+\mathbb{E}_{\theta_{i-1}}[y^{e}_{t_{j}} f^{'}_{t_{j}} A^{h'}|\Omega_{T}]\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[Af_{t}f^{'}_{t}A^{h}|\Omega_{T}]+\mathbb{E}_{\theta(i-1)}[Af_{t_{j}}f^{'}_{t_{j}}A^{h}|\Omega_{T}]\right)^{-1} \\ 
\end{eqnarray}
$$ 
where $$y^{e}_{t_{j}} $$ represents an expectation $$h $$ periods ahead and the subindex $$ t_{j}$$  represents the periods of time where the surveys are available, which
may or may not coincide with the periods of where the actual variable they represent is observed.

Again, in the presence of missing values, the loadings matrix $$ \Lambda^{i} $$ at each iteration 
$$i$$ is  calculated **for each variable** by using only the periods of time for which data is available (case 1). However, notice that when we introduce a survey variable 
that represents the expected growth for, say inflation, you may want to assume that the loadings of both inflation and its expectation variable are identical (case 2). This brings further
parsimony to the model specication and has the advantage of improving the estimation for recent surveys that do not accumulate many years of history. However,
this implies that if a survey variable does not exist for many periods in the history of the series, this M-step cannot use **both** components of the formula for $$ \Lambda^{i}$$. Therefore,
our recommentation is to use few iterations of this M-step  and proceed immediately with the full numberical optimization procedure.


Try better display by using [colors](http://adereth.github.io/blog/2013/11/29/colorful-equations/) for $$A$$, I am not sure where I should include the config instruction:

` 
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ TeX: { extensions: ["color.js"] }});
</script>
`

### Numerical optimization methods

