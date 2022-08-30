---
author: "Pantelis Sopasakis"
title:  Projection on the epigraph of the squared Euclidean norm
draft: true
date: 2022-08-26
math: true
summary: How to project on the epigraph of the squared Euclidean norm
series: ["Mathematix"]
tags: ["Convex Analysis", "Optimization"]
showtoc: false
---

<p>Here we discuss how we can project on the epigraph of the squared norm function.</p>

<p>Define $f:{\rm I\!R}^n\to{\rm I\!R}:x\mapsto \|x\|^2$ with $\nabla f(x) = 2x$ and take $(z,\tau)\notin \mathrm{epi} f$.</p>

<p>Let $\Pi_f(z,\tau) = (\bar{x},\bar{s})$. Following the <a href="../projection-on-epigraph">previous post</a>, the optimality conditions are</p>

<p>$$\begin{aligned}z - \bar{x} &= 2(\|\bar{x}\|^2 - \tau)\bar{x},\\ \bar{s} &= \|\bar{x}\|^2.\end{aligned}$$</p>

<p>Then, the first optimality condition becomes</p>

<p>$$\begin{aligned}& z - \bar{x} = 2(\bar{s} - \tau)\bar{x}\\ \Leftrightarrow & \bar{x} = \frac{z}{1+2\bar{s}-2\tau}\end{aligned}$$</p>

<p>Then,</p>

<p>$$\begin{aligned}&\bar{s} = \|\bar{x}\|^2 = \left\| \frac{z}{1+\bar{s}-\tau} \right\|^2 = \frac{\|z\|^2}{(1+2\bar{s}-2\tau)^2} \\ \Leftrightarrow\ & \bar{s}(1+2\bar{s}-2\tau)^2 = \|z\|^2 \\ \Leftrightarrow\ & 4\bar{s}^3 + 4\theta \bar{s}^2 + \theta^2 \bar{s} - \|z\|^2 = 0,\end{aligned}$$</p>

<p>where $\theta = 1-2\tau$. This third-order polynomial equation can be solved numerically, it has a root $\bar{s}=\bar{s}(\theta, \|z\|^2)$ which satisfies the second optimality condition above. Once $\bar{s}$ has been determined, $\bar{x}$ can be computed.</p>

<p>The above can be trivially extended to the case where $f(x) = \sum_{i=1}^{n}\alpha_i x_i^2$, with $\alpha_i>0$. However, the projection onto the epigraph of $f(x) = x^\intercal P x$ where $P$ is a symmetric positive (semi)definite matrix is more complex, and we cannot derive explicit formulas in the general case.</p>

<p>Here is a simple MATLAB function to compute the projection onto the epigraph of the squared Euclidean norm efficiently:</p>

<script src="https://gist.github.com/alphaville/235495235fb0c1f378b021926a4dbb60.js"></script>