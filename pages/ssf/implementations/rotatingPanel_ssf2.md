---
layout: left-menu
title: Autocorrelation
tagline: technical documentation for JDemetra+ using GitHub Pages
description: State space of a rotating panels error structure
category: "Rotating Panel"
order: 2012
---

# {{page.description}}

#### [Error Specification in a Rotating Panel](../implementations/rotatingPanel_ssf0.html)

The error term $$e^{(i)}_{t}$$ has a particular structure
that is given by the rotating survey design:

$$
\begin{eqnarray}
e^{(i)}_{t} = \underbrace{ b^{(i)}_{t}}_{ bias} + \underbrace{ \color{red}\varepsilon^{(i)}_{t}}_{\color{red} autocorrelation}
\end{eqnarray}
$$

Here, we describe the $$\color{red} \text{autocorrelated}$$ part of the wave specific error component

The autocorrelation accross waves is given by the fact that a proportion of the respondents that do not update their responses on the basis of new information, so 
in principle it is possible that first wave individuals' responses persist until the last wave $$W$$. However, it is typically assumed that 
the error in the first response is correlated to the error in the second response (following survey period), but uncorrelated to the error 
in the third response (two survey periods ahead). 

$$ \varepsilon^{(i)}_{t} = \phi^{(i)}_{1} \varepsilon^{(i-1)}_{t-nlags} + \epsilon^{(i)}_{t}$$, 

where $$\epsilon^{(i)}_{t} \sim N\left(0, (1-(\phi^{(i)}_{1})^{2})(k^{(i)})^{2}  \right) $$. Note 
that $\phi^{(i)}_{1}=0$ for  $i=1$. 

The component $(k^{(i)})^{2}$ that appears in the design-based variances will appear in the measurement 
equation by defining $$ \tilde{\varepsilon}^{(i)}_{t}= k^{(i)} \varepsilon^{(i)}_{t} $$



A representation of all possible correlation patterns in a panel defined by $ W=5 $ and $ nlags=3 $ follows in this table:

 


##### State vectors: 
Assuming that individuals in each wave do not fully update their beliefs in two consecutive survey periods, the transition equation 
will need to capture the correlation of $$\tilde{\varepsilon}^{(i)}_{t}$$  and $$\tilde{\varepsilon}^{(i-1)}_{t-nlags}$$. The required state 
vector follows
 
$$ \alpha_t= \begin{pmatrix} \tilde{\varepsilon}^{(1)}_{t}  \\ \tilde{\varepsilon}^{(2)}_{t} \\ \vdots \\ \tilde{\varepsilon}^{(W)}_{t} \\ \hline \tilde{\varepsilon}^{(1)}_{t-1}  \\ \tilde{\varepsilon}^{(2)}_{t-1} \\ \vdots \\ \tilde{\varepsilon}^{(W)}_{t-1}
\\ \hline \vdots \\ \hline \tilde{\varepsilon}^{(1)}_{t-nlags+1} \\ \tilde{\varepsilon}^{(2)}_{t-nlags+1}   \\ \vdots \\ \tilde{\varepsilon}^{(W)}_{t-nlags+1}  \end{pmatrix}$$  

Note, however, that the pattern of correlations may be more complex. In the limit, when $$\tilde{\varepsilon}^{(i)}_{t}$$  may be correlated
with $$\tilde{\varepsilon}^{(i-W+1)}_{t-nlags\times(W-1)}$$, the resulting state vector will contain $$\alpha_t, \cdots, \alpha_{t-nlags}, \cdots, \alpha_{t-nlags\times(W-1) }$$. 


##### Dynamics

The transition matrix has the following block structure

$$ T_t = \begin{pmatrix} 0 & 0 & \cdots &  \Phi \\  \mathrm{I} & 0 & \cdots &  0\\ \vdots & \ddots & \cdots & \vdots \\ 0 & 0 & \mathrm{I} & 0 \end{pmatrix}$$

where $$0$$ and $$\mathrm{I}$$ represent zero and identity matrices, respectively. The dots  $$\cdots$$   and   $$\vdots$$    represent 
zero matrices of dimension $$W$$ and the dots   $$\ddots$$   stand for an identity matrix of dimension $$ d =(nlags - 3)\times W $$.  

The correlation patterns appear in the block $$\Phi$$, which is a square matrix of dimension $$W $$, defined as follows:


$$ \Phi = \begin{pmatrix}  0 & 0 & \cdots & 0  \\ \phi^{(2)}_{1} &  0 & \cdots & 0 \\ \vdots &  \ddots & \cdots & \vdots \\ 0 &  0 &  \phi^{(W)}_{1} & 0 \end{pmatrix} $$,


where   $$ \cdots $$   and   $$ \vdots $$    represent zeroes.


$$ S_t = \begin{pmatrix} S & 0 & \cdots & 0 \\  0 & 0 & \cdots &  0\\ \vdots & \ddots & \cdots & \vdots \\ 0 & 0 & 0 & 0 \end{pmatrix} $$


where  


$$ S = \begin{pmatrix}  1 & 0 & \cdots & 0  \\ 0 &  \sqrt{1- (\phi^{(2)}_{1})^2}  & \cdots & 0 \\ \vdots &  \ddots & \cdots & \vdots \\ 0 &  0 &  0 & \sqrt{1-(\phi^{(W)}_{1})^2}  \end{pmatrix} $$,

$$ V_t = S S' $$


Note it is also possible to assume individuals update ineficiently for more than two consecutive survey periods. All possible correlation 
patterns can be summarized in a compact manner as follows:

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

#### Initialization 

$$ a_0 =  \mathrm{0_{W \times 1}}$$

$$ P_*=    \Omega $$

where $$ \Omega $$ is the unconditional variance of the state vector, which is 
calculated by iterating the Kalman filter $W\times nlags $ times. Note that every $W\times nlags$  periods, the
individuals participating in the panel are completely renewed, so the temporal dependency disappears.

#### Measurement

 
$$Z_t = \begin{pmatrix}  k^{1}_{t} & 0  & \cdots & 0 &  0 & \cdots   \\ 0 &  k^{2}_{t} & \cdots & 0 &  0 & \cdots\\ \vdots &  \vdots & \ddots & \vdots & \vdots & \cdots  \\ 0 &  0 & \cdots  &   k^{W}_{t} &   0 & \cdots  \end{pmatrix} $$,

where  horizontal $$ \cdots$$  and vertical $$ \vdots$$  represent zeroes. 

$$ H_t = 0 $$

 
 

#### Implementation

[identify]
ARMA models are implemented in the class `demetra.arima.ssf.SsfArima`

