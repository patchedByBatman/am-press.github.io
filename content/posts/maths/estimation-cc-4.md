---
author: "Pantelis Sopasakis"
title:  "Estimation Crash Course IV: Sufficient Statistics"
date: 2023-08-31
description: "Sufficient statistics"
summary: "Sufficient statistics"
math: true
series: ["Mathematix"]
tags: ["Probability"]
collapsible: true
draft: false
---

<p>If we are given a sample $X_1,\ldots,X_N{}\overset{\text{iid}}{\sim}{}\mathcal{N}(\mu, \sigma^2)$, where $\sigma^2$ is known, and we need to determine $\mu$ we saw in <a href="../estimation-cc-3#x:umvue-sample-mean" target="_blank">Example III.1</a> of this series that we can use the statistic (estimator)</p>
<p>$$\bar{X}_N(X_1, \ldots, X_N) = \frac{\sum_{i=1}^{N}X_i}{N},$$</p>
<p>which is a UMVUE.</p>
<p>So, do we need to know the entire sample to estimate $\mu$? We see that we just need to know the sum of the observations. Would the knowledge of all observations be of any use? Can we do anything better if we have all the observations instead of their sum? (spoiler: no) Such statistics that summarise the data in such a way that the knownledge of the data themselves is not needed are called sufficient.</p>

<p>A statistic is <em>sufficient</em> for a statistical model and a certain parameter if, roughly speaking, the knownledge of the sample offers no additional information than the statistic itself. To express this mathematically we say that a statistic $T(X_1, \ldots, X_N)$ is sufficient if the conditional distribution of the sample, $X_1,\ldots,X_N$, given $T=t$ and $\theta$ does not depend on $\theta$.</p>

<p>However, this definition is difficult to use in practice. Instead, to show that a given statistic is sufficient we can use the following theorem that we state without a proof.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="thm:factorisation-sufficient-statistic">
  <p><b>Theorem 1 (Fisher-Neymann Factorisation Theorem).</b> Suppose $X_1,\ldots, X_N$ are iid samples. A statistic $T(X_1,\ldots, X_N)$ is sufficient if and only if the likelihood of $\theta$ given the observations can be written as</p>
    <p>$$L(\theta; x_1,\ldots, x_N)
      {}={}
      u(x_1, \ldots, x_N)
      {}\cdot{}
      v(t, \theta),$$</p>
    <p>where $t=T(x_1,\ldots, x_N)$ and where $u$ and $v$ are nonnegative functions.</p>
</div>

<p>Let us give a few examples of sufficient statistics for various statistical models.</p>

<p><b>Example 1 (Normal data, unknown mean/known variance).</b> Let $X_1,\ldots, X_N {}\overset{\text{iid}}{\sim}{} \mathcal{N}(\mu, \sigma^2)$ with known variance, $\sigma^2$, and unknown mean, $\mu$. We will show that the statistic $T(X_1,\ldots, X_N)=\sum_{i=1}^{N}X_i$ is sufficient for this statistical model for $\mu$. The likelihood of $\mu$ given the observations is</p>
<p>$$\begin{aligned}
  L(\mu; x_1,\ldots, x_N)
  {}={} &
  c\exp\left(-\frac{\sum_{i=1}^{N}(x_i-\mu)^2}{2\sigma^2}\right)
  \\
  {}={} &
  c\exp\left(-\frac{1}{2\sigma^2}\sum_{i=1}^{N}x_i^2
  {}+{}
  \frac{\mu}{2\sigma^2}
  \underbrace{\sum_{i=1}^{N}x_i}_{T}
  -
  \frac{N\mu^2}{2\sigma^2}\right),
\end{aligned}$$</p>
<p>where the constant $c$ does not depend on $\mu$. We can now define</p>
<p>$$\begin{aligned}
    u(x_1, \ldots, x_N)
    {}={} &
    c\exp\left(-\frac{1}{2\sigma^2}\sum_{i=1}^{N}x_i^2\right),
    \\
    v(T, \mu)
    {}={} &
    \exp\left(\frac{N\mu^2}{2\sigma^2}+ \frac{\mu}{\sigma^2}T \right).
  \end{aligned}$$</p>
<p>According to <a href="#thm:factorisation-sufficient-statistic">Theorem 1</a>, $T$ is a sufficient statistic. $\heartsuit$</p>

<p id="x:bernoulli-sufficient-statistic"><b>Example 2 (Bernoulli data).</b> Let $X_1,\ldots, X_N{}\overset{\text{iid}}{\sim}{} {\rm Ber}(\theta)$, where $p$ is unknown. The joint pdf of the sample is</p>
<p>$$p(x_1,\ldots, x_N; \theta)
  {}={}
  \prod_{i=1}^{N}\theta^{x_i}(1-\theta)^{1-x_i}
  {}={}
  \underbrace{\theta^{\sum_{i=1}^{N}x_i}}_{u(x_1,\ldots,x_N)}
  \underbrace{(1-\theta)^{N-\sum_{i=1}^{N}X_i}}_{v(\sum_{i=1}^{N}X_i, \theta)},$$</p>
<p>from which we see that $T=\sum_{i=1}^{N}X_i$ is a sufficient statistic for $\theta$. $\heartsuit$</p>

<p><b>Exercise 1 (Gamma data, unknown $\alpha$, known $\beta$).</b> Let $X_1,\ldots,X_N{}\overset{\text{iid}}{\sim}{}\Gamma(\alpha, \beta)$, where $\alpha$ is an unknown parameter and $\beta$ is known. (i) Show that the statistic $$T_1(X_1, \ldots, X_N) = \sum_{i=1}^{N}\log X_i,$$ is a sufficient statistic for $\alpha$. (ii) Show that the statistic $$T_2(X_1,\ldots, X_N)=\prod_{i=1}^{N}X_i,$$ is also a sufficient statistic.</p>


<p id="x:uniform-sufficient-statistic"><b>Exercise 2 (Sufficient statistic for $U(0, \theta)$).</b>} Let $\theta>0$ be an unknown parameter and $X_1, \ldots, X_N{}\overset{\text{iid}}{\sim}{}U(0, \theta)$ (uniform distribution on $[0, \theta]$). Determine a sufficient statistic for $\theta$ for this statistical model</p>

> <p>Spoiler: show that $T=\max_i X_i$ is a sufficient statistic.</p>

<p id="ex:poisson-sufficient-statistic"><b>Exercise 3 (Poisson data).</b> Suppose $X_1,\ldots,X_N{}\overset{\text{iid}}{\sim}{}{\rm Poisson}(\lambda)$ with unknown parameter $\lambda>0$. Show that $T(X_1,\ldots,X_N)=\sum_{i=1}^{N}X_i$ is a sufficient statistic.</p>

<p id="ex:table-sufficient-statistic"><b>Exercise 4 (Sufficient statistics).</b> Fill in the following table with a sufficient statistic:</p>

| Statistical model | Parameter | Sufficient Statistic
| ----------- | -------- | -------- |
| $U(0, \theta)$ | $\theta$ | $\max_i X_i$ | 
| ${\rm Ber}(p)$  |$p$  | $\sum_{i=1}^{N}X_i$ |
| $\Gamma(\alpha, \beta)$ | $\alpha$ | $\sum_{i=1}^{N}\log X_i$ |
| $\Gamma(\alpha, \beta)$ | $\beta$ | ? |
| ${\rm Poisson}(\lambda)$  | $\lambda$ | ? |
| ${\rm Exp}(\lambda)$ | $\lambda$ | ? | 
| $\mathcal{N}(\mu, \sigma^2)$ | $\mu$ | ? |
| $\mathcal{N}(\mu, \sigma^2)$ | $\sigma^2$ | ? |

<p id="ex:exponential-families"><b>Exercise 5 (Exponential families)</b> A parametric distribution, $p_X(x; \theta)$, is said to belong to the <em>exponential family</em> if it can be written as</p>
<p>$$p_X(x; \theta)
  {}={}
  h(x)\exp\left[
    \eta(\theta) t(x) - a(\theta)
    \right].$$</p>
<p>(i) show tha the normal, exponential, Poisson, Bernoulli, and gamma (either with $\theta=\alpha$ or $\theta=\beta$) distributions belong to the exponential family, (ii) $T(X_1,\ldots, X_N)=\sum_{i=1}^{N}t(X_i)$ is a sufficient statistic, (iii) show that the normal distribution, $\mathcal{N}(\mu, 1)$, and the exponential distribution, ${\rm Exp}(\lambda)$, belong to the exponential family.</p>