## General form

The general linear gaussian state-space model can be written in many different ways. The measurement equation and the state equation considered in JD+ 3.0 are presented below.

$$ y_t = Z_t \alpha_t + \epsilon_t,\quad \epsilon_t \sim N\left(0, \sigma^2 H_t\right) $$
$$ \alpha_{t+1} = T_t \alpha_t + \mu_t, \quad \mu_t \sim N \left(0, \sigma^2 V_t \right)$$
<br>
$$ y_t $$  is the observation at period t, 
$$ \alpha_t $$  is the state vector.
$$ \epsilon_t, \mu_t $$ 
are assumed to be serially independent at all time points and independent between them at all time points.  

The residuals of the state equation will be modelled as
$$ \mu_t = S_t \xi_t, \quad \xi_t \sim N\left( 0, \sigma^2 I\right) $$
In other words, 
$$ V_t=S_t S_t' $$

The initial conditions of the filter are defined as follows:
$$ \alpha_{-1} = a_{-1} + A_{-1}\delta + \mu_{-1}, \quad \delta \sim N\left(0, \kappa I \right),\: \mu_{-1} \sim N\left(0, P_*\right)$$

where 
$$ \kappa $$
is arbitrary large.
$$ P_* $$
is the variance of the stationary part of the initial state vector and
$$ A_{-1}A_{-1}'=P_\infty $$
models the diffuse part.   
The model used in JD+ is quasi-identical to the model discussed in [1].

#### Bibliography

[1] _DURBIN J. AND KOOPMAN S.J._ (2012): "Time Series Analysis by State Space Methods", second edition. Oxford University Press.
