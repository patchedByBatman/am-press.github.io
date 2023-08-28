---
author: "Pantelis Sopasakis"
title:  "Estimation Crash Course II: Fisher information"
date: 2023-08-23
description: "Introduction to Fisher information"
summary: "Fisher information for one-parameter models"
math: true
series: ["Mathematix"]
tags: ["Probability"]
collapsible: true
draft: false
---

> <p><b>Previous article:</b> <a href="../estimation-cc-1">Estimation Crash Course I: Statistics and Estimators</a></p>

> <p><b>Next article:</b> <a href="../estimation-cc-3">Estimation Crash Course III: The Cramér-Rao bound</a></p>

## Fisher Information for one-parameter models


<p>We shall introduce the concept of the Fisher information via an example. Let $X\sim\mathcal{N}(\mu, \sigma^2)$ where $\sigma^2$ is known and $\mu$ is unknown. Let us consider two cases:<p>
<ul>
  <li>Case I: $X\sim\mathcal{N}(\mu, 20)$ (large variance),</li>
  <li> Case II: $X\sim\mathcal{N}(\mu, 0.1)$ (small variance),</li>
</ul>
<p>where the value of $\mu$ is the same in both cases. Suppose we obtain one measurement, $X=x$, so the log-likelihood of $\mu$ is</p>
<p>$$\ell(\mu; x) = \log p_X(x; \mu) = -\log(\sqrt{2\pi} \sigma) -\frac{(x-\mu)^2}{2\sigma^2}.\tag{1}$$</p>

<p>Figure <a href="#fig:normal-fisher">1</a> shows the log-likelihood functions, $\ell(\mu; x)$, for a few samples $X\sim\mathcal{N}(\mu, 0.1)$ (Case I). We can say that each observation is quite <em>informative</em> about the parameter $\mu$.</p>

<div id="fig:normal-fisher">
<img src="/low_variance_log_likelihood.png" alt="Low-variance log-likelihood function"  style="width: 97%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 1.</strong> (Case I) Plot of $\ell(\mu; x_i)$ for $N=20$ measurements. The likelihood function has, on average, a healthy curvature (it is not too flat).</em></p>
</div>


<p>It is not difficult to guess the true value of $\mu$ from the above plot (in fact it is $\mu=1$). On the other hand, in Case II we have the following plot (Figure <a href="#fig:normal-fisher2">2</a>) of the log-likelihood function for each observation</p>

<div id="fig:normal-fisher2">
<img src="/hi_variance_log_likelihood.png" alt="Low-variance log-likelihood function"  style="width: 97%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 2.</strong> (Case II) Plot of $\ell(\mu; x_i)$ for $N=20$ measurements. The likelihood function is, on average, quite flat.</em></p>
</div>


<p>Here it is more difficult to guess what the true value of $\mu$ is, or, to put it differently, the data are <em>less informative</em> about $\mu$, the main reason being that</p>

<p>Fisher proposed the following quantity to quantify the <em>information</em> that an observation $X$ (or several observations, $X_1,\ldots, X_N$) offers about the parameter $\theta$:</p>
<p>$$I(\theta)
  {}={}
  -{\rm I\!E}\left[
  \left.
  \frac{\partial^2}{\partial \theta^2}\ell(\theta; X)
  \right|
  {}\theta
  \right],\tag{2}$$</p>
<p>where the expectation is taken with respect to $X$ and $\ell$ denotes the log-likelihood. In other words, using the pdf of $X$,</p>
<p id="eq:fisher:expectation_second_deriv_pdf">$$
  I(\theta)
  {}={}
  \int_E \frac{\partial^2}{\partial \theta^2}\ell(\theta; x)p_X(x; \theta){\rm d} x.\tag{3}$$</p>

<p>This quantity is known as the <em>Fisher information</em> of the statistical model. The Fisher information quantifies how much information the data gives us for the unknown parameter.<p>

<p>There is an alternative expression for the determination of $I(\theta)$ --- we will prove it in a moment --- which uses the first derivative of $\ell$:</p>
<p>$$I(\theta)
  {}={}
  {\rm I\!E}\left[
  \left.
  \left(\frac{\partial \ell(\theta; X)}{\partial \theta}\right)^2
  \right|
  {}\theta
  \right].\tag{4}$$</p>
<p>Again, as we did in Equation <a href="#eq:fisher:expectation_second_deriv_pdf">(3)</a>, we can use the pdf of $X$ to compute $I(\theta)$, that is,</p>
<p id="eq:8bb3a8f6-94b6-4231-8c38-c5e09df9791a">$$I(\theta)
  {}={}
  \int_E \left(\frac{\partial \ell(\theta; x)}{\partial \theta}\right)^2 p_X(x; \theta){\rm d} x.\tag{5}$$</p>
<p>The Fisher information is defined if the following <em>basic regularity conditions</em> are satisfied: (i)~$p_X(x; \theta)$ is differentiable wrt $\theta$ almost everywhere,
(ii)~the support of $p_X(x; \theta)$ does not depend on $\theta$. In other words, the set $\{x{}:{} p_X(x;\theta)>0\}$ does not depend on $\theta$,
and
(iii)~it holds that $\frac{\partial}{\partial \theta}\int p_X(x;\theta){\rm d} x = \int \frac{\partial}{\partial \theta} p_X(x;\theta){\rm d} x$.</p>

<p>Note that the first assumption is <em>not satisfied for the uniform distribution</em>, $U(0, \theta)$, and the Fisher information is not defined for $U(0, \theta)$.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="thm:mse_var_bias">
<p><strong>Theorem 1 (Fisher Information Equivalent Formulas).</strong> Suppose  $\ell(\theta; X)$ is the likelihood of a parameter $\theta$ given some observation(s) $X$ and the above regularity assumptions are satisfied. Then,</p>
    <p>$${\rm I\!E}\left[
      \left.
      \frac{\partial \ell(\theta; X)}{\partial \theta}
      \right|
      {}\theta
      \right] = 0.\tag{6}$$</p>
<p>Additionally, assume that it is twice differentiable and (iv) assumption (iii) holds for the second order derivative wrt $\theta$. Then, the Fisher information is given by</p>
<p id="eq:fisher-equivalent">$$\begin{aligned}I(\theta)
      {}={}&
      -{\rm I\!E}\left[
      \left.
      \frac{\partial^2}{\partial \theta^2}\ell(\theta; X)
      \right|
      {}\theta
      \right]\\
      {}={}&
      {\rm I\!E}\left[
      \left.
      \left(\frac{\partial \ell(\theta; X)}{\partial \theta}\right)^2
      \right|
      {}\theta
      \right]
      {}={}
      {\rm Var}\left[
      \left.
      \frac{\partial \ell(\theta; X)}{\partial \theta}
      \right|
      {}\theta
      \right] \tag{7}.\end{aligned}$$</p>
</div>


<p>We have</p>
<p>$$\begin{aligned}
    {\rm I\!E}\left[
    \left.
    \frac{\partial \ell(\theta; X)}{\partial \theta}
    \right|
    {}\theta
    \right]
    {}={} &
    {\rm I\!E}\left[
    \left.
    \frac{\partial \log p(X; \theta)}{\partial \theta}
    \right|
    {}\theta
    \right]
    {}={}
    \int_E
    \frac{\frac{\partial p_X(x; \theta)}{\partial \theta}}{\cancel{p_X(x; \theta)}}\cancel{p_X(x; \theta)}{\rm d} x
    \\
    {}={} &
    \int_E \frac{\partial p_X(x; \theta)}{\partial \theta}{\rm d} x
      {}\overset{\text{Ass.~(iii)}}{=}{}
    \frac{\partial}{\partial \theta} \underbrace{\int_E p_X(x; \theta) {\rm d} x}_{=1} = 0,\tag{8}
  \end{aligned}$$</p>
  <p>so the last equality in Equation <a href="#eq:fisher-equivalent">(7)</a> follows.</p>

  <p>To prove that the two expectations are equal we use the fact that</p>
  <p id="eq:7683fad9-8a3d-4fc3-9bee-40309179c923">$$\begin{aligned}
    \frac{\partial^2}{\partial \theta^2}\log p_X(X; \theta)
    {}={}&
    \frac{\frac{\partial^2 p_X(X; \theta)}{\partial \theta^2}}{p_X(X; \theta)}
    {}-{}
    \left(\frac{\frac{\partial^2 p_X(X; \theta)}{\partial \theta^2}}{p_X(X; \theta)}\right)^2
    \\
    {}={}&
    \frac{\frac{\partial^2 p_X(X; \theta)}{\partial \theta^2}}{p_X(X; \theta)}
    {}-{}
    \left(
    \frac{\partial}{\partial \theta}\log p_X(X; \theta)
    \right)^2.\tag{9}\end{aligned}$$</p>
  <p>Note that</p>
  <p id="eq:683959f9-00ec-487d-a2aa-9c09de928150">$$\begin{aligned}{\rm I\!E}\left[\frac{\frac{\partial^2 p_X(X; \theta)}{\partial \theta^2}}{p_X(X; \theta)}\right]
    {}={}&
    \int_E
    \frac{\frac{\partial^2 p_X(x; \theta)}{\partial \theta^2}}{\cancel{p_X(x; \theta)}}
    \cancel{p_X(x; \theta)}
    {\rm d} x
    \\
      {}\overset{\text{(iv)}}{=}{}&
    \frac{\partial^2 p_X(x; \theta)}{\partial \theta^2}
    \underbrace{\int_E p_X(x;\theta){\rm d} x}_{=1}=0.\tag{10}\end{aligned}$$</p>
  <p>Now taking the expectation on Equation <a href="#eq:7683fad9-8a3d-4fc3-9bee-40309179c923">(9)</a> and using Equation <a href="#eq:683959f9-00ec-487d-a2aa-9c09de928150">(10)</a>, Equation <a href="#eq:fisher-equivalent">(7)</a> follows. $\Box$</p>

<p id="x:exponential-fisher-information"><b>Example 1 (Fisher information of Exponential).</b> Suppose $X{}\overset{\text{iid}}{=} {} {\rm Exp}(\lambda)$ where $\lambda>0$ is an unknown value. We want to quantify how informative a measurement of $X$. The likelihood function is $L(\lambda, x) = \lambda e^{-\lambda x}$, where $x\geq 0$, so the log-likelihood is $\ell(\lambda, x) = \log \lambda - x\lambda$. Suppose that the true value of $\lambda$ is $3$. Let us samples some values $x_1,\ldots, x_10$ using Python (<code>numpy.random.Generator.exponential</code>) and plot $\ell(\lambda, x_i)$ which is shown in Figure <a href="#fig:exp-fisher">3</a>.</p>


<div id="fig:exp-fisher">
<img src="/log-likelihood-fisher.png" alt="Low-variance log-likelihood function"  style="width: 90%; margin-left: auto; margin-right: auto;">
<p><em><strong>Figure 3.</strong> Log-likelihood, $\ell(\lambda; x_i)$, for different values sampled from ${\rm Exp}(3)$.</em></p>
</div>


<p>In this example we see that the log-likelihood is not quadratic in $\lambda$, so its curvature depends on $\lambda$. In particular, the curvature is</p>
<p>$$\frac{\partial^2 }{\partial \lambda^2}\ell(\lambda; X) = -\frac{1}{\lambda^2},\tag{11}$$</p>
<p>therefore, the Fisher information is $I(\lambda) = -\frac{1}{\lambda^2}$. $\heartsuit$</p>

<p id="x:bernoulli-fisher-information"><b>Example 2 (Fisher information of Bernoulli).</b> The likelihood function of a Bernoulli trial is $L(p; X) = p^X (1-p)^{1-X}$, so the log-likelihood is</p>
<p>$$\ell(p; X) = X\log p + (1-X)\log(1-p)\tag{12}$$</p>
<p>The second derivative of $\ell$ with respect to $p$ is</p>
<p>$$\frac{\partial^2 \ell(p; X)}{\partial p^2} {}={} \frac{X}{p^2} + \frac{1-X}{(1-p)^2}.\tag{13}$$</p>
<p>The Fisher information is</p>
<p id="eq:bernoulli:fisher">$$I(p)
  {}={}
  {\rm I\!E}\left[\left.\frac{\partial^2 \ell(p; X)}{\partial p^2}\right| p \right]
  {}={}
  {\rm I\!E}\left[\left.\frac{X}{p^2} + \frac{1-X}{(1-p)^2}\right| p \right] = \ldots = \frac{1}{p(1-p)}.\tag{14}$$</p>

<p>The plot of the Fisher information, $I(p)$, is shown in Figure <a href="#fig:bernoulli-fisher">4</a>.</p>

<div id="fig:bernoulli-fisher">
<img src="/fisher-bernoulli.png" alt="Low-variance log-likelihood function"  style="width: 90%; margin-left: auto; margin-right: auto;">
<p><em><strong>Figure 4.</strong> Fisher information for ${\rm Ber}(p)$ as a function of $p$. The outcomes of blatantly unfair coins are more informative about the parameter $p$.</p>
</div>

<p>We see that the Fisher information increases for values of $p$ close to $0$ or $1$ (for blatantly unfair coins). $\heartsuit$</p>


> <p><b>Read next:</b> <a href="../estimation-cc-3">Estimation Crash Course III: The Cramér-Rao bound</a></p>