---
layout: left-menu
title: Descriptive statistics
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Descriptive statistics
category: Descriptive statistics
order: 10
---
# {{page.description}}

### Auto-covariances and auto-correlations

We consider the sample $\lbrace y_t \rbrace_{t \in [0, n]}$ from a population $P$

When the mean of the population is known ($=\mu$), we compute the sample auto-covariance of rank k by 

$$cov_k(y_t)=1/n \sum_{j=k}^{j \lt n} (y_j -\mu) (y_{j-k}-\mu)$$

So, when $\mu = 0$, we simply have that

$$cov_k(y_t)=1/n \sum_{j=k}^{j \lt n} y_j y_{j-k}$$

When the mean of the population is unknown, we define  

$$cov_k(y_t)=1/(n-k) \sum_{j=k}^{j \lt n} (y_j-\overline y)( y_{j-k}-\overline y)$$

where $\overline y$ is the sample mean:

$$\overline y=1/n \sum_{j=0}^{j \lt n} y_j$$

The sample auto-correlations are defined by $\gamma_k(y_t)=cov_k(y_t)/cov_0(y_t)$

### Implementations in JD+



The properties of samples with unkonwn mean and with 0 mean are provided respectively by the classes `demetra.stats.samples.DefaultOrderedSample` and `demetra.stats.samples.OrderedSampleWithZeroMean`.