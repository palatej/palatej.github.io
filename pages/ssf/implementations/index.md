---
layout: left-menu
title: Introduction
tagline: JD+. State space models
description: Implementation of states space models
order: 0
---
# {{page.description}}

The state vector can often be split in independent blocks; each block has its own initialization and dynamics. The transition matrices $T_t$, the covariances of the transition innovations $V_t$ and the initialization matrices are then block diagonal. 

 Univariate models are defined by a single equation, which reassemble the various block by means of different loading factors. Multi-variate models are straightforward extensions; they only differ by the number of equations.

The framework provides numerous building blocks – elements of the state vector or loading factors – that can be combined to create the actual state space model. Some blocks are self-sufficient - they represent an actual model - but in most cases, the user will need to glue several of them.

We present in this documentation the different matrices of each block. See [the general model](../overview/index.md) for the meaning of each matrix

