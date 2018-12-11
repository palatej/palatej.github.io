---
layout: left-menu
title: Overview
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Nowcasting
order: 0
---
# {{page.description}}

 
**Nowcasting** is often defined as the prediction of the present, the very near future and the very recent past. The plug-in 
developed at the National Bank of Belgium helps to operationalize the process of nowcasting. It 
can be used to specify and estimate dynamic factor models and visualize how the real-time dataflow updates expectations, as 
for instance in [Banbura and Modugno (2010)](https://www.ecb.europa.eu/pub/pdf/scpwps/ecbwp1189.pdf). The software can also be 
used to perform pseudo out-of-sample forecasting evaluations that consider the calendar of data releases, contributing to the formalization 
of the nowcasting problem originally proposed by  [Giannone, _et al_. (2008)](https://ideas.repec.org/a/eee/moneco/v55y2008i4p665-676.html) or 
[Evans (2005)](http://www.nber.org/papers/w11064.pdf). 
 
Examples built with JDemetra+_Nowcasting_ :

- [Nowcasting Belgium](http://ec.europa.eu/eurostat/documents/3217494/7114363/KS-GP-15-002-EN-N.pdf/d9058a50-353c-436a-91f0-d606e1e7d988), by De-Antonio-Liedo D. (2015) _Eurostat Review of National Accounts and Macroeconomic Indicators_, Special Issue on New Techniques and Technologies for Statistics   **2**, 7-41.
- [Nowcasting euro area GDP: Understanding the role of qualitative surveys](https://link.springer.com/article/10.1007%2Fs41549-017-0022-9), by R. Basselier, D. De-Antonio-Liedo and G. Langenus  (2016) _Journal of Business Cycle Research_  **14**, 1-46.([working paper](https://www.nbb.be/en/articles/nowcasting-real-economic-activity-euro-area-assessing-impact-qualitative-surveys)[|model](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/Basselier_DeAntonio_Langenus_2016/January2017.zip))
- [Nowcasting Spanish GDP](https://www.inderscience.com/info/inarticle.php?artid=80667), by De-Antonio-Liedo D. and E. Fernandez (2016) _International Journal of Computational Economics and Econometrics_,  **7**,5-42 ([pre-print](https://github.com/nbbrd/jdemetra-nowcasting/wiki/papers/Hyper.pdf) / [download  data and model workspace](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/ES/ES.rar))
- [US output-inflation interactions](http://fr.slideshare.net/DaviddeAntonioLiedo/a-realtime-forecasting-evaluation-library-for-jdemetra-45630748), by Charles P., M. Maggi, J.Palate and D. de-Antonio-Liedo,  (2015)
- Nowcasting Euro Area GDP ([download examples based on Banbura and Modugno, 2014](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/Banbura_Modugno_2014_Example/Banbura_Modugno_2014_Example.rar))
- Nowcasting German GDP ([download  data and model workspace](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/DE/DE.rar) or download [presentation](http://www.slideshare.net/DaviddeAntonioLiedo/kiel-fe-public))
- Forecasting models for business cycle indicators in all the European Union countries: [download data](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/BDCOMP/BDCOMP.rar) and  feel free to add more data to **build your own** models.
 
### Overview

![MainTabs](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/MainTabs.png) 


1. [Open an Existing Model (`MODEL tab`)](https://palatej.github.io/pages/nowcast/OpenExistingModel.html) 	
	* [Open a model](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Open-Existing-Model#1-open-a-model) 
	* [Refresh the data](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Open-Existing-Model#2-refreshing-the-data-to-be-read-by-the-model) 
2. Create a New Model or Improve an Existing one (`MODEL tab`)	
	* [Load the data first](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Load-Data) 
	* [Build a model for your data](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Build-Model) 
3. [Estimation (`PROCESSING tab`)](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Estimation)	
	* [Options: EM, Levenberg-Marquardt](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Estimation#1-options) 
	* [Example: Estimating a large model](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Estimation#2-example) 
4. [Results from the estimation (`OUTPUT tab`)](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Estimation-Results)	
	* [Estimation: fit, residuals, etc](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Estimation-Results#the-estimation-branch) 
	* [Forecasts](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Estimation-Results#the-forecasts-branch) 
5. [News Analysis (`NEWS tab`)](https://github.com/nbbrd/jdemetra-nowcasting/wiki/News)
6. [Real-Time Simulation (`SIMULATION tab`)](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Simul)	
	* [Simulation set-up](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulSetup)
	* [Visual Evaluation](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulVisual)
	* [Accuracy Tests](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulTests)
	* [Forecasting Uncertainty](https://github.com/nbbrd/jdemetra-nowcasting/wiki/SimulRMSE)
 
