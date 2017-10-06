---
layout: left-menu
title: Friedman test
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Friedman Test (non-parametric)
category: Seasonality tests
order: 2040
---
# {{page.description}}

The Friedman test is a non-parametric method for testing that samples are drawn from the same population or from populations with equal medians. 
The significance of the month (or quarter) effect is tested. The Friedman test requires no distributional assumptions. It uses the rankings of the observations. 
If the null hypothesis of no stable seasonality is rejected at the 0.10% significance level then the series is considered to be seasonal 
and the test’s outcome is displayed in green.

The test statistic is constructed as follows. Consider first the matrix of data $$ \left\{x_{ij}\right\}_{n \times k} $$ with $$ n $$ rows (the blocks, 
i.e. number of years in the sample), $$ k $$ columns (the treatments, i.e. either 12 months or 4 quarters, depending on the frequency of the data).  
The data matrix needs to be replaced by a new matrix $$ \left\{r_{ij}\right\}_{n \times k} $$, where the entry $$ r_{ij} $$ is the rank of  $$ x_{ij} $$ 
within block $$ i $$ .

The test statistic is given by

$$
Q=\frac{SS_t}{SS_e}
$$

where $$ SS_t=n \sum_{j=1}^{k}(\bar{r}_{.j}-\bar{r})^2 $$ and $$ SS_e=\frac{1}{n(k-1)} \sum_{i=1}^{n}\sum_{j=1}^{k}(r_{ij}-\bar{r})^2 $$ 
It represents the variance of the average ranking across treatments j  relative to the total.  

Under the hypothesis of no seasonality, all months can be equally treated. For the sake of completeness:
- $$ \bar{r}_{.j} $$ is the average ranks of each treatment (month) j within each block (year)
- The average rank is given by $$ \bar{r}= \frac{1}{nk}\sum_{i=1}^{n}\sum_{j=1}^{k}(r_{ij})$$

For large $$ n $$ or $$ k $$ , i.e. n > 15 or k > 4, the probability distribution of $$ Q $$ can be approximated by that of 
a chi-squared distribution. Thus, the p-value is given by $$ P( \chi^2_{k-1}>Q) $$ . 


####  Related tests

- 	When using this kind of design for a binary response, one instead uses the Cochran's Q test.
- 	Kendall's W is a normalization of the Friedman statistic between 0 and 1.
- 	The Wilcoxon signed-rank test is a nonparametric test of non-independent data from only two groups.


####  References

- Friedman, Milton (December 1937). "The use of ranks to avoid the assumption of normality implicit in the analysis of variance". Journal of the American Statistical Association (American Statistical Association) 32 (200): 675–701. doi:10.2307/2279372. JSTOR 2279372. 

- Friedman, Milton (March 1939). "A correction: The use of ranks to avoid the assumption of normality implicit in the analysis of variance". Journal of the American Statistical Association (American Statistical Association) 34 (205): 109. doi:10.2307/2279169. JSTOR 2279169. 

- Friedman, Milton (March 1940). "A comparison of alternative tests of significance for the problem of m rankings". The Annals of Mathematical Statistics 11 (1): 86–92. doi:10.1214/aoms/1177731944. JSTOR 2235971.

