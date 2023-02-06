---
author: "Pantelis Sopasakis"
title:  "The Kalman Filter VII: Recursive maximum a posteriori"
date: 2023-02-05
draft: true
description: "The Kalman filter is a recursive maximum a posteriori estimator"
summary: "We show that the Kalman filter is a recursive maximum a posteriori estimator. This "
math: true
series: ["Mathematix"]
tags: ["Estimation"]
collapsible: true
---

> <b>Read first:</b> <a href="../kalman-5">Kalman Filter V: it's BLUE!</a><br>

<p>Consider the dynamical system</p>

<p>$$\begin{aligned}
            x_{t+1} {}={} & Ax_t + w_t,
            \\
            y_t {}={}     & Cx_t + v_t,
        \end{aligned}$$</p>

<p>under the independence assumptions we stated <a href="../kalman-1#assumptions">earlier</a> and assuming that $w_t$, $v_t$, and $x_0$ are normally distributed, that is,</p>
<p>$$\begin{aligned}
            p_{w_t}(w) {}\propto{}   & \exp \left[-\tfrac{1}{2}\|w\|_{Q^{-1}}^2\right],
            \\
            p_{v_t}(v) {}\propto{}   & \exp \left[-\tfrac{1}{2}\|v\|_{R^{-1}}^2\right],
            \\
            p_{x_0}(x_0) {}\propto{} & \exp \left[-\tfrac{1}{2}\|x_0-\bar{x}_0\|_{P_{0}^{-1}}^{2}\right].
        \end{aligned}$$</p>

<p>Given a set of measurements $y_0, y_1, \ldots, y_{N-1}$ we need to estimate $x_0, x_1, \ldots, x_{N}$.</p>



## Useful results

<p>In what follows we use the convenient notation $x_{0:N}=(x_0, \ldots, x_N)$, and likewise we define $y_{0:N}$, $w_{0:N}$ and so on.</p>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition VI.1 (Joint distribution of outputs).</strong> Let $N\in{\rm I\!N}$. Then</p>
<p>$$p(y_{0:N})
        {}={}
        p(y_0)\prod_{t=1}^{N}p(y_t {}\mid{} y_{0:t-1}),$$</p>
<p>where $y_{0:t} = (y_0, \ldots, y_t)$.</p>
</div>

<br/>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition VI.2 (Joint distribution of states).</strong> For any $N\in{\rm I\!N}$</p>
<p>$$p(x_{0:N})
        {}={}
        p(x_0)\prod_{t=0}^{N-1}p_{w_t}(x_{t+1} - Ax_{t}).$$</p>
</div>

<br/>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition VI.3 (Joint distribution of states and $w$'s).</strong> For any $N\in{\rm I\!N}$</p>
<p>$$\begin{aligned}p(x_{0:N}, w_{0:N-1})
        {}={}
        \begin{cases}
            0,                                         & \text{if not } x_{t+1} = Ax_t + w_t,
            \\
            p_{x_0}(x_0)\prod_{t=0}^{N-1}p_{w_t}(w_t), & \text{otherwise}
        \end{cases}\end{aligned}$$</p>
</div>

<br/>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition VI.4 (Joint distribution of states given outputs).</strong> For any $N\in{\rm I\!N}$</p>
<p>$$\begin{aligned}p(x_{0:N} {}\mid{} y_{0:N-1})
            {}\propto{}
            p_{x_0}(x_0)\prod_{t=0}^{N-1}p_{v_t}(y_t - Cx_t)p_{w_t}(x_{t+1}-Ax_t).\end{aligned}$$</p>
</div>