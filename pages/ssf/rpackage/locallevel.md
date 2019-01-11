---
layout: left-menu
title: Local Level
tagline: JD+. State space models
description: Local level (random walk) model
category: Models
order: 1
---
# {{page.description}}


## [Definition](../implementations/ll.html) 
The local level block describes a random walk component. When the innovation variance is set to 0, it also describes a constant term (known when the initialization is specified, estimated otherwise)

$$ l_{t+1} = l_t + \mu_t $$

$$ \mu_t \sim N(0, \sigma^2 \sigma^2_l)$$

It conforms to the [general SSF](../overview/index.html) by setting $ T_t = 1 $, $ V_t =  \sigma^2\sigma^2_l $.

Depending on the estimation algorithm used, it may be preferrable to slightly modify the model and set $\sigma^2=1$


### jd3_ssf_locallevel
***
R users can use this function to define a local level model that belongs to the JD+ class `JD3_SsfItem` 

#### output
Object of the JD+ class `JD3_SsfItem`: 

#### usage 
 
jd3_ssf_locallevel(name, variance, fixed, initial)
 

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
    <td class="tg-0pky">variance</td>
    <td class="tg-0pky"> <i>double </i> for the value of $\sigma^2_l$ </td>
    <td class="tg-0pky">1</td>
    <td class="tg-0pky">variance of the innovation is actually  $\sigma^2\sigma^2_l$</td>
  </tr>
  <tr>
    <td class="tg-0pky">fixed</td>
    <td class="tg-0pky"> <i>logical</i>  that triggers estimation of $\sigma^2_l$ (<b>FALSE</b>) or  
	fixes it (<b>TRUE</b>) to a pre-specified  value set by the parameter variance </td>
    <td class="tg-0pky"><b>FALSE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
  <tr>
    <td class="tg-0pky">initial</td>
    <td class="tg-0pky">  <i>double </i>  setting the value of $l_0$</td>
    <td class="tg-0pky"> <b>NaN</b></td>
    <td class="tg-0pky">The default  <b>NaN</b>  triggers the [diffuse initialization](../algorithms/dk.html)</td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

 
#### Examples of use 
```R
jd3_ssf_locallevel("trend")
jd3_ssf_locallevel("trend", variance=1, fixed=FALSE, initial=NaN) // default
jd3_ssf_locallevel("trend", variance=1, fixed=TRUE)               // fix variance to 1
jd3_ssf_locallevel("trend", variance=1, fixed=TRUE, initial=0)    // fix variance to 1 and initial state to 0
```



### Application 1

In this example we design a model based on a local level specification with default settings (i.e. random walk)

**Create Model**:

- The very first thing one needs to do is to create the model object, which will be called "yourModel":
```R
yourModel<-jd3_ssf_model()
```

**Specify latent variables (transition equations)**:

- Second, we add our random walk and name it as "trend". In the absence of further arguments, this function 
triggers the default specification, which is a random walk without drift:
```R
  add(yourModel, jd3_ssf_locallevel("trend"))
```
 
**Measurement equation design**:

Let's define the following measurement equation   ([see Measurements](../rpackage/measurement.html))

$$ eq1 :  y_{t} =   l_t + \epsilon_{t} $$

where  $$ \epsilon_{t} $$ is I.I.D. with $$ var(\epsilon_{t}) =\sigma^2 \sigma^2_{\epsilon} $$

- Let's assign the name "eq1" to our measurement equation, where the time series called "yourData" ($$ y_{t} $$) is 
assumed to depend on the factor "trend" ($$ l_t $$). By default, the trend enters with coefficient equal to 1. 
The I.I.D. measurement error component $$ \epsilon $$ has a variance equal to zero by 
default (i.e. $$ var(\epsilon_{t})=\sigma^2 \sigma^2_{\epsilon} $$ where  $$\sigma^2_{\epsilon} =0$$ by default):
```R
eq1 <-jd3_ssf_equation("yourData")                            
add(eq1, "trend")                                         
```

-  Since $$ var(\epsilon_{t}) =\sigma^2 \sigma^2_{\epsilon} $$ , the measurement error component is 
exactly identified by fixing $$ \sigma^2_{\epsilon}=1 $$. However, we have said that the default 
specification fixes $$ \sigma^2_{\epsilon}=0 $$ . In order
to impose the restriction $$\sigma^2_{\epsilon}=1 $$, we use the following notation:
```R
eq1 <-jd3_ssf_equation("yourData",variance=1, fixed = TRUE) )                            
add(eq1, "trend")                                         
add(eq1, "constant")                                         
```
-  By default, the coefficient associated to the factor (trend) is equal to one. In order to relax this assumption
and estimate a different model:
$$ eq1 :  y_{t} =\alpha \tau_{t} + \epsilon_{t} $$, 
we use the following arguments:
```R
eq1 <-jd3_ssf_equation("yourData",variance=1, fixed = TRUE) )                            
add(eq1, "trend", 0.5, FALSE)                                         
add(eq1, "constant")                                         
```
where $$ \alpha $$  is a free parameter that is set to  $$ \alpha =0.5 $$ only for the purposes of initialization.

### Application 2 (multivariate)

In this example we design a model with two observables and two factors. The first one is a local level specification with 
default settings (i.e. random walk) and the second factor is a new local level that degenerates to a constant term.

Thus, we have two different measurements $$ y_{1,t}, y_{2,t}$$  for the level $$ l_t  $$. The two measurement
equations follow:

$$ eq1 :    y_{1,t} =c_{1} + \alpha_{1} l_{t} + \epsilon_{1,t} $$, 

$$ eq2 :    y_{2,t} =  \alpha_{2} l_{t} + \epsilon_{2,t} $$, 

This multivariate model would be specified as follows in R:

```R 
// create model

newModel<-jd3_ssf_model()

// specify latent variables

add(newModel, jd3_ssf_locallevel("tau"))
add(newModel, jd3_ssf_locallevel("c1", variance = 0, fixed = TRUE)) 

// two measurement equations

eq1 <-jd3_ssf_equation("y1",variance=1, fixed = TRUE) )                            
add(eq1, "tau", 0.5, FALSE)                                         
add(eq1, "c1")                                         

eq2 <-jd3_ssf_equation("y2",variance=1, fixed = FALSE) // by default it would be (variance=0, fixed = TRUE)                            
add(eq1, "tau", 0.5, FALSE)                                         

```

In this example, the second equation helps to identify $$c_{1}$$. The reason is
that the initial value of $$l_{t}$$ and $$c_{1}$$ in the first equation cannot be separately identified.
