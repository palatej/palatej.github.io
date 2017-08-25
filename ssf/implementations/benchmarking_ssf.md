## Temporal disaggregation and benchmarking 


Temporal disaggregation and benchmarking are closely related. In both cases, we try to estimate an unobserved high-frequency series that respects some low-frequency constraints. In the case of temporal disaggregation, we will model the target by means of high-frequency information. We will prefer the term benchmarking when the problem consists in modifying an initial approximation of the target to fulfil the constraints. Temporal disaggregation will usually rest on statistical modelling techniques, while benchmarking will often be based on the minimization of some penalty functions. However, many benchmarking problems can also be put in a form that corresponds to some model-based problems, so that the last distinction is usually not relevant, from a technical point of view. Most of the solutions proposed in JD+ will use model-based (state-space forms) implementations.

We use below the following conventions / notations:
High-frequency series will be noted by means of lower case letters and low-frequency series will be noted by (corresponding) bold letters. 

We will consider below the case of aggregation by sum. Aggregations based on averages (prices) are similar. Aggregation based on the last observations (stock variables) corresponds to a simple problem of missing observations and are not treated here.

Each period of the aggregated time series contains $c$ periods of the high-frequency time series; the different time series start at the same date (which can be achieved by adding missing values, if need be). All indices start at 0.


### Generic state space form


We write

$$y_t^{\underline{C}}=\sum_{k=t-t\mod{c}}^{t-1}{y_k}$$

It represents the cumulator variable, from the beginning of each benchmarking period (included) to the current period (excluded).
and 

$$y_t^{C}=\sum_{k=t-t\mod{c}}^t{y_k} = y_t^{\underline{C}}+y_t $$

So that $y_t^C=\mathbf{y}_{t/c}$  when $t+1$ is a multiple of $c$ and is unobserved otherwise.


We consider that the unobserved disaggregated series has a state space form (SSF) identified by the state $\tilde\alpha_t$ and the system matrices $\left[{\tilde Z}_t,{\tilde H}_t,\tilde T_t,\tilde V_t, \tilde S_t, \tilde a_{-1}, \tilde P_*,\tilde B,\tilde P_\infty \right]$ (see [Ssf model](../model.md) ).

The benchmarking SSF is the original SSF extended by the cumulator variable


### State vector

The state is $\alpha_t=\begin{pmatrix}y_t^C & \tilde\alpha_t \end{pmatrix}$ 

### Initialization

$$ a_{-1} = \begin{pmatrix} 0 & \tilde a_{-1}\end{pmatrix}$$
<br>

$$ B = \begin{pmatrix} 0 \\ \tilde B\end{pmatrix}$$
<br>

$$ P_*= \begin{pmatrix} 0 & 0 \\ 0 &\tilde P_*\end{pmatrix} $$
<br>

$$ P_\infty= \begin{pmatrix} 0 & 0 \\ 0 &\tilde P_\infty\end{pmatrix} $$

### Dynamics

$$ T_t =\begin{cases}  \begin{pmatrix} 0 & 0 \\ 0 &\tilde T_t\end{pmatrix} if\; {t+1} \mod c = 0 \\\begin{pmatrix} 0 & \tilde Z_t \\ 0 &\tilde T_t\end{pmatrix} if\; t \mod c = 0 \\\begin{pmatrix} 1 & \tilde Z_t \\ 0 &\tilde T_t\end{pmatrix}  otherwise \end{cases} $$
<br>

$$ V_t= \begin{pmatrix} 0 & 0 \\ 0 &\tilde V_t\end{pmatrix} $$
<br>

$$ S_t = \begin{pmatrix} 0 \\ \tilde S_t\end{pmatrix}$$


### Measurement

$$ Z_t = \begin{cases} \begin{pmatrix} 0 & \tilde Z_t \end{pmatrix} if \; t \mod c = 0 \\ \begin{pmatrix} 1 & \tilde Z_t \end{pmatrix} if \; t \mod c \neq 0\end{cases}$$


### Regression model

The regression model is now built on the cumulated series $y_t^C = X_t^C \beta+\mu_t^C$.

The problem is then a simple problem of missing observations, which can be easily computed by means of the Kalman smoother. 
