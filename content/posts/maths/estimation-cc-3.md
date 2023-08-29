---
author: "Pantelis Sopasakis"
title:  "Estimation Crash Course III: Cramér-Rao bound"
date: 2023-08-30
description: "The Cramér-Rao bound"
summary: "The Cramér-Rao Bound is a lower bound on the variance of an unbiased estimator. Here we focus on one-parameter models."
math: true
series: ["Mathematix"]
tags: ["Probability"]
collapsible: true
draft: true
---

> <p><b>Previous article:</b> <a href="../estimation-cc-2">Estimation Crash Course II: Fisher information</a></p>

<p>The Cramér-Rao Bound is a lower bound on the variance of an unbiased estimator. The result we are about to state relies on the following weak regularity assumptions on the likelihood function, $\ell(\theta)$, and the estimator, $\widehat{\theta}$.</p>

<p><b>Regularity assumptions.</b> In addition to the basic regularity assumptions we stated <a  href="../estimation-cc-2#par:basic-regularity-assumptions" title="Estimation Crash Course II" target="_blank">in this previous post</a>, suppose that for all $x$ for which $p_X(x; \theta)>0$, the derivative $\frac{\partial}{\partial \theta}{}\;{}p_X(x; \theta)$ exists, and the following holds</p>
<p>$$
  \frac{\partial}{\partial \theta}\int_E \widehat{\theta}(x)p_X(x; \theta){\rm d} x
  {}={}
  \int_E \widehat{\theta}(x) \frac{\partial}{\partial \theta}p_X(x; \theta){\rm d} x\tag{1}$$</p>
<p>whenever the right hand side exists and is finite.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="thm:crlb">
<p><b>Theorem 1 (Cramér-Rao lower bound).</b> Let $X$ be a sample from with pdf $p_X(x;\theta)$ and $\widehat{\theta}$ is an unbiased estimator of $\theta$. Suppose that the regularity assumptions hold. Then,</p>
<p>$${\rm var}[\widehat{\theta}] {}\geq{} \frac{1}{I(\theta)}.\tag{2}$$</p>
</div>

<p>It follows from <a href="#thm:crlb" title="Cramér-Rao bound">Theorem 1</a> that if an unbiased estimator attains the lower bound, i.e., if ${\rm var}[\widehat{\theta}]{}={}\frac{1}{I(\theta)},$ then it is a <u style="text-decoration:underline dotted" title="unbiased minimum variance estimator">UMVUE</u>. However, this lower bound is not tight in the sense that not all UMVUEs attain this lower bound. Let us give an example where this happens.</p>

<p id="x:umvue-sample-mean"><b>Example 1 (UMVUE via Cramér-Rao bound).</b> In <a href="../estimation-cc-1#x:sample-mean-unbiased" target="_blank">Example 1 in Part I</a> we showed that the sample mean, $\bar{X}_N$, is an unbiased estimator of the mean $\mu$ and in <a href="../estimation-cc-1#x:mse-sample-mean" target="_blank">Example 2 in Part I</a> we showed that its variance is $\mathrm{var}[\bar{X}_N] = \sigma^2/N$ (and $\sigma^2$ is assumed to be known). Now assume that $X_1,\ldots,X_N{}\overset{\text{iid}}{\sim}{}\mathcal{N}(\mu,\sigma^2)$ for which the regularity assumptions hold and the Fisher information for $\mu$ is</p>
<p>$$I(\mu) = \frac{N}{\sigma^2}.\tag{3}$$</p>
<p>We see that $\mathrm{var}[\bar{X}_N] = 1/I(\mu)$, therefore, $\bar{X}_N$ is a UMVUE for $\mu$. $\heartsuit$</p>


<p id="x:estimator-bernoulli-umvue"><b>Example 1 (Estimator of Bernoulli parameter is UMVUE).</b> Let $X_1, \ldots, X_N {}\overset{\text{iid}}{\sim}{} {\rm Ber}(p)$. The estimator</p>
<p>$$\widehat{p}(X_1,\ldots, X_N)
  {}={}
  \tfrac{1}{N}\sum_{i=1}^{N}X_i,\tag{4}$$</p>
<p>is unbiased (why?) and its variance is (see <a href="../estimation-cc-1#eq:4" title="estimator variance" target="_blank">Part I, Eq. (4)</a>)</p>
<p>$${\rm var}[{}\widehat{p}{}]
  {}={}
  {\rm Var}\left[\left.\tfrac{1}{N}\sum_{i=1}^{N}X_i\right|p\right]
  {}\overset{\text{indep.}}{=}{}
  \tfrac{1}{N^2}\sum_{i=1}^{N}{\rm Var}[X_i] = \frac{p(1-p)}{N}.\tag{5}$$</p>

<p>Now if $X\sim{\rm Ber}(p)$, according to <a href="../estimation-cc-2#eq:bernoulli:fisher" target="_blank">Equation (14) in Part II</a> the Fisher information of $p$ is $I(p) = \tfrac{1}{p(1-p)}$ and following <a href="../estimation-cc-2#ex:fisher-multiple-observations" target="_blank">Exercise 2 in Part II</a>, the Fisher information for the case of $N$ independent observations becomes</p>
<p>$$I(p) = \frac{N}{p(1-p)}.\tag{6}$$</p>
<p>The reader can verify that the regularity assumptions hold of the Bernoulli distribution. We see that ${\rm var}[{}\widehat{p}{}] = I(p)^{-1}$, therefore, $\widehat{p}$ is a UMVUE of $p$. $\heartsuit$</p>

<p>An unbiased estimator that attains the Cramér-Rao lower bound is called an <em>efficient</em> estimator. All efficient estimators are UMVUE, however not all UMVUEs are efficient.</p>

<p>We shall now state a very useful result that can be used to determine an efficient estimator (if it exists). The proof is a bit technical, so we will skip it.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="thm:efficient-factorisation">
<p><b>Theorem 2 (Factorisation for efficient estimators).</b> An efficient estimator, $\widehat{\theta}$, exists if and only if</p>
<p id="eq:factorisation-efficient">$$\frac{\partial \ell(\theta; x)}{\partial \theta} {}={} I(\theta)[\widehat{\theta}(x) - \theta].\tag{7}$$</p>
</div>

<p>If follows from the theorem that  $\mathrm{var}[\widehat{\theta}] = I(\theta)^{-1}$. Let us give an example where we "factorise" $\frac{\partial \ell(\theta; x)}{\partial \theta}$ as in <a href="#eq:factorisation-efficient">Equation (7)</a> to determine an efficient estimator.</p>


<p><b>Example 2 (Estimator of $\sigma^2$ with known mean).</b> Suppose $X_1,\ldots, X_N {}\overset{\text{iid}}{\sim}{}\mathcal{N}(\mu, \sigma^2)$, where $\mu$ is known and $\sigma^2$ is an unknown parameter. The likelihood of $\sigma^2$ given a measurements $X=x$ is</p>
<p>$$\ell(\sigma^2)
  {}={}
  \log p_X(x; \mu, \sigma^2)
  {}={}
  -\tfrac{1}{2}\log(2\pi\sigma^2)
  -\frac{(x-\mu)^2}{2\sigma^2}.\tag{8}$$</p>
<p>We leave it to the reader to verify that the Fischer information for one observation is  $\frac{1}{2\sigma^4},$ so for $N$ observations the Fisher information is (see <a href="../estimation-cc-2#ex:fisher-multiple-observations">Exercise 2 in Part II</a>)</p>
<p id="eq:fisher-information-variance-normal">$$I(\sigma^2) = \frac{N}{2\sigma^4}.\tag{9}$$</p>
<p>In <a href="../estimation-cc-1#x:bessel-correction">Example 4 in Part 1</a> we showed that $s^2_{\rm corr} = \frac{1}{N-1}\sum_{i=1}^{N}(X_i-\bar{X}_N)^2$ is an unbiased estimator of $\sigma^2$. It can be shown that the variance of this estimator is</p>
<p>$$\mathrm{var}[s^2_{\rm corr}] = \frac{2\sigma^4}{n-1} > \frac{\sigma^4}{n},\tag{10}$$</p>
<p>so $s^2_{\rm corr}$ does not attain the lower bound of the Cramér-Rao inequality. Let us now try to factorise $\frac{\partial \ell(\sigma^2; x)}{\partial \sigma^2}$ as in <a href="#eq:factorisation-efficient">Equation (7)</a>:</p>

<p>$$\begin{aligned}
  \frac{\partial \ell(\theta; x)}{\partial \sigma^2}
  {}={} &
  \frac{\partial}{\partial \sigma^2}\log p(x_1, x_2, \ldots, x_N; \mu, \sigma^2)
  \\
  {}={} &
  \frac{\partial}{\partial \sigma^2}\log \prod_{i=1}^{N}p(x_i; \mu, \sigma^2)
  {}={}
  \frac{\partial}{\partial \sigma^2} \sum_{i=1}^{N}\log p(x_i; \mu, \sigma^2)
  \\
  {}={} &
  \frac{\partial}{\partial \sigma^2} \sum_{i=1}^{N} \log\left[\tfrac{1}{\sqrt{2\pi}\sigma}\exp\left(-\frac{(x_i-\mu)^2}{2\sigma^2}\right)\right]
  \\
  {}={} &
  \frac{\partial}{\partial \sigma^2}\sum_{i=1}^{N}\left[-\tfrac{1}{2}\log(2\pi\sigma^2) - \frac{(x_i-\mu)^2}{2\sigma^2}\right]
  \\
  {}={} &
  \frac{\partial}{\partial \sigma^2} \left[-\frac{N}{2}\log(2\pi\sigma^2) - \sum_{i=1}^{N}\frac{(x_i-\mu)^2}{2\sigma^2}\right]
  \\
  {}={} &
  -\frac{N}{2\sigma^2} + \sum_{i=1}^{N}\frac{(x_i-\mu)^2}{2\sigma^4}.
\end{aligned}$$</p>
<p>If we now take out as a common factor $\frac{N}{2\sigma^4}$ - i.e., the Fisher information according to <a href="#eq:fisher-information-variance-normal">Equation (9)</a> - we have</p>
<p>$$\begin{aligned}
  \frac{\partial \ell(\theta; x)}{\partial \sigma^2}
  {}={} &
  \underbrace{\frac{N}{2\sigma^4}}_{I(\sigma^2)}
  \left(
  \underbrace{\frac{\sum_{i=1}^{N}(x_i-\mu)^2}{N}}_{\text{efficient estimator}}-\sigma^2
  \right).\tag{11}
\end{aligned}$$</p>
<p>The regularity assumptions are satisfied in this case so from <a href="#thm:efficient-factorisation">Theorem 2</a> we conclude that the estimator</p>
<p>$$\widehat{\sigma}^2 = \frac{\sum_{i=1}^{N}(x_i-\mu)^2}{N},\tag{12}$$</p>
<p>is an efficient estimator of $\sigma^2$ (thus UMVUE) and, by definition, its variance is $1/I(\sigma^2)=\frac{\sigma^4}{N}$. There is no other unbiased estimator of $\sigma^2$ with a lower variance. Note that this holds only under the assumption that $\mu$ is known. $\heartsuit$</p>


