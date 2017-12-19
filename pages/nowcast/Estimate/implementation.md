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
)):

$$ 
\begin{eqnarray}
log &\quad & \ell(f_{0}, f_{1}, \ldots,  f_{T}, y_{1},\ldots,  y_{T}|\theta)= \nonumber \\
&-& \frac{1}{2} log \left|Q_{0}\right| - \frac{1}{2} f^{'}_{0}Q^{-1}_{0} f_{0} -  \frac{T}{2}log \left|Q\right|  
- \frac{1}{2}\mathrm{tr}\left[ Q^{-1}\sum^{T}_{t=1} (f_{t}-A f_{t-1})(f_{t}-A f_{t-1})^{-1}\right]   \nonumber \\
&-& \frac{T}{2} log \left|R_{\psi}\right| - \frac{1}{2}\mathrm{tr}\left[ R_{\psi}^{-1}\sum^{T}_{t=1} (y_{t}-\Lambda f_{t})(y_{t}-\Lambda f_{t})^{-1}\right]   
\label{like}
\end{eqnarray}
$$ 

with a parameters vector $$\theta=Q_{0},Q,A, R_{\psi},\Lambda$$.

The equations resulting from the M-step at each iteration $$i$$ follow. Note that they are calculated under 
the assumption that the initial conditions are given ( i.e.  $$ f_{0},Q_{0}$$  are fixed):


$$ 
\begin{eqnarray}
A^{i} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[f_{t}f^{'}_{t-1}|\Omega_{T}]\right)  \left(\sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[f_{t-1}f^{'}_{t-1} | \Omega_{T}]\right)^{-1}  \\
\Lambda^{i} &=& \left( \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[y_{t}f^{'}_{t}|\Omega_{T}]\right) \left( \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[f_{t}f^{'}_{t}|\Omega_{T}]\right)^{-1} \\
Q^{i} &=& diag \left( \frac{1}{T} \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[f_{t}f^{'}_{t}|\Omega_{T}]- A^{i} \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[f_{t-1}f^{'}_{t}|\Omega_{T}] \right)  \\
R^{i}_{\psi} &=& diag \left( \frac{1}{T} \sum^{T}_{t=1} \mathbb{E}_{\theta_{i-1}}[y_{t}y^{'}_{t}|\Omega_{T}]- \Lambda^{i} \sum^{T}_{t=1} \mathbb{E}_{\theta(i-1)}[f_{t}y^{'}_{t}|\Omega_{T}] \right)
\end{eqnarray}
$$ 

#### Missing Values

In the presence of missing values, the loadings matrix $$ \Lambda^{i} $$ and $$ R^{i} $$  are 
calculated **for each variable** by using only the periods of time for which data is available. That means that if a variable does not exist for a given 
period $$t$$, **both** components of the formula for $$ A^{i}$$  will not be used for that period.
 
#### Restrictions in the parameters


- The loadings for quarterly variables, for example, load on a weighted average of the factors. For those variables, the formula is exactly the same as above 
with only one difference: we above expectations containing montly factors are replaced by an equivalent expression where the factors are quarterly. That is:
$$ 
f^{Q}_{t}={\frac{1}{3} f_{t}} +\frac{2}{3}{f_{t-1}} + {f_{t-2}} +\frac{2}{3}{f_{t-3}} +\frac{1}{3}{f_{t-4}}
$$ 

- When a model has a lower triangular matrix for the transition matrix, the derivative of expression (\ref{like}) with respect to the lower triangular part, does it 
yield the same outcome as expression (5)?
[develope it] 

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

By noticing that  $$A^{h} $$ now **also** appears in the last part of equation , and 
that  $$ \frac{d}{dA}\text{trace}(f_{t}A^{h})  = \sum^{h-1}_{r=0}(A^{r}f_{t}A^{h-4-1})'$$, we obtain a new formula where solvig for $$A $$ becomes
more complex:

[develop it, perhaps we could deal with this step numerically]

The new formula uses more information to improve the estimation of $$A$$. This affects the persistence of the variables, which is key for understanding the dynamics of the variables. In the case of inflation
for example, the persistance is a key parameter that monetaricy policy makers look at. 
But $$ A$$  also enters now the measurement equations as follows:

[develop it, easy]


Try better display by using [colors](http://adereth.github.io/blog/2013/11/29/colorful-equations/) for $$A$$, I am not sure where I should include the config instruction:

` 
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ TeX: { extensions: ["color.js"] }});
</script>
`

### Numerical optimization methods

