---
layout: left-menu
title: Outliers detection
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Outliers detection in X13
category: X13
order: 300
---
# {{page.description}}

### Detection of a single outlier

$$ \begin{pmatrix} \beta_X \\ \beta_o \end{pmatrix} = \begin{pmatrix} X_l' X_l && X_l' o_l\\ o_l' X_l && o_l' o_l \end{pmatrix}^{-1}\begin{pmatrix} X_l' y_l \\ o_l' y_l \end{pmatrix} = \Omega z $$

$$T_o = \beta_o / \left(\sigma_{r} \sqrt{\Omega_{o,o}}\right) $$

$$ \begin{pmatrix} X_l' X_l && X_l' o_l\\ o_l' X_l && o_l' o_l \end{pmatrix} = \begin{pmatrix} AA' && Aa'\\ aA' && b^2 \end{pmatrix}$$

Using inversion formulae of partitioned symmetric matrices, we get:

$$\Omega =  \begin{pmatrix} ... & ...\\- aA^{-1}\left(b^2 -aa'\right)^{-1} & \left(b^2 -aa'\right)^{-1} \end{pmatrix} $$

Using $w=X_l' o_l$, we also get:

$$\begin{cases} A = R'\\ a' = A^{-1}w\\ b = \sqrt{o_l' o_l}\end{cases}$$

The covariance of the coefficient corresponding to the new variable is given by $var_o=\Omega_{oo}  mad$ and the corresponding T-stat by $\beta_o / \sqrt{var_o}$

We have that

$$var_o= mad\left(b^2-aa'\right)^{-1}$$ 

$$\beta_o = \left(o_l' y_l - aA^{-1}X_l' y_l\right)/ \left(b^2-aa'\right)$$

so that

$$T_o = \frac{o_l' y_l - aA^{-1}X_l' y_l}{mad \sqrt{b^2-aa'}} $$

It should be noted that the expression $A^{-1}X_l' y_l$ doesn't depend on the new regression variable and must be computed only once