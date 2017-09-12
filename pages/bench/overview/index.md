---
layout: left-menu
title: Introduction
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Temporal disaggregation and benchmarking. Introduction
order: 0
---
Temporal disaggregation and benchmarking are closely related. In both cases, we try to estimate an unobserved high-frequency series that respects some low-frequency constraints. In the case of temporal disaggregation, we will model the target by means of high-frequency information. We will prefer the term benchmarking when the problem consists in modifying an initial approximation of the target to fulfil the constraints. Temporal disaggregation will usually rest on statistical modelling techniques, while benchmarking will often be based on the minimization of some penalty functions. However, many benchmarking problems can also be put in a form that corresponds to some model-based problems, so that the last distinction is usually not relevant, from a technical point of view. Most of the solutions proposed in JD+ will use model-based (state-space forms) implementations.

We use below the following conventions / notations:
High-frequency series will be noted by means of lower case letters and low-frequency series will be noted by (corresponding) bold letters. 

We will consider below the case of aggregation by sum. Aggregations based on averages (prices) are similar. Aggregation based on the last observations (stock variables) corresponds to a simple problem of missing observations and are not treated here.

Each period of the aggregated time series contains $c$ periods of the high-frequency time series; the different time series start at the same date (which can be achieved by adding missing values, if need be). All indices start at 0.

