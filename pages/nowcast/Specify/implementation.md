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

{: .alert .alert-info}
_Let $$ F_{t} $$ be the monthly level of the economy and let $$ f_{t}=ln F_{t}-ln F_{t-1} $$ be its monthly growth rate. Now, 
define $$ F^{Q}_{t} $$ as the geometric mean of the last three levels. This implies that $$ ln F^{Q}_{t} = \frac{1}{3}(ln F_{t}+ln F_{t-1}+ln F_{t-2}) $$. The 
resulting quarterly growth rate of the factors, which we denote as $$ f^{Q}_{t} $$, can be expressed as $$ ln F^{Q}_{t}-ln F^{Q}_{t-3} $$. By 
substituting both terms by the geometric mean approximation we obtain $$ f^{Q}_{t}=\frac{1}{3}(ln F_{t}-ln F_{t-3})+\frac{1}{3}(ln F_{t-1}-ln F_{t-4})+\frac{1}{3}(ln F_{t-2}-ln F_{t-5}) $$.  Finally, 
a simple expression for the quarterly growth rate of the factors in terms of their monthly growth rates can be obtained as follows: $$ f^{Q}_{t}=\frac{1}{3}(f_{t}+f_{t-1}+f_{t-2})+\frac{1}{3}(f_{t-1}+f_{t-2}+f_{t-3})+\frac{1}{3}(f_{t-2}+f_{t-3}+f_{t-4}) $$. Rearranging 
terms yields the expression $$ f^{Q}_{t}={\frac{1}{3} f_{t}} +\frac{2}{3}{f_{t-1}} + {f_{t-2}} +\frac{2}{3}{f_{t-3}} +\frac{1}{3}{f_{t-4}} $$ presented above._

**The link between the time series and the factors** can be very sophisticated. Three options are possible for the moment:
 
-   Variables expressed in terms of monthly growth rates can be linked to a factor representing the underlying monthly growth rate of the economy if "M" is selected
    
	![M](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/M.png) 
	
 
-   Monthly or quarterly variables that are correlated with the the underlying quarterly growth rate of the economy can be linked to a weighted average _of the factors representing the underlying monthly growth rate of the economy_. Such a weighted average is meant to represent quarterly growth rates, and it is implemented by selecting "Q":

	![M](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/Q.png)
 
-   The variables can also be linked to the cumulative sum of the last 12 monthly factors. If the model is designed in such a way that the monthly factors represent monthly growth rates, the resulting cumulative sum boils down to the year-on-year growth rate. Thus, variables expressed in terms of year-on-year growth rates or surveys that are correlated with the year-on-year growth rates of the reference series should be linked to the factors using this link:

	![M](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/YoY.png)

-   Variables representing expectations or forecasts with a precise  horizon:

	![M](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/YoY.png)
	
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


