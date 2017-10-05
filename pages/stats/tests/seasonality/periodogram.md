---
layout: left-menu
title: Periodogram test
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Seasonality test based on the periodogram
category: Seasonality tests
order: 2100
---
# {{page.description}}

####  Periodogram

The periodogram $$ I(\omega_j)$$  of $$ x \in \mathbb{C}^n $$ is defined as the squared of the Fourier transform

$$
I(\omega_{j})=a_{j}^{2}=n^{-1}\left| \sum_{t=1}^{n}x_t e^{-it\omega_j} \right|^{2},
$$

where the Fourier frequencies  $$ \omega_{j} $$  are given by multiples of the fundamental frequency $$ \frac{2\pi}{n} $$:

$$
\omega_{j}= \frac{2\pi j}{n}, -\pi < \omega_{j} \leq \pi 
$$

In JDemetra+, the periodogram of $$ x \in \mathbb{R}^n $$ is computed for the standardized time series. It represents the contribution of the jth 
harmonic to the total sum of squares, as illustrated by Brockwell and Davis (1991) using the table below:

| Source   | Degrees of freedom  |  $$~~~~$$ Sum of squares decomposition |
|---|:---:|---:|
| Frequency $$ \omega_{0} $$  | 1  | $$ a_{0}^{2}= n^{-1}(\sum_{t=1}^{n}x_t )^2 =I(0)$$ |
| Frequency $$ \omega_{1} $$    |  2 | $$ 2 r^{2}_{1} = 2 \left\| a_{1} \right\|^{2} = 2 I(\omega_{1}) $$  |
| $$ \vdots $$  |   $$ \vdots $$   |  $$ \vdots $$  |
| Frequency $$ \omega_{k} $$  | 2  | $$ 2 r^{2}_{k} = 2 \left\| a_{k} \right\|^{2} = 2 I(\omega_{k}) $$    |
| $$ \vdots $$  |  $$ \vdots $$    |   $$ \vdots $$  |
| Frequency $$ \omega_{n/2}=\pi $$    | 1  | $$ a_{n/2}^{2} = I(\pi) $$  |
| (excluded if $$ n $$ is odd)   |   |   |
|  $$ ========= $$ | $$ ====== $$ | $$ ============ $$   |
|  Total |  n |    $$ \sum_{t=1}^{n}x^2_t $$|


We use an orthonormal basis in  $$ \mathbb{R}^n $$ to project the data and obtain the decomposition above:

$$ 
\left\{ e_0, ~~~~~~c_1, s_1, ~~~~~\ldots~~~~~\ , ~~~~c_{[(n-1)/2]}, s_{[(n-1)/2]}~~~~,~~~~~~ e_{n/2}  \right\}
$$ 

where $$ e_{n/2} $$ is excluded if $$ n $$ is odd.  


####  F-test

The test

