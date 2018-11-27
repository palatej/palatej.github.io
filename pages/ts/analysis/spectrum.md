---
layout: left-menu
title: Blackman-Tukey Spectrum
tagline: technical documentation for JDemetra+ using GitHub Pages
description:  Blackman-Tukey Spectrum
order: 20
category: analysis
---
# {{page.description}}

The Blackman-Tukey spectrum (or correlogram) is defined as follows

$$ S_{BT}(\omega)=\sum_{k=-M+1}^{M-1} w_k \hat r_k e^{-i \omega k}$$

where $w_k$  are window weights and $\hat r_k$ are standard sample covariance (or correlation) estimates

### Implementation

The Blackman-Tukey periodogram is implemented in the `demetra.data.SmoothedPeriodogram` class.

#### Details 

The estimation of the spectrum is defined as follows:

- The series is corrected for mean effect ($y_t^c=y_t-\overline y$)
- Optionally, tapering is applied on the series
- The $M-1$ first sample correlations are computed
- The spectrum is computed, using the provided smoothing window (Tukey window by default)
- it is evaluated at frequencies defined by $2 \pi k / \left(r\left(2M-1\right)\right)$, where $r$ is the relative (in $]0,1]$) resolution defined by the user (.5 by default)

#### Example

````Java
        SmoothedPeriodogram periodogram = SmoothedPeriodogram.builder()
                .data(DoubleSequence.of(data))
                .taper(new TukeyHanningTaper(.1))
                .windowLength(85)
                .relativeResolution(1)
                .windowFunction(DiscreteWindowFunction.Tukey)
                .build();

````