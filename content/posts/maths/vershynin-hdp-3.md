---
author: "Pantelis Sopasakis"
title:  "Reading Vershynin's HDP III: Subexponential random variables"
date: 2023-08-30
description: "Subexponential RVs"
summary: "We study the class of sub-exponential random variables"
math: true
series: ["Mathematix"]
tags: ["Probability", "Vershynin"]
collapsible: true
draft: true
---

> See first: <a href="../vershynin-hdp-2">Reading Vershynin's HDP II: Subgaussianity</a>

<p>Subexponential random variables are defined very similarly to subgaussian ones. Roughly speaking, a continuous random variable is subexponential if the tails of its pdf go down exponentially fast. Subexponential random variables have <em>thicker</em> tails compared to subgaussian ones. All subgaussian random variables are subexponential, but the converse is not true.</p>
<p>Let us start with a characterisation of subexponential RVs, which is very similar to our <a href="../vershyning-hdp-2#subGaussianityProp" target="_blank">previous</a> characterisation of subgaussianity.</p>

<!-- PROPOSITION 1: Characterisation of subGaussianity -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="subExpCharacterisation">
    <p><strong>Proposition 1 (Subexponential properties).</strong> Let $X$ be a random variable. Then the following properties are equivalent</p>
    <ol>
        <li id="subExpProp:1">The tails of $X$ satisfy ${\rm P}[|X| \geq t] \leq 2 \exp(-t/K_1)$, for all $t\geq 0$, for some constant $K_1 > 0$</li>
        <li id="subExpProp:2">The moments of $X$ satisfy $\|X\|_{L^p} \leq K_2 p$, for all $p\geq 1$, for some constant $K_2$</li>
        <li id="subExpProp:3">The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $|X|$ satisfies ${\rm I\!E}[\exp(\lambda |X|)] \leq \exp(K_3 \lambda)$, for all $\lambda$ such that $0\leq\lambda\leq 1/K_3$</li>
        <li id="subExpProp:4">The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $|X|$ is bounded at some point, namely, ${\rm I\!E}[\exp(|X|/K_4)] \leq 2$</li>
    </ol>
    <p>Moreover, if ${\rm I\!E}[X] = 0$ the above properties are also equivalent to</p>
    <ol start=5>
        <li id="subExpProp:5">The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $X$ satisfies ${\rm I\!E}[\lambda X] \leq \exp(K_5^2 \lambda^2)$ for all $|\lambda| \leq 1/K_5$</li>
    </ol>
    <p>Lastly, there is a constant $C$ so that for any two constants $K_i$, $K_j$, $i,j=1,\ldots, 5$, we have $K_j \leq C K_i$.</p>
</div>

<p><em>Proof (Exercise 2.7.2 in [<a href="#cite:ver19" title="Vershynin, HDP">1</a>]).</em> I'll do this later.</p>


<p>As we mentioned above, a random variable can be subexponential, but not subgaussian. Let us give an example.</p>

<p><b>Example 1 (Subexponential, not subgaussian).</b> Let $X \sim \mathcal{N}(0, 1)$ and let $Y=X^2 - 1$ for which ${\rm I\!E}[Y] = 0$. To verify that this is subexponential we use <a href="#subExpProp:5">Theorem 1, Property 5</a>. We have </p>
<p>$$\begin{aligned}{\rm I\!E}[\exp(\lambda Y)] 
{}={} &
\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}e^{\lambda(x^2 - 1)}e^{x^2/2}{\rm d}x
\\
{}={}&
\ldots
\\
{}={}&
\frac{e^{-\lambda}}{\sqrt{1-2\lambda}}.
\end{aligned}$$</p>
<p>We see that the mgf of $Y$ is defined for $|\lambda| < \frac{1}{2}$, so $Y$ is not subgaussian. For $|\lambda| > \frac{1}{4}$ we have</p>
<p>$$\begin{aligned}
{\rm I\!E}[\exp(\lambda Y)] \leq e^{2\lambda^2},
\end{aligned}$$</p>
<p>so, $Y$ is subexponential. $\heartsuit$</p>


### Connection to subgaussianity

<p>Let us first define the subexponential norm or $\psi_1$-norm. It is</p>
<p>$$\begin{aligned}
\|X\|_{\psi_1} {}={} \inf \{t > 0 {}:{} {\rm I\!E}[\exp(|X|/t)] \leq 2\}.
\end{aligned}$$</p>
<p>The following result states that $X$ is subgaussian if and only if $X^2$ is sub-exponential.</p>


<!-- Lemma 2 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="subExp-vs-subGauss">
    <p><strong>Lemma 2 (Relationship between subexpoential and subgaussian RV).</strong> Let $X$ be subgaussian. Then $X^2$ is subexponential and</p>
    <p>$$\|X^2\|_{\psi_1} {}={} \|X\|_{\psi_2}^2.$$</p>
</div>

<p><em>Proof.</em> We have</p>
<p>$$\begin{aligned}
\|X^2\|_{\psi_1}
{}={}&
\inf \{t > 0 {}:{} {\rm I\!E}[\exp(X^2/t)] \leq 2\}
\\
{}={}&
\inf \{t = u^2 > 0 {}:{} {\rm I\!E}[\exp(X^2/u^2)] \leq 2\}
{}={} \|X\|_{\psi_2}^2.\end{aligned}$$</p>
<p>This completes the proof. $\Box$</p>

<p>Next we will show that the product of two subgaussians is a subexponential.</p>

<!-- Lemma 3 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="productOfsubGauss">
    <p><strong>Lemma 3 (Product of subgaussian RV).</strong> Let $X, Y$ be subgaussian. Then $XY$ is subexponential and</p>
    <p>$$\|X Y\|_{\psi_1} {}\leq{} \|X\|_{\psi_2}\|Y\|_{\psi_2}.$$</p>
</div>

<p><em>Proof.</em> See [<a href="#cite:ver19" title="Vershynin, HDP">1</a>, p. 31]</p>

### Bernstein's inequality

<p>Bernstein's inequality is for subexponential random variables what <a href="../vershynin-hdp-2#hoeffding-subgaussian">Hoeffding's inequality</a> is for subgaussian random variables. </p>
<!-- <p></p> -->
<!-- <p>$$\begin{aligned}\end{aligned}$$</p> -->


## References 

<ol>
  <li id="cite:ver19">R. Vershynin, High Dimensional Probabiltiy: an introduction with applications in data science, Cambridge University Press, 2019</li>  
</ol>
