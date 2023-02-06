---
author: "Pantelis Sopasakis"
title:  Projections on epigraphs
date: 2023-02-15
math: true
summary: How to project on the epigraph of a convex function
series: ["Mathematix"]
tags: ["Convex Analysis", "Optimization"]
showtoc: true
collapsible: true
---

<p>Here we study the problem of projecting onto the epigraph of a convex continuous function. Unlike the computation of the proximal operator of a function or the projection on its sublevel sets, the projection onto epigraphs is more complex and there exist only a few functions for which semi-explicit formulas are available.</p>

## KKT Optimality Conditions

<p>Let $f:{\rm I\!R}^n\to{\rm I\!R}\cup\{\infty\}$ be a proper, convex, continuous function;  its epigraph is the nonemtpy convex closed set</p>

<p>$$
\begin{aligned}
\mathrm{epi} f := \{(x,t) \in {\rm I\!R}^n\times {\rm I\!R} {}\mid{} f(x) \leq t \}.
\end{aligned}
$$</p>

<p>For convenience, we define the projection of a pair $ (x, t)\in{\rm I\!R}^n\times {\rm I\!R}$ onto the epigraph of $ f$ as</p>
<p>$$\begin{aligned}
\Pi_f(x, t) := \mathrm{proj}_{\mathrm{epi} f}(x, t).
\end{aligned}$$</p>

<p>Let $ (x, t)\in{\rm I\!R}^n\times {\rm I\!R}$. If $ (x, t)\in\mathrm{epi} f$, then $\Pi_f(x, t) = (x, t)$.</p> 
<p>Suppose $(x, t)\notin\mathrm{epi} f$. Let $x^{\star}=x^{\star}(x, t)$ and $t^{\star}=t^{\star}(x, t)$ so that $\Pi_f(x, t)=(x^{\star}, t^{\star})$.</p> 


<div style="border-style:solid;border-width:1.5px;padding: 10px 10px 0px 12px; margin-bottom: 10px" id="prop1">
<p><strong>Proposition 1 (Optimality conditions).</strong> Let $f:{\rm I\!R}^n\to{\rm I\!R}\cup\{\infty\}$ be a proper, convex, continuous function. For a given $(x, t) \notin \mathrm{epi} f$, we have that $\Pi_f(x,t)=(x^{\star}, t^{\star})$ if and only if</p>
<p id="eq1">$$\begin{aligned}x - x^{\star} {}\in{} (f(x^{\star})-t) \partial f(x^{\star}),\tag{1}\end{aligned}$$</p>
<p>and $f(x^{\star}) {}={} t^{\star}.$</p>
</div>

<button onclick="toggleCollapseExpand('proofProp1Button', 'proofProp1Container', 'Proof')" id="proofProp1Button">
  <i class="fa fa-cog fa-spin"></i> Click to reveal the proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px; " id="proofProp1Container">
<p><em>Proof.</em> Given a pair \((x, t)\), the pair $(x^{\star}, t^{\star})$ solves the optimization problem</p>
<p>$$
\begin{aligned}{\rm I\!P}(x, t) {}:{}\operatorname*{Minimize}_{\chi, \tau :\ f(\chi)\leq \tau}\ \tfrac{1}{2}\|\chi-x\|^2 + \tfrac{1}{2}(\tau-t)^2.\end{aligned}$$</p>
<p>The KKT conditions of this problem are</p>
<p>$$\begin{aligned}f(x^{\star}) &\leq t^{\star}\\\exists y^{\star}\geq 0: y^{\star} (f(x^{\star})-t^{\star}) &= 0\\x-x^{\star} &\in y^{\star} \partial f(x^{\star})\\t - t^{\star} &= -y^{\star}.\end{aligned}$$</p>

<p>Clearly, $y^{\star}>0$ since $(x,t)\notin \mathrm{epi} f$. Then, because of the second condition, $t^{\star} = f(x^{\star})$ and, because of the fourth condition, $y^{\star}=f(x^{\star})-t$, so the third condition yields Equation <a href="#eq1">(1)</a>. $\blacksquare$</p>
</div>

<p></p>
<p>It might be necessary to employ numerical methods to solve the optimality conditions.</p>



## Dual epigraphical projection


<div style="border-style:solid;border-width:1.5px;padding: 10px 10px 0px 12px; margin-bottom: 10px" id="prop2">
<p><strong>Proposition 2 (Dual problem).</strong> The dual problem is</p>
<p>$$
\begin{aligned}
\operatorname*{Maximize}_{y\geq 0}\ q(y) \coloneqq y (f^y(x) - \tfrac{y}{2} -t),
\end{aligned}$$</p>
<p>where $f^y$ is the Moreau envelope of $f$ with parameter $y$.</p>
</div>

<p>Consider again the optimization problem ${\rm I\!P}(x, t)$ which defines the epigraphical projection. We introduce the Lagrangian</p>

<p>$$
\begin{aligned}
\mathcal{L}(\chi,\tau, y) = \tfrac{1}{2}\|\chi - x\|^2 + \tfrac{1}{2}(\tau - t)^2 + y(f(x)-\tau).
\end{aligned}$$</p>

<p>We compute the partial subdifferentials of $\mathcal{L}$ with respect to the primal variables $ (\chi, \tau)$:</p>

<p>$$
\begin{aligned}
\partial_{\chi}\mathcal{L}(\chi, \tau, y) &= \chi - x + y\partial f(x),\\
\partial_{\tau}\mathcal{L}(\chi, \tau, y) &= \tau - t - y.
\end{aligned}$$</p>

<p>The dual function $ q$  is defined as</p>

<p>$$ q(y) = \inf_{x,s}\mathcal{L}(\chi, \tau, y).$$</p>

<p>The optimality conditions for the optimization problem which defines the dual function are $ 0\in \partial_x\mathcal{L}(\chi, \tau, y)$ and $ 0\in\partial_{\tau}\mathcal{L}(\chi, \tau, y)$, therefore, $ q(y)=\mathcal{L}(x^\star(y), t^\star(y), y)$ with</p>

<p>$$
\begin{aligned}
&0 \in x^\star - x + y \partial f(x^\star)\\
\Leftrightarrow\ &0 \in (I+y \partial f)(x^\star) - x\\
\Leftrightarrow\ &x \in (I+y \partial f)(x^\star)\\
\Leftrightarrow\ &x^\star(y) = (I+y \partial f)^{-1}(x)\\
\Leftrightarrow\ &x^\star(y) = \mathrm{prox}_{yf}(x),
\end{aligned}$$</p>
<p>and</p>
<p>$$\begin{aligned}t^\star(y) = t + y.\end{aligned}$$</p>

<p>Then, the Lagrangian dual function becomes</p>

<p>$$
\begin{aligned}
q(y) &= \mathcal{L}(x^\star(y), s^\star(y), y)\\
&= \tfrac{1}{2}\|\mathrm{prox}_{yf}(x)-x\|^2 + y f(\mathrm{prox}_{yf}(x)) + \frac{y^2}{2} - ty\\
&= y f^y(x) + \tfrac{y^2}{2} -(t+y)y\\
&= y (f^y(x) - \tfrac{y}{2} -t),
\end{aligned}$$</p>
<p>where $f^y$ is the <em>Moreau envelope</em> function of $f$ with parameter $y$.  Then, the dual problem is the following one-dimensional optimization problem</p>

<p>$$
\begin{aligned}
\operatorname*{Maximize}_{y\geq 0}\ q(y).
\end{aligned}$$</p>




## Via proximal operator


<div style="border-style:solid;border-width:1.5px;padding: 10px 10px 0px 12px; margin-bottom: 10px" id="prop3">
<p><strong>Proposition 3 (Projection on epigraph).</strong> Let $f:{\rm I\!R}^n\to{\rm I\!R}\cup\{\infty\}$ be a proper, convex, continuous function. For a given $(x, t) \notin \mathrm{epi} f$ and $ \Pi_f(x, t)=(x^{\star},t^{\star})$. Define $h_{t}(x) = \tfrac{1}{2}\max\{0, f(x) - t\}^2$. Then</p>
<p>$$\begin{aligned}x^{\star} {}={}& \mathrm{prox}_{h_{t}}(x), \\ t^{\star} {}={}& f(x^{\star}).\end{aligned}$$</p>
</div>

<p>We take the infimum which corresponds to the optimization problem that defines the projection on the epigraph and we have</p>

<p>$$\begin{aligned}
&\inf_{\chi, \tau: f(\chi) \leq \tau} \left\{ \tfrac{1}{2}\|\chi - x\|^2 + \tfrac{1}{2}(\tau - t)^2\right\}\\
=&\inf_{\substack{x,\tau,\xi\geq 0 \\ f(\chi) \leq \tau, \tau - t \leq \xi}} \left\{ \tfrac{1}{2}\|\chi - x\|^2 + \tfrac{1}{2}\xi^2\right\}\\
=&\inf_{\chi,\xi\geq 0: f(\chi) \leq t + \xi} \left\{ \tfrac{1}{2}\|\chi - x\|^2 + \tfrac{1}{2}\xi^2\right\}\\
=&\inf_{\chi,\xi\geq 0: f(\chi) - t \leq  \xi} \left\{ \tfrac{1}{2}\|\chi - x\|^2 + \tfrac{1}{2}\xi^2\right\}\\
=&\inf_{\chi} \left\{ \tfrac{1}{2}\|\chi - x\|^2 + \underbrace{\tfrac{1}{2}\max\{0, f(\chi) - t\}^2}_{h_t(\chi)}\right\} \\
=&\inf_{\chi} \left\{ \tfrac{1}{2}\|\chi - x\|^2 + h_{t}(\chi)\right\},
\end{aligned}$$</p>
<p>and we notice that this is minimized at $x^{\star} = \mathrm{prox}_{h_{s}}(x),$ and as we know from <a href="#prop1">Proposition 1</a>. $\blacksquare$</p>


## Projection on epigraph of exponential function

<p>Let $f(x)=e^x$. Then, from <a href="#prop1">Proposition 1</a> we have that if $e^x > t$, the projection $(x^\star, t^{\star})$  satisfies</p>
<p id="eq2">$$x-x^{\star} = (e^{x^{\star}} - t)e^{x^{\star}}.\tag{2}$$</p>
<p>If $t = 0$, the solution of the above equation is </p>
<p id="eq3">$$x^{\star} = x - \tfrac{1}{2} W_0(2e^{2x}),\tag{3}$$</p>
<p>where $W_0$ is the <a href="https://en.wikipedia.org/wiki/Lambert_W_function">Lambert $W$</a> function. In a nutshell,</p>
<p>$$\Pi_{f}(z, 0) = \left(x^{\star}, \exp(x^{\star})\right),$$</p>
<p>where $x^{\star}$ is given by Equation <a href="#eq3">(3)</a>, that is,</p>
<p>$$\Pi_{f}(x, 0) = \left(x - \tfrac{1}{2} W_0(2e^{2x}), \exp\left(x - \tfrac{1}{2} W_0(2e^{2x})\right)\right).$$</p>

<div id="fig-1">
<img src="/proj-on-exp.jpg" alt="Projection on the epigraph of the exponential function of points on the x axis" style="width: 75%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 1.</strong> Projection of some points $(x, 0)$ on the epigraph of $f(x) = e^x$.</em></p>
</div> <!-- end of figure 1 -->

<p>In the more general case, Equation <a href="#eq2">(2)</a> can be solved numerically. </p>

<div id="fig-1">
<img src="/proj-on-exp2.jpg" alt="Projection on the epigraph of the exponential function" style="width: 75%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 2.</strong> Projection of some points $(x, t)$ on the epigraph of $f(x) = e^x$.</em></p>
</div> <!-- end of figure 1 -->

