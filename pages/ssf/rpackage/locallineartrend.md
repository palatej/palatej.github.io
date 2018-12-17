---
layout: left-menu
title: Local Linear Trend
tagline: JD+. State space models
description: Local linear trend model
category: R package
order: 40
---
# {{page.description}}


## [Definition](../implementations/llt.html) 
The local linear trend block describes the following trend component:

$$ l_{t+1} = l_t + n_t +  \xi_t $$

$$ n_{t+1} = n_t + \mu_t $$

$$ \xi_t \sim N(0, \sigma^2\sigma^2_l)$$

$$ \mu_t \sim N(0, \sigma^2\sigma^2_n)$$

It conforms to the [general SSF](../overview/index.html)  by setting the state vector 

$$\alpha_t=\begin{pmatrix} l_t \\ n_t  \end{pmatrix}$$

and the transition matrices

$$ T_t = \begin{pmatrix} 1 && 1 \\ 0 && 1 \end{pmatrix} $$

$$ V_t = \begin{pmatrix} \sigma^2\sigma^2_l && 0 \\ 0 && \sigma^2\sigma^2_n \end{pmatrix} $$

Depending on the estimation algorithm used, it may be preferrable to slightly modify the model and set $\sigma^2=1$

### jd3_ssf_locallineartrend
***
R users can use this function to define local linear trend model that belongs to the JD+ class `JD3_SsfItem`

#### output
Object of the JD+ class `JD3_SsfItem`: 

#### usage 
 
jd3_ssf_locallineartrend(name, levelVariance, slopevariance, fixedLevelVariance, fixedSlopeVariance )
 

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
    <th class="tg-0pky"><b>Argument</b></th>
    <th class="tg-0pky"><b>Definition</b></th>
    <th class="tg-0pky"><b>Default</b></th>
    <th class="tg-0pky"><b>Remarks</b></th>
  </tr>
  <tr>
    <td class="tg-0pky">name</td>
    <td class="tg-0pky">  <i>string </i> with the name of the component </td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky">ex. <font color="red">"trend"</font>, do not forget the commmas </td>
  </tr>
  <tr>
    <td class="tg-0pky">levelVariance</td>
    <td class="tg-0pky"> <i>double </i> for the value of $\sigma^2_l$ </td>
    <td class="tg-0pky">1</td>
    <td class="tg-0pky">variance of the level innovation is actually  $\sigma^2\sigma^2_l$</td>
  </tr>
  <tr>
    <td class="tg-0pky">slopeVariance</td>
    <td class="tg-0pky"> <i>double </i> for the value of $\sigma^2_n$ </td>
    <td class="tg-0pky">0.01</td>
    <td class="tg-0pky">variance of the slope innovation is actually  $\sigma^2\sigma^2_n$</td>
  </tr>
  <tr>
    <td class="tg-0pky">fixedLevelVariance</td>
    <td class="tg-0pky"> <i>logical</i>  that triggers estimation of $\sigma^2_l$ (<b>FALSE</b>) or  
	fixes it (<b>TRUE</b>) to a pre-specified  value set by the parameter levelVariance </td>
    <td class="tg-0pky"><b>FALSE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
   <tr>
    <td class="tg-0pky">fixedSlopeVariance</td>
    <td class="tg-0pky"> <i>logical</i>  that triggers estimation of $\sigma^2_n$ (<b>FALSE</b>) or  
	fixes it (<b>TRUE</b>) to a pre-specified  value set by the parameter slopeVariance </td>
    <td class="tg-0pky"><b>FALSE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

 
#### Examples of use 
```R
jd3_ssf_locallineartrend("trend")
jd3_ssf_locallineartrend("trend", levelVariance=1, slopeVariance=0.001,fixedLevelVariance=FALSE, fixedSlopeVariance=FALSE) // default
jd3_ssf_locallineartrend("trend", levelVariance=1, slopeVariance=0.001,fixedLevelVariance=TRUE, fixedSlopeVariance=FALSE) // default
```



### Application

In this example we design a model based on a random walk with drift specification. 

**Create Model**:

- The very first thing one needs to do is to create the model object, which will be called "yourModel":
```R
yourModel<-jd3_ssf_model()
```

**Specify latent variables (transition equations)**:

- Second, we add our random walk with drift and name it as "trend". We fix the slope variance to zero in order to ensure 
that this component becomes a constant. In the absence of further arguments the variance of the level is not specified among the arguments and it is therefore 
the only parameter to estimate (by default, fixedLevelVariance=FALSE):
```R
  add(yourModel, jd3_ssf_locallineartrend("trend", slopeVariance=0, fixedSlopeVariance=TRUE) )
```
 
**Measurement equation design**:

Let's define the following measurement equation ([see Measurements](../rpackage/measurement.html))   
 
 
$$ eq1 :  y_{t} =    l_t +  \epsilon_{1,t} $$

$$ eq2 :  y_{t+h|t} =   l_t + h c + \epsilon_{2,t} $$

The first equation represents an observed variable  $y_{t}$  that measures (with an error $\epsilon_{1,t}$) the latent factor  $l_t $, 
which is assumed to follow a random walk with drift. The second variable represents a h-steps ahead forecast for $y_{t}$, which is given 
by the h-steps ahead forecast of the trend  $l_t + h c  $. Note that $l_t$ and $n_{t}=c$ are the two elements of the state vector in the 
local linear trend model defined above. The 
subindex $t$ in $n_{t}$ in not necessary because we have set the slopeVariance to zero and therefore this term is constant over time (i.e. it 
represents the constant drift component).   


- Let's assign the names "eq1" and "eq2" to our measurement equations, where the time series are called "y" ($ y_{t} $) and "yh" ($ y_{t+h|t} $) 
The I.I.D. measurement error component $ var(\epsion_{1,t})=\sigma^2 \sigma^2_{\epsilon_1} $ will be identified using the normalization 
assumption that $ \sigma^2_{\epsilon_1}=1 $. In turn, $ var(\epsion_{2,t}) $ is left unrestricted. 
```R
eq1 <-jd3_ssf_equation("y1", variance=1, fixed=TRUE)                            
add(eq1, "trend")                                         
eq2 <-jd3_ssf_equation("yh", variance=1, fixed=FALSE)                            
add(eq2, "trend", jd3_ssf_loadings(c(1,2),c(1,h)) )                                         
```
