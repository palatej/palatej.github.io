---
layout: left-menu
title: Rotating Panels
tagline: JD+. State space models
description: A model to exploit surveys constructed with rotating panels
category: Examples
order: 4
---
# {{page.description}}


## [Definition](../implementations/rotatingPanels.html) 

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
    <td class="tg-0pky">  $nlags$ </td>
   </tr>
  <tr>
    <td class="tg-0pky">Stint</td>
    <td class="tg-0pky"> Division of the survey period (e.g. week). Each individual is surveyed always at the same stint of the survey period   </td>
    <td class="tg-0pky"> $t_j$</td>
  </tr>
  <tr>
    <td class="tg-0pky">Wave</td>
    <td class="tg-0pky"> The $i$th wave comprises a group of individuals that have been surveyed for the $i$th time  </td>
    <td class="tg-0pky"> wave $i$ </td>
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
    <td class="tg-0pky"> Part of the wave-specific error at time $t$ that is correlated to the error of the previous wave at time $t-nlags$       </td>
    <td class="tg-0pky"> $\epsilon^{(i)}_t$</td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>



* * *




### jd3_ssf_msae
***
This R function is used to define an error structure corresponding to a rotating panel. The error model belongs to the JD+ class `JD3_SsfItem` 

#### output
Object of the JD+ class `JD3_SsfItem`: 

#### usage 
 
jd3_ssf_msae(name, nwaves, ar, fixedar=TRUE, lag=1)
 

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
    <td class="tg-0pky">ex. <font color="red">"errorStructure"</font>, do not forget the commmas </td>
  </tr>
 <tr>
    <td class="tg-0pky">nwaves</td>
    <td class="tg-0pky"> <i>integer </i> representing the number of waves </td>
    <td class="tg-0pky"> </td>
    <td class="tg-0pky">The first wave contains individuals that have been surveyed for the first time. The second wave contains the individuals
     that have been surveyed for the second time. The last wave corresponds to the individuals that have been surveyed for the last time (they will 
	 not participate in the survey again). Note that the rotating panel design ensures that all individuals are interviewed only once in the same
	 survey period and this happens always at the same stint (e.g. week). </td>
  </tr>
  <tr>
    <td class="tg-0pky">ar</td>
    <td class="tg-0pky"> <i>R matrix</i> representing the covariance structure of the wave specific survey error. </td>
    <td class="tg-0pky"><b>FALSE</b></td>
    <td class="tg-0pky"> If for example, nwaves=5, one can assume 
    that the errors specific to the first wave of a given survey period are independent from the errors specific to the last wave of the previous survey period  
	( $\varepsilon^{1}_{t}\perp  \varepsilon^{5}_{t-nlags} $, so 
    the coefficient $\phi^{(1)}$ is equal to zero, but $\phi^{(2)}$, $\phi^{(3)}$, $\phi^{(4)}$ and $\phi^{(5))}$ may be estimated or calibrated) </td>
  </tr>
  <tr>
    <td class="tg-0pky">fixedar</td>
    <td class="tg-0pky"> <i>logical</i> that triggers the estimation of the correlation patterns (<b>TRUE</b>) or 
	 fixes them to the values given by the entries of the input matrix above (<b>FALSE</b>) </td>
    <td class="tg-0pky"><b>TRUE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
  <tr>
    <td class="tg-0pky">lag</td>
    <td class="tg-0pky"> <i>integer</i>  specifying the number of time periods (in the base frequency) that compose the survey period. This coincides with the 
	number of time periods an individual has to wait between two different waves. Note that if the survey period is one quarter,
	 a given proportion of the individuals belonging to the same wave have already responded in the previous wave exactly 3 months ago (because
	 individuals are always interviewed at the same stint during each survey period).  </td>
    <td class="tg-0pky"><b>1</b></td>
    <td class="tg-0pky"> </td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

 
#### Examples of use 
[to do ]




