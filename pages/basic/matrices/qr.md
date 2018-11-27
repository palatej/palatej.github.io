---
layout: left-menu
title: QR decomposition
tagline: technical documentation for JDemetra+ using GitHub Pages
description: QR decomposition
order: 1060
category: Decomposition
---
# {{page.description}}

#### Introduction

The QR factorization of a matrix $X$ consists in finding an orthogonal matrix $Q$ and an upper triangular matrix $R$ such that $X=QR$. As Q is orthogonal, we also have that $Q'X=R$.

This is usually achieved by means of Householder reflections.

The QR decomposition leads to a robust solution of the least squares problem.

#### Description of the algorithm

We consider that $X$ is an $n \times k$ matrix.

#### Least squares by QR decomposition

We want to solve the least squares problem

$$\min_a \mid\mid y - X a \mid\mid $$

Suppose that $X=QR$. We can write that

$$\mid\mid y - X a \mid\mid^2 = \mid\mid Q'y - R a \mid\mid^2 = \mid\mid (Q'y)_I - (R a)_I \mid\mid^2 + \mid\mid (Q'y)_{II} \mid\mid^2 $$ 

wherer $Z_I$ corresponds to the first $k$ rows and  $Z_{II}$ to the last $n-k$ rows.  

The norm is minimum for $a=R^{-1}(Q'y)_I$

In that case, it is equal to $\mid\mid (Q'y)_{II} \mid\mid^2$ and we call $(Q'y)_{II}$ the QR-residuals ($e_{qr}$).

We also have the following useful results:

$$(X'X)^{-1}= (R'Q'QR)^{-1}=(R'R)^{-1}$$

$$|(X'X)^{-1}|=(\sum_i{r_{ii}})^{-2}$$


#### Bibliography

<hr>

#### Implementation

QR decompositions are implemented in the classes `demetra.math.matrices.internal.Householder`, `demetra.math.matrices.internal.RobustHouseholder` and `demetra.math.matrices.internal.HouseholderWithPivoting`

Householder is describe above.

Robust Householder uses the Neumaier's algorithm to diminish round-off errors in sums. 

Householder with pivoting follows the "LAPACK" implementation.