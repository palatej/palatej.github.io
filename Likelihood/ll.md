# Likelihood of gaussian models

The pdf of a multivariate normal distribution is:

$$p\left( y \right) = \left( 2 \pi \right)^{-\frac{n}{2}} \vert \Sigma \vert ^{-\frac{1}{2}}e^{ {-\frac{1}{2}y' \Sigma ^{-1} y} } $$

If we set
$$ y' \Sigma ^{-1} y=u'u \:\: or \:\:  L^{-1}y = u $$ 

the log-likelihood is:

$$ l \left( y | \theta \right) =- \frac{1}{2} \left(\log{2 \pi}+ \log{|\Sigma |} +u'u\right) $$

In most cases, we will use a covariance matrix with a (unknown) scaling factor:

$$ \Sigma = \sigma^2 \Omega $$

If we set

$$ L^{-1}y = e , \: LL' = \Omega$$ 

the log-likelihood can be written:

$$ l \left( y | \theta, \sigma\right ) = - \frac{1}{2} \left(n \log{2 \pi}+ n \log {\sigma^2} + \log{|\Omega |} + \frac{1}{\sigma ^2} e'e \right) $$

The scaling factor can be concentrated out of the likelihood. Its estimator is

$$ \widehat{\sigma ^2} = \frac{e' e}{n} $$

so that :

$$ l_c \left( y | \theta\right ) = - \frac{1}{2} \left(n \log{2 \pi}+ n + n\log{\frac{e'e}{n}} + \log{|\Omega |}\right) $$

or

$$ l_c \left( y | \theta\right ) = - \frac{n}{2} \left(\log{2 \pi}+ 1 - \log {n} + \log{e'e} + \log{|\Omega |^\frac{1}{n}}\right) $$

Maximizing
$$ l_c $$ 
is equivalent to minimizing the deviance 

$$ f \left( y | \theta\right ) = e'e |\Omega |^\frac{1}{n} = v'v, \: where v =e  |\Omega |^\frac{1}{2 n} $$ 

