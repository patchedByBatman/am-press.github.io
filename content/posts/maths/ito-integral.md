---
author: "Pantelis Sopasakis"
title: Itô's Integrals
date: 2022-08-23
description: Table of Itô stochastic integrals
summary: Table of Itô stochastic integrals and their variances
math: true
series: ["Mathematix"]
tags: ["Stochastic calculus"]
showtoc: false
---

<style>
table {
  border-collapse: collapse;
  width: 100%;
  table-layout: fixed;
}

td, th {

  text-align: left;
  padding: 8px;
  width: 33%
}


</style>

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}

<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}


In this post we will define the following results:

{{< math.inline >}}
<div>
<table>
  <tr>
    <th>Stochastic integral</th>
    <th>Result </th>
    <th>Variance</th>
  </tr>
  <tr>
    <td>\(\int_0^t \mathrm{d}B_s\)</td>
    <td>\(B_t\)</td>
    <td>\(t\)</td>
  </tr>
  <tr>
    <td>\(\int_0^t s \mathrm{d}B_s\)</td>
    <td>\(tB_t - \mathrm{ibm}(t, \omega)\)</td>
    <td>\(\tfrac{1}{3}t^3\)</td>
  </tr>
  <tr>
    <td>\(\int_0^t B_s \mathrm{d}B_s\)</td>
    <td>\(\tfrac{1}{2}B_t^2 - \tfrac{1}{2}t\)</td>
    <td>\(\tfrac{1}{2}t^2\)</td>
  </tr>
  <tr>
    <td>\(\int_0^t B_s^2 \mathrm{d}B_s\)</td>
    <td>\(\tfrac{1}{3}B_t^3 - \mathrm{ibm}_t\)</td>
    <td>\(t^3\)</td>
  </tr>
  <tr>
    <td>\(\int_0^t B_s^k\mathrm{d}B_s\)</td>
    <td>\(\tfrac{1}{k+1}B_t^{k+1} - k \int_0^t B_s^{k-1} \mathrm{d}s\)</td>
    <td></td>
  </tr>
  <tr>
    <td>\(\int_0^t \exp\left(B_s - \tfrac{s}{2}\right)\mathrm{d}B_s\)</td>
    <td>\(\exp(B_t - \tfrac{t}{2}) - 1\)</td>
    <td>\(e^t - 1\)</td>
  </tr>
</table>
</div>
{{</ math.inline >}}



## Introduction
{{< math.inline >}}
<p>Recall that the integrated Brownian motion (IBM), which is defined as</p>

<p id="ibm">$$\begin{aligned} \mathrm{ibm}(t, \omega) = \int_0^t B_s \mathrm{d}s, \end{aligned}$$</p>

<p>is a random variable which follows the normal distribution with zero mean and variance \(t^3/3\). We will use the notation \(\mathrm{ibm}_t\) hereafter.</p>

<p>This <a href="https://quant.stackexchange.com/questions/29504/integral-of-brownian-motion-w-r-t-time">MSE thread</a> is worth reading.</p>

<p>Hereafter, we will give a few examples of stochastic integrals of the Itô type which are given by</p> 

<p>$$I(t, \omega) {}={} \int_0^t f(t, \omega) \mathrm{d}B_t,$$</p>

<p>where \(f\) is an Itô-integrable function. We shall also use the shorthand notation \(I_t(\omega) = I(t, \omega)\).</p>
{{</ math.inline >}}

<p>Let us recall some important results from stochastic calculus:</p>

<div style="border-style:solid;border-width:1.5px;padding-left:10px;padding-top:15px" id="thm1">
<p><strong>Theorem 1 (Itô isometry).</strong> Let \(f:(t_1, t_2)\times \Omega \to {\rm I\!R}\) be an Itô-itegral function on \((t_1, t_2)\). Then</p>
<p>$${\rm I\!E}\left[\left(\int_{t_1}^{t_2}f(t, \omega){\rm d}B_t\right)^2\right] {}={} {\rm I\!E}\left[\int_{t_1}^{t_2}f^2(t, \omega){\rm d}t\right].$$</p>
</div>
<br/>

<div style="border-style:solid;border-width:1.5px;padding-left:10px;padding-top:15px" id="thm2">
<p><strong>Theorem 2 (Itô's lemma).</strong> Let \(X_t\) be an Itô process with</p>
<p>$${\rm d}X_t = u{\rm d}t + v{\rm d}B_t.$$</p>
<p>Let \(g:[0, \infty) \times {\rm I\!R} \to {\rm I\!R}\) be twice continuously differentiable on \([0, \infty) \times {\rm I\!R} \). Then, the process \(Y_t = g(t, X_t)\) is an Itô process with</p>
<p>$${\rm d}Y_t = \frac{\partial g}{\partial t}(t, X_t){\rm d}t +  \frac{\partial g}{\partial x}(t, X_t){\rm d}X_t + \tfrac{1}{2} \frac{\partial^2 g}{\partial x^2}(t, X_t)({\rm d}X_t)^2,$$</p>
<p>where \(({\rm d}X_t)^2 = ({\rm d}X_t) \cdot ({\rm d}X_t)\) is computed according to the rules</p>
<p>$${\rm d}t \cdot {\rm d}t = {\rm d}t\cdot  {\rm d}B_t = {\rm d}B_t \cdot  {\rm d}t = 0, \ {\rm d}B_t \cdot {\rm d}B_t = {\rm d}t.$$</p>
</div>
<br/>




## Stochastic Integrals

### Stochastic integral No 1
{{< math.inline >}}
<p>Consider the stochastic integral</p>

<p>$$\begin{aligned}I_1(t, \omega) = \int_0^t s \mathrm{d}B_s = t B_t - \mathrm{ibm}_t, \end{aligned}$$</p>

<p>where \(\mathrm{ibm}_t\) denotes the <a href="#ibm">integrated Brownian motion</a> given above. </p>

<p>The expected value of \(I_1\) is \({\rm I\!E}[I_1] = {\rm I\!E}[\int_0^t s \mathrm{d}\mathrm{B}_s] = 0\) and its variance is given by</p>

<p>$$\begin{aligned} \mathrm{Var}[I_1] = {\rm I\!E}[I_1^2] {}={}& {\rm I\!E}\left[\left(\int_0^t s \mathrm{d}B_s\right)^2\right]\\{}={}& {\rm I\!E}\left[\int_0^t s^2 \mathrm{d}s\right] {}={}\frac{t^3}{3}.\end{aligned}$$</p>

<p>We have used the <a href="#thm1">Itô isometry</a>.</p> 

<p>Note that the above computation is easier than trying to do</p>

<p>$${\rm I\!E}[I_1^2] {}={} {\rm I\!E}[(tB_t - \mathrm{ibm}_t)^2].$$</p>
{{</ math.inline >}}

---

### Stochastic integral No 2

{{< math.inline >}}
<p>Define</p>

<p>$$\begin{aligned}I_2 = \int_0^t B_s \mathrm{d}B_s\end{aligned}$$</p>

<p>Using <a href="#thm2">Itô's lemma</a>, we obtain</p>

<p>$$\begin{aligned}I_2 = \tfrac{1}{2}B_t^2 - \tfrac{1}{2}t\end{aligned}$$</p>

<p>and \({\rm I\!E}[I_2] = 0\), while the variance is</p>

<p>$$\begin{aligned} \mathrm{Var}[I_2] = {\rm I\!E}[I_2^2] {}={}& {\rm I\!E}[(\tfrac{1}{2}B_t^2 - \tfrac{1}{2}t)^2] \\ {}={}& \tfrac{1}{4}{\rm I\!E}[(B_t^2 - t)^2] \\ {}={}& \tfrac{1}{4}{\rm I\!E}[B_t^4 + t^2 - 2tB_t^2]\end{aligned}$$</p>

<p>and using the fact that \({\rm I\!E}[B_t^2] = t\) and \({\rm I\!E}[B_t^4] = 3t^2\), it is \({\rm I\!E}[I_2^2] = \tfrac{1}{2}t^2\).</p>
{{</ math.inline >}}

---

### Stochastic integral No 3

{{< math.inline >}}
<p>Define the following stochastic integral which involves the squared Brownian motion</p>

<p>$$\begin{aligned}I_3 = \int_0^t B_s^2 \mathrm{d}B_s\end{aligned}$$</p>

<p>This can be computed by applying <a href="#thm2">Itô's formula</a> to \(f(t, x) = \tfrac{1}{3}x^3\) and gives</p>

<p>$$\begin{aligned}I_3 = \tfrac{1}{3}B_t^3 -\mathrm{ibm}_t,\end{aligned}$$</p>

<p>where \(\mathrm{ibm}_t\) is the <a href="#ibm">integrated Brownian motion</a>.</p>

<p>The expectation of \(I_3\) is clearly \({\rm I\!E}[\int_0^t B_s^2 \mathrm{d}B_s] = 0\) and its variance is </p>

<p>$$\begin{aligned}\mathrm{Var}[I_3] = {\rm I\!E}[I_3^2] {}={}& {\rm I\!E}[(\tfrac{1}{3}B_t^3 -I_t)^2]\\ {}={}& \tfrac{1}{9}{\rm I\!E}[B_t^6] + {\rm I\!E}[I_t^2] - \tfrac{2}{3} {\rm I\!E}[B_t^3 I_t],\end{aligned}$$</p>

<p>and \({\rm I\!E}[B_t^6] = 15 t^3\), \({\rm I\!E}[I_t^2] = t^3/3\) and </p>

<p>$$\begin{aligned}{\rm I\!E}[B_t^3 I_t] = {\rm I\!E} \left[ B_t^3 \int_0^t B_s \mathrm{d}s\right] = {\rm I\!E} \left[ \int_0^t B_t^3 B_s \mathrm{d}s\right] = \int_0^t {\rm I\!E}[B_t^3 B_s]\mathrm{d}s,\end{aligned}$$</p>

<p>Now using <a href="https://en.wikipedia.org/wiki/Isserlis%27_theorem">Isserlis's Theorem</a> and the fact that \(0 \leq s \leq t\) and \({\rm I\!E}[B_t B_s] = s\) and \({\rm I\!E}[B_t^2] = t\) we have \({\rm I\!E}[B_t^3 B_s] = 3ts\), therefore </p>

<p>$${\rm I\!E}[B_t^3 I_t] =  \int_0^t {\rm I\!E}[B_t^3 B_s]\mathrm{d}s =  \int_0^t 3ts \mathrm{d}s = \tfrac{3}{2}t^3.$$</p>

<p>Overall,</p>

<p>$$\begin{aligned} \mathrm{Var}[I_3] = t^3.\end{aligned}$$</p>

<p>We can generalise the above result using the formula</p>

<p>$$\begin{aligned}\int_0^t B_s^k \mathrm{d}B_s = \tfrac{1}{k+1}B_t^{k+1} - k \int_0^t B_s^{k-1}\mathrm{d}s\end{aligned}$$</p>

<p>and proceeding as above.</p>
{{</ math.inline >}}

---


### Stochastic integral No 4

{{< math.inline >}}
Consider the stochastic integral

$$\begin{aligned}I_4 = \int_0^t \exp (B_s - \tfrac{1}{2}s) \mathrm{d}B_s\end{aligned}$$

Using <a href="#thm2">Itô's formula</a>, we may show that this is equal to

$$\begin{aligned}I_4 = \exp (B_t - \tfrac{1}{2}t) - 1 = e^{B_t}e^{-\tfrac{1}{2}t} - 1.\end{aligned}$$

Since \(B_t\) follows the normal distribution with zero mean and variance \(t\), the random variable \(e^{B_t}\) follows the log-normal distribution.

<p>The expectation of \(I_4\) is \({\rm I\!E}[\int_0^t \exp (B_s - \tfrac{1}{2}s) \mathrm{d}B_s] = 0\) and its variance is </p>

<p>$$\begin{aligned}\mathrm{Var}[I_4] {}={} {\rm I\!E}[I_4^2] {}={}& {\rm I\!E}[(\exp (B_t - \tfrac{1}{2}t) - 1)^2]\\ {}={}& {\rm I\!E}[\exp (2B_t - t) - 2\exp (B_t - \tfrac{1}{2}t) + 1]\end{aligned}$$</p>

<p>where \({\rm I\!E}[\exp (2B_t - t)] = e^{-t}{\rm I\!E}[\exp (2B_t)]\). Since \(2B_t \sim \mathcal{N}(0, 4t)\), \({\rm I\!E}[e^{2B_t}] = e^{\frac{4t}{2}} = e^{2t}\), so \({\rm I\!E}[\exp (2B_t - t)] = e^t\).</p>

<p>Similarly, \({\rm I\!E}[2\exp (B_t - \tfrac{1}{2}t)] = 2e^{-\frac{t}{2}}{\rm I\!E}[e^{B_t}] = 2\). </p>

<p>Overall,</p>

<p>$$\begin{aligned}\mathrm{Var}[I_4] {}={} e^t - 1.\end{aligned}$$</p>
{{</ math.inline >}}
