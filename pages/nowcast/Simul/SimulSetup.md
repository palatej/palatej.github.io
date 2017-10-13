---
layout: left-menu
title: Simulations set-up
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Simulations set-up
category: Simulations
order: 65
---
# {{page.description}}

Once we have modeled the real-time dataflow, we need to decide for how many years we want to run the model. Also, as shown below, we will specify dates in which the dynamic factor model will be re-estimated. The estimation options are the same ones that have been used initially. In this example, the re-estimation takes place on the first day of each year, even if the forecasts are updated every time there is a new release:

![setup2](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/SimulationSpecify.gif)

**Remarks**:

- Running the simulation can take a long time if the estimation options require a very large number of iterations or the convergence criteria are very strict. 
- Before starting to run the forecasting simulations, the program will ask you to specify a folder where the forecasts will be stored. However, it is not necessary to look at it, since all results are also accessible through the `OUTPUT` tab.

	![](http://i.imgur.com/AmQkEXj.png)

