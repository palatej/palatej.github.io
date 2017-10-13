---
layout: left-menu
title: Existing Models
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Opening an _existing workspace_
order: 20
---
# {{page.description}}
 
A workspace can contain a large number of models. Let's consider a dynamic factor model for the euro area proposed in the empirical 
application of one of the reference papers in the field of nowcasting. The largest model proposed 
by [Banbura and Modugno (2010)](https://www.ecb.europa.eu/pub/pdf/scpwps/ecbwp1189.pdf) accounts for the comovements of 101 indicators in 
terms of only five factors, r=5, following a VAR(p) with p=2. 

Open the workspace [**BM2014_JAE**](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/Banbura_Modugno_2014_Example/Banbura_Modugno_2014_Example.rar), which contains three different versions of the same model. They only differ because of the sample used for the estimation of its parameters and the optimization method used to maximize the likelihood: 

### 1. Open a Model 

- The first one has been estimated with the first vintage of data used in the forecasting exercise proposed by the authors, which corresponds to October 1999. The estimation method is mainly based on a numerical optimization algorithm.
- The second model is exactly the same. The only difference is that it was  estimated using the Expectation-Maximization (EM) algorithm.
- The last model is again identical, but it is estimated using the whole sample. 

This figure shows how to open the worskpace containing the three models and subsequently activate one of them by double clicking on it. Notice that 
the model with the very long name

`Large DFM (r=5, p=2) Data=first vintage, Est=NumOptim`  

is active and is displayed on the right-hand side window.  It includes four different tabs: `MODEL`  , `PROCESSING`  , `OUTPUT`  , `NEWS`   and `SIMULATION`  

 ![OpeningModel](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/OpenModel.gif) 
 
Right clicking on any of the models included in the Worspace tab (left-hand side of the screen), you will have the following options:

- `Delete`
- `Rename`
- `Clone`: a new copy of the model is created and it has its own life independent of the one used as a model. The references to the data sources 
remain unchanged too, but refreshing the data in the clone model does not automatically refresh the data in the original model (and also not the other way round)


### 2. Refreshing the data to be read by the model 

You can see the name of the active model in the general menu bar. Only one model can be activated at a time. By clicking on its name, which appears in the bar, as shown below, you will have the following options:

- `Refresh`
- `Archive`
- `Remove last archieve`
- `Unlock`

Here, we assume that the input data has already been updated in you Excel file. Now, such data has to be read by the model in order to update the forecasts. In this 
video, you can see that the data appears with the label "frozen", which disappears after the "refresh" action has been executed.  

 ![RefreshData](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/RefreshData.gif) 
 

The option, `archive`   can be used to freeze the data, but it locks the model at the same time. A model that is locked cannot be re-estimated 
and its specification cannot change. This is a way to make sure that someone borrowing the model does not change its properties accidentally. As 
it will be explained later on, re-estimating the model parameters is not necessary before updating the forecasts. 

{: .alert .alert-info}
_Archived models can be `unlocked` in order to re-estimate their parameters, but also to change their specification (N, r, and p). The `remove last archive` option 
redefines the model specification and data that had been saved before the last archive action, but it does not unlock the model._



