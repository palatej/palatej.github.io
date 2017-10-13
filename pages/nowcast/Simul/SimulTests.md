---
layout: left-menu
title: Accuracy 
tagline: technical documentation for JDemetra+ using GitHub Pages
description:  Quantifying and Testing Accuracy
category: Simulations
order: 75
---
# {{page.description}}


The various results are organized in the form of tables and can be copied and pasted externally. As shown in the video, one can focus the evaluation on a particular subsample by simply clicking on the  `Filter sample` button in the upper-right corner of the table:

![](http://i.imgur.com/2IqQ4KC.gif)

### A. Quantifying 

The forecasts errors resulting for a given subsample are averaged in different ways, as shown in the following table:

<table class="tg">
  <tr>
    <th class="tg-baqh"></th>
    <th class="tg-amwm">Root Mean Squared</th>
    <th class="tg-amwm">Mean Absolute</th>
    <th class="tg-amwm">Median Absolute</th>
  </tr>
  <tr>
    <td class="tg-9hbo">Scale Dependent</td>
    <td class="tg-baqh">RMSE</td>
    <td class="tg-baqh">MAE</td>
    <td class="tg-baqh">MdAE</td>
  </tr>
  <tr>
    <td class="tg-9hbo">(Percentage) Errors</td>
    <td class="tg-baqh">RMS(P)E</td>
    <td class="tg-baqh">symmetric MA(P)E</td>
    <td class="tg-baqh">symmetric MdA(P)E</td>
  </tr>
  <tr>
    <td class="tg-9hbo">(Scaled) Errors</td>
    <td class="tg-baqh">RMS(S)E</td>
    <td class="tg-baqh">MA(S)E</td>
    <td class="tg-baqh">MdA(S)E</td>
  </tr>
</table>

- The first row represents the widely used Root Mean Squared Error (RMSE), Mean Absolute Error (MAE) and Mediean Absolute Error (MdAE). For a precise definition, check for example [Hyndmnn and Koehler (2006)](http://dx.doi.org/10.1016/j.ijforecast.2006.03.001). Given that those measures depend on the scale of the
data, they are useful only when comparing different methods at forecasting the same set of variables. 
- In order to be able to compare different methods across data sets that have different scales, one can look at percentage errors (second row). The percentage error is undefined it the variable happens to hits close enough to the value zero. Moreover, it has been argued that the MA(P)E and MdA(P)E put a hevier penalty on positive errors than on negative errors. This problem is solved as in [Makridakis (1993)](http://www.sciencedirect.com/science/article/pii/016920709390044N?via%3Dihub) by slightly modifying the definition of percentage error (the "symmetric" absolute percentage error is defined by dividing the absolute error by the sum of the actual value and forecast). 
- The third row contains scaled errors, which is the solution proposed by [Hyndmnn and Koehler (2006)](http://dx.doi.org/10.1016/j.ijforecast.2006.03.001) to quantify forecasting accuracy independently of scale. In practice, the scaled errors are obtained by dividing the errors by the mean absolute error of the random walk over the evaluation sample. Therefore, the three measures will be smaller than one if the forecasts are more precise than those of a random walk.

Our proposed way to eliminate the scale dependency is to simply use an ARIMA model as a naïve benchmark against which our forecasts can be compared. Thus, the three blocks of measures obtained for a given nowcasting model are divided by those resulting from a univariate benchmark (ARIMA) recursively specified and estimated for each time series by the most recent implementation of the TRAMO algorithm:

![](http://i.imgur.com/LCfjQOh.png) 

### B. Testing

The algorithms used in the current version of *J*Demetra*+* represent the first attempt to let users decide whether the nowcasts produced at a given point in time are *significantly* different from those coming from a univariate benchmark. For detailed information, click on the technical note ["A forecasting evaluation library for *J*Demetra*+*"](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/ForecastingEvaluationLibrary.pdf).

#### Overview of all tests

Summing up, we follow the original formulation of the **Diebold-Mariano** (henceforth **DM**) test, which looks at the forecast errors differentials to test the null hypothesis that the difference between our (e.g. squared) errors and those of a benchmark (i.e. loss differential) are equal to zero. The test statistic is defined as the sample average of the loss differential, which should be close to zero under the null, divided the the [Newey-West HAC](http://www.ssc.wisc.edu/~kwest/publications/1980/A%20Simple%20PSD%20HAC%20Covariance%20Matrix.pdf) estimator of the variance, and converges asympotically to a standard normal disbribution.  

The **DM** test has been used since 1995 in spite of its well known size distorsion (i.e. the hypothesis that our forecasts are significantly different from those of the benchmark will be rejected by mistake more often than expected from the test design). The oversize problem, which can be more visible in small samples, is fixed by deviating from the standard asymptotic theory: we follow the proposal by **Coroneo and Iacone (2016)**, which is referred to as Fixed Smoothing Asymptotics (henceforth, **FSA**) . Based on this idea, our evaluation of point forecasts is reported as follows:

<table class="tg">
  <tr>
    <th class="tg-9hbo">Test</th>
    <th class="tg-amwm">Null hypothesis</th>
    <th class="tg-amwm">Report</th>
    <th class="tg-amwm">Colour code for rejection</th>
  </tr>
  <tr>
    <td class="tg-9hbo">Diebold-Mariano (Standard vs FSA)</td>
    <td class="tg-baqh">equality in forecasting accuracy</td>
    <td class="tg-baqh">pvalue</td>
    <td class="tg-14nr">blue</td>
  </tr>
  <tr>
    <td class="tg-9hbo">Forecast encompasses Benchmark (FSA)</td>
    <td class="tg-baqh">our model predictions encompass the benchmark forecasts</td>
    <td class="tg-baqh">weight of the benchmark</td>
    <td class="tg-cmwg">red (weight significantly different from zero)</td>
  </tr>
  <tr>
    <td class="tg-9hbo">Forecast is encompased by Benchmark (FSA)</td>
    <td class="tg-baqh">our model predictions are encompassed by those of the benchmark</td>
    <td class="tg-baqh">weght of our forecast</td>
    <td class="tg-9ia8">green (weight significantly different from zero)</td>
  </tr>
  <tr>
    <td class="tg-9hbo">Bias (FSA)</td>
    <td class="tg-baqh">our forecasts are not biased (i.e. the average error is significantly different from zero)</td>
    <td class="tg-baqh">average error</td>
    <td class="tg-cmwg">red</td>
  </tr>
  <tr>
    <td class="tg-9hbo">Autocorrelation (FSA)</td>
    <td class="tg-baqh">our forecasts are not biased (i.e. the average error is significantly different from zero)</td>
    <td class="tg-baqh">autocorrelation of errors</td>
    <td class="tg-cmwg">red</td>
  </tr>
</table>

Warnings:

- As highlighted by [Diebold (2015)](http://www.tandfonline.com/doi/abs/10.1080/07350015.2014.983236),  one should be warned against the temptation of using the DM test for *model* comparisons. The test, which is based on a given subsample of simulated out-of-sample forecast errors, is mainly useful to evaluate predictive accuracy during particular historical episodes.  
- The graphical interface allows the user to change the evaluation period in the blink of a click. Thus, it is very easy to check whether the results are robust or not to the addition or deletion of parts of the sample. By  discarding the possibility that results are driven by the choice of the evaluation sample, one can insure against the oversize problem. Formal *robust* tests for evaluating accuracy have been independently proposed by [Hansen and Timmerman (2011)]( http://www.eui.eu/Documents/DepartmentsCentres/Economics/Researchandteaching/Conferences/TSEConference-NewDevelopmentsinTimeSeries/Hansen.pdf) and [Rossi and Inoue (2012)](http://www.tandfonline.com/doi/abs/10.1080/07350015.2012.693850).


#### Visualization in JDemetra+

The figure below shows that the tests results are displayed in the lower part of the table. 

- As it can be shown below for the case of German GDP growth, the p-values of the DM test are slightly below 0.2 when the forecast is made from 68 to 60 days *before* the end of the quarter. Results for information sets ranging from -59 to 0 (end of the quarter) and from +1 to +44 (one day before the official GDP release) are not visible in this image, but they can displayed within *J*Demetra*+* by  moving the lower bar to the right.
- When the FSA-DM test is used, the exact p-values are not displayed. In this case, we simply fill the cells with an increasingly saturated colour tone when the p-values are within the intervals [0.2, 0.1), [0.1, 0.05),[0.05, 0), respectively. No colour is applied when the p-value is larger than 0.2; which happens to be the case in our example. 
- As mentioned in the summary table above, the values reported for the test "our model encompasses the benchmark" are associated to the weight of the benchmark, which turns out to be close to zero in our example, so we do not reject the null hypothesis. 
- The next row corresponds to the test "our model encompasses the benchmark", which contains the weights associated to our model, which become increasingly close to one as we approach the end of the quarter we are forecasting. In the example, we can see that 66 days before the end of the quarter, the green colour indicates that the null hypothesis is rejected. 
- The next two rows test whether bias and autocorrelation are significant. It is not the case in our example.
 
For further clarifications regarding the interpretation of the tests and their implementation, please read the technical note ["A forecasting evaluation library for JDemetra+"](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/ForecastingEvaluationLibrary.pdf).

![](http://i.imgur.com/d4ySe6c.png)

### References used

- Hyndman R. and A. B. Koehler (2006). [Another look at measures of
forecast accuracy](http://dx.doi.org/10.1016/j.ijforecast.2006.03.001). *International Journal of Forecasting*. **22**, 679-688

- Coroneo, L. and F. Iacone (2016). [Comparing predictive accuracy](https://www.york.ac.uk/media/economics/documents/discussionpapers/2015/1515.pdf)
in small samples using Fixed-smoothing asymptotics.  Discussion Papers University
of York, 15/15

- Diebold, F.X. and R.S. Mariano (1995). <a href="http://dx.doi.org/10.1016/j.ijforecast.2006.03.001">Comparing predictive accuracy</a>. *Journal of Business and Economic Statistics*. **13**, 253-265

-  Harvey, Leybourne and Newbold (1998). [Tests for forecast encompassing](https://www.jstor.org/stable/1392581?seq=1#page_scan_tab_contents). *Journal of Business and Economic Statistics*. **16**, 254-259

- De Antonio Liedo , D. (2017). [A forecasting evaluation library for JDemetra+](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/ForecastingEvaluationLibrary.pdf). Technical note, National Bank of Belgium.
