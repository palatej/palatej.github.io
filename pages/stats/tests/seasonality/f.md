---
layout: left-menu
title: F test
tagline: technical documentation for JDemetra+ using GitHub Pages
description: F Test on seasonal dummies
category: Seasonality tests
order: 2030
---
# {{page.description}}

We use the GLS $$ F^{M} $$ -statistic of Lytras, Feldpausch and Bell (2007). It requires defining stable or fixed seasonal regressors, $$ M_{j,t} $$. 
For monthy data each one of the 11 regressors required is defined as follows: 

$$
M_{j,t}=\left\{ \begin{matrix}
   1 &\;& in \; month \; j=1,...,11 \\
   -1 &\;& in \; December \\
   0  &\;& otherwise\\
\end{matrix}  \right\} 
$$

Those regressors would enter in a regARIMA model, resulting on the following general expression:

$$
\left( 1 - B \right)^{d}(Y_{t} - \beta_1 M_{1,t} -  \ldots  - \beta_{11} M_{11,t} - \gamma X_{t}) = \left( 1 + L \right)\alpha_t
$$

One can use the individual t-statistics to assess whether seasonality for a given month is significant, or a chi-squared test statistic if the null hypothesis is 
that the parameters are collectively all zero. The chi-squared test statistic   
$$
\hat{\chi}^2 = \hat{\beta}^{'}[Var(\hat{\beta})]^{-1}\hat{\beta} 
$$ 

is in this case compared to critical values from chi-squared distribution with 11 degrees of freedom. 

Since $$ Var(\hat{\beta}) $$ is computed using the estimated variance of $$ \alpha_t $$ may be actual variance in small samples, this test is 
corrected using the proposed $$ F^{M} $$ -statistic:

$$
F^{M}= \frac{\hat{\chi}^2}{11} \times \frac{n-d-k}{n-d}
$$ 

where $$ n $$ is the sample size, $$ d $$ is the degree of differencing and $$ k $$ is the total number of regressors in the regARIMA model (including 11 seasonal
dummies $$ M_{j,t} $$ and the intercept). This statistic follows a $$ F_{11,n-d-k} $$ distribution under the null.

####  References

Lytras, D. P., Feldpausch, R. M., and Bell, W. R. (2007), “Determining Seasonality: A Comparison of Diagnostics from X-12-ARIMA,” Proceedings of the Third International Conference on Establishment Surveys, Montreal, Canada

