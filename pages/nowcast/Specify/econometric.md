---
layout: left-menu
title: Econometric model
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Flexible specification of dynamic factor models in JDemetra+
category: Specification
order: 35
---
# {{page.description}}

We present here a common approach to link GDP growth, which is the quarterly variable that we use 
as a target, with the unobserved factors, which are specified at a monthly frequency and 
determine the joint dynamics of the whole system. The same modeling approach can be used for variables others than GDP.

### Measurement Equation
We can specify more than one factor, but for the sake of simplicity, the following expression links the **monthly growth rates 
of all the variables** included in $$ y_{t} $$ to only one monthly factor: 

$$ 
\begin{eqnarray}
y_{t}&=&\bar{y}+\Lambda_{y} f_{1,t} + \psi_{t}  ~~~~~~~~~~~ \text{Measurement equation for monthly series}
\label{mbe}
\end{eqnarray}
$$ 

where $$ \psi_{t} $$ represents the measurement error, which is assumed to be uncorrelated with the factor at all 
leads and lags. It is also assumed to be independent and identically distributed (iid) and following 
a normal distribution: $$ \psi_{t}\sim N(0,R_{\psi}) $$. The covariance matrix is assumed to be 
diagonal, which  implies that the factor will account for 100 $\%$ of the comovements implicit in the model. 

Variables expressed in terms of monthly growth rates can be linked to a factor representing the underlying monthly growth rate of the economy if "M" is 
selected in the graphical interface of `MODEL tab`:
    
![M](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/M.png) 

Because the model has been designed for short-term analysis, it makes sense to represent all these series, including GDP, 
in terms of monthly growth rates or differences. However, the monthly growth rates of official 
GDP figures are not published, hence, equation  \ref{mbe} will need to be modified. Thus, GDP growth 
rates published by the statistical agencies (i.e. $y^{Q}_{t}$ for the euro area, for example) are linked to the 
quarterly growth rate of the underlying factor, which can be approximated as a moving average of the monthly growth rates:

$$ 
\begin{eqnarray}
y^{Q}_{t}&=&\bar{y}^{Q}+\Lambda^{Q}_{y}f^{Q}_{1,t}+ \psi^{Q}_{t},~~~~~~~~~~~~~t=3,6,9,\ldots  ~~~~~ \text{Measurement equation for quarterly series} 
\label{mbe2}  
\end{eqnarray}
$$ 

where $$ f^{Q}_{1,t}={\frac{1}{3} f_{1,t}} +\frac{2}{3}{f_{1,t-1}} + {f_{1,t-2}} +\frac{2}{3}{f_{1,t-3}} +\frac{1}{3}{f_{1,t-4}} $$ 

Monthly or quarterly variables that are correlated with the the underlying quarterly growth rate of the economy can be linked to a weighted average _of the factors representing the underlying monthly growth rate of the economy_. Such a weighted average is meant to represent quarterly growth rates, and it is implemented by 
selecting "Q" in the graphical interface of `MODEL tab`:

![M](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/Q.png)

{: .alert .alert-info}
_**Approximation**: Let $$ F_{t} $$ be the monthly level of the economy and let $$ f_{t}=ln F_{t}-ln F_{t-1} $$ be its monthly growth rate. Now, 
define $$ F^{Q}_{t} $$ as the geometric mean of the last three levels. This implies that $$ ln F^{Q}_{t} = \frac{1}{3}(ln F_{t}+ln F_{t-1}+ln F_{t-2}) $$. The 
resulting quarterly growth rate of the factors, which we denote as $$ f^{Q}_{t} $$, can be expressed as $$ ln F^{Q}_{t}-ln F^{Q}_{t-3} $$. By 
substituting both terms by the geometric mean approximation we obtain $$ f^{Q}_{t}=\frac{1}{3}(ln F_{t}-ln F_{t-3})+\frac{1}{3}(ln F_{t-1}-ln F_{t-4})+\frac{1}{3}(ln F_{t-2}-ln F_{t-5}) $$.  Finally, 
a simple expression for the quarterly growth rate of the factors in terms of their monthly growth rates can be obtained as follows: $$ f^{Q}_{t}=\frac{1}{3}(f_{t}+f_{t-1}+f_{t-2})+\frac{1}{3}(f_{t-1}+f_{t-2}+f_{t-3})+\frac{1}{3}(f_{t-2}+f_{t-3}+f_{t-4}) $$. Rearranging 
terms yields the expression $$ f^{Q}_{t}={\frac{1}{3} f_{t}} +\frac{2}{3}{f_{t-1}} + {f_{t-2}} +\frac{2}{3}{f_{t-3}} +\frac{1}{3}{f_{t-4}} $$ presented above._

Modeling yearly growth rate of a flow variable like GDP. In this case, the measurent equation requires a larger number of lagged factors. 
The new measurement equation for these variables takes the following form:
$$ 
\begin{equation}
y^{Y}_{t}=\bar{y}^{Y}+\Lambda^{Y}_{y}f^{Y}_{t}+ \psi^{Y}_{t},~~~~~~~~~~~~~t=12,24,36,\ldots  ~~~~~ \text{Measurement equation for yearly growth rates} 
\label{mbeY}  
\end{equation}
$$ 

where $$ \tiny f^{Y}_{t}=\frac{1}{12} f_{t} + \frac{2}{12}f_{t-1}  +\frac{3}{12}f_{t-2} + \frac{4}{12}f_{t-3} +\frac{5}{12}f_{t-4} +\frac{6}{12}f_{t-5} +\frac{7}{12}f_{t-6}+\frac{8}{12}f_{t-7} +\frac{9}{12}f_{t-8} +\frac{10}{12}f_{t-9} +\frac{11}{12}f_{t-10} +f_{t-11} + \frac{11}{12}f_{t-12}+\frac{10}{12}f_{t-13} +\frac{9}{12}f_{t-14} +\frac{8}{12}f_{t-15} +\frac{7}{12}f_{t-16} + \frac{6}{12}f_{t-17} +\frac{5}{12}f_{t-18} +\frac{4}{12}f_{t-19} +\frac{3}{12}f_{t-20}  +\frac{2}{12}f_{t-21}  +\frac{1}{12}f_{t-22} $$ 	
The icon needed to implement this concept is

![X](https://palatej.github.io/pages/nowcast/Specify/images/Y.png)

{: .alert .alert-info}
_**Approximation**:Let $$ F_{t} $$ be the monthly level of the economy and let $$ f_{t}=ln F_{t}-ln F_{t-1} $$ be its monthly growth rate. Now, 
define $$ F^{Y}_{t} $$ as the geometric mean of the last twelve levels. This implies that $$ ln F^{Y}_{t} = \frac{1}{12}(ln F_{t}+ln F_{t-1} ... + ln F_{t-11}) $$. The 
resulting yearly growth rate of the factors, which we denote as $$ f^{Y}_{t} $$, can be expressed as $$ ln F^{Y}_{t}-ln F^{Y}_{t-12} $$. By 
substituting both terms by the geometric mean approximation and using the same method as in the approximation of quarterly growth we 
obtain  $$  \tiny f^{Y}_{t}=\frac{1}{12} f_{t} + \frac{2}{12}f_{t-1}  +\frac{3}{12}f_{t-2} + \frac{4}{12}f_{t-3} +\frac{5}{12}f_{t-4} +\frac{6}{12}f_{t-5} +\frac{7}{12}f_{t-6}+\frac{8}{12}f_{t-7} +\frac{9}{12}f_{t-8} +\frac{10}{12}f_{t-9} +\frac{11}{12}f_{t-10} +f_{t-11} + \frac{11}{12}f_{t-12}+\frac{10}{12}f_{t-13} +\frac{9}{12}f_{t-14} +\frac{8}{12}f_{t-15} +\frac{7}{12}f_{t-16} + \frac{6}{12}f_{t-17} +\frac{5}{12}f_{t-18} +\frac{4}{12}f_{t-19} +\frac{3}{12}f_{t-20}  +\frac{2}{12}f_{t-21}  +\frac{1}{12}f_{t-22}  $$ ._

	
 
	
### Measurement Equations for Surveys 	

**The link between the time series and the factors** can be more sophisticated. Appart from the two options mentioned above, the measurement equation 
for some variables  (typically survey data)  may require an additional effort. 

- Variables such as the euro area economic sentiment indicator produced by the European Comission, which are
correlated with the year-on-year growth rate of GDP. Those variables may be linked to the cumulative sum of the last 12 monthly factors. If 
the model is designed in such a way that the monthly factors represent monthly growth rates, the resulting cumulative sum boils down to 
the year-on-year growth rate. Thus, variables expressed in terms of year-on-year growth rates or surveys that are correlated with the 
year-on-year growth rates of the reference series should be linked to the factors using this link:

	![Y](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/YoY.png)

- Variables representing expectations or forecasts with a precise horizon may be added to the measurement equation in a model-consistent way. For example, 
think of a quantitative or qualitative survey $$ S_t $$ where respondents have been asked to report how much they expect prices to change over the 
next three months. That is, $$  S_{t}=P_{t+h | t}-P_{t} $$, where $$ P_{t+h | t} $$ stands for the price level expected three months ahead 
when $$ h=3 $$. Variables that contains expectations about the future are likely to be informative about the current state of the economy,  
$$ f_t$$, so in principle they could be linked to the factors in the usual way:
$$
\begin{eqnarray}
S_{t} &=& \Lambda_{s} f_{t}  + \psi^{s}_{t} 
\label{naive}
\end{eqnarray}
$$
However, we can be more precise and introduce a model-consistent link between the surveys and the factors:
$$
\begin{eqnarray}
S_{t} &=& \Lambda_{s}(f_{t+3| t} +f_{t+2| t} + f_{t+1| t}  ) + \psi^{s}_{t} \\
S_{t} &=& \Lambda_{s}(A^3 + A^2  + A ) f_{t} + \psi^{s}_{t} ,~~~~~ \text{Measurement equation for surveys regarding t+3 } \label{modelConsistentM}
\end{eqnarray}
$$
Equation (\ref{modelConsistentM}) is obtained, without loss of generality, by assuming that the factors follow a VAR(1), i.e. $$ f_{t}=A f_{t-1} + u_{t} $$, so
that $$ f_{t+h| t} = A^{h} f_{t} $$. Notice that while the factor loadings in measurement equation (\ref{naive}) are equal  to $$ \Lambda_{s}$$ ,
the factor that enters the more sophisticated measurement equation (\ref{modelConsistentM}) loads on $$ \Lambda_{s}(A^3 + A^2  + A ) $$.  

	![X](https://palatej.github.io/pages/nowcast/Specify/images/X.png)

- Modeling quarterly growth forecasts for a given quarter in the future. GDP forecasts of others can also be modeled in a model consistent way. You 
may think it is a good idea to simply introduce quantitative surveys representing GDP growth forecasts exactly as you would do with the remaining
indicators. However, you may want to achieve efficiency gains by making those forecasts consistent with your model. The presence of a measurement error 
provides some insurance agains model misspecification. How to do it? A GDP growth forecast for, say $$ h $$ quarters ahead is represented as $$ GDP_{t+h\times 3|t}$$
because $$t$$ refers to the montly frequency and a quarter has 3 months. This is introduced in a model as follows:
$$
\begin{eqnarray}
GDP_{t+h \times 3|t} &=& \Lambda_{GDP} f^{Q}_{t+h\times 3 | t}  + \psi^{Q}_{t+ h \times 3} \nonumber \\
GDP_{t+h \times 3|t} &=& \Lambda_{GDP} (\frac{1}{3}A^{h \times 3} +\frac{2}{3}A^{h \times 3-1}  + A^{h \times 3-2}  +\frac{2}{3} A^{h \times 3-3}  +\frac{1}{3}A^{h \times 3-3}) f_{t}  + \psi^{Q}_{t+h \times 3} \nonumber \\
GDP_{t+h \times 3|t} &=& \Lambda_{GDP} (\frac{1}{3}A^{h \times 3}f_{t} +\frac{2}{3}A^{h \times 3-1} f_{t} + A^{h \times 3-2}f_{t} +\frac{2}{3} A^{h \times 3-3} f_{t } +\frac{1}{3}A^{h \times 3-3} f_{t+h \times 3-4} )  + \psi^{Q}_{t+h \times 3}  \nonumber \\
GDP_{t+h \times 3|t} &=& \Lambda_{GDP} (\frac{1}{3}f_{t+h \times 3| t} +\frac{2}{3}f_{t+h \times 3-1 | t} + f_{t+h \times 3-2 | t} +\frac{2}{3}f_{t+h \times 3-3 | t} +\frac{1}{3}f_{t+h \times 3-4| t} )  + \psi^{Q}_{t+h \times 3} 
\label{modelConsistentQ}
\end{eqnarray}
$$
In this case, Equation (\ref{modelConsistentQ}) has a more complex loading structure than equations (\ref{naive}) and  (\ref{modelConsistentM}). As before, it is obtained, without loss of generality, by assuming that the factors follow a 
VAR(1), i.e. $$ f_{t}=A f_{t-1} + u_{t} $$, so that $$ f_{t+h| t} = A^{h} f_{t} $$. 
The icon you need to select to implement this idea	is different than the previous one. After using the "Q" icon to to link quarterly growth rates with the moving average of the factors,
we need to tell the sofware we are dealing with a forcast using the following icon:

	![X](https://palatej.github.io/pages/nowcast/Specify/images/Sh.png)

- Modeling yearly growth forecasts at for given year in the future. The procedure is equivalent to the one followed in the previous point. After using the "Y" icon to to link quarterly growth rates with the moving average of the factors,
we need to tell the sofware we are dealing with a forcast using the following icon, where $$h$$	may be set to 12 if our variable represents a forecast for the previous year:

	![X](https://palatej.github.io/pages/nowcast/Specify/images/Sh.png)

	
- Modeling expectations regarding cummulative growth over $$h$$ quarters. Instead of using icon Shift(h), you will select the icon $$X(h)$$, where $$h=12$$ for instance. In this case, you will be modeling the expected 
growth rate over the next 4 quarters (12 months, since the base frequency in our current set up is monthly):
$$
\begin{eqnarray}
GDP_{t+1 \times 3|t}+GDP_{t+2 \times 3|t}+GDP_{t+3 \times 3|t}+GDP_{t+4 \times 3|t} &=& \Lambda_{GDP} (f^{Q}_{t+1\times 3 | t}+f^{Q}_{t+2\times 3 | t}+f^{Q}_{t+3\times 3 | t}+f^{Q}_{t+h\times 3 | t})  + \psi^{Q}_{t+ h \times 3} \nonumber \\
\label{modelConsistentY}
\end{eqnarray}
$$
which is different from GDP growth expected for the last quarter of the year, i.e. Shift(h) with $$h=12$$ and also different from yearly growth rates that are typically reported (they compare the GDP flow of a year with that of the 
previous year), so be careful with this. This exapression can be expanded by replacing $$ f^{Q}_{t+h| t}$$ by the corresponding weighted average, and of course,
by dividing both sides of this expressioin by 4, we get the average growth rate for all quarters of the year. 

 


    
### Transition Equation

Specifying the joint dynamics of all variables requires a second equation representing the factor as a vector autoregressive (VAR) process 
with a non-diagonal covariance matrix for the error term.  Because the measurement equation links GDP growth with a moving average of the monthly factors, 
the dimension of the state vector must be at least equal to 5. The minimum dimension would be 12 if at least one of the variables is expressed on year-on-year
growth rates. To sum up, the representation given by equations \ref{mbenchmark} and \ref{ssbenchmark} conforms 
to the so-called state-space representation of this model in the case where you observed both quarterly and monthly growth rates: 

$$ 
\begin{eqnarray}
\label{mbenchmark}  
\left( \begin{array}{c}
y^{Q}_{t}- \bar{y}^{Q}\\
y_{t}-\bar{y} \end{array} \right)&=& \left( \begin{array}{ccccc}
\Lambda_{y}^{Q} & 2\Lambda_{y}^{Q} & 3\Lambda_{y}^{Q} & 2\Lambda_{y}^{Q} & \Lambda_{y}^{Q} \\ 
\Lambda_{y}     &    0         &   0           & 0    &   0  
\end{array} \right)
\left( \begin{array}{c}
f_{1,t} \\
f_{1,t-1} \\
f_{1,t-2} \\
f_{1,t-3} \\
f_{1,t-4} \\
\end{array} \right)+ 
\left( \begin{array}{c}
\psi^{Q}_{t}\\
\psi_{t} \\
\end{array} \right)     \\
\label{ssbenchmark}
\left( \begin{array}{c} %
f_{1,t} \\
f_{1,t-1} \\
f_{1,t-2} \\
f_{1,t-3} \\
f_{1,t-4} \\
\end{array} \right)&=&
\left( \begin{array}{ccccc}
A_{11}          &    A_{12}         &   A_{13}           & A_{14}      &   0   \\
I               &    0         &   0           & 0      &   0         \\
0               &    I         &   0           & 0      &   0        \\
0               &    0         &   I           & 0      &   0    \\
0               &    0         &   0           & I      &   0     \\
\end{array} \right)
\left( \begin{array}{c}
f_{1,t-1} \\
f_{1,t-2} \\
f_{1,t-3} \\
f_{1,t-4} \\
f_{1,t-5} \\
\end{array} \right)
+
\left( \begin{array}{c}
u^{f}_{t} \\
0\\
0\\
0\\
0\\
\end{array} \right) 
\end{eqnarray}
$$ 

This equation represents a VAR of order 4 for the factor, but one could restrict it to a VAR(1) by setting $$ A_{12} = A_{13} = A_{14} = 0 $$. The error 
component $$ u^{f}_{t} $$   is uncorrelated with the measurement error term $$ \psi_{t}$$ , in line with the literature on factor models.

### State-Space framework in JDemetra+

The sophisticated measurement and transition equations that have been described below conform a state-space representation (SSF) of the mixed-frequencies dynamic factor model. Such
state-space system inherits all properties and algorithms of the [`general linear gaussian` state-space model used throughout  JD+ 3.0.](https://palatej.github.io/pages/ssf/algorithms/)
The particularities of the design for the dynamic factor models used for nowcasting is described in [Section: Design issues in Java](https://palatej.github.io/pages/nowcast/Specify/implementation.html). You
will observe that the matrices in expressions  (\ref{mbenchmark}) and (\ref{ssbenchmark}) are sparse, i.e. they have a lot of zeros. Since multiplying by zeroes and inverting large matrices
is inneficient, we exploit the object oriented framework of Java in such a way that the algorithms of the different dynamic factor models that can be constructed have been 
optimized to a very large extent. This will ensure estimation is feasible even for large models without the need to use the EM algorithm. 

As it will be discussed in [Section: Design issues in Java](https://palatej.github.io/pages/nowcast/Specify/implementation.html), our approach is very different from that 
of alternative softwares packages built in Matlab, SAS, and OX.

