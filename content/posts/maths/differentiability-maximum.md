---
author: "Pantelis Sopasakis"
title: Differentiability of pointwise maximum
date: 2022-08-21
description: Differentiability of pointwise maximum
summary: Some notes on the differentiability of the pointwise max of a family of functions and the Fritz-John and Mangasarian-Ffromowitz optimality conditions
mathjax: true
series: ["Mathematix"]
tags: ["Variational Analysis", "Convex Analysis", "Directional derivative", "Optimization"]
showtoc: false
---

<p>These are some notes on some differentiability properties of the maximum of a finite number of functions based on some results taken mainly from the book of Borwein and Lewis and Rockafellar and Wets's "Variational Analysis". </p>

## Directional Differentiability

{{< math.inline >}}
<p>Let $ X$ be a finite-dimensional real Euclidean space and $ g_i: C \to \mathbb{R}$ for $ i\in{0,1, \ldots N}$ are continuous functions, where $ C \subseteq X$ with a nonempty interior. It is convenient to define $ \mathcal{N} = \{0,1,\ldots, N\}$. Let $ \bar{x}$ be a point in the interior of $ C$. Define the function </p>

<p>$$\begin{align} g(x) = \max_{i\in\mathcal{N}}\{g_i(x)\}.\end{align}$$</p>

<p>Suppose that $ g_i$ are Gâteaux-differentiable at $ \bar{x}$.</p>

<p>For a function $ f: X \to \mathbb{R}$ we define its directional derivative at a point $ \bar{x}$ for a direction $ d \in X$ as the following one-sided limit, when it exists</p>

<p>$$\begin{align}f'(\bar{x}; d) = \lim_{t \downarrow 0} \frac{f(\bar{x} + td) - f(\bar{x})}{t}.\tag{$*$}\end{align}$$</p>

<p>The following proposition gives the directional derivative of $ g$ along a direction $ d\in X$.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 5px 0px 10px; margin-bottom: 10px"><p><strong>Proposition 1.</strong> Let $ \mathcal{I}_{\bar{x}} = \{i {}:{} g_i(\bar{x}) = g(\bar{x})\}$. Then, for all $ d\in X$ the directional derivative of $ g$ along the direction $ d$ is </p>
<p>$$\begin{align}g'(\bar{x}; d) = \max_{i\in\mathcal{I}_{\bar{x}}} {\langle \nabla g_i(\bar{x}), d\rangle}.\tag{1}\end{align}$$</p></div>

<p><em>Proof.</em> Let us have a look at the following figure</p>

<img src="https://mathematix.files.wordpress.com/2021/10/directional_derivative_max_1_v2.png?w=1024" alt="Function g and a point where some of the functions return the same (maximum) value while other ones give a smaller value. "/>

<p>At any point $ \bar{x}$ we have that $ g(\bar{x}) = g_i(\bar{x})$ for all $ i \in \mathcal{I}_{\bar{x}}$ and $ g(\bar{x}) > g_i(\bar{x})$ for all $ i \not\in \mathcal{I}_{\bar{x}}$. By the continuity of $ g_i$, there is a neighbourhood, $ \mathcal{U}_{\bar{x}}$, of $ \bar{x}$ where  $ g(x) > g_i(x)$, therefore the directional derivative at $ x$ is not affected by those $ g_i$ with $ i \not\in \mathcal{I}_{\bar{x}}$, so without loss of generality we can assume that $ \mathcal{I}_{\bar{x}} = \mathcal{N}$.</p>

<p>Next, we have that </p>

<p>$$\begin{align}\liminf_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t} {}\geq{}& \liminf_{t \downarrow 0} \frac{g_i(\bar{x} + td) - g(\bar{x})}{t} \\ {}={}& \liminf_{t \downarrow 0} \frac{g_i(\bar{x} + td) - g_i(\bar{x})}{t}\end{align}$$</p>

<p>that is,</p>

<p>$$\liminf_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t} {}\geq{} \left\langle \nabla g_i(\bar{x}), d \right\rangle.\tag{2}$$</p>

<p>It remains to show that </p>

<p>$$\begin{align}\limsup_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t} {}\leq{}& \left\langle \nabla g_i(\bar{x}), d \right\rangle,\tag{3}\end{align}$$</p>

<p>for all $ i$, or, what is the same</p>

<p>$$\begin{align}\limsup_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t} {}\leq{}& \max_{i\in\mathcal{N}}\left\langle \nabla g_i(\bar{x}), d \right\rangle.\end{align}$$</p>

<p>Instead, assume that</p>

<p>$$\begin{align}\limsup_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t} {}>{} \max_{i\in\mathcal{N}}\left\langle \nabla g_i(\bar{x}), d \right\rangle,\end{align}$$</p>

<p>that is, there is $ \epsilon > 0$ and a sequence $ (t_k)_k$ with $ t_k \downarrow 0$, such that</p>

<p>$$\begin{align}\frac{g(\bar{x} + t_k d) - g(\bar{x})}{t_k} {}\geq{} \max_{i\in\mathcal{N}}\left\langle \nabla g_i(\bar{x}), d \right\rangle + \epsilon.\end{align}$$</p>

<p>Let $ j_k$ (depends on $ t_k$) be such $ g(\bar{x} + t_k d) = g_{j_k}(\bar{x}_k + t_k d)$. Since $ (j_k)_k \subseteq \mathcal{N}$ (there are only finitely many such indices) there is a subsequence $ (t_{\nu_k})_{k \in \mathbb{N}}$ of $ (t_k)_{k\in\mathbb{N}}$ such that $ j_{\nu_k} = \iota$ (the same index), i.e.,</p>

<p>$$\begin{align}\frac{g_{\iota}(\bar{x} + t_{\nu_k} d) - g_{\iota}(\bar{x})}{t_{\nu_k}} {}\geq{} \max_{i\in\mathcal{N}}\left\langle \nabla g_i(\bar{x}), d \right\rangle + \epsilon.\end{align}$$</p>

<p>By taking the limit as $ \epsilon \downarrow 0$ on both sides, we have</p>

<p>$$\begin{align} \langle \nabla g_{\iota}(\bar{x}), d \rangle {}\geq{} \max_{i\in\mathcal{N}}\left\langle \nabla g_i(\bar{x}), d \right\rangle + \epsilon,\end{align}$$</p>

<p>which is a contradiction! Therefore,</p>

<p>$$\begin{align}\limsup_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t} {}\overset{(3)}{\leq}{} \max_{i\in\mathcal{N}}\left\langle \nabla g_i(\bar{x}), d \right\rangle {}\overset{(2)}{\leq}{} \liminf_{t \downarrow 0} \frac{g(\bar{x} + td) - g(\bar{x})}{t},\end{align}$$</p>

<p>which completes the proof. $ \blacksquare$</p>


<p><strong>Note:</strong> One should not assume that there exists a region of the form $ [0, \epsilon)$ for some $ \epsilon>0$ such that $ g(\bar{x} + \epsilon d) = g_{i}(\bar{x} + \epsilon d)$, for $ i \in \mathcal{I}_{\bar{x}}$. As a counterexample, consider the functions </p>

<p>$$\begin{align}g_1(x) {}={}& \begin{cases}x^3 \sin\tfrac{1}{x}, &\text{ for } x > 0, \\ 0, & \text{otherwise}\end{cases}, \\ g_2(x) {}={}& -g_1(x)\end{align}$$</p>

<img src="https://mathematix.files.wordpress.com/2021/10/g1g2.jpg?w=1024" alt="Functions g1 and g2 are differentiable at 0, but in all intervals of the form (0, ε), none of them dominates the other.">

<p>This is how the derivative of $g_1$ looks like:</p>

<img src="https://mathematix.files.wordpress.com/2021/10/g1_der-1.jpg?w=1024" alt="Derivative of g_1. The derivative at 0 is equal to 0.">

{{</ math.inline >}}





## Fritz John Optimality Conditions

{{< math.inline >}}
<p><a href="#prop1">Proposition 1</a> is very useful for proving the <a href="https://encyclopediaofmath.org/wiki/Fritz_John_condition" target="_blank">Fritz John optimality conditions</a> for constrained minimisation problems with differentiable constraints and cost function. Consider the following optimisation problem</p>

<p>$$\begin{align} \mathbb{P} {}:{} \mathrm{Minimise}_{x \in X} &f(x) \\ \text{subject to: } & g_i(x) \leq 0, i\in \mathcal{N}.\end{align}$$</p>

<p>For every $ x \in X$ such that $ g_i(x) \leq 0$ we define the set of active indices as $ \mathcal{I}(x) = \{i \in \mathcal{N} {}:{} g_i(x) = 0\}$.</p>

<p>Observation. The Fritz John optimality conditions rely on the realisation that if a point $ \bar{x}$ is a local minimiser of $ \mathbb{P}$ then it is a local minimiser of the following function </p>

<p>$$\begin{align} g(x) = \max\{f(x) - f(\bar{x}), g_i(x), i \in \mathcal{I}(\bar{x})\}.\end{align}$$</p>

<p>Indeed, since $ \bar{x}$ is a local minimum of $ \mathbb{P}$, there is a region of the form $ \mho_{\bar{x}, \epsilon} = \{x \in  X {}:{} g_i(x) \leq 0, \|x - \bar{x}\| < \epsilon\}$, for some $ \epsilon > 0$, such that $ f(x) \leq f(\bar{x})$ for all $ x\in\mho_{\bar{x}, \epsilon}$. Note that $ g(\bar{x}) = 0$ and for all $ x \in \mho_{\bar{x}, \epsilon}$, $ g(x) \leq g(\bar{x})$.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 5px 0px 10px; margin-bottom: 10px"><p><strong>Theorem 2 (Fritz John Optimality Conditions).</strong> Consider the optimisation problem $ \mathbb{P}$ where $ f$ and $ g_i$ are assumed to be differentiable at a point $ \bar{x}$ which is a local minimum of the problem. Then, there exist $ \lambda_0, \lambda_i \geq 0$, not all equal to 0, such that</p>
<p>$$\begin{align}\lambda_0 \nabla f(\bar{x}) + \sum_{i\in\mathcal{I}(\bar{x})}\lambda_i \nabla g_i(\bar{x}) = 0.\end{align}$$</p>
</div>

<p>Proof. As discussed above, since $ \bar{x}$ is a local minimiser of $ \mathbb{P}$ it is also a local minimiser of $ g$, therefore, for all directions $ d \in X$, $ g'(x; d) \geq 0$, that is</p>

<p>$$\begin{align}g'(x; d) = \max\{\langle \nabla f(\bar{x}), d \rangle, \langle \nabla g_i(\bar{x}), d \rangle, i \in \mathcal{I}(\bar{x})\} \geq 0.\end{align}$$</p>

<p>Equivalently, there is no $ d \in X$ such that </p>

<p>$$\begin{align}\langle \nabla f(\bar{x}), d \rangle < 0, \text{ and } \langle \nabla g_i(\bar{x}), d \rangle < 0.\end{align}$$</p>

<p>From Gordan's Theorem (essentially, by virtue of the <a href="https://en.wikipedia.org/wiki/Hyperplane_separation_theorem" target="_blank">hyperplane separation theorem</a>) the proof is complete. $ \blacksquare$</p>
{{</ math.inline >}}


## Mangasarian Fromowitz Optimality Conditions
{{< math.inline >}}
<p>From the Fritz John optimality conditions we conclude that either we have $ \lambda_0 \neq 0$ and </p>

<p>$$\begin{align}\nabla f(\bar{x}) + \sum_{i\in\mathcal{I}(\bar{x})}\tfrac{\lambda_i}{\lambda_0} \nabla g_i(\bar{x}) = 0,\end{align}$$</p>

<p>or, $ \lambda_0 = 0$ and the optimality conditions read</p>

<p>$$\begin{align}\sum_{i\in\mathcal{I}(\bar{x})} \lambda_i \nabla g_i(\bar{x}) = 0,\tag{4}\end{align}$$</p>

<p>which do not depend on the cost function. One could require that (4) should imply that $ \lambda_1 = \lambda_2 = \ldots = \lambda_m$, or in other words that the gradients $ \{\nabla g_i(\bar{x})\}_{i\in\mathcal{I}(\bar{x})}$ are linearly independent. According to Theorem 2, this would imply that $ \lambda_0 \neq 0$ (since not all lambdas can be equal to zero). These are the linear independence constraint qualifications aka LICQ.</p>

<p>An alternative approach is to require that there is a direction $ d \in X$ such that $ \langle \nabla g_i(\bar{x}), d \rangle < 0$ for all $ i \in \mathcal{I}(\bar{x})$. These are the Mangasarian-Fromowitz constraint qualifications (MFCQ), which are weaker than LICQ (LICQ implies MFCQ).</p>

<p>If MFCQ holds, then the case $ \lambda_0 = 0$ can be excluded, therefore we can find $ \lambda_i' = \lambda_i / \lambda_0 \geq 0$ such that $ \nabla f(\bar{x}) + \sum_{i\in\mathcal{I}(\bar{x})} \lambda_i' \nabla g_i(\bar{x}) = 0$. In other words, there is a Lagrange multiplier that corresponds to $ \bar{x}$.</p>
{{</ math.inline >}}



## Subdifferentiability
{{< math.inline >}}
<p>The subderivative of $ f$ at $ \bar{x}$ for $ d$ is given by</p>

<p>$$\begin{align}{\rm d}f(\bar{x})(d) = \lim_{t \downarrow 0, d' \to d}\frac{f(\bar{x} + td) - f(\bar{x})}{t}\tag{5}.\end{align}$$</p>

<p>It turns out that $ g(x) = \max_{i\in\mathcal{N}}\{g_i(x)\}$ is subdifferentiable with</p>

<p>$$\begin{align}{\rm d}f(\bar{x})(d) = f'(x; d) = \max_{i\in\mathcal{I}(\bar{x})}\{\left\langle\nabla g_i(x), d \right\rangle\}.\tag{6}\end{align}$$</p>

<p>This is Exercise 8.31 in Rockafellar and Wets's "Variational Analysis."</p>
{{</ math.inline >}}



## Regular Subgradient
{{< math.inline >}}
<p>For a function $ f : X \to \overline{\mathbb{R}}$  and a point $ \bar{x} \in X$ where $ f$ is finite, we say that a vector $ v \in X$ is a regular subgradient of $ f$ at $ \bar{x}$ (denoted as $ v \in \widehat{\partial}f(\bar{x})$) if</p>

<p>$$\begin{align}f(x) \geq f(\bar{x}) + \langle v, x - \bar{x}\rangle + o(\|x - \bar{x}\|),\end{align}$$</p>

<p>where the little-o notation is to be interpreted as </p>

<p>$$\begin{align}\liminf_{x \to \bar{x}, x \neq \bar{x}} \frac{f(x) - f(\bar{x}) - \langle v, x - \bar{x}\rangle }{\|x-\bar{x}\|} \geq 0.\end{align}$$</p>

<p>It can be shown that (Exercise 8.4 in [2])</p>

<p>$$\begin{align}\widehat{\partial}f(\bar{x}) {}={} \{v \in X {}:{} \langle v, w \rangle \leq {\rm d}f(\bar{x})(w), \forall w \in X\}.\end{align}$$</p>

<p>We will state this without a proof.</p>

<p>So going back to $ g(x) = \max_{i\in\mathcal{N}} \{g_i(x) \}$ with $ g_i:X \to \mathbb{R}$ being differentiable functions, we have</p>

<p>$$\begin{align}\widehat{\partial}g(\bar{x}) {}={}& \{v \in X {}:{} \langle v, w \rangle \leq {\rm d}g(\bar{x})(w), \forall w \in X\} \\ {}={}& \left\{v \in X {}:{} \langle v, w \rangle \leq \max_{i\in\mathcal{I}(\bar{x})} \langle \nabla g_i(\bar{x}), w\rangle, \forall w \in X\right\} \\ {}={}& \left\{v \in X {}:{} \max_{i\in\mathcal{I}(\bar{x})} \langle \nabla g_i(\bar{x}) - v, w\rangle \geq 0, \forall w \in X\right\}.\end{align}$$</p>

<p>It is straightforward to show that $ \mathrm{conv}\{\nabla g_i(x), i \in \mathcal{I}(\bar{x})\} \subseteq \widehat{\partial}f(\bar{x})$, where $ \mathrm{conv}$ denotes the convex hull. Then by virtue of the separation theorem, we can show that</p>

<p>$$\begin{align}\widehat{\partial}f(\bar{x}) {}={} \mathrm{conv}\{\nabla g_i(x), i \in \mathcal{I}(\bar{x})\},\end{align}$$</p>

<p>This has been shown for the convex subgradient of the pointwise maximum of a set of convex functions - see for example <a href="https://see.stanford.edu/materials/lsocoee364b/01-subgradients_notes.pdf" target="_blank">these lecture notes</a> (Section 3.4).</p>
{{</ math.inline >}}