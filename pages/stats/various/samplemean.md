#Sample mean in an AR(1) model

Suppose that $X_t=\rho X_{t-1}+\epsilon_t$ where $\epsilon_t \sim N(0, \sigma^2)$

We have that

$$ var(X)=\frac{\sigma^2}{1-\rho^2} $$

$$ var(\bar{X_n}) =var(\frac{1}{n}\sum_{t=1}^n X_t) $$

$$=\frac{1}{n} \frac{n-2\rho-n\rho^2+2\rho^{n+1}}{n(1-\rho)^2} \frac{\sigma^2}{1-\rho^2} $$

$$=\frac{1}{n_{\text{eff}}}  \frac{\sigma^2}{1-\rho^2}$$


If $\sigma^2$ is unknown (which is often the case), we will use the variance of the sample: 

$$\frac{\hat \sigma^2}{1-\hat \rho^2}=\frac{\sum_1^n (X_t-\bar{X_t})^2}{n(-1)}$$

When $n \rightarrow \infty$, it is easy to see that $n_{\text{eff}} \rightarrow n\frac{1-\rho}{1+\rho}$

We have then that

$$ \hat \sigma(\bar X_t) = \frac{\hat \sigma(X)}{\sqrt {{n_{\text{eff}}}} } $$

and the T-stat (df = $n_{\text{eff}}$) is applied on 

$$\frac{\bar X_n}{\hat \sigma / \sqrt{n_{\text{eff}(\rho)}} } $$