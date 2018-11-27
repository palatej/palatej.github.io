---
layout: left-menu
title: Maximum likelihood
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Properties of the maximum likelihood of gaussian models
category: Likelihood
order: 1010
---

# {{page.description}}

$$ \sqrt{n}\left( \hat\theta_{mle}-\theta_0\right)\rightarrow N\left(0, I^{-1}\right) $$

where

$$I\left(\theta\right)=-E\left[\frac{\partial
^2}{\partial \theta^2}\log {l(\theta\mid y)} \mid \theta\right] $$

In the practice, we will use the observed information

$$J\left(\hat \theta\right)=-\frac{\partial
^2}{\partial \theta^2}\log {l(\hat\theta\mid y)}$$



The score vector is defined as

$$ \frac{\partial \log{l(\theta\mid y)} }{\partial \theta}$$

We should have that

$$ \frac{\partial \log{l(\theta\mid y)} }{\partial \theta}\biggr\rvert_{\hat\theta}=0$$
