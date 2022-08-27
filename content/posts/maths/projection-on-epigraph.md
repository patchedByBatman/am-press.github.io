---
author: "Pantelis Sopasakis"
title:  Projections on epigraphs
draft: true
date: 2022-08-26
math: true
summary: How to project on the epigraph of a convex function
series: ["Mathematix"]
tags: ["Convex Analysis", "Optimization"]
showtoc: false
---

<p>Here we study the problem of projecting onto the epigraph of a convex continuous function. Unlike the computation of the proximal operator of a function or the projection on its sublevel sets, the projection onto epigraphs is more complex and there exist only a few functions for which semi-explicit formulas are available.</p>

## KKT Optimality Conditions

<p>Let $f:{\rm I\!R}^n\to{\rm I\!R}\cup\{\infty\}$ be a proper, convex, continuous function;  its epigraph is the nonemtpy convex closed set</p>

<p>$$
\begin{aligned}
\mathrm{epi} f := \{(x,\alpha) \in {\rm I\!R}^n\times {\rm I\!R} {}\mid{} f(x) \leq \alpha \}.
\end{aligned}
$$</p>

<p>For convenience, we define the projection of a pair $ (z,\tau)\in{\rm I\!R}^n\times {\rm I\!R}$ onto the epigraph of $ f$ as</p>

<p>$$
\begin{aligned}
\Pi_f(z,\tau) := \mathrm{proj}_{\mathrm{epi} f}(z,\tau).
\end{aligned}
$$</p>

<p>Let $ (z,\tau)\in{\rm I\!R}^n\times {\rm I\!R}$; if $ (z,\tau)\in\mathrm{epi} f$, then $ \Pi_f(z, \tau) = (z,\tau)$.</p> 
<p>Suppose $ (z,\tau)\notin\mathrm{epi} f$. Let $ \bar{x}=\bar{x}(z,\tau)$ and $ \bar{s}=\bar{s}(z,\tau)$ so that $ \Pi_f(z,\tau)=(\bar{x},\bar{s})$.</p> 


<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="prop2">
<p><strong>Proposition 1 (name).</strong> Let $f:{\rm I\!R}^n\to{\rm I\!R}\cup\{\infty\}$ be a proper, convex, continuous function. For a given $(z, \tau) \notin \mathrm{epi} f$, we have that $ \Pi_f(z,\tau)=(\bar{x},\bar{s})$ if and only if there is a $y \geq 0$ such that </p>
<p>$$
\begin{aligned}
f(\bar{x}) &\leq \bar{s}\\
\bar{y} (f(\bar{x})-\bar{s}) &= 0\\
z-\bar{x} &\in \bar{y} \partial f(\bar{x})\\
\tau - \bar{s} &= -\bar{y}.
\end{aligned}
$$</p>
</div>

<p>this pair solves the optimization problem</p>

<p>$$
\begin{aligned}
{\rm I\!P}(z, \tau) {}:{}
\operatorname*{Minimize}_{x,s:\ f(x)\leq s}\ \tfrac{1}{2}\|x-z\|^2 + \tfrac{1}{2}(s-\tau)^2.
\end{aligned}
$$</p>

<p>The KKT conditions for $ \bar{x},\bar{s}$ are</p>

<p>$$
\begin{aligned}
f(\bar{x}) &\leq \bar{s}\\
\exists \bar{y}\geq 0: \bar{y} (f(\bar{x})-\bar{s}) &= 0\\
z-\bar{x} &\in \bar{y} \partial f(\bar{x})\\
\tau - \bar{s} &= -\bar{y}.
\end{aligned}
$$</p>

<p>Clearly, $ \bar{y}>0$ since $ (z,\tau)\notin \mathrm{epi} f$. Then, because of the second condition, $ \bar{s} = f(\bar{x})$ and, because of the fourth condition, $ \bar{y}=f(\bar{x})-\tau$, so the third condition yields</p>

<p>$$
\begin{aligned}
z-\bar{x} \in (f(\bar{x})-\tau) \partial f(\bar{x}).
\end{aligned}
$$</p>

<p>It might be necessary to employ numerical methods to solve the optimality conditions.</p>

## Dual epigraphical projection

<p>Consider again the optimization problem which defined the epigraphical projection. We introduce the Lagrangian</p>

<p>$$
\begin{aligned}
\mathcal{L}(x,s,y) = \tfrac{1}{2}\|x-z\|^2 + \tfrac{1}{2}(s-\tau)^2 + y(f(x)-s).
\end{aligned}$$</p>

<p>We compute the partial subdifferentials of $ \mathcal{L}$ with respect to the primal variables $ (x,s)$:</p>

<p>$$
\begin{aligned}
\partial_x\mathcal{L}(x,s,y) &= x - z + y\partial f(x)\\
\partial_s\mathcal{L}(x,s,y) &= s - \tau - y.
\end{aligned}$$</p>

<p>The dual function $ q$  is defined as</p>

<p>$$ q(y) = \inf_{x,s}\mathcal{L}(x,s,y).$$</p>

<p>The optimality conditions for the optimization problem which defines the dual function are $ 0\in \partial_x\mathcal{L}(x,s,y)$ and $ 0\in\partial_s\mathcal{L}(x,s,y)$, therefore, $ q(y)=\mathcal{L}(x^\star(y), s^\star(y), y)$ with</p>

<p>$$
\begin{aligned}
&0 \in x-z+y\partial f(x^\star)\\
\Leftrightarrow\ &0 \in (I+y\partial f)(x^\star) - z\\
\Leftrightarrow\ &z \in (I+y\partial f)(x^\star)\\
\Leftrightarrow\ &x^\star(y) = (I+y\partial f)^{-1}(z)\\
\Leftrightarrow\ &x^\star(y) = \mathrm{prox}_{yf}(z),
\end{aligned}$$</p>
<p>and</p>
<p>$$\begin{aligned}s^\star(y) = \tau + y.\end{aligned}$$</p>

<p>Then, the Lagrangian dual function becomes</p>

<p>$$
\begin{aligned}
q(y) &= \mathcal{L}(x^\star(y), s^\star(y), y)\\
&= \tfrac{1}{2}\|\mathrm{prox}_{yf}(z)-z\|^2 + y f(\mathrm{prox}_{yf}(z)) + \tfrac{y^2}{2} - sy\\
&= y f^y(z) + \tfrac{y^2}{2} -(\tau+y)y\\
&= y (f^y(z) - \tfrac{y}{2} -s),
\end{aligned}$$</p>
<p>where $ f^y$ is the Moreau envelope function of $ f$ with parameter $ y$.  Then, the dual problem is the following 1-dimensional optimization problem</p>

<p>$$
\begin{aligned}
\operatorname*{Maximize}_{y\geq 0}\ q(y).
\end{aligned}$$</p>

## Via proximal operator

<p>We take the infimum which corresponds to the optimization problem that defines the projection on the epigraph and we have</p>

<p>$$\begin{aligned}
&\inf_{x,s: f(x) \leq s} \left\{ \tfrac{1}{2}\|z-x\|^2 + \tfrac{1}{2}(s-\tau)^2\right\}\\
=&\inf_{x,\xi\geq 0: f(x) \leq \tau + \xi} \left\{ \tfrac{1}{2}\|z-x\|^2 + \tfrac{1}{2}\xi^2\right\}\\
=&\inf_{x,\xi\geq 0: f(x) - \tau \leq  \xi} \left\{ \tfrac{1}{2}\|z-x\|^2 + \tfrac{1}{2}\xi^2\right\}\\
=&\inf_{x} \left\{ \tfrac{1}{2}\|z-x\|^2 + \tfrac{1}{2}\max\{0, f(x) - \tau\}^2\right\},
\end{aligned}$$</p>

<p>where we have done the converse of an epigraphical relaxation; we define the function $h(x) = \max\{0, f(x) - \tau\}^2$ and notice that this is minimized at</p>

<p>$$\bar{x} = \mathrm{prox}_{h}(z),$$</p>

<p>and $\bar{s} = \max\{\tau, f(\bar{x})\}$. This is of course only useful to the extent that $\mathrm{prox}_{h}$ is computable.</p>


