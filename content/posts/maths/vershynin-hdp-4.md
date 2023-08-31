---
author: "Pantelis Sopasakis"
title:  "Reading Vershynin's HDP IV: Concentration of Euclidean norm"
date: 2023-08-31
description: "Concentration of Euclidean norm"
summary: "Concentration of Euclidean norm"
math: true
series: ["Mathematix"]
tags: ["Probability", "Vershynin"]
collapsible: true
draft: true
---

<p>The objective is to show that the Euclidean norm of a random vector concentrates tightly around its mean. Assuming $X_i$ are independent, zero-mean, unit-variance random variables, then</p>
<p>$${\rm I\!E}[\|X\|^2] = n,$$</p>
<p>so we would expect $\|X\|$ to concentrate around $\sqrt{n}$ with high probability. <b>But</b> given that ${\rm I\!E}[\|X\|^2] = n$ it does not follow that ${\rm I\!E}[\|X\|] = \sqrt{n}$ - and in fact it may not be. Instead, we will show that</p>
<p>$$\|\|X\|_2 - \sqrt{n}\|_{\psi_2} \lesssim (\max_i \|X_i\|_{\psi_2} )^2.$$</p>

<!-- Prop 1 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="prop:1">
    <p><strong>Proposition 1 (Concentraion of Euclidean norm).</strong> Let $X_1, \ldots, X_N$ be independent, zero-mean, subgaussian with ${\rm I\!E}[X_i^2] = 1$. Then,</p>
    <p>$$\|\|X\|_2 - \sqrt{n}\|_{\psi_2} \leq C (\max_i \|X_i\|_{\psi_2} )^2,$$</p>
    <p>where $C$ is an absolute constant</p>
</div>

<p><em>Proof.</em> The proof requires some results from the previous sections; in particular,</p>
<ol>
    <li>the fact that if $X$ is subgaussian then $X^2$ is subexponential and</li>
    <li>in particular $\|X\|_{\psi_2}^2 = \|X^2\|_{\psi_1}$</li>
    <li>the centering property $\|X - {\rm I\!E}[X]\|_{\psi_2} \lesssim \|X\|_{\psi_2}$</li>
    <li><a href="#../vershynin-hdp-3#bernsteins-inequality" target="_blank">Bernstein's inequality</a>, which is a concentration inequality for zero-mean subexponentials.</li>
</ol>
<p>So, assume $K = \max_i \|X_i\|_{\psi_2} \geq 1$. Since $X_i$ is subgaussian, $X_i^2 - 1$ is subexponential and</p>
<p>$$\begin{aligned}
\|X_i^2 - 1\|_{\psi_1} 
{}\lesssim{}&
\|X_i^2\|_{\psi_1}
\\
{}={}& \|X_i\|^2_{\psi_2}
\\
{}\lesssim{}&
K^2.
\end{aligned}$$</p>
<p>By <a href="#../vershynin-hdp-3#bernsteins-inequality" target="_blank">Bernstein's inequality</a> for all $u\geq 0$</p>
<p>$$\begin{aligned}
{\rm P}\left[\left|\frac{1}{n}\|X\|_2^2 - 1\right| \geq u \right] \leq 2 \exp\left[ - \frac{cn}{K^4}\min(u, u^2)\right]\tag{*}
\end{aligned}$$</p>
<p>This inequality is a concentation result for $\|X\|^2$ from which we will derive a concentration result for $\|X\|$. We will use the fact that</p>
<p>$$\begin{aligned}|z-1|\geq \delta \implies |z^2-1| \geq \max(\delta, \delta^2).\end{aligned}$$</p>
<p>As a result,</p>
<p>$$\begin{aligned}
{\rm P}\left[\left| \frac{1}{\sqrt{n}}\|X\|_2 - 1 \right| \geq \delta \right]
\leq{}& 
{\rm P}\left[ \left|\frac{1}{n}\|X\|_2^2 - 1\right| \geq \max(\delta, \delta^2)\right]
\\
\leq{}& 2 \exp\left(-\frac{cn}{K^4}\delta^2 \right).
\end{aligned}$$</p>
<p>Let us choose $t = \delta\sqrt{n}$. Then,</p>
<p>$$\begin{aligned}
{\rm P}\left[\left| \|X\|_2 - \sqrt{n}\right| \geq t \right]
\leq 
2 \exp\left(-\frac{ct^2}{K^4}\right),\tag{\#}
\end{aligned}$$</p>
<p>for all $t\geq 0$, which proves the assertion. $\Box$</p>



<!-- Prop 1 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="prop:2">
    <p><strong>Proposition 2 (Expectation and standard deviation of the norm).</strong> Under the assumptions of Proposition 1, let $S = \|X\|_2^2$. Then</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[S] {}={}& n,
    \\
    {\rm std}[S]{}={}& O(\sqrt{n}).
    \end{aligned}$$</p>    
</div>

<p><em>Proof.</em> We have already seen that ***</p>

<!-- <p>$$\begin{aligned}\end{aligned}$$</p> -->