---
layout: left-menu
title: Linear filters
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Local polynomials
category: Filters
order: 40
---
# {{page.description}}

### Symmetric filters

We consider the kernel K


### Asymmetric filters


#### Description

At the end of the period, the series is modelled as follows:

$$ y = U \gamma + Z \delta + \epsilon, \: \epsilon \sim N\left(0, D\right) $$

Usually, $U$ and $Z$ are parts of the polynomial matrix $X$

Constraints on the asymmetric weights are imposed by the Matrix $U=\begin{pmatrix} U_p \\ U_f \end{pmatrix}$:

$$ U'_p v = U' w $$

The system should impose at least that the sum of the weights is equal to $1$ (which means that $U$ should contain the vector of ones).

The solution can be expressed as:

$$ v=w_p + Lw_f +M w_f$$

$$ Lw_f =D_p^{-1} U_p\left(U_p'D_p^{-1}U_p \right)^{-1} U_f'w_f$$


$$ M w_f = RZ_p \delta \delta' \left( I+ Z_p'  RZ_p \delta \delta'\right)^{-1} \left(Z_f'w_f-Z_p D_p^{-1}U_p\left( U_p'D_p^{-1}U_p\right)^{-1} U_f'w_f \right)$$

or 

$$ M w_f = RZ_p \delta \delta' \left( I+ Z_p'  RZ_p \delta \delta'\right)^{-1} \left(Z_f'w_f-Z_p L w_f \right)$$


$$ R = D_p^{-1} - D_p^{-1} U_p\left(U_p'D_p^{-1}U_p \right)^{-1} U_p'D_p^{-1}$$

$$  L, M \sim p \times f $$
$$  R \sim p \times p $$

#### Computation

- $t_1= D_p^{-1} U_p$  $\sim p \times u$
- $t_2=U_p't_1 = U_p' D_p^{-1} U_p$  $\sim u \times u$
- $t_3=U_f'w_f$   $\sim u \times 1$
- $t_4=t_2^{-1} t_3= \left(U_p'D_p^{-1}U_p \right)^{-1} U_f' w_f$   $\sim u \times 1$ 
- $t_5=t_1 t_4 =D_p^{-1} U_p \left(U_p'D_p^{-1}U_p \right)^{-1} U_f' w_f$   $\sim p \times 1$
- $t_6=t_1 t_2^{-1} t_1'=D_p^{-1} U_p\left(U_p'D_p^{-1}U_p \right)^{-1} U_p' D_p^{-1}$   $\sim p \times p$
- $R=D_p^{-1}-t_6$    $\sim p \times p$
- $d_2=\delta \delta'$    $\sim z \times z$
- $r_1=Z_p d_2=Z_p \delta \delta'$  $\sim p \times z$
- $r_2=R r_1$  $\sim p \times z$
- $r_3=Z_p' r_2 = Z_p'R Z_p \delta \delta'$  $\sim z \times z$


### Bibliography

