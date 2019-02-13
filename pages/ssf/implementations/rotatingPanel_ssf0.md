---
layout: left-menu
title: Definition
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space of a rotating panels error structure
category: "Rotating Panel"
order: 2010
---

# {{page.description}}

#### Introduction

The following concepts are required to define a rotating panel:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border-color:#ccc;margin:0px auto;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#fff;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#f0f0f0;}
.tg .tg-if4e{background-color:#f9f9f9;font-weight:bold;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-fymr{font-weight:bold;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-btxf{background-color:#f9f9f9;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg-sort-header::-moz-selection{background:0 0}.tg-sort-header::selection{background:0 0}.tg-sort-header{cursor:pointer}.tg-sort-header:after{content:'';float:right;margin-top:7px;border-width:0 5px 5px;border-style:solid;border-color:#404040 transparent;visibility:hidden}.tg-sort-header:hover:after{visibility:visible}.tg-sort-asc:after,.tg-sort-asc:hover:after,.tg-sort-desc:after{visibility:visible;opacity:.4}.tg-sort-desc:after{border-bottom:none;border-width:5px 5px 0}@media screen and (max-width: 767px) {.tg {width: auto !important;}.tg col {width: auto !important;}.tg-wrap {overflow-x: auto;-webkit-overflow-scrolling: touch;margin: auto 0px;}}</style>
<div class="tg-wrap"><table id="tg-rBYYg" class="tg">
  <tr>
    <th class="tg-0pky"><b>Concept</b></th>
    <th class="tg-0pky"><b>Definition</b></th>
    <th class="tg-0pky"><b>Symbol</b></th>
   </tr>
  <tr>
    <td class="tg-0pky">Base frequency</td>
    <td class="tg-0pky"> Frequency of the model latent variables (e.g. months, quarters)     </td>
    <td class="tg-0pky"> $t$ </td>
   </tr>
 <tr>
    <td class="tg-0pky">Survey period</td>
    <td class="tg-0pky"> Number of periods (in the base frequency) during which the survey continiously takes place </td>
    <td class="tg-0pky">  $lag$ </td>
   </tr>
  <tr>
    <td class="tg-0pky">Stint</td>
    <td class="tg-0pky"> Division of the survey period (e.g. week). Each individual is surveyed always at the same stint of the survey period   </td>
    <td class="tg-0pky"> $t_j$</td>
  </tr>
  <tr>
    <td class="tg-0pky">Wave</td>
    <td class="tg-0pky"> The $i$th wave comprises a group of individuals that have been surveyed for the $i$th time  </td>
    <td class="tg-0pky"> waves $1,\ldots,i,\ldots,   W $ </td>
  </tr>
    <tr>
    <td class="tg-0pky">Persistence</td>
    <td class="tg-0pky"> The total number of waves or, equivalently, the number of consecutive survey periods that a first wave individual will remain in the panel </td>
    <td class="tg-0pky"> $W $ </td>
  </tr>
  <tr>
    <td class="tg-0pky">Wave-specific error</td>
    <td class="tg-0pky"> For a given wave, the difference between the average response and the actual perception (subset of the wave corresponding to base period $t$)      </td>
    <td class="tg-0pky"> $e^{(i)}_t$ </td>
  </tr>
    <tr>
    <td class="tg-0pky">Bias term</td>
    <td class="tg-0pky"> Part of the wave-specific error that accumulates over the survey period (it is assumed to be zero on average for all waves)     </td>
    <td class="tg-0pky"> $b^{(i)}_t$ </td>
  </tr>
    <tr>
    <td class="tg-0pky">Correlation term</td>
    <td class="tg-0pky"> Part of the wave-specific error at time $t$ that is independent from the bias component, and may be correlated with the error at time $t-lag$       </td>
    <td class="tg-0pky"> $\epsilon^{(i)}_t$</td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

* * *

The model presented here is complatible with the measurement error structure arising from rotating panels such 
as the Labour Force Survey in the UK. 

We assume the aggregate response of individuals belonging to wave ($i$) at time $t$, i.e. $y^{(i)}_{t}$,  has an errors in variables structure:

$$y^{(i)}_{t} = Y_{t} + e^{(i)}_{t}$$,

where  $$Y_{t}$$ is a variable representing the true value of the economic concept for which the group of individuals $i$ has been 
surveyed. Thus, orthogonal to this variable we have $$e^{(i)}_{t}$$, which is considered to be a measurement error. This is given by the
fact that only a small fraction of the population is answering to the survey. However, we will assume that $$e^{(i)}_{t}$$ has a particular structure
that is given by the rotating survey design:

$$e^{(i)}_{t} = b^{(i)}_{t} + \varepsilon^{(i)}_{t}$$

__Bias component__

The first term follows a random walk process and it represents bias, although the sum of the bias terms accross waves is equal to zero:

$$b^{(i)}_{t} = b^{(i)}_{t-1} + w^{(i)}_{t}$$, 

where  $$w^{(i)}_{t} \sim N\left(0, \sigma^2_{i} \right)$$.

Most of the times, this component cannot be identified together with additional trend components. Thus, one identification restriction
is to assume that the bias terms for all weights is equal to zero (cite [example]()): 

$$b^{(1)}_{t} = -\sum_{i=2}^{W} b^{(i)}_{t} $$

Alternatively, one could assume that there is no bias in the first wave (cite [example]()).

__Autocorrelation component__

The second term represents an autocorrelated wave specific survey error. Given that each wave $i$ for time $t$ comprises a group of individuals that has been surveyed 
for the $ith$ time, and the same group of individuals responded during the previous survey period (i.e.  $t-nlags$) for the  $i-1$th time, a correlation pattern 
may arise when the responses are not updated efficiently. Thus, the error in wave $i$ for time $t$ may be correlated with the error 
in wave $i-1$ for time $t-nlags$, for $i>1$ (i.e. the first response of the individuals may be biased, but it is not correlated with previous responses, simply because
it is the very first time they are asked to respond):

$$ \varepsilon^{(i)}_{t} = \phi^{(i)}_{1} \varepsilon^{(i-1)}_{t-nlags} + \epsilon^{(i)}_{t}$$, 

where $$\epsilon^{(i)}_{t} \sim N\left(0, (1-(\phi^{(i)}_{1})^{2})(k^{(i)})^{2}  \right) $$. Note 
that $\phi^{(i)}_{1}=0$ for  $i=1$. 

The autocorrelated wage specific errors are driven by a proportion of individuals that do not update their responses on the basis of new information, so 
in principle it is possible that first wave individuals' responses persist until the last wave $$W$$. However, it is typically assumed that 
the error in the first response is correlated to the error in the second response, but uncorrelated to the error in the third response. 

A representation of all possible correlation patterns in a panel defined by $ W=5 $ and $ nlags=3 $ follows in this table:

<br/>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border-color:#ccc;margin:0px auto;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#fff;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#f0f0f0;}
.tg .tg-zhlz{background-color:#9aff99;color:#fe0000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-4fps{background-color:#efefef;color:#000000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-64au{background-color:#ffffff;color:#3531ff;border-color:#c0c0c0;text-align:left;vertical-align:top}
.tg .tg-vq2r{background-color:#ffccc9;color:#000000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-2iub{background-color:#efefef;color:#000000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-ephz{background-color:#ffffff;color:#32cb00;border-color:#c0c0c0;text-align:left;vertical-align:top}
.tg .tg-msbt{background-color:#cbcefb;color:#fe0000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-h7fs{background-color:#9aff99;color:#000000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-ajer{background-color:#ffccc9;color:#3531ff;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-hc6b{background-color:#efefef;color:#3531ff;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-ns90{background-color:#ffccc9;color:#036400;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-dn45{background-color:#ffffff;color:#fe0000;border-color:#c0c0c0;text-align:left;vertical-align:top}
.tg .tg-iks7{background-color:#ffffff;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-f6zi{background-color:#efefef;color:#fe0000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-9gyk{background-color:#efefef;color:#036400;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-alwn{background-color:#ffffff;color:#000000;border-color:#c0c0c0;text-align:left;vertical-align:top}
.tg .tg-lzr2{background-color:#ffccc9;color:#fe0000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-usd3{background-color:#9aff99;color:#036400;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-817c{background-color:#9aff99;color:#3531ff;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-zjti{background-color:#cbcefb;color:#000000;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-7hn9{background-color:#cbcefb;color:#036400;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-kqhi{background-color:#cbcefb;color:#3531ff;border-color:#000000;text-align:left;vertical-align:top}
.tg-sort-header::-moz-selection{background:0 0}.tg-sort-header::selection{background:0 0}.tg-sort-header{cursor:pointer}.tg-sort-header:after{content:'';float:right;margin-top:7px;border-width:0 5px 5px;border-style:solid;border-color:#404040 transparent;visibility:hidden}.tg-sort-header:hover:after{visibility:visible}.tg-sort-asc:after,.tg-sort-asc:hover:after,.tg-sort-desc:after{visibility:visible;opacity:.4}.tg-sort-desc:after{border-bottom:none;border-width:5px 5px 0}@media screen and (max-width: 767px) {.tg {width: auto !important;}.tg col {width: auto !important;}.tg-wrap {overflow-x: auto;-webkit-overflow-scrolling: touch;margin: auto 0px;}}</style>
<div class="tg-wrap"><table id="tg-qig81" class="tg">
  <tr>
    <th class="tg-iks7" colspan="4">Input Correlation Matrix with $ W=5 $ and $ nlags=3 $</th>
    <th class="tg-4fps">$\varepsilon^{(1)}_{t}$</th>
    <th class="tg-4fps">$\varepsilon^{(2)}_{t}$</th>
    <th class="tg-4fps">$\varepsilon^{(3)}_{t}$</th>
    <th class="tg-4fps">$\varepsilon^{(4)}_{t}$</th>
    <th class="tg-4fps">$\varepsilon^{(5)}_{t}$</th>
  </tr>
  <tr>
    <td class="tg-2iub">$\varepsilon^{(1)}_{t-3}$</td>
    <td class="tg-2iub">$\varepsilon^{(2)}_{t-3}$ </td>
    <td class="tg-2iub">$\varepsilon^{(3)}_{t-3}$</td>
    <td class="tg-2iub">$\varepsilon^{(4)}_{t-3}$</td>
    <td class="tg-wltw">0</td>
    <td class="tg-alwn">$\phi^{2}_{1}$</td>
    <td class="tg-alwn">$\phi^{3}_{1}$</td>
    <td class="tg-alwn">$\phi^{4}_{1}$</td>
    <td class="tg-alwn">$\phi^{5}_{1}$</td>
  </tr>
  <tr>
    <td class="tg-lzr2"></td>
    <td class="tg-lzr2">$\varepsilon^{(1)}_{t-3\times 2}$</td>
    <td class="tg-lzr2">$\varepsilon^{(2)}_{t-3\times 2}$</td>
    <td class="tg-lzr2">$\varepsilon^{(3)}_{t-3\times 2}$</td>
    <td class="tg-dn45">0</td>
    <td class="tg-dn45">0</td>
    <td class="tg-dn45">$\phi^{3}_{2}$</td>
    <td class="tg-dn45">$\phi^{4}_{2}$</td>
    <td class="tg-dn45">$\phi^{5}_{2}$</td>
  </tr>
  <tr>
    <td class="tg-usd3"></td>
    <td class="tg-usd3"></td>
    <td class="tg-usd3">$\varepsilon^{(1)}_{t-3\times 3}$</td>
    <td class="tg-usd3">$\varepsilon^{(2)}_{t-3\times 3}$</td>
    <td class="tg-ephz">0</td>
    <td class="tg-ephz">0</td>
    <td class="tg-ephz">0</td>
    <td class="tg-ephz">$\phi^{4}_{3}$</td>
    <td class="tg-ephz">$\phi^{5}_{3}$</td>
  </tr>
  <tr>
    <td class="tg-zjti"></td>
    <td class="tg-msbt"></td>
    <td class="tg-7hn9"></td>
    <td class="tg-kqhi">$\varepsilon^{(1)}_{t-3\times 4}$</td>
    <td class="tg-64au">0</td>
    <td class="tg-64au">0</td>
    <td class="tg-64au">0</td>
    <td class="tg-64au">0</td>
    <td class="tg-64au">$\phi^{5}_{1}$</td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>


[HTML Tables generator](https://www.tablesgenerator.com/html_tables)
	

<br/>


If we assume that the error in the first response is correlated to the error in the second response and third responses, the coefficients in 
green and blue will be zero. The resulting representation would then have the following form:

$$
\begin{eqnarray}
\varepsilon^{(i)}_{t} = \phi^{(i)}_{1} \varepsilon^{(i-1)}_{t-nlags} + {\color{red}\phi^{(i)}_{2}} \varepsilon^{(i-2)}_{t- nlags\times 2} + \epsilon^{(i)}_{t}, 
\end{eqnarray}
$$

with  $$ \phi^{(i)}_{1}=0 $$ for  $$ i=1 $$ and  $$ \phi^{(i)}_{2}=0 $$  for $$ i=1,2 $$. 

<br/>

#### References

[to be added]
  
 - HARVEY, A. and C.H. Chung(2000),  [Estimating the underlying change in unemployment in the UK](https://doi.org/10.1111/1467-985X.00171), *Journal of the Royal Statistical Society: Series A*, Volume **163**, p. 303-339
 - van den BRAKEL, J. and S. Krieg (2009),  Structural time series modelling of the monthly unemployment rate in a rotating panel] , *Discussion Paper*, 09031
 - ELLIOT, E. (2017),  Increasing frequency and improving timeliness of key variables in the UK Labour Force Survey, *University of Southampton*
 

