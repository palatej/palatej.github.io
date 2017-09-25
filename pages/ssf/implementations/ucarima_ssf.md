---
layout: left-menu
title: UCARIMA model
tagline: JD+. State space models
description: State space representation of UCARIMA model
category: "Arima"
order: 2100
---
{{page.description}}

#### Introduction

UCARIMA models are defined as [aggregates](./aggegate.md) of simple [ARIMA models]((./arima_ssf.md).

<br>

#### Implementation

The state space form of an UCARIMA model can be built by means of the class `demetra.ucarima.ssf.SsfUcarima` or
using directly `demetra.ssf.implementations.CompositeSsf` with instances of `demetra.arima.ssf.SsfArima`.