---
layout: left-menu
title: Estimation 
tagline: JD+. State space models
description: Functions to run and estimate the model 
category: R package
order: 20
---

# {{page.description}}
Once the [transition](../rpackage/state.html) and [measurement](../rpackage/measurement.html) equations have been specified, we are ready to 
estimate the model parameters and to calculate the latent variables conditional con the data. 

Estimation can be conducted using two alternative likelihood definitions. For models where non-stationary latent variables enter the measurement equations
with a coefficient, the correct approach is to use the marginal likelihood definition by [Francke et al.(2010)](https://doi.org/10.1111/j.1467-9892.2010.00673.x). Alternatively, the more usual diffuse
likelihood remains valid for models where the parameters of the measurement equation are independent from the non-stationary latent factors. 

In both cases, it is possible to use the so-called concentrated likelihood. You can think of it 
as if all the stochastic disturbances defined in the model would have a common term that is
isolated. The [Levenberg-Marquardt](https://en.wikipedia.org/wiki/Levenberg%E2%80%93Marquardt_algorithm) numerical optimization method is applied in this case. When the model is specified, 
the user needs to understand whether the parameters are identifiable. If none of the shock variances are fixed,
the software will fix to one the one that could be larger a priory. Since all variances are multiplied by a scale (concentrating factor), this operation does 
not result on an overidentification of the model. However, the sofware (or the user) may end up fixing a variance for a stochastic process that is almost deterministic. In that case,
the resulting scaling or concentrating factor may be very close to zero, which would lead to serious instabilities during the Levenberg-Marquardt optimization procedure. For the remaining shocks,
when the sofware detects that their estimates may be close to zero, the algorithm continues under the assumption that they are equal to zero, and after a few iterations, such an assumption is relaxed 
through the use of the Broyden–Fletcher–Goldfarb–Shanno algorithm, which does not exploit the concentrated likelihood.

Alternatively, choosing upfront not to concentrate the likelihood will trigger the [Broyden–Fletcher–Goldfarb–Shanno](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) 
method. In this case, the parameter regions with small variances can be explored effectively. In this case, none of the variances are fixed by the alrogithm. However, it remains
responsibility of the user to ensure that the model parameters are identifiable. 



## estimate
***
#### output
Creates a JD+ object of the class `JD3_ProcResults`, which includes the estimated parameters, the value of the likelihood function and the first and second
moments of the latent variables conditional on the data 

#### usage 
estimate(object,data, precision, marginal, concentrated, initialParameters)   

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
    <td class="tg-0pky">object </td>
    <td class="tg-0pky">  state-space model belonging to JD3_SsfModel class  </td>
    <td class="tg-0pky"> </td>
    <td class="tg-0pky"> </td>
  </tr>
  <tr>
    <td class="tg-0pky">data </td>
    <td class="tg-0pky"> data matrix (one time series per column, time series dimension on the rows) </td>
    <td class="tg-0pky"> <b></b> </td>
    <td class="tg-0pky">the data can have missing values  </td>
  </tr>
  <tr>
    <td class="tg-0pky">precision</td>
    <td class="tg-0pky">  <i>double</i> indicating the largest likelihood deviations that make the algorithm stop </td>
    <td class="tg-0pky"> 1e-15 </td>
    <td class="tg-0pky"> </td>
  </tr>
    <tr>
    <td class="tg-0pky">marginal</td>
    <td class="tg-0pky">  <i>logical</i> value used to specify whether the marginal likelihood definition is used  (TRUE) or not (FALSE) during the optimization </td>
    <td class="tg-0pky"> FALSE </td>
    <td class="tg-0pky"> The marginal likelihood is recommended when there is at least one variable that loads
    on a non-stationary latent variable and the loading coefficient needs to be estimated. In this situation, Francke et al. (2010) show that using the likelihood 	
	function might be misleading</td>
  </tr>
    <tr>
    <td class="tg-0pky">concentrated</td>
    <td class="tg-0pky">  <i>logical</i> value used to specify whether the likelihood is concentrated  (TRUE) or not (FALSE) during the optimization	</td>
    <td class="tg-0pky"> TRUE </td>
    <td class="tg-0pky"> The optimization algorithm used is different in each case</td>
  </tr>
    <tr>
    <td class="tg-0pky">initialParameters</td>
    <td class="tg-0pky">  numeric <i>array</i> containing the value of the parameters	</td>
    <td class="tg-0pky"> NULL </td>
    <td class="tg-0pky"> By default, the parameter values specified when both measurement and transition equations are used is defined. If the estimated parameters of your
     model are given by p=result(model, "parameters"), it makes sense to use the variable p as initial parameters for an estimation based on
     an updated sample (i.e. initialParameters=p)	 </td>
  </tr>

</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

#### Examples of use 
```R 
results <-estimate(modelName,data, precision=1e-15, marginal=TRUE, concentrated=TRUE, initialParameters=p )                                            
results <-estimate(modelName,data )                                            
``` 

## compute
***
#### output
Creates a JD+ object of the class `JD3_ProcResults`,  which includes the model parameters, the value of the likelihood function and the first and second
moments of the latent variables conditional on the data

#### usage 
compute(object,data, precision, marginal, concentrated)   


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
    <td class="tg-0pky">object </td>
    <td class="tg-0pky">  state-space model belonging to JD3_SsfModel class  </td>
    <td class="tg-0pky"> </td>
    <td class="tg-0pky"> </td>
  </tr>
  <tr>
    <td class="tg-0pky">data </td>
    <td class="tg-0pky"> data matrix (one time series per column, time series dimension on the rows) </td>
    <td class="tg-0pky"> <b></b> </td>
    <td class="tg-0pky">the data can have missing values  </td>
  </tr>
  <tr>
    <td class="tg-0pky">precision</td>
    <td class="tg-0pky">  <i>double</i> indicating the largest likelihood deviations that make the algorithm stop </td>
    <td class="tg-0pky"> 1e-15 </td>
    <td class="tg-0pky"> </td>
  </tr>
    <tr>
    <td class="tg-0pky">marginal</td>
    <td class="tg-0pky">  <i>logical</i> value used to specify whether the marginal likelihood definition is used  (TRUE) or not (FALSE) during the optimization </td>
    <td class="tg-0pky"> FALSE </td>
    <td class="tg-0pky"> The marginal likelihood is recommended when there is at least one variable that loads
    on a non-stationary latent variable and the loading coefficient needs to be estimated. In this situation, Francke et al. (2010) show that using the likelihood 	
	function might be misleading</td>
  </tr>
    <tr>
    <td class="tg-0pky">concentrated</td>
    <td class="tg-0pky">  <i>logical</i> value used to specify whether the likelihood is concentrated  (TRUE) or not (FALSE) during the optimization	</td>
    <td class="tg-0pky"> TRUE </td>
    <td class="tg-0pky"> The optimization algorithm used is different in each case</td>
  </tr>

</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

#### Examples of use 
```R 
results <-compute(modelName,data, precision=1e-15, marginal=TRUE, concentrated=TRUE )                                            
results <-compute(modelName,data )                                            
``` 