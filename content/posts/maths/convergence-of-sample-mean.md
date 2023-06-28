---
author: "Pantelis Sopasakis"
title:  "Reading Vershynin's HDP - Chapters 1 and 2"
date: 2023-06-25
description: "A result on the convergence of sample mean"
summary: "<p>We show that the sample mean converges to the true mean at a rate of 1 / sqrt(k)</p>"
math: true
series: ["Mathematix"]
tags: ["Probability"]
collapsible: true
draft: true
---

<p>These are my notes on Ronan Vershynin's "High dimensional probability", Chapters 1 and 2 [<a href="#cite:ver19" title="Vershynin, HDP">1</a>] and some solved exercises.</p>

## Preliminaries

<!-- EXERCISE 1.1.3 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex113">
<p><strong>Exercise 1.1.3.</strong> Let \(X_1, X_2, \ldots\) be a sequence of iid random variables with mean \(\mu\) and a finite variance. Show that</p>
<p>$${\rm I\!E}\left|\frac{1}{N}\sum_{i=1}^{N}X_i\right| {}={} O\left(\frac{1}{\sqrt{N}}\right).$$</p>
</div>

<p><em>Solution.</em> Without loss of generality we shall assume that $\mu=0$.</p> <p>Firstly, we will get rid of that annoying absolute value as follows: Let us define</p>
<p>$$\bar{X}_N = \frac{1}{N}\sum_{i=1}^{N}X_i.$$</p>
<p>Then,</p>
<p>$${\rm I\!E}|\bar{X}_N| = {\rm I\!E} \sqrt{\bar{X}_N^2} \leq \sqrt{{\rm I\!E}[\bar{X}_N^2]},$$</p>
<p>where we used <a href="https://en.wikipedia.org/wiki/Jensen%27s_inequality" target="_blank">Jensen's inequality</a> (using the fact that the square root is a concave function).</p>

<p>Now for ${\rm I\!E}[\bar{X}_N^2]$ we have</p>
<p>$${\rm I\!E}[\bar{X}_N^2] = \frac{1}{N^2} {\rm I\!E}\left(\sum_{i=1}^{N}X_i\right)^2 = \frac{1}{N^2} {\rm I\!E}\left[\sum_{i=1}^{N}X_i^2\right] =\frac{1}{N^2} N\sigma^2 = \frac{\sigma^2}{N}.$$</p>

<p>As a result</p>
<p>$${\rm I\!E}\left|\frac{1}{N}\sum_{i=1}^{N}X_i\right| {}\leq{} \sqrt{{\rm I\!E}[\bar{X}_N^2]} = \frac{\sigma}{\sqrt{N}}.$$</p>

<p>This completes the proof. $\Box$</p>


<p>Let us juxtapose the above result to the classical Lindeberg-Lévy central limit theorem (CLT):</p>

<!-- LL-CLT -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ll-clt">
<p><strong>Theorem 1 (Lindeberg-Lévy CLT).</strong> Let \(X_1, X_2, \ldots\) be a sequence of iid random variables with mean \(\mu\) and a finite variance \(\sigma^2\). Define $S_N = \sum_{i=1}^{N}X_i$ and</p>
<p>$$Z_N = \frac{S_N - {\rm I\!E[S_N]}}{\sqrt{{\rm Var}[S_N]}} = \frac{1}{\sigma\sqrt{N}}\sum_{i=1}^{N}(X_i - \mu).$$</p>
<p>Then, as \(N\to\infty\)</p>
<p>$$Z_N \overset{d}{\to} N(0, 1),$$</p>
<p>where \(\overset{d}{\to}\) means "convergence in distribution."</p>
</div>

<p>We see that the Lindeberg-Lévy CLT also gives a \(1/\sqrt{N}\) type convergence result, but in the sense of convergence in distribution and it also gives us that "limit distribution", which is a normal.</p>

## Tails of the normal distribution

<!-- EXERCISE 2.1.4 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex214">
<p><strong>Exercise 2.1.4. (Truncated normal distribution)</strong> Let \(g\sim\mathcal{N}(0,1)\). Show that for all $t\geq 1$, we have</p>
<p>$$\begin{aligned}{\rm I\!E}[g^2 1_{g>t}] ={}& t \tfrac{1}{\sqrt{2\pi}}e^{-\tfrac{t^2}{2}} + {\rm P}[g > t] \\  \leq{}& \left(t+\tfrac{1}{t}\right)\tfrac{1}{\sqrt{2\pi}} e^{-\tfrac{t^2}{2}}.\end{aligned}$$</p>
</div>

<p><em>Solution.</em> We have</p>
<p>$$\begin{aligned}{\rm I\!E}[g^2 1_{g>t}] 
={}& 
\int_t^\infty x^2 e^{-\tfrac{x^2}{2}}\tfrac{1}{\sqrt{2\pi}} {\rm d}x
\\
{}={}& 
\tfrac{1}{\sqrt{2\pi}} \int_t^\infty x^2 e^{-\tfrac{x^2}{2}} {\rm d}x
\\
{}={}& 
\tfrac{1}{\sqrt{2\pi}} \int_t^\infty - x \left(e^{-\tfrac{x^2}{2}}\right)' {\rm d}x
\\
{}={}& 
-\tfrac{1}{\sqrt{2\pi}} \left[ \left.x e^{-\tfrac{x^2}{2}}\right|_{t}^{\infty} - \int_t^\infty e^{-\tfrac{x^2}{2}} {\rm d}x\right]
\\
{}={}& 
-\tfrac{1}{\sqrt{2\pi}} \left[ -te^{-\tfrac{t^2}{2}} -  \int_t^\infty e^{-\tfrac{x^2}{2}}{\rm d}x\right]
\\
{}={}&
\tfrac{1}{\sqrt{2\pi}}  te^{-\tfrac{t^2}{2}} + {\rm P}[g > t]
\end{aligned}$$</p>
<p>We now invoke Proposition 2.1.2 in [<a href="#cite:ver19" title="Vershynin, HDP">1</a>] according to which</p>
<p>$${\rm P}[g > t] \leq \tfrac{1}{t} \tfrac{1}{\sqrt{2\pi}} e^{-\tfrac{t^2}{2}}.$$</p>
<p>This completes the proof. $\Box$</p>






## A quick brush-up on probability inequalities

<p>Let us start with Markov's inequality, which is one of the most fundamental probability inequalities. Many other well-known inequalities are derived from this.</p>

<!-- MARKOV -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="markov-ineq">
<p><strong>Proposition 1 (Markov's inequality).</strong> Let \(X\) be a nonnegative random variable and \(t>0\). Then</p>
<p>$${\rm P}[X \geq t] \leq \frac{{\rm I\!E[X]}}{t}.$$</p>
</div>

<p>Chebyshev's inequality is a corollary of Markov's inequality.</p>

<!-- CHEBSHEV'S INEQUALITY -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="cheby-ineq">
<p><strong>Corollary 2 (Chebyshev's inequality).</strong> Let \(X\) be a random variable with mean $\mu$ and variance $\sigma^2$ and \(t>0\). Then</p>
<p>$${\rm P}[|X-\mu| \geq t] \leq \frac{\sigma^2}{t^2}.$$</p>
</div>

<p><em>Proof.</em> The left-hand side of Chebyshev's inequality is ${\rm P}[|X-\mu| \geq t] = {\rm P}[(X-\mu)^2 \geq t^2]$. The random variable $Y=(X-\mu)^2$ is nonnegative, so we can apply Markov's inequality:</p>
<p>$${\rm P}[(X-\mu)^2 \geq t^2] \leq \frac{{\rm I\!E}[(X-\mu)^2 ]}{t^2} = \frac{\sigma^2}{t^2}.$$</p>
<p>This completes the proof. $\Box$</p>




<div id="fig1">
<img src="/prob-ineq.png" alt="Probability inequalities"  style="width: 90%; margin-left: auto;margin-right: auto;">

<p><em><strong>Figure 1.</strong> The Markov, Chebyshev, and Hoeffding inequalities.</em></p>
</div>

## Hoeffding's inequality and more

<!-- EXERCISE 2.2.3 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex223">
<p><strong>Exercise 2.2.3. (Bounding the hyperbolic cosine)</strong> Show that for all $x\in{\rm I\!R}$</p>
<p>$$\cosh (x) \leq \exp(x^2/2).$$</p>
</div>


<!-- EXERCISE 2.2.8 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex228">
<p><strong>Exercise 2.2.8. (Boosting randomised algorithms)</strong> Lala</p>
</div>


<!-- EXERCISE 2.2.10 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex2210">
<p><strong>Exercise 2.2.10. (Small ball probabilities)</strong> Lala</p>
</div>



## References 

<ol>
  <li id="cite:ver19">R. Vershynin, High Dimensional Probabiltiy: an introduction with applications in data science, Cambridge University Press, 2019</li>
</ol>
<!-- [2] Karl Simgman. <a href="http://www.columbia.edu/~ks20/stochastic-I/stochastic-I.html" target="_blank">Lecture notes on stochastic modeling I</a>, 2009: Lecture notes by K. Sigman, Columbia
University.

[3] Gordan Zitkovic, <a href="https://web.ma.utexas.edu/users/gordanz/notes/uniform_integrability.pdf" target="_blank">Uniform integrability</a>, Lecture notes on "Theory of Probability I", 2015.  -->