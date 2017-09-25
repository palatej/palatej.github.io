---
layout: left-menu
title: QR decomposition
tagline: technical documentation for JDemetra+ using GitHub Pages
description: QR decomposition
order: 1000
category: Decomposition
---
# {{page.description}}

#### Introduction

The QR factorization of a matrix $A$ consists in finding an orthogonal matrix $Q$ such that $QA$ is an upper triangular matrix $R$. As Q is orthogonal, we also have that $Q'R=A$.

This is usually achieved by means of Householder reflections.

The QR decomposition leads to a robust solution of the least squares problem.

#### Description of the algorithm

We consider that $A$ is an $n \times m$ matrix.

#### Bibliography

<hr>

#### Implementation

QR decompositions are implemented in the classes `demetra.math.matrices.internal.Householder`, `demetra.math.matrices.internal.RobustHouseholder` and `demetra.math.matrices.internal.HouseholderWithPivoting`

Householder is describe above.

Robust Householder uses the Neumaier's algorithm to diminish round-off errors in sums. 

Householder with pivoting follows the "LAPACK" implementation.