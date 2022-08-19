---
author: "Pantelis Sopasakis"
title: Normal and tangent cones
date: 202-00-19
description: Support functions, tangent and normal cones; the basics of convex analysis
summary: Useful convex analysis stuff
math: true
ShowBreadCrumbs: false
series: ["Mathematix"]
tags: ["Convex Analysis"]
---

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}

<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}


This is a collection of some simple, yet useful results from convex analysis. We will give examples of support functions of convex sets, and normal cones. Of course special focus will be given to the two most popular sets of convex analysis: balls (Euclidean balls and ellipsoids) and polyhedra.

## 0. Introduction and Notation

{{< math.inline >}}
<p>We denote by \(\overline{\mathbb{R}}=\mathbb{R} \cup \{\infty\}\) Given a function \(f:\mathbb{R}^n \to \overline{\mathbb{R}}\), its epigraph is the set \(\mathrm{epi} f = \{(x, t): f(x) \leq t\}\) and its domain is the set \(\mathrm{dom} f = \{x\in \mathbb{R}^n: f(x) < \infty\}.\) A function is called closed if its epigraph is closed.</p>

<p>A set \( K\) is a cone if for every \( \lambda \geq 0\) and \( x \in K\), \( \lambda x \in K.\) Given a cone \( K\), the dual cone is denoted by \( K^*=\{z\in\mathbb{R}^n: \langle z, x\rangle \geq 0, \forall x\in K\}\) and the polar cone is \( K^\circ = -K^*.\) Note that the notation \( K^\circ\) and \( K^\circ\), and even the term polar cone, are used differently by different authors.</p>

<p>The convex hull of a set \( C\) is the smallest convex set that contains \( C\) and is denoted by \( \mathrm{conv}(C).\) It is</p>

<p>$$\mathrm{conv}(C) = \left\{\sum_{i=1}^{k}\alpha_k x_k, x_i\in C, \alpha_i\geq 0, \forall i=1,\ldots, k, \sum_{i=1}^{k}\alpha_1 = 1\right\}.$$</p>
<!--more-->


<p>The convex hull of a collection of sets is the convex hull of their union.</p>

<p>The convex hull of a function \( f:\mathbb{R}^n \to \overline{\mathbb{R}}\) is the largest convex function that lower bounds \( f\). It is a function \( \mathrm{conv} f:\mathbb{R}^n \to \overline{\mathbb{R}}\) whose epigraph is the convex hull of the epigraph of \( f\), that is, \( \mathrm{epi}\;\mathrm{conv}\;{}f = \mathrm{conv}\;\mathrm{epi} f.\) This means that \( \mathrm{conv}f(x) \leq t\) if and only if there exist \( x_1,\ldots, x_k \in \mathbb{R}^n\) and \( t_1,\ldots, t_k \in \mathbb{R}\) and scalars \( \alpha_1,\ldots, \alpha_k \geq 0\) with \( \sum_{i=1}^k\alpha_i = 1\) such that \( f(x_i) \leq t_i\) for all \( i\).</p>

<p>The convex hull of a collection of functions, \( f_i: \mathbb{R}^n \to \overline{\mathbb{R}}\) with \( i\in I\) is a function \( f := \mathrm{conv}(f_i)_i\) with \( \mathrm{epi} f = \mathrm{conv}\bigcup_{i\in I}\mathrm{epi}f_i.\)</p>

<p>The conic hull of a set \( C \subseteq \mathbb{R}^n\) is the smallest cone that contains \( C\) and it is \( \mathrm{cone}(C) = \{y = c_1x_1 + y_2 x_2 + \ldots + c_k x_i\in C, c_i \geq 0, i=1,\ldots,k \}.\)</p>

<p>The Minkowski sum of two sets is denoted by \( A \oplus B = \{a + b: a\in A, b\in B\}.\) The interior, relative interior and closure of a set \( C\) are denoted by \( \mathrm{int}(C)\), \( \mathrm{relint}(C)\) and \( \mathrm{cl}(C)\).</p>
{{</ math.inline >}}

---

## 1. Support Functions
{{< math.inline >}}
<p>Let us start by stating the definition of the support function:</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Definition 1.1 (Support Function).</strong> The support function of a nonempty set \(C \subseteq \mathbb{R}^n\) is defined as the function \(\delta^*_C(y) = \sup_{x\in C}\langle y, x\rangle\).
</p>
</div>

<p>In convex analysis, the support function plays a central role. Inter alia, it can be used to tell (i) whether a set is a subset of another, (ii) whether a point is in the interior, (iii) relative interior, or (iv) affine hull of a set. The following proposition summarises some of the most important properties of the support function of convex sets.</p>


<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;" id="prop12">
<p><strong>Proposition 1.2 (Properties of the support function).</strong> Let \( A, B, (A_i)_{i\in I}\) be nonempty and convex subsets of \( \mathbb{R}^n\). The following hold:</p>
<ol>
<li>\( \delta_A^*\) is the convex conjugate of the indicator function of \( A\).</li>
<li> Then, \( \delta_A^*\) is positively homogeneous, closed, and convex. Conversely, every positive homogeneous, closed and convex function is the support function of a closed convex set.</li>
<li> If \( A \subseteq B\), then \( \delta_A^* \leq \delta_B^*\)</li>
<li>If \( \delta_A^* \leq \delta_B^*\), then \( \mathrm{cl}A \subseteq \mathrm{cl}B\)</li>
<li>\( \delta_A^* = \delta_{\mathrm{cl} A}^*\)</li>
<li>\( \mathrm{cl}A=\{x\in\mathbb{R}^n: \langle x, y\rangle \leq \delta_A^*(y), \forall y \in \mathbb{R}^n\}\)</li>
<li>\( \mathrm{dom}\delta_A^* = \mathbb{R}^n\) if and only if \( A\) is bounded</li>
<li>Let \( C = aA {}\oplus{} bB\) with \( a,b \geq 0\). Then \( \delta_C^* = a\delta_A^* + b\delta_B^*\)</li>
<li>\( \delta_{-A}^*(y) = \delta_A^*(-y)\)</li>
<li>Let \( A = \mathrm{conv}\bigcup_{i\in I}A_i\). Then \( \delta_A^* = \sup_{i\in I}\delta_{A_i}^*\)</li>
<li>Suppose that \( A = \bigcap_{i\in I}A_i\) is nonconvex. Then \( \delta_A^* = \mathrm{cl}\; \mathrm{conv} (\delta_{A_i}^*)_i\), where \( \mathrm{conv}\) denotes the convex hull of a collection of functions</li>
<li>If \( A\) is a convex cone, then \( \delta^*_{A} = \delta_{A^\circ}\)</li>
<li>\( 0 \in A\) if and only if \( \delta_A^*\geq 0\)</li>
<li>Let \( L:\mathbb{R}^n\to\mathbb{R}^m\) be a linear operator with adjoint \( L^*\) with respect to an inner product \( \langle \cdot, \cdot \rangle\). Then \( \delta_{\mathrm{cl}L(A)}^*(y) = \delta_{A}^*(L^*y)\)</li>
</ol>
</div>

<br>
<p>It is easy to see that \( \delta_{\{x_0\}}(y) = \langle x_0, y\rangle\), so from <a href="#prop12">Proposition 1.2(8)</a> we see that \( \delta_{A + x_0}^*(y) = \delta_A^*(y) + \langle x_0, y\rangle\).</p>

{{</ math.inline >}}



### 1.1. Support function of unit norm ball
{{< math.inline >}}
<p>Let \( C = \{x\in\mathbb{R}^n : \|x\| \leq 1\}\). Then</p>

$$\delta^*_C(y) = \sup_{\|x\|\leq 1}\langle y, x\rangle = \|y\|_*,$$

<p>that is, the support function of a norm-ball is the dual norm. For instance, if \( C = \{x: \|x\|_2 \leq 1\}\), then \( \delta^*(y) = \|y\|_2\). If \( C = \{x: \|x\|_1 \leq 1\}\), then \( \delta^*(y) = \|y\|_\infty\), and if \( C = \{x: \|x\|_\infty \leq 1\}\), then \( \delta^*(y) = \|y\|_1\).</p>

<p>More generally, we can see from <a href="#prop12">Proposition 1.2(8)</a> that</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 1.3 (Support function of norm-ball).</strong> For a \( \|\cdot\|\)-ball of radius \( r&gt;0\), \( \delta_{\mathcal{B}_r}^*(y) = r\|y\|_*\).
</p>
</div>
{{</ math.inline >}}

### 1.2. Support function of a polyhedron
{{< math.inline >}}
<p>If \( C\) is a polytope, then by the Minkowski-Weyl theorem there are \( a_1, \ldots, a_p\) such that \( C = \mathrm{conv}(\{a_1, \ldots, a_p\})\). This has the form mentioned in <a href="prop12">Proposition 1.2(10)</a>, leading to the following result.</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;" id="prop14">
<p>
<strong>Proposition 1.4 (Support function of polytope).</strong> Consider the polytope \( A = \mathrm{conv}(\{a_1, \ldots, a_p\})\) (given in its V-representation). Then 
</p>
<p>\( \begin{aligned}\delta_A^*(y) = \max_{i=1,\ldots, p}\langle a_i, y\rangle\end{aligned}\)</p>
</div>

<p>More generally, a set \( C\) is polyhedral if and only if it is the Minkowski sum of a polytope and a finitely generated cone, that is</p> 

$$\begin{aligned}C = \mathrm{conv}(\{a_1,\ldots a_p\}) \oplus \mathrm{cone}(\{b_1, \ldots, b_r\}).\end{aligned}$$

<p>This is known as the <strong>Weyl-Minkowski representation</strong> of the set. Given <a href="prop12">Proposition 1.2(8)</a> and 1.2(12) and <a href="prop14">Proposition 1.4</a> the following result follows suit:</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;" id="prop15">
<p>
<strong>Proposition 1.5 (Support function of polyhedron 1).</strong> Let \( C\) be a polyhderal set. Then, there are vectors \( (a_i)_{i=1}^{p}\) and \( (b_i)_{i=1}^{r}\) such that \( C = P \oplus K\) where \( P=\mathrm{conv}(\{a_1,\ldots a_p\}) \) and \( K = \mathrm{cone}(\{b_1, \ldots, b_r\}).\) Then,
</p>
<p>$$\begin{aligned}\delta_C^*(y) = \max_{i=1,\ldots, p}\langle a_i, y\rangle +  \delta_{K^\circ}(y),\end{aligned}$$</p>
<p>where \( K^\circ = \{x \in\mathbb{R}^n: \langle b_i, x\rangle \leq 0, i=1,\ldots, r\}\).</p>
</div>

<p>Halfspaces are special cases of <a href="#prop15">Proposition 1.5</a>. In particular if \( C = \{x\in\mathbb{R}^n: \langle a, x\rangle \leq b\}\) we can write \( C = x_0 + K,\) where \( K = {x\in\mathbb{R}^n: \langle a, x\rangle \leq 0}\) and \( \langle a, x_0 \rangle = b\). We can show that</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 1.6 (Support function of halfspace).</strong> Let \( C = \{x\in\mathbb{R}^n : \langle a, x\rangle \leq b\}\) be a halfspace. Then,</p>
<p>\( \begin{aligned}\delta^*_C(y) = \begin{cases}\lambda b, &amp;\text{ if } y=\lambda a, \lambda \geq 0 \\ \infty, &amp;\text{ otherwise}\end{cases}\end{aligned}\)</p>
</div>

<p><em>Proof.</em> To prove this, let us first write \( C = K + x_0\) where \( K = \{x\in \mathbb{R}^n : \langle a, x\rangle \leq 0\}\) and \( x_0\) is a vector such that \( \langle a, x_0\rangle = b\) (the reader can verify this as an exercise).  Note that \( K\) is a cone (a homogeneous halfspace). Then, from <a href="prop12">Proposition 1.2(8)</a>, \( \delta_C^*(y) = \delta_K^*(y) + \langle x_0, y\rangle\) and \( \delta_K^*(y) = \delta_{K^\circ}(y)\). The polar of \( K\) is given by</p>

$$\begin{aligned}K^\circ {}={}& \{ y\in\mathbb{R}^n : \langle y, x\rangle 0, \forall x\in K\}    \\    {}={}& \{ y\in\mathbb{R}^n : \langle y, x\rangle 0, \forall x\in \mathbb{R}^n : \langle a, x\rangle \leq 0\}    \\    {}\subseteq{}& \{  y\in\mathbb{R}^n : \langle y, x_1\rangle \leq 0, \langle y, -x_1\rangle \leq 0, \text{ where } \langle a, x_1 \rangle = 0, x_1 \neq 0  \} \\ {}={}& \mathrm{span}(\{a\}), \end{aligned}$$

<p>but \( K^\circ \subseteq K^\circ\), so \( K^\circ \subseteq \mathrm{cone}(\{a\})\). It is easy to show that \( K^\circ \supseteq \mathrm{cone}(\{a\})\). As a result \( K^\circ {}={} \mathrm{cone}(\{a\})\), so \( \delta_C^*(y) = \delta_{\mathrm{cone}(\{a\})}(y) + \langle x_0, y \rangle,\) which proves the assertion. \(\Box\)</p>

<p>Given that a polyhedron can be written as an intersection of finitely many halfspaces (in its H representation), in light of <a href="prop12">Proposition 1.2(11)</a> we have the following result.</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 1.7 (Support function of polyhedron 2).</strong> Let \( C = \{x\in\mathbb{R}^n : Ax \leq b\}\) be a polyhedron - or, equivalently \( C = \{x\in\mathbb{R}^n : \langle a_i, x\rangle \leq b, i=1,\ldots, p\}\). Then, if \( y \in \mathrm{cone}(\{a_1, \ldots, a_p\})\)</p>
<p>\( \begin{aligned}\delta^*_C(y) =&amp; \min\{t : t\geq c_1 b_1 + \ldots + c_p b_p: y=c_1 a_1 + \ldots + c_p a_p, c_1,\ldots, c_p \geq 0\} \\ =&amp; \min\{c_1 b_1 + \ldots + c_p b_p: y=c_1 a_1 + \ldots + c_p a_p, c_1,\ldots, c_p \geq 0\} \\ =&amp; \min\{b^\intercal c: A^\intercal c = y, c \geq 0\},\end{aligned}\)</p>
<p>while \( \mathrm{dom}\delta^*_C = \mathrm{cone}(\{a_1, \ldots, a_p\})\).</p>
</div>

<p><em>Proof.</em> Note that \( C\) can be written as</p>

$$\begin{aligned}C = \bigcap_{i=1}^{p}\{x\in\mathbb{R}^n : \langle a_i, x\rangle \leq b\}.\end{aligned}$$

<p>Define \( C_i = \{x\in\mathbb{R}^n : \langle a_i, x\rangle \leq b\}\). By virtue of <a href="prop12">Proposition 1.2(11)</a>,  \( \delta_C^* = \mathrm{cl}\; \mathrm{conv}(\delta_{C_i}^*).\) From <a href="prop12">Proposition 1.2(2)</a>, \( \mathrm{epi}\delta_{C_i}^*\) are closed sets, so their union is closed, therefore, \(  \delta_C^* = \mathrm{conv}(\delta_{C_i}^*).\)</p>

<p>Firstly note that \( (y, t) \in \mathrm{epi}\delta_{C_i}^*\) if and only if \( y = \lambda a_1\) for some \( \lambda\geq 0\) and \( \lambda b_i \leq t.\)</p>

<p>From the definition of the convex hull of a collection of functions (see Section 0) we have that \( \delta_C^*(y) \leq t\) if and only if there exist \( \alpha_1, \ldots, \alpha_p \geq 0\) with \( \alpha_1+\ldots + \alpha_p = 1\) and \( y=\alpha_1 y_1 + \ldots + \alpha_p y_p\), \( t = \alpha_1 t_1 + \ldots + \alpha_p t_p\) such that \( y_j = \lambda_j \alpha_j\), \( \lambda_j \geq 0\) and \( \lambda_j b_j \leq t_j\) for \( j=1,\ldots, k\). Let \( c_j = \alpha_j \lambda_j \geq 0\). We see that these conditions are equivalent to \( y = c_1 a_1 + \ldots + c_p a_p\) and \( t \geq c_1 b_1 + \ldots + c_p b_p\). This proves the assertion. \(\Box\)</p>

<p><em>Remark.</em> Note that the determination of the support function of the polyhedral set \( C = \{x\in\mathbb{R}^n: Ax \leq b\}\) is equivalent to solving the linear program</p>

$$\begin{aligned}\mathrm{Minimise}_c \ & b^\top c \\ \text{s.t. } &A^\intercal c = y, \\ & c \geq 0\end{aligned}$$

<p>Note that this is precisely the dual LP that corresponds to the definition of the support function of a polyhedral set (which is an LP).</p>
{{</ math.inline >}}



## 2. Normal and Tangent Cones

{{< math.inline >}}
<p>In this section we will focus only nonempty closed and convex sets. Rockafellar and Wets in [2] provide an excellent treatment of the more general case of nonconvex and not necessarily closed sets.</p>

<p>Let \( C\subseteq \mathbb{R}^n\) be a nonempty closed convex set and let \( \bar{x} \in C\). A \( d \in \mathbb{R}^n\) is said to be a normal vector to \( C\) at \( \bar{x}\) if \( \langle d, x - \bar{x}\rangle\leq 0\) for all \( x \in C\). The set of normal vectors to \( C\) at \( \bar{x}\) is denoted by \( N_C(\bar{x})\) and can be easily shown to be a convex cone. It is </p>

<p>$$\begin{aligned}N_C(\bar{x}) = \left\{d\in\mathbb{R}^n: \langle d, x-\bar{x}\rangle \leq 0, \forall x\in C\right\}.\end{aligned}$$</p>

<p>Equivalently</p>

<p>$$\begin{aligned}N_C(\bar{x}) =& \left\{d\in\mathbb{R}^n: \sup_{x\in C}\langle d, x-\bar{x}\rangle \leq 0\right\}\\=&\left\{d\in\mathbb{R}^n: \sup_{x\in C}\langle d, x\rangle \leq \langle d, \bar{x}\rangle\right\}\\=&\left\{d\in\mathbb{R}^n: \delta^*_C(d) \leq \langle d, \bar{x}\rangle\right\},\end{aligned}$$</p>

<p>where \( \delta^*_C\) is the support function of \( C\). If \( \bar{x} \notin C\), then \( N_C(\bar{x}) = \emptyset.\)</p>

<p>A vector \( w\in\mathbb{R}^n\) is a tangent vector of \( C\) at \( \bar{x}\) if there are sequences \( (x^\nu)_\nu \subseteq C\), \( x^\nu \to \bar{x}\) and \( \tau^\nu \to 0^+\) such that \( (x^\nu - \bar{x})/\tau^\nu \to w\).</p>

<p>The set of all tangent vectors of \( C\) at \( \bar{x}\in C\) is denoted by \( T_C(\bar{x})\) and it is a closed cone that can be written as the outer limit <p/>

<p>$$\begin{aligned}T_C(\bar{x}) = \limsup_{\tau \to 0^+}\tau^{-1}(C-\bar{x}).\end{aligned}$$</p>

<p>The tangent cone can also be expressed as </p>

<p>$$\begin{aligned}T_C(\bar{x}) {}={}& \mathrm{cl} \{w = \lambda (x-\bar{x}), x\in C, \lambda \geq 0\}  \\  {}={}& \mathrm{cl}\;\mathrm{cone}(C - \bar{x}).\end{aligned}$$</p>

{{</ math.inline >}}

### 2.1. Properties of the normal and tangent cones
{{< math.inline >}}
<p>A first notable property of the normal cone is the following:</p>


<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.1 (Normal at the interior).</strong> Suppose that \( C \subseteq \mathbb{R}^n\) has a nonempty interior and \( \bar{x} \in \mathrm{int}C\). Then \( N_C(\bar{x}) = \{0\}\) and \( T_C(\bar{x}) = \mathbb{R}^n\).</p>
</div>

<p>Next, let us state an important duality result between the tangent cone and the normal cone.</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.2 (Tangent-Normal cone duality).</strong> Let \( C \subseteq \mathbb{R}^n\) be a closed convex set. Then for \( \bar{x} \in C\)</p>
<p>\( \begin{aligned}N_C(\bar{x}) ={}&amp; T_C(\bar{x})^\circ, \\ T_C(\bar{x}) ={}&amp; N_C(\bar{x})^\circ.\end{aligned}\)</p>
</div>

<p>Sometimes it is more convenient to determine either the normal or the tangent cone; the other one can be determined by virtue of the above proposition.</p>

<p>Some further properties of the normal and tangent cones are stated below (some of these properties are taken from [3, Section 5.3]:</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.3 (Properties of the normal and tangent cone).</strong> Let \( C, C_1, C_2 \subseteq \mathbb{R}^n\) be closed convex sets. Then,</p>
<ol>
  <li>For all \( \bar{x}\in C\), \( N_C(\bar{x})\) and \( T_C(\bar{x})\) are closed convex cones</li>
  <li>Let \( y\in \mathbb{R}^n\) and \( y \notin C\). Then \( x = \Pi_C(y)\) if and only if \( y - x \in N_C(x)\)</li>
  <li>\( x \in \mathrm{int}C\) if and only if \( N_C(x) = \{0\}\)</li>
  <li>For \( \bar{x} \in C_1 \cap C_2\), 
    <ul>
      <li>\( N_{C_1 \cap C_2}(\bar{x}) \supseteq N_{C_1}(\bar{x}) \oplus N_{C_2}(\bar{x})\) and</li>
      <li>\( T_{C_1\cap C_2}(\bar{x}) \subseteq T_{C_1}(\bar{x}) \oplus T_{C_2}(\bar{x})\)</li>
    </ul>
If \( 0 \in \mathrm{relint}(C_1 - C_2)\) or \( \mathrm{relint}(C_1) \cap \mathrm{relint}(C_2) \neq \emptyset\), then the above inclusions hold with equality
</li>
 <li>For \( (\bar{x}_1, \bar{x}_2) \in C_1 \times C_2\), 
<ul>
 <li>\( N_{C_1 \times C_2}(\bar{x}_1, \bar{x}_2) = N_{C_1}(\bar{x}_1) \times N_{C_2}(\bar{x}_2)\) and</li>
 <li> \( T_{C_1 \times C_2}(\bar{x}_1, \bar{x}_2) = T_{C_1}(\bar{x}_1) \times T_{C_2}(\bar{x}_2)\)</li>
</ul>
</li>
</ol>
</div>

<p>Let us now give some examples most of which are taken from Exercise 2 in [1].</p>
{{</ math.inline >}}

### 2.2. Trivial case: normal cone of a singleton
{{< math.inline >}}
This is a trivial example: \( N_{\{x_0\}}(x_0)=\mathbb{R}^n\).
{{</ math.inline >}}

### 2.3. Normal cone of a closed interval
{{< math.inline >}}
<p>Let \( C = [a, b] \subseteq \mathbb{R}\). Then, if \( \bar{x} \in (a, b)\), it is \( N_{[a, b]}(\bar{x}) = \{0\}\). If \( \bar{x} = a\), then \( N_{[a, b]}(a) = \{d \in \mathbb{R}: d(x-a) \leq 0, \forall x \in[a, b]\}\), where \( x-a \geq 0\), so \( N_{[a, b]}(a) = (-\infty, 0]\). Likewise, \( N_{[a,b]}(b) = [0, \infty)\). Overall,</p>


<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.4 (Normal cone of a closed interval).</strong> It is</p>
<p>\( \begin{aligned}N_{[a,b]}(\bar{x}) = \begin{cases}\{0\},&amp;\text{ if } a &lt; x &lt; b\\(-\infty, 0], &amp;\text{ if } \bar{x}=a\\ [0, \infty),&amp;\text{ if } \bar{x} = b\end{cases}\end{aligned}\)</p>
</div>
{{</ math.inline >}}

### 2.4. Normal cone of a unit norm-ball
{{< math.inline >}}
<p>In this section we will prove the following result</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.5 (Normal cone of a unit norm-ball).</strong> Let \( Q \in \mathbb{R}^{n\times n}\) be a symmetric positive definite matrix; we can define the inner product \( \langle x, y\rangle_Q = x^\intercal Q y\) and the corresponding norm \( \|x\|_Q = \sqrt{\langle x, x\rangle_Q}\). Let \( C = \{x \in \mathbb{R}^n: \|x\|_Q \leq 1\}\). Then, for \( \bar{x} \in \mathbb{R}^n\) with \( \|\bar{x}\|_Q =1\), we have</p>
<p>\( \begin{aligned}N_{C}(\bar{x}) ={}&amp; \mathrm{cone}(Q\bar{x}), \\ T_C(\bar{x}) ={}&amp; \{w \in \mathbb{R}^n : \langle \bar{x}, w \rangle_Q \leq 0\}.\end{aligned}\)</p>
</div>

<p>We will provide two proofs to this result.</p>
{{</ math.inline >}}

#### 2.4-A. Normal cone of a unit norm-ball (method #1)
{{< math.inline >}}
<p>For this, we will use the result of Exercise 6.7 from [2], which states the following: Let \( F:\mathbb{R}^n \to \mathbb{R}^m\) be a smooth matting and \( C = F^{-1}(D)\), where \( D \subseteq \mathbb{R}^m\) and suppose that \( \nabla F\) has rank \( m\) at \( \bar{x} \in C\) with \( \bar{u} = F(\bar{x}) \in D\). Then</p>

$$\begin{aligned}T_C(\bar{x}) =& \{w : \nabla F(\bar{x}) w \in T_D(\bar{u})\} \\ N_C(\bar{x}) =& \{\nabla F(\bar{x})^\intercal y : y \in N_{D}(\bar{u})\}  \\ \widehat{N}_C(\bar{x}) =& \{\nabla F(\bar{x})^\intercal y : y \in \widehat{N}_{D}(\bar{u})\} \end{aligned}$$

<p>In this case we have \( C = \{x : \|x\| \leq 1\}\). Suppose that \( \|x\| = \sqrt{\langle x, x\rangle}\) for a given inner product on \( \mathbb{R}^n\). This means that there is a symetric positive definite matrix \( Q\) such that \( \|x\| = \sqrt{x^\intercal Q x}\) and we can write \( C = \{x \in \mathbb{R}^n : x^\intercal Q x \leq 1\}\). Define \( F(x) = \tfrac{1}{2}x^\intercal Q x - \tfrac{1}{2}\) and \( D = (-\infty, 0]\). Then \( \nabla F(x) = Qx\), so for \( \|\bar{x}\| = 1\),</p>

$$\begin{aligned} N_C(\bar{x}) =& \{\nabla F(\bar{x})^\intercal y : y \in N_{D}(\bar{u})\} = \{ yQ\bar{x} : y \geq 0\}, \end{aligned}$$

<p>which means that \( N_C(\bar{x}) = \mathrm{cone}(Q\bar{x})\) whenever \( \|\bar{x}\| = 1\) and since the tangent cone is the polar of the normal cone,</p>

$$\begin{aligned}T_C(\bar{x}) = \{w \in \mathbb{R}^n : \langle Q\bar{x}, w \rangle \leq 0\}.\end{aligned}$$
{{</ math.inline >}}


#### 2.4-B. Normal cone of a unit norm-ball (method #2)
{{< math.inline >}}
<p>Here is an alternative approach: the tangent cone of \( C\) at a point \( \bar{x}\) with \( \|\bar{x}\|_Q = 1\) can be determined using the fact that</p>

$$\begin{aligned}T_C(\bar{x}) = \limsup_{\tau \to 0^+}\tau^{-1}(C - \bar{x}) = \mathrm{cl}\bigcup_{\tau \to 0^+}\tau^{-1}(C - \bar{x}),\end{aligned}$$

<p>where the second equality is because \( C\) is a closed clonex set, and</p>

$$\begin{aligned}\tau^{-1}(C - \bar{x}) = \{x \in \mathbb{R}^n: \|\tau x + \bar{x}\|_Q \leq 1\} = \mathcal{B}^{\|\cdot\|_Q}\left(\tfrac{\bar{x}}{\tau}, \tfrac{1}{\tau}\right).\end{aligned}$$

<p>Let \( \langle \cdot, \cdot \rangle_Q\) denote the inner product that corresponds to \( \|\cdot\|_Q\). We claim that \( T_C(\bar{x}) = \{w \in \mathbb{R}^n: \langle w, \bar{x} \rangle_Q \leq 0\}.\)</p>

<p>Firstly we will show that \( \tau^{-1}(C - \bar{x}) = \mathcal{B}^{\|\cdot\|_Q}\left(\tfrac{\bar{x}}{\tau}, \tfrac{1}{\tau}\right) \subseteq \{w \in \mathbb{R}^n: \langle w, \bar{x} \rangle_Q \leq 0\}.\) Take \( w \in \mathcal{B}^{\|\cdot\|_Q}\left(\tfrac{\bar{x}}{\tau}, \tfrac{1}{\tau}\right),\) i.e., \( \|w + \tau^{-1}\bar{x}\|_Q \leq \tau^{-1}\). We need to show that \( \langle w, \bar{x}\rangle_Q \leq 0\). Indeed,</p>

$$\begin{aligned}\|w + \tau^{-1}\bar{x}\|_Q^2 \leq \tau^{-2} \Rightarrow& \|w\|_Q^2 + \|\tau^{-1}\bar{x}\|_Q^2 + 2 \langle w, \tau^{-1}\bar{x}\rangle_Q \leq \tau^{-2} \\ \Rightarrow& 2\langle w, \tau^{-1}\bar{x}\rangle_Q \leq \tau^{-2} -  \|\tau^{-1}\bar{x}\|_Q^2 - \|w\|_Q^2 \leq -\|w\|_Q^2 \\ \Rightarrow& \langle w, \tau^{-1}\bar{x} \rangle_Q \leq 0\end{aligned}$$

<p>Since the set \( \{w \in \mathbb{R}^n: \langle w, \bar{x} \rangle_Q \leq 0\}\) is closed we have that</p>

$$\begin{aligned}T_C(\bar{x}) = \mathrm{cl} \bigcup_{\tau \to 0^+} \mathcal{B}^{\|\cdot\|_Q}\left(\tfrac{\bar{x}}{\tau}, \tfrac{1}{\tau}\right) \subseteq \{w \in \mathbb{R}^n: \langle w, \bar{x} \rangle_Q \leq 0\}.\end{aligned}$$

<p>We now want to show the converse. We start by showing that \( \{w \in \mathbb{R}^n: \langle w, \bar{x} \rangle_Q < 0\} \subseteq T_C(\bar{x})\). In particular, we will show that for every \( w\in\mathbb{R}^n\) with \( \langle w, \bar{x}\rangle_Q < 0\), there is a \( \tau>0\) such that \( \mathcal{B}^{\|\cdot\|_Q}\left(\tfrac{\bar{x}}{\tau}, \tfrac{1}{\tau}\right) \ni w\), or what is the same</p>

$$\begin{aligned}\left\|w + \tau^{-1}\bar{x}\right\|_Q^2 \leq \tau^{-2} \Leftrightarrow \ldots \Leftrightarrow \tau \leq -2\frac{\langle w, \bar{x}\rangle_Q}{\|w\|_Q^2},\end{aligned}$$

<p>where the right hand side is positive.</p>

<p>It remains to show that all vectors \( w\in\mathbb{R}^n\) with \( \langle w, \bar{x}\rangle_Q = 0\) are in the tangent cone. To that end, we will determine a sequence of points \( x_\tau\) that converge to \( w\) while \( x_\tau \in \mathcal{B}^{\|\cdot\|_Q}\left(\tfrac{\bar{x}}{\tau}, \tfrac{1}{\tau}\right).\) The selection of these points is shown in the following figure.</p>

<img src="https://mathematix.files.wordpress.com/2022/05/tangent-space-of-ball-1.png?w=687" alt="x"/>

<p>The blue line is the locus of the points \( x_\tau\) for \( \tau > 0\). In this figure we use the Euclidean norm and \( \bar{x}=(0, -1)\), \( w=(8,0) \perp \bar{x}\). In two dimensions, this locus is part of a curve known as the <a href="https://en.wikipedia.org/wiki/Strophoid" target="_blank">right strophoid</a>.</p>

<p>Given a \( w\) with \( \langle w, \bar{x}\rangle_Q = 0\), we take \( x_\tau\) to be the point where the ball intersects the line segment that connects \( w\) with \( \bar{x}/\tau\). This point is </p>

$$\begin{aligned}x_\tau = -\frac{\bar{x}}{\tau} + \frac{1}{\tau} \frac{w + \frac{\bar{x}}{\tau}}{\left\|w + \frac{\bar{x}}{\tau} \right\|_Q}.\end{aligned}$$

<p>This is a linear combination of \( w\) and \( \bar{x}/\tau\) and can be written as a linear combination of \( w\) and \( \bar{w}\) as \( x_\tau = \lambda(\tau) w + \beta(\tau)\bar{x}\), where</p>

$$\begin{aligned}\lambda(\tau) =& \frac{1}{\|\tau w + \bar{x}\|_Q}, \\ \beta(\tau) =& \frac{1}{\tau}\left(\frac{1}{\tau\left\|w + \frac{\bar{x}}{\tau}\right\|_Q} - 1\right).\end{aligned}$$

<p>We will show that \( \lim_{\tau \to 0^+}\lambda(\tau)=1\) and \( \lim_{\tau \to 0^+}\beta(\tau)=0\). For the first limit we have</p> 

$$\begin{aligned}\lim_{\tau \to 0^+}\lambda(\tau) =& \lim_{\tau \to 0^+}\frac{1}{\sqrt{\tau^2\|w\|_Q^2 + 1}} = 1,\end{aligned}$$

<p>where we used the fact that \( \|\bar{x}\|_Q=1\) and \( \langle w, \bar{x}\rangle_Q = 0\). Next,</p>

$$\begin{aligned} \lim_{\tau \to 0^+}\beta(\tau) =& \lim_{\tau \to 0^+}\frac{1}{\tau}\left(\frac{1}{\tau\left\|w + \frac{\bar{x}}{\tau}\right\|_Q} - 1\right) \\ =& \lim_{\tau \to 0^+}\frac{1}{\tau^2\sqrt{\|w\|_Q^2 + \frac{1}{\tau^2}}} - \frac{1}{\tau} \\ =& \lim_{\tau \to 0^+}\frac{1}{\tau \sqrt{\|w\|_Q^2 \tau^2 + 1}} - \frac{1}{\tau} \\ =& \lim_{\tau \to 0^+} \frac{1 - \sqrt{\|w\|_Q^2 \tau^2 + 1}}{\tau \sqrt{\|w\|_Q^2 \tau^2 + 1}} \\ =& \lim_{\tau \to 0^+} \frac{1}{\sqrt{\|w\|_Q^2 \tau^2 + 1}} \cdot \lim_{\tau \to 0^+}\frac{1 - \sqrt{\|w\|_Q^2 \tau^2 + 1}}{\tau}\end{aligned}$$

<p>where we used the product rule of the limit. The first limit is equal to 1. The second one is as follows:</p>

$$\begin{aligned} \lim_{\tau \to 0^+}\beta(\tau) =& \lim_{\tau \to 0^+}\frac{\left(1 - \sqrt{\|w\|_Q^2 \tau^2 + 1}\right)\left(1 + \sqrt{\|w\|_Q^2 \tau^2 + 1}\right)}{\tau\left(1 + \sqrt{\|w\|_Q^2 \tau^2 + 1}\right)} \\ =& \lim_{\tau \to 0^+}\frac{-\|w\|_Q^2 \tau }{1 + \sqrt{\|w\|_Q^2 \tau^2 + 1}} = 0 \end{aligned}$$

<p>This completes the proof. We have shown that \( T_{\mathcal{B}^{\|\cdot\|_Q}}(\bar{x}) = \{w: \langle w, \bar{x}\rangle_Q \leq 0\},\) whenever \( \|\bar{x}\|_Q = 1\).</p>
{{</ math.inline >}}


### 2.6. Normal cone of a subspace

{{< math.inline >}}
<p>Suppose that \( C\) is a subspace of \( \mathbb{R}^n\) spanned by the vectors \( \{e_1, \ldots, e_p\}\). Then every \( x \in C\) can be written as \( x = a_1 e_1 + \ldots + a_p e_p\). Take \( \bar{x} \in C\). This means that we can write \( \bar{x} = \bar{a}_1 e_1 + \ldots + \bar{a}_p e_p\) for some \( \bar{a}_1,\ldots, \bar{a}_p\). We have</p>

$$\begin{aligned}N_C(\bar{x}) =& \left\{d\in\mathbb{R}^n: \langle d, x-\bar{x}\rangle \leq 0, \forall x \in C\right\} \\ =& \left\{ d \in \mathbb{R}^n : \langle d, (a_1 - \bar{a}_1)e_1 + \ldots + (a_p - \bar{a}_p)e_p \rangle \leq 0, \forall a_1,\ldots, a_p \in \mathbb{R}\right\} \\ =& \left\{ d \in \mathbb{R}^n : \langle d, b_1 e_1 + \ldots + b_p e_p\rangle  \leq 0, \forall b_1,\ldots, b_p \in \mathbb{R}\right\} \end{aligned}$$

<p>It is not difficult to conclude that \( N_C(\bar{x}) = C^\perp\): firstly, if \( d \in N_C(\bar{x})\) if we choose \( b_1 = 1\) and \( b_2=\ldots=b_p=0\) we have that \( \langle d, e_1\rangle \leq 0\). Then, by choosing \( b_1 = -1\) and \( b_2=\ldots=b_p=0\) we see that \( \langle d, -e_1\rangle \leq 0\), so \( \langle d, e_1 \rangle = 0\). Similarly, we have that \( \langle d, e_i \rangle = 0\) for \( i=1,\ldots, p\), therefore, \( N_C(\bar{x}) \subseteq C^\perp\). The converse is straightforward.</p>
{{</ math.inline >}}



### 2.7. Normal cone of a closed halfspace

{{< math.inline >}}
<p>Let \( C = \{x \in \mathbb{R}^n : \langle a, x\rangle \leq b\}\) and \( \bar{x} \in C\). Here is is more convenient to start by determining \( T_C(\bar{x})\). </p>

<p>If \( \langle a, \bar{x}\rangle < b\) then and only then \( x\in\mathrm{int} C\), so \( N_C(\bar{x}) = \{0\}\) and \( T_C(\bar{x}) = \mathbb{R}^n\). Take \( \bar{x}\) on the boundary of \( C\), that is, \( \langle a, \bar{x}\rangle = b\). Then,</p>

$$\begin{aligned}\tau^{-1}(C - \bar{x}) = \{x \in \mathbb{R}^n : \langle a, x \rangle \leq 0\} \Rightarrow T_C(\bar{x}) = \{x \in \mathbb{R}^n : \langle a, x\rangle \leq 0\}.\end{aligned}$$

<p>Then, since \( N_C(\bar{x}) = T_C(\bar{x})^\circ\), it is </p>

$$\begin{aligned}N_C(\bar{x}) =& \{y\in\mathbb{R}^n: \langle y, x\rangle \leq 0, \forall x: \langle a, x\rangle \leq 0\} \\   =& \left\{y\in\mathbb{R}^n: \sup_{\langle a, x\rangle \leq 0}\langle y, x\rangle \leq 0 \right\} \\ =& \{y\in\mathbb{R}^n: \delta_{\{x: \langle a, x\rangle \leq 0\}}^*(y) \leq 0\}\end{aligned}$$

<p>But we know that \( \delta^*_{\{x: \langle a, x\rangle \leq 0\}}(y) = \delta_{\{\lambda a; \lambda \geq 0\}}(y),\) therefore,</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.6 (Normal and tangent cone of a halfspace).</strong> Consider the set \( C = \{x \in \mathbb{R}^n : \langle a, x\rangle \leq b\}\) and \( \bar{x}\) be such that \( \langle a,\bar{x} \rangle = b\). Then \( N_C(\bar{x}) = \mathrm{cone}(\{a\}).\)</p>
</div>
{{</ math.inline >}}



### 2.8. Normal cone of polyhedral set

{{< math.inline >}}
<p>In this section we will derive the normal and tangent cones of polyhedral sets given then V and H representations. We start with the following proposition for polyhedra given in their H representation:</p>

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.7 (Normal and tangent cone of a polyhedron).</strong> Let \( C = \{x\in\mathbb{R}^n : \langle a_i, x\rangle \leq b_i, i=1,\ldots, p\}\). Given \( \bar{x} \in C\) define the <i>active set</i> of \( \bar{x}\) as \( \mathcal{I}(\bar{x}) = \{i\in\{1,\ldots, p\}: \langle a_i, \bar{x}\rangle = b_i\}\). Then,</p>
<p>\( \begin{aligned}N_C(\bar{x}) ={}&amp; \mathrm{cone}(\{a_i\}_{i\in\mathcal{I}(\bar{x})}),  \\  T_C(\bar{x}) {}={}&amp; \{w \in \mathbb{R}^n : \langle a_i, w \rangle \leq 0, \forall i \in \mathcal{I}(\bar{x})\}.\end{aligned}\)</p>
</div>

<em>Proof.</em> We will start with the tangent cone. Firstly, we will make a few observations.

<strong>Claim 1.</strong> For every \( \epsilon > 0\), \( T_{C}(\bar{x}) = T_{C \cap \mathcal{B}(\bar{x}, \epsilon)}(\bar{x}).\)

This is simply because \( T_C\) is defined as a limit, so it is a local property. The following property can be verified very easily:

<strong>Claim 2.</strong> For every nonempty convex clossed set \( C\subseteq\) and \( \bar{x} \in C\), \( T_C(\bar{x}) = T_{C - \bar{x}}(0).\)

Now define the set \( C_{\mathcal{I}(\bar{x})} = \{x \in \mathbb{R}^n: \langle a_i, x \rangle \leq b_i, \forall i \in \mathcal{I}(\bar{x})\}.\) For all \( j \notin \mathcal{I}(\bar{x}),\) \( \langle a_j , \bar{x} \rangle \neq 0\), so due to the continuity of the inner product, there is a neighbourhood of \( \bar{x}\), \( \mathcal{B}(\bar{x}, \epsilon)\) where \( \langle a_j , x \rangle \neq 0\) for all \( x\in \mathcal{B}(\bar{x}, \epsilon).\) As a result, \( C \cap \mathcal{B}(\bar{x}, \epsilon) = C_{\mathcal{I}}(\bar{x}) \cap \mathcal{B}(\bar{x}, \epsilon).\) From Claims 1 and 2 we have 

$$\begin{aligned}T_C(\bar{x}) {}={}& T_{C-\bar{x}}(0) \\ {}={}& T_{(C-\bar{x}) \cap \mathcal{B}(\epsilon)}(0) \\  {}={}&  T_{(C_{\mathcal{I}(\bar{x})}-\bar{x}) \cap \mathcal{B}(\epsilon)}(0)  \end{aligned}$$

and note that \( C_{\mathcal{I}(\bar{x})}-\bar{x} = \{x: \langle a_i, x\rangle \leq 0, \forall i \in \mathcal{I}(\bar{x})\},\) which is a cone. The result follows.

<div style="border-color:black;border-style:solid;border-width:1.5px;padding-left:10px;">
<p>
<strong>Proposition 2.8 (Normal and tangent cone of a polytope).</strong> Consider a polytope in its V representation, that is, \( C = \mathrm{conv}(\{a_1, \ldots, a_p\})\) and \( \bar{x} \in C\). Then,
</p><ol>
<li>\( N_C(\bar{x}) = \{d \in \mathbb{R}: \langle d, a_i - \bar{x} \rangle \leq 0, \forall i=1,\ldots, p\},\) and</li>
<li>\( T_C(\bar{x}) = \mathrm{cone}(\{a_i - \bar{x}\}_{i})\)<p></p></li>
</ol>  
</div>

<p>This can be proven using the support function of \(C\) (see <a href="#prop15">Proposition 1.5</a>).</p>
{{</ math.inline >}}

## References

[1] JM Borwein and AS Lewis, Convex analysis and nonlinear optimization: theory and examples, Springer, CMS Books in Mathematics, 2010.

[2] RT Rockafellar and RJB Wets, Variational Analysis, Springer, 2009

[3] J-B Hiriart-Urruty and C. Lemaréchal, Fundamentals of Convex Analysis, Springer, 2001







Work in progress... (read [here](https://mathematix.wordpress.com/2022/05/22/useful-convex-analysis-stuff-support-functions-normal-and-tangent-cones/))

