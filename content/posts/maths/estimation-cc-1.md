---
author: "Pantelis Sopasakis"
title:  "Estimation Crash Course I: Statistics and Estimators"
date: 2023-08-20
description: "Statistics and Estimators"
summary: "Statistics and Estimators: definitions of statisics and an introduction to the concepts of bias and variance of an estimator; several examples."
math: true
series: ["Mathematix"]
tags: ["Probability"]
collapsible: true
draft: false
---

> <p><b>Next article:</b> <a href="../estimation-cc-2">Estimation Crash Course II: Fisher information</a></p>

## Statistics and Estimators: Definitions

<p>Here we focus on the problem of estimating a <em>deterministic</em> parameter, $\theta$ (can be scalar or vector-valued), given a collection of observations. Note that $\theta$ is assumed to be a <em>deterministic parameter</em>, so we will not assume a prior distribution on $\theta$. In other words, we shall follow a <em>frequentist</em> rather than a <em>Bayesian</em> approach here.</p>

<p>We assume that we measure the values of $N$ random variables, $X_1,\ldots, X_N$, that take values in a set $E$ (e.g., can be $E\subseteq{\rm I\!R}$ or $E\subseteq{\rm I\!R}^n$) which are typically independently identically distributed according to a parametric distribution with pdf $p_\theta$. This collection of random variables is referred to as our (random) <em>sample</em>.</p>

<p>The parameter $\theta$ is assumed to be drawn from a set $\Theta$ called the <em>parameter set</em>. The collection $\{p_\theta; \theta\in\Theta\}$ is known as the <em>statistical model</em>. A desirable property of the statistical model is that different parameter values correspond to different distributions, that is, $p_{\theta} = p_{\theta'} \Rightarrow \theta = \theta'.$
If this holds we say that the statistical model is <em>identifiable</em>.</p>

<p>As an example, consider the case of $\R$-valued random variables, $X_1,\ldots, X_N{}{}\overset{\text{iid}}{\sim}{}{}\mathcal{N}(\mu, \sigma^2)$, where $\theta=(\mu,\sigma^2)$ and $\Theta=\R\times (0, \sigma^2)$. It can be easily checked that this statistical model is identifiable.</p>

<p>We define a <em>statistic</em> as a (measurable) function of our sample, that is, $T=r(X_1,\ldots, X_N)$. Note that since $X_1,\ldots, X_N$ are random variables, $T$ is a random variable as well. A well known and widely used statistic is the <em>sample mean</em></p>

<p>$$\begin{aligned}\bar{X}_N = \tfrac{1}{N}\sum_{i=1}^{N}X_i.\tag{1}\end{aligned}$$</p>

<p>Another popular statistic is the <em>sample variance</em> defined as</p>
<p id="eq:2">$$\begin{aligned}s^2 = \tfrac{1}{N}\sum_{i=1}^{N}(X_i-\bar{X}_N)^2.\tag{2}\end{aligned}$$</p>

<p>Other statistics can be $T=\max\{X_1,\ldots, X_N\}$, $T=\min\{X_1,\ldots, X_N\}$, $T=X_1$ or even $T=100$ - there is an infinite choice of statistics given a sample.</p>

<p>A statistic that is used to estimate a parameter $\theta$ is referred to as an <em>estimator</em> of $\theta$; an estimator is a statistic that is ``close to'' $\theta$ in some sense.</p>

<p>We define the <em>bias</em> of an estimator $\widehat{\theta} = \widehat{\theta}(X_1, \ldots, X_N)$ to be the expectation of the estimation error, $\widehat{\theta}-\theta$, given $\theta$, that is</p>
<p>$$\begin{aligned}
  {\rm bias}(\widehat{\theta})
  {}={}
  {\rm I\!E}[\widehat{\theta} - \theta {}\mid{} \theta],\tag{3}
\end{aligned}$$</p>
<p>if the expectation exists.</p>

> <p><b>Note:</b> Strictly speaking, in this context, the bias is <em>not</em> a conditional expectation since $\theta$ is not a random variable. We write it like this to underline the that that the bias is a function of $\theta$. We could write ${\rm bias}(\widehat{\theta}){}={}{\rm I\!E}[\widehat{\theta} - \theta]$.</p>

<p>In principle the bias of $\widehat{\theta}$ can depend on $\theta$ - our estimator can have a different bias for different values of the (unknown) parameter $\theta$. If ${\rm bias}(\widehat{\theta})=0$ for all $\theta$ we say that the estimator is <em>unbiased</em>.</p>

<p>The <em>variance</em> of an estimator $\widehat{\theta}$ is defined as</p>
<p id="eq:4">$$\begin{aligned}
  {\rm var}(\widehat{\theta})
  {}={}
  {\rm Var}\left[{}\widehat{\theta} {}\mid{} \theta{}\right]
  {}={}
  {\rm I\!E}\left[{}(\widehat{\theta}-{\rm I\!E}[\widehat{\theta} {}\mid{} \theta])^2{}\mid{}\theta{}\right],\tag{4}
\end{aligned}$$</p>
<p>if the expectation exists.</p>
<p>We also define the <em>mean square error</em> (MSE) of $\widehat{\theta}$ as</p>
<p>$$\begin{aligned}
  {\rm mse}(\widehat{\theta})
  {}={}
  {\rm I\!E}[(\widehat{\theta}-\theta)^2 {}\mid{} \theta],\tag{5}
\end{aligned}$$</p>
<p>if the above expectation exists.</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="thm:mse_var_bias">
<p><strong>Theorem 1 (MSE, Variance and Bias).</strong> The mean square error of an estimator is given by</p>
    <p id="eq:6">$$\begin{aligned}
      {\rm mse}(\widehat{\theta})
      {}={}
      {\rm var}(\widehat{\theta})
      {}+{}
      {\rm bias}(\widehat{\theta})^2.\tag{6}
    \end{aligned}$$</p>
</div>  

<p><em>Proof.</em> The proof relies on the definition of the MSE in Equation <a href="#eq:6">(6)</a> and the formula ${\rm Var}[X{}\mid{}Y]={\rm I\!E}[X^2{}\mid{}Y]-{\rm I\!E}[X{}\mid{}Y]^2$. This proof is left to the reader as an exercise. $\Box$</p>


<p>Note that according to Equation <a href="#eq:6">(6)</a>, if an estimator $\widehat{\theta}$ is unbiased, its MSE is equal to its variance.</p>

<p>In practice it is typically desirable for an estimator to exhibit minimum MSE; at the same time, we want it to be unbiased. These requirements are sometimes impossible to reconcile. In some cases, no unbiased estimators exist. Let us give a few examples to understand the above concepts.</p>

<p id="x:sample-mean-unbiased"><b>Example 1 (Sample mean is unbiased).</b> Suppose that $X_1, \ldots, X_N$ are iid samples with mean $\mu$. The sample mean is given in Equation <a href="#eq:1">(1)</a> and is an estimtor of $\mu$. We can easily see that the bias of $\bar{X}_N$ is</p>
<p>$$\begin{aligned}
  {\rm bias}(\bar{X}_N)
  {}={}
  {\rm I\!E}[\bar{X}_N - \mu {}\mid{} \mu]
  {}={}
  {\rm I\!E}\left[\left.
    \tfrac{1}{N}\sum_{i=1}^{N}X_i\right|\mu\right]
  {}={}
  \tfrac{1}{N}\sum_{i=1}^{N}{\rm I\!E}[X_i{}\mid{}\mu] = \mu.
\end{aligned}$$</p>
<p>This proves that $\bar{X}_N$ is an unbiased estimator of $\mu$. $\heartsuit$</p>

<p id="x:mse-sample-mean"><b>Example 2 (MSE of sample mean).</b> Assume that the variance of $X_i$ is known and equal to $\sigma^2$ for all $i\in\N_{[1, N ]}$. According to Equation <a href="#eq:4">(4)</a>, the variance of the sample mean is<p>
<p>$$\begin{aligned}
  {\rm var}(\bar{X}_N)
  {}={} &
  {\rm Var}[\bar{X}_N {}\mid{} \mu]
  \\
  {}={}&
  {\rm Var}\left[\tfrac{1}{N}\sum_{i=1}^{N}X_i\right]
  \\
  {}={} &
  \tfrac{1}{N^2}{\rm Var}\left[\sum_{i=1}^{N}X_i\right]
  {}\overset{\text{indep.}}{=}{}
  \tfrac{1}{N^2}\sum_{i=1}^{N}{\rm Var}[X_i]
  {}={}
  \frac{\sigma^2}{N}.
\end{aligned}$$</p>
<p>Since the estimator is unbiased, according to Theorem <a href="#thm:mse_var_bias">1</a>, its MSE is equal to its variance. We see that as $N\to\infty$, the MSE of this estimator converges to zero (at a rate of $\mathcal{O}(1/N)$). $\heartsuit$</p>

<p><b>Example 3 (Sample variance is biased).</b> The sample variance given in Equation <a href="#eq:2">(2)</a> is a biased estimator of $\sigma^2$. Indeed,</p>
<p>$$\begin{aligned}
  {\rm I\!E}[s^2 {}\mid{} \sigma^2]
  {}={} &
  {\rm I\!E}\left[\tfrac{1}{N}\sum_{i=1}^{N}(X_i-\bar{X}_N)^2\right]
  \\
  {}={} &
  {\rm I\!E}\left[\tfrac{1}{N}\sum_{i=1}^{N}((X_i-\mu)^2-(\bar{X}_N-\mu)^2)^2\right]
  \\
  {}={} &
  \tfrac{1}{N}\sum_{i=1}^{N}\underbrace{{\rm I\!E}[(X_i-\mu)^2]}_{{\rm Var}[X_i]} - \tfrac{1}{N}\sum_{i=1}^{N}\underbrace{{\rm I\!E}[(\bar{X}_N-\mu)^2]}_{{\rm Var}[\bar{X}_N]}
  {}={} \sigma^2 - \frac{\sigma^2}{N},
\end{aligned}$$</p>
<p>therefore, the bias of $s^2$ is</p>
<p>$$\begin{aligned}
  {\rm bias}(s^2)
  {}={}
  {\rm I\!E}[s^2 {}\mid{} \sigma^2] - \sigma^2 = -\frac{\sigma^2}{N}.
\end{aligned}$$</p>
<p>We see that $s^2$ is a biased estimator, but the bias converges to $0$ as $N{}\to{}\infty$. We say that $s^2$ is an <em>asymptotically unbiased</em> estimator of $\sigma^2$.  $\heartsuit$</p>


<p id="x:bessel-correction"><b>Example 4 (Unbiased estimator of the variance).</b> Following the same procedure as above we can show that the following estimate of $\sigma^2$ is an unbiased estimator</p>
<p>$$\begin{aligned}
  s^2_{\rm corr} = \frac{1}{N-1}\sum_{i=1}^{N}(X_i-\bar{X}_N)^2.
\end{aligned}$$</p>
<p>This estimator is known as <em>Bessel's correction</em>. $\heartsuit$</p>

<p><b>Example 5 (Lack of unbiased estimator).</b> There are cases where there are no unbiased estimators. For example, suppose that $X{}\sim{}{\rm Exp}(\lambda)$, $\lambda>0$. Recall that the pdf of the exponential distribution, ${\rm Exp}(\lambda)$, is</p>
<p>$$\begin{aligned}
  p_X(x; \lambda) = \lambda e^{-\lambda x}, x \geq 0.
\end{aligned}$$</p>
<p>Suppose that $\widehat{\lambda}=\widehat{\lambda}(X)$ is an unbiased estimator of $\lambda$. Then, by definition the following needs to hold for all $\lambda>0$</p>
<p>$$\begin{aligned}
  {\rm bias}(\widehat{\lambda}) = 0
  {}\Leftrightarrow{} &
  {\rm I\!E}[\widehat{\lambda} {}\mid{} \lambda] = \lambda
  \\
  {}\Leftrightarrow{} &
  \int_0^\infty \widehat{\lambda}(x)p_X(x){\rm d} x = \lambda
  \\
  {}\Leftrightarrow{} &
  \int_0^\infty \widehat{\lambda}(x)\lambda e^{-\lambda x}{\rm d} x = \lambda
  \\
  {}\Leftrightarrow{} &
  \int_0^\infty \widehat{\lambda}(x) e^{-\lambda x}{\rm d} x = 1
  \\
  {}\Leftrightarrow{} &
  \{\mathscr{L}\widehat{\lambda}(x)\}(\lambda) = 1,
\end{aligned}$$</p>
<p>where the last equality is due to the fact that $\int_0^\infty \widehat{\lambda}(x)\lambda e^{-\lambda x}{\rm d} x$ is the Laplace transform of $\widehat{\lambda}$ evaluated at $\lambda$.
However such a function, $\widehat{\lambda}(x)$ cannot exist; the reason is that the property $\lim_{\lambda\to\infty}\{\mathscr{L}\widehat{\lambda}(x)\}(\lambda)=0$ should be satisfied. $\heartsuit$</p>

<p>Lastly, we define a uniformly minimum-variance unbiased estimator (UMVUE) to be an unbiased estimator such that there is no other unbiased estimator with a lower variance. Formally, let $X_1,\ldots, X_N$ be a random sample and $\widehat{\theta}(X_1,\ldots, X_N)$ is an <em>unbiased</em> estimator of a parameter $\theta$. Then, $\widehat{\theta}$ is UMVUE if</p>
<p>$${\rm var}[\widehat{\theta}] \leq {\rm var}[\widetilde{\theta}],$$</p>
<p>for all $\theta$ and for all unbiased estimators $\widetilde{\theta}$.</p>

<p><b>Bias-Variance Tradeoff:</b> UMVUEs are considered good estimators. But sometimes, we may decide to choose an estimator that has some small nonzero bias, but comes with a lower variance. This is known as the bias-variance tradeoff problem or dilemma.</p>

> <p><b>Read next:</b> <a href="../estimation-cc-2">Estimation Crash Course II: Fisher information</a></p>