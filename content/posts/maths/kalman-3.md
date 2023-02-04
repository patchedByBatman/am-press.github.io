---
author: "Pantelis Sopasakis"
title:  "The Kalman Filter III: Measurement and time updates"
date: 2023-02-04
description: "Update equations of the Kalman fiter"
summary: "Update equations of the Kalman fiter"
math: true
series: ["Mathematix"]
tags: ["Estimation"]
collapsible: true
---

> <b>Read first:</b> <a href="../kalman-2">Kalman Filter II: Conditioning</a><br/>
> <b>Read next:</b> <a href="../kalman-4">Kalman Filter IV: Application to position estimation</a>

<p>Consider again the dynamical system (without an input)</p>

<p id="main-system">$$\begin{aligned}x_{t+1} {}={} & A_t x_t + G_t w_t,\\y_t {}={}     & C_t x_t + v_t,\tag{1}\end{aligned}$$</p>

<p>where $x_t\in{\rm I\!R}^{n_x}$ is the system state, $y_t\in{\rm I\!R}^{n_y}$ is the <em>output</em>, $w_t\in{\rm I\!R}^{n_w}$ is a noise term acting on the system dynamics known as <em>process noise</em>, and $v_t\in{\rm I\!R}^{n_v}$ is a measurement noise term.</p>

<p>Hereafter we shall assume that </p>
<ol>
<li>${\rm I\!E}[w_t]=0$ and ${\rm I\!E}[v_t]=0$ for all $t\in{\rm I\!N}$,</li>
<li>$x_0$, $(w_t)_t$ and $(v_t)_t$ are mutually independent random variables (therefore, ${\rm I\!E}[w_tw_l^\intercal]=0$ for $t{}\neq{}l$, and ${\rm I\!E}[v_tv_l^\intercal]=0$ for $t{}\neq{}l$),</li>
<li>$w_t$ and $v_t$ are normally distributed and ${\rm I\!E}[w_tw_t^\intercal]=Q_t$, ${\rm I\!E}[v_tv_t^\intercal]=R_t$.</li>
<li>$x_0$ is a random variable and $x_0 \sim \mathcal{N}(\tilde{x}_0, P_0)$</li>
</ol>

<p>In the following video you will find a complete presentation of the derivation of the Kalman filter.</p>

<iframe alt="YouTube video on the Kalman Filter" style="margin:auto;display:block;"  width="560" height="315" src="https://www.youtube.com/embed/YP6AbR4qPLE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Update Equations

<p>The random variables $x_0$ and $y_0$ are jointly normal with ${\rm I\!E}[x_0]=\tilde{x}_0$, ${\rm I\!E}[y_0]={\rm I\!E}[C_0x_0+v_0] = C_0\tilde{x}_0$.</p>

<p>The variance of $x_0$ is ${\rm Var}[x_0] = {P_0}$. The variance of $y_0$ is</p>

<p>$${\rm Var}[y_0] = {\rm Var}[C_0 x_0 + v_0] = {C_0P_0C_0^\intercal + R_0}.\tag{2}$$</p>

<p>The covariance of $x_0$ with $y_0$ is</p>

<p>$$\begin{aligned}
  {\rm Cov}(x_0, y_0) {}={} & {\rm I\!E}[(x_0-\tilde{x}_0)(y_0 - \tilde{y}_0)^\intercal],\quad \text{ where } \tilde{y}_0 = {\rm I\!E}[y_0]
                                                                                                                           \\
  {}={}                & {\rm I\!E}[(x_0-\tilde{x}_0)(C_0x_0 + v_0 - C_0\tilde{x}_0)^\intercal]
                                                                                                                           \\
  {}={}                & {\rm I\!E}[(x_0-\tilde{x}_0)(C_0(x_0 - \tilde{x}_0) + v_0)^\intercal]
                                                                                                                           \\
  {}={}                & {\rm I\!E}[(x_0-\tilde{x}_0)(x_0 - \tilde{x}_0)^\intercal C_0^\intercal + (x_0-\tilde{x}_0)v_0^\intercal] = {P_0C_0^\intercal}.
\end{aligned}$$</p>
<p>Therefore,</p>
<p id="eq:aee0f39f-c926-4c39-98c5-bdfd6eadd21e">$$
  \begin{bmatrix}
    x_0 \\y_0
  \end{bmatrix}
  {}\sim{}
  \mathcal{N}\left(
  \begin{bmatrix}\tilde{x}_0\\C_0\tilde{x}_0\end{bmatrix},
  \begin{bmatrix}
      {P_0}    & {P_0C_0^\intercal}
      \\
      {C_0P_0} & {C_0P_0C_0^\intercal + R_0}
    \end{bmatrix}
  \right).\tag{3}$$</p>

<p>Suppose we measure $y_0$. What is $x_0$ given $y_0$?</p>

<p>Since $(x_0, y_0)$ is jointly normally distributed as in Equation <a href="eq:aee0f39f-c926-4c39-98c5-bdfd6eadd21e">(3)</a>, $x_0{}\mid{}y_0$ is normally distributed.</p>

<p>We may define the estimator \(\hat{x}_{0{}\mid{}0} \coloneqq  {\rm I\!E}[x_0 {}\mid{} y_0] \), which is (<a href="../kalman-2#thm:normal_conditioning">ref</a>)</p>

<p id="eq:xhat00">$$
  \hat{x}_{0{}\mid{}0}
  {}={}
  \tilde{x}_0
  {}+{}
  {P_0C_0^\intercal}
  ({C_0P_0C_0^\intercal + R_0})^{-1}
  (y_0 - C_0\tilde{x}_0),\tag{4}$$</p>

<p>and the estimator variance, \(\Sigma_{0{}\mid{}0} \coloneqq  {\rm Var}[x_0{}\mid{}y_0]\), which is</p>

<p id="eq:sigma00">$$\Sigma_{0{}\mid{}0}
  {}={}
    {P_0}
    {}-{}
  {P_0C_0^\intercal}
  ({C_0P_0C_0^\intercal + R_0})^{-1}
    {C_0P_0}\tag{5}$$</p>

<p>Having observed $y_0$ at $t=0$ we want to estimate $x_1$; we compute \(\hat{x}_{1{}\mid{}0} \coloneqq {\rm I\!E}[x_1 {}\mid{} y_0]\) which is</p>

<p>$$\hat{x}_{1{}\mid{}0} {}={} A_0 \hat{x}_{0\mid 0}.\tag{6}$$</p>

<p>The estimator variance, \(\Sigma_{1{}\mid{}0} = {\rm Var}[x_1 {}\mid{} y_0]\), is</p>

<p id="eq:sigma10">$$\Sigma_{1{}\mid{}0} {}={} A_0 \Sigma_{0{}\mid{}0}A_0^\intercal + G_0Q_0G_0^\intercal.\tag{7}$$</p>

<p>The output at $t=1$ given the observation of $y_0$ is expected to be</p>

<p>$$\hat{y}_{1{}\mid{}0} = {\rm I\!E}[y_1 {}\mid{} y_0] = C_1\hat{x}_{1{}\mid{}0},\tag{8}$$</p>

<p>and its (conditional) variance is</p>

<p>$${\rm Var}[y_1 {}\mid{} y_0] = {C_1\Sigma_{1{}\mid{}0}C_1^\intercal + R_1},\tag{9}$$</p>

<p>(can you see why?) and the covariance between $x_1$ and $y_1$, conditional on $y_0$, is</p>

<p>$${\rm Cov}(x_1, y_1 {}\mid{} y_0)
  {}\coloneqq {}
  {\rm I\!E}[(x_1 - \tilde{x}_1)(y_1 - \tilde{y}_1)^\intercal {}\mid{} y_0]
  {}={} {\Sigma_{1{}\mid{}0} C_1^\intercal}.\tag{10}$$</p>

<p>Overall,</p>

<p>$$\left.
  \begin{bmatrix}
    x_1 \\ y_1
  \end{bmatrix}
  \right|
  y_0
  {}\sim{}
  \mathcal{N}\left(
  \begin{bmatrix}\hat{x}_{1{}\mid{}0}\\C_1\hat{x}_{1{}\mid{}0}\end{bmatrix},
  \begin{bmatrix}
      {\Sigma_{1{}\mid{}0}}    & {\Sigma_{1{}\mid{}0}C_1^\intercal}
      \\
      {C_1\Sigma_{1{}\mid{}0}} & {C_1\Sigma_{1{}\mid{}0}C_1^\intercal + R_1 }
    \end{bmatrix}
  \right).\tag{11}$$</p>

<p>Once we obtain a measurement $y_1$,</p>

<p>$$\begin{aligned}
    \hat{x}_{1{}\mid{}1} {}={} & {\rm I\!E}[x_1 {}\mid{} y_0, y_1] = \hat{x}_{1{}\mid{}0} + {\Sigma_{1{}\mid{}0}C_1^\intercal}
    ({C_1\Sigma_{1{}\mid{}0}C_1^\intercal + R_1 })^{-1}(y_1 - C_1\hat{x}_{1{}\mid{}0}),
    \\
    \Sigma_{1{}\mid{}1} {}={}  & {\rm Var}[x_1 {}\mid{} y_0, y_1] =
    {\Sigma_{1{}\mid{}0}}
    {}-{}
    {\Sigma_{1{}\mid{}0}C_1^\intercal}
    ({C_1\Sigma_{1{}\mid{}0}C_1^\intercal + R_1 })^{-1}
      {C_1\Sigma_{1{}\mid{}0}}.
  \end{aligned}$$</p>

<p>We can now state the update equations of the Kalman filter</p>

<p>$$\begin{aligned}
    \text{Measurement} &
    \left[
    \begin{array}{l}
      \hat{x}_{t{}\mid{}t}
      {}={}
      \hat{x}_{t{}\mid{}t-1}
      {}+{}
      \Sigma_{t{}\mid{}t-1}C_t^\intercal
      (C_t\Sigma_{t{}\mid{}t-1}C_t^\intercal + R_t)^{-1}(y_t - C_t\hat{x}_{t{}\mid{}t-1})
      \\
      \Sigma_{t{}\mid{}t}
      {}={}
      \Sigma_{t{}\mid{}t-1}
      {}-{}
      \Sigma_{t{}\mid{}t-1}C_t^\intercal
      (C_t\Sigma_{t{}\mid{}t-1}C_t^\intercal + R_t)^{-1}
      C_t\Sigma_{t{}\mid{}t-1}
    \end{array}
    \right.
    \\
    \text{Time update}        &
    \left[
    \begin{array}{l}
      \hat{x}_{t+1{}\mid{}t}
      {}={}
      A_t \hat{x}_{t{}\mid{}t}
      \\
      \Sigma_{t+1{}\mid{}t}
      {}={}
      A_t \Sigma_{t{}\mid{}t} A_t^\intercal + G_tQ_tG_t^\intercal
    \end{array}
    \right.
    \\
    \text{Initial conditions} &
    \left[
    \begin{array}{l}
      \hat{x}_{0{}\mid{}-1}
      {}={}
      \tilde{x}_0
      \\
      \Sigma_{0{}\mid{}-1}
      {}={}
      P_0
    \end{array}
    \right.
  \end{aligned}$$</p>

<p>Note that we have defined: (i) $\hat{x}_{t{}\mid{}t} \coloneqq  {\rm I\!E}[x_t {}\mid{} y_0, y_1, \ldots, y_t]$,
(ii) $\hat{x}_{t+1{}\mid{}t} \coloneqq  {\rm I\!E}[x_{t+1} {}\mid{} y_0, y_1, \ldots, y_t]$,
(iii) $\Sigma_{t{}\mid{}t} \coloneqq  {\rm Var}[x_t {}\mid{} y_0, y_1, \ldots, y_t]$, and
(iv) $\Sigma_{t+1{}\mid{}t} \coloneqq  {\rm Var}[x_{t+1} {}\mid{} y_0, y_1, \ldots, y_t]$.</p>

## How it works

<p>The Kalman filter involves three steps.</p> 

<p><b>Initialisation.</b> At the beginning, an initialisation step is applied where we provide our <em>prior</em> information about the initial state in terms of a normal distribution. In particular, we need to provide an estimate of the initial state, $\tilde{x}_0$. This is our best guess about the state. Alongside, we need to provide the initial variance-covariance matrix, $P_0$. If we are not very confident about our guess, $P_0$ should be taken to be "large" (e.g, a diagonal matrix with large diagonal entries).</p>

<p><b>Measurement update step.</b> Once a new measurement, $y_t$, is available, we apply the measurement update step where we update $\hat{x}_{t\mid t}$ and $\Sigma_{t\mid t}$. The Kalman filter can be applied when the measurements are available intermittently. Then, we will simply skip the measurement update step and we will proceed with the time update.</p>

<p><b>Time update step.</b> At every time instant, after the measurement update (if any), we need to apply the time update step where we predict the next state $\hat{x}_{t+1\mid t}$ and we determine the corresponding variance, $\Sigma_{t+1 \mid t}$ (see the <a href="../kalman-1">Gauss-Markov model</a>).</p>


## Tuning

<p>The tuning of the Kalman filter consists, mainly, in determining $Q$ and $R$ (they can be time-varying). A "small" $Q$ means that we trust the model, while a "small" $R$ means that we trust the sensors. When it comes to $R$, it is easier to determine it by collecting data from the sensors in a controlled environment (usually we can do this), or by looking at the datasheets. On the other hand, $Q$ may be more difficult to determine accurately, especially if we cannot measure the state directly. Often, both $Q$ and $R$ are determined by trial and error.</p>

> <b>Read next:</b> <a href="../kalman-4">Kalman Filter IV: Application to position estimation</a>

