---
layout: left-menu
title: AR(p)
tagline: JD+. State space models
description: Autoregressive model of order p
category: Models
order: 3
---
# {{page.description}}


## [Definition](../implementations/ar.html) 
The AR process is defined by

$$\Phi\left(B\right)y_t=\epsilon_t $$ 

where:  

$$\Phi\left(B\right)=1+\varphi_1 B + \cdots + \varphi_p B^p $$   

is an auto-regressive polynomial. 

It conforms to the [general SSF](../overview/index.html) by setting the state vector 

$$ \alpha_t= \begin{pmatrix} y_t \\ y_{t-1} \\ \vdots \\ y_{t-p+1} \end{pmatrix}$$  

and the transition matrices

$$ T_t = \begin{pmatrix}-\varphi_1 & \cdots & \cdots  & -\varphi_p  \\
                        1          & \cdots &  \cdots &  0          \\ 
						\vdots     & \ddots &  \ddots & \vdots\\ 
						0          &   0    &  1      & 0  \end{pmatrix}$$

$$ S_t = \begin{pmatrix} \sigma_{ar} \\ 0 \\ \vdots\\ 0 \end{pmatrix} $$  

$$ V_t = S S' $$

Depending on the estimation algorithm used, it may be preferrable to slightly modify the model and set $\sigma_{ar}^2=1$


### jd3_ssf_ar
***
This R function is used to define an autoregressive model that belongs to the JD+ class `JD3_SsfItem` 

#### output
Object of the JD+ class `JD3_SsfItem`: 

#### usage 
 
jd3_ssf_ar(name, ar, fixedar, variance, fixedvariance, nlags, zeroinit)
 

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
    <td class="tg-0pky">ar</td>
    <td class="tg-0pky"> <i>double array </i> of AR coefficients, i.e. $\varphi_1$, $\ldots$, $\varphi_p$ </td>
    <td class="tg-0pky"> </td>
    <td class="tg-0pky">The autoregressive order is determined by the size of the array, e.g. of your write c(1.5, -0.6), you are implicitely fixing the order of your AR(p) model to $p=2$ with $\varphi_{1}=1.5$ and  $\varphi_{2}=-0.6$ </td>
  </tr>
  <tr>
    <td class="tg-0pky">fixedar</td>
    <td class="tg-0pky"> <i>logical</i>  that triggers estimation of the AR coefficients  $\varphi_1$, $\ldots$, $\varphi_p$ (<b>FALSE</b>) or  
	fixes them (<b>TRUE</b>) to a pre-specified  values above, set by the parameter ar  </td>
    <td class="tg-0pky"><b>FALSE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
  <tr>
    <td class="tg-0pky">variance</td>
    <td class="tg-0pky"> <i>double </i> for the value of $\sigma^2_{ar}$ </td>
    <td class="tg-0pky">1</td>
    <td class="tg-0pky">variance of the innovation is actually  $\sigma^2\sigma^2_{ar}$</td>
  </tr>
  <tr>
    <td class="tg-0pky">fixedvariance</td>
    <td class="tg-0pky"> <i>logical</i>  that triggers estimation of $\sigma^2_{ar}$ (<b>FALSE</b>) or  
	fixes it (<b>TRUE</b>) to a pre-specified  value set by the parameter variance </td>
    <td class="tg-0pky"><b>FALSE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
 <tr>
    <td class="tg-0pky">nlags</td>
    <td class="tg-0pky"> <i>integer </i> specifying how many lags of the state variable are needed</td>
    <td class="tg-0pky">0 </td>
    <td class="tg-0pky">Note that the number of lags desired are independent from the order of the AR model. You may have an order $p=2$ and and do not need to specify any of its lags in the measurement equation (in this case, the default nlags=0 would be sufficient) </td>
  </tr>
  <tr>
    <td class="tg-0pky">zeroinit</td>
    <td class="tg-0pky">  <i>logical </i>  determining the initial condition for the state variable, which is equal to zero if  <b>TRUE</b> is chosen. The default  <b>FALSE</b>  triggers the an initialization based on the unconditional mean and variance of the AR(p) process   </td>
    <td class="tg-0pky"> <b>FALSE</b></td>
    <td class="tg-0pky"> </td>
  </tr>
</table></div>
<script charset="utf-8">var TGSort=window.TGSort||function(n){"use strict";function r(n){return n.length}function t(n,t){if(n)for(var e=0,a=r(n);a>e;++e)t(n[e],e)}function e(n){return n.split("").reverse().join("")}function a(n){var e=n[0];return t(n,function(n){for(;!n.startsWith(e);)e=e.substring(0,r(e)-1)}),r(e)}function o(n,r){return-1!=n.map(r).indexOf(!0)}function u(n,r){return function(t){var e="";return t.replace(n,function(n,t,a){return e=t.replace(r,"")+"."+(a||"").substring(1)}),l(e)}}function i(n){var t=l(n);return!isNaN(t)&&r(""+t)+1>=r(n)?t:NaN}function s(n){var e=[];return t([i,m,g],function(t){var a;r(e)||o(a=n.map(t),isNaN)||(e=a)}),e}function c(n){var t=s(n);if(!r(t)){var o=a(n),u=a(n.map(e)),i=n.map(function(n){return n.substring(o,r(n)-u)});t=s(i)}return t}function f(n){var r=n.map(Date.parse);return o(r,isNaN)?[]:r}function v(n,r){r(n),t(n.childNodes,function(n){v(n,r)})}function d(n){var r,t=[],e=[];return v(n,function(n){var a=n.nodeName;"TR"==a?(r=[],t.push(r),e.push(n)):("TD"==a||"TH"==a)&&r.push(n)}),[t,e]}function p(n){if("TABLE"==n.nodeName){for(var e=d(n),a=e[0],o=e[1],u=r(a),i=u>1&&r(a[0])<r(a[1])?1:0,s=i+1,v=a[i],p=r(v),l=[],m=[],g=[],h=s;u>h;++h){for(var N=0;p>N;++N){r(m)<p&&m.push([]);var T=a[h][N],C=T.textContent||T.innerText||"";m[N].push(C.trim())}g.push(h-s)}var L="tg-sort-asc",E="tg-sort-desc",b=function(){for(var n=0;p>n;++n){var r=v[n].classList;r.remove(L),r.remove(E),l[n]=0}};t(v,function(n,t){l[t]=0;var e=n.classList;e.add("tg-sort-header"),n.addEventListener("click",function(){function n(n,r){var t=d[n],e=d[r];return t>e?a:e>t?-a:a*(n-r)}var a=l[t];b(),a=1==a?-1:+!a,a&&e.add(a>0?L:E),l[t]=a;var i=m[t],v=function(n,r){return a*i[n].localeCompare(i[r])||a*(n-r)},d=c(i);(r(d)||r(d=f(i)))&&(v=n);var p=g.slice();p.sort(v);for(var h=null,N=s;u>N;++N)h=o[N].parentNode,h.removeChild(o[N]);for(var N=s;u>N;++N)h.appendChild(o[s+p[N-s]])})})}}var l=parseFloat,m=u(/^(?:\s*)([+-]?(?:\d+)(?:,\d{3})*)(\.\d*)?$/g,/,/g),g=u(/^(?:\s*)([+-]?(?:\d+)(?:\.\d{3})*)(,\d*)?$/g,/\./g);n.addEventListener("DOMContentLoaded",function(){for(var t=n.getElementsByClassName("tg"),e=0;e<r(t);++e)try{p(t[e])}catch(a){}})}(document);</script>

 
#### Examples of use 
```R
jd3_ssf_ar("cycle", c(1.5,-0.4), fixedar=FALSE, variance=1, fixedvariance=TRUE, nlags=4, zeroinit=FALSE) // 
jd3_ssf_ar("cycle", c(1.5,-0.4), fixedar=FALSE, variance=1, fixedvariance=FALSE, nlags=0, zeroinit=FALSE) // default
jd3_ssf_ar("cycle", c(1.5,-0.4)) 

```


