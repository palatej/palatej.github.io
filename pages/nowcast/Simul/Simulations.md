---
layout: left-menu
title: Real-Time Simulations
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Simulate out-of-sample forecasts compatible with the real-time dataflow 
category: Simulations
order: 60
---
# {{page.description}}

One of the biggest advantages of using this software is the possibility to simulate forecasts in a way that the calendar of data releases is taken into account. Forecasting simulations are important because they help to understand how accurate the model is before using it in practice. 

### Modeling the real-time dataflow
The illustrations of this page have been taken from the paper by [Basselier, De-Antonio-Liedo and Langenus (2016)](https://www.dropbox.com/s/bpzovfcuvf84ixn/EASurveys.pdf?dl=0), who use a dynamic factor model to construct a ranking of the most useful data releases. Such ranking depends not only on their quality but also on their timeliness.  In their context, there are more than 30 variables each one published at a different point in time, which can be represented in a very stylized way for the purposes of this Wiki. The y-axis represents either the point in time in which the indicators are released (red triangles) or the period of time to which the indicator refers (blue bars).  

![dataflow](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/RealtimeDataflow.gif)

It is common in the academic literature to define stylized representations of the data availability in order to avoid dealing with the complexity of real-time dataflow. However, the information coming from a detailed calendar may be essential to build **realistic forecasting simulations**. Fortunately, we show below that such information can be introduced in *J*Demetra+Nowcasting in a straightforward manner without the need to use simplifications: one just needs to specify in the  `MODEL` tab the publication lag for each indicator in terms of days. Surveys, which are often released before the month has ended, will require the specification of a negative publication lag. As it is clear from the picture below, the `MODEL` tab that we use to parameterize the factor model is also used here to model the real-time dataflow:

![setup](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/SimulationSetup.png)

In this case, the forecasts will be stored for all variables and they will be updated every time there is a new release.

### Real-time simulation set-up and results

[Simulation set-up](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulSetup)
 
[Visual Evaluation](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulVisual)
 
[Accuracy Tests](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulTests)
 
[Forecasting Uncertainty](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulRMSE)