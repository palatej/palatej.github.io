---
layout: left-menu
title: X13
tagline: technical documentation for JDemetra+ using GitHub Pages
description: X13
order: 300
---
# {{page.description}}

### 1. Log-level test

_pre-specified_ means _not to be tested_

#### Model for logs

- Transformations (to be applied in the given order)
  - Fixed regression effects
  - Interpolation of missing values
  - Log transformation 
  - Length of period adjustment: _pre-specified_ or _automatic_, if td included in the initial model (_pre-specified_ or _remove_ option)
- ARIMA
  - _Pre-specified_ or airline 
  - _Pre-specified mean correction_
- Regression
  - _Pre-specified variables_
  - Trading days (remove option)
  - Easter (remove option)
  - Leap year (remove option, no automatic pre-adjustment)

#### Model for levels

- Transformations 
  - Fixed regression effects
  - Interpolation of missing values
- ARIMA
  - _Pre-specified_ or airline 
  - _Pre-specified mean correction_
- Regression
  - _Pre-specified variables_
  - Trading days (remove option)
  - Easter (remove option)
  - Leap year (remove option)

Automatic pre-adjustment is not taken into account in the model in levels.
When logs are chosen and automatic pre-adjustment is enabled, the model after log/level test is adapted: the length of period variable is no longer considered in the regression and is replaced by a pre-adjustment (which corresponds, in the case of a leap year correction, to a fixed regression effect of $\pm 3 \%$). If automatic pre-adjustment is disabled, the length-of-period variable remains in the regression). 

### 2. Trading days test

The model chosen in (1) is compared with the same model with/without trading days effects.

In the case of a log transformation, a pre-adjustment or a length-of-period regression variable will be considered, following the pre-adjustment option, as discussed above.

The selection is based on an AIC test