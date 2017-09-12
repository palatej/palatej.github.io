## State space representation of a cubic spline function

### Introduction

We try to approximate a time series $y_t$ by a smooth function $\mu_t$, chosen by minimizing the criterion:

$$ \sum_{t=0}^{t<n}\left[y_t-\mu_t\right]^2 + \lambda \sum_{t=0}^{t<n}\left[\Delta^2 \mu_t\right]^2$$

We consider the following model:

$$ y_t = \mu_t + \epsilon_t $$

$$ \Delta^2 \mu_t = \eta_t $$

$$ var(\epsilon_t)= \sigma^2, \quad var(\eta_t)= \sigma^2/\lambda $$


### Initialization


### Dynamics

$$ T_t = \begin{pmatrix}1 & 1 \\ 0 & 1 \end{pmatrix} $$
<br>

$$ V_t = \begin{pmatrix} 1/3 & 1/2 \\ 1/2 & 1 \end{pmatrix} $$
<br>

$$ T_t = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} $$

### Measurement


### Implementation