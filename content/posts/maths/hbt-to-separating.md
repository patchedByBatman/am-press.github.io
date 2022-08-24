---
author: "Pantelis Sopasakis"
title: From Hahn-Banach to separating theorems
date: 2022-08-23
description: From the Hahn-Banach theorem to the three separating theorems
summary: From the Hahn-Banach theorem to the three separating theorems
math: true
series: ["Mathematix"]
tags: ["Convex Analysis", "Functional Analysis", "Analysis"]
showtoc: false
---

<style>
table {
  border-collapse: collapse;
  width: 100%;
  table-layout: fixed;
}

td, th {

  text-align: left;
  padding: 8px;
  width: 33%
}


</style>

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}

<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}


## Nonnegative sublinear functionals
{{< math.inline >}}
<div style="border-style:solid;border-width:1.5px;padding:10px; margin-bottom: 10px">
<p><strong>Definition 1 (Banach functional).</strong> Let \(X\) be a vector space. A \(p:X\to{\rm I\!R}\) is called a <strong>nonnegative sublinear functional</strong> (NSF) if the following conditions are satisfied</p>
<ol>
    <li>\(p\) is nonnegative valued on \(X\)</li>
    <li>\(p\) is positively homogeneous on \(X\), that is, \(p(\lambda x) = \lambda p(x)\) for all \(\lambda\geq 0\) and \(x\in X\)</li>
    <li>\(p\) is sublinear, that is, \(p(x+y) \leq p(x) + p(y)\)</li>
</ol>
</div>
<p>Note that <abbr title="nonnegative sublinear functionals">NSFs</abbr> are not necessarily symmetrix (\(p(-x)\) is not equal to \(p(x)\)) and it is not necessary that \(x=0\) whenever \(p(x) = 0\).</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Proposition 2 (Continuity of <abbr title="nonnegative sublinear functionals">NSFs</abbr>).</strong> Let \(X\) be a <a href="https://en.wikipedia.org/wiki/Topological_vector_space" target="_blank">topological vector space</a> (TVS) and \(p:X\to{\rm I\!R}\) is an <abbr title="nonnegative sublinear functional">NSF</abbr>. Then, the following are equivalent</p>
<ol>
    <li>\(p\) is continuous</li>
    <li>\(p\) is continuous at \(0\)</li>
    <li>\(p\) is bounded in a neighbourhood of \(0\)</li>
</ol>
</div>

<p><em>Proof.</em> It is obvious that 1 implies 2, which implies 3. We shall prove that 3 implies 2. Let \(V\) be a neighbourhood of \(0\) and \(p(V)\) is bounded, i.e., \(p(V) \subseteq (-M, M)\) for some \(M>0\). For \(x\in V\) we have that</p>
<p>$$p\left(\tfrac{\epsilon}{M}x\right){}={}\tfrac{\epsilon}{M} p(x) \in (-\epsilon, \epsilon),$$</p>
<p>which implies that</p>
<p>$$p\left(\tfrac{\epsilon}{M}V\right) \subseteq (-\epsilon, \epsilon),$$</p>
<p>so, \(p\) is continuous at \(0\).</p>

<p>Let us now show that 2 implies 1. Let \(p\) be continuous at \(0\) and \(x_0 \in X\). Let \(\epsilon > 0\). Then, there is \(V\), star-shaped neighbourhood of \(0\) such that \(p(V) \subseteq (-\epsilon, \epsilon)\). We will show that \(p(x_0 + V) \subseteq (p(x_0)-\epsilon, p(x_0) + \epsilon)\).</p>

<p>By taking \(v\in V\) we see that \(p(x_0 + v) \leq p(x_0) + p(v) < p(x_0) + \epsilon\). Likewise, \(p(x_0+v) = p(x_0 - (-v)) \geq p(x_0) - p(-v) > p(x_0) - \epsilon\). This completes the proof. \(\blacksquare\)</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Proposition 3 (<abbr title="nonnegative sublinear functionals">NSFs</abbr> have convex sublevel sets).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(p:X\to{\rm I\!R}\) is an <abbr title="nonnegative sublinear functional">NSF</abbr>. Then, its sublevel sets, \(\{x: p(x) \leq a\}\), are convex.</p></div>

<p><em>Proof.</em> Straightforward. \(\blacksquare\)</p>

<p>Next, we will show that any linear functional that is bounded above by a continuous <abbr title="nonnegative sublinear functional">NSF</abbr>, is continuous.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Proposition 4 (Continuity of linear functionals).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr>,   \(p:X\to{\rm I\!R}\) is an <abbr title="nonnegative sublinear functional">NSF</abbr>,  \(A: X\to{\rm I\!R}\) is linear, and</p>
<p>$$A(x) \leq p(x),$$</p>
<p>for all \(x\in X\). If \(p\) is continuous, then \(A\) is continuous.</p>
</div>

<p><em>Proof.</em> To show that \(A\) is continuous, it suffices to show that for every \(\epsilon > 0\), there is an open neighbourhood of \(0_X\) such that \(A(V) \subseteq (-\epsilon, \epsilon)\). Since \(p\) is continuous (at \(0\)), there is a star-shaped neighbourhood of \(0\) such that \(p(V) \subseteq (-\epsilon, \epsilon)\).</p>

<p>For \(x \in V\) we have </p>
<p>$$A(x) \leq p(x) < \epsilon.$$</p>
<p>Moreover,</p>
<p>$$A(x) = A(-(-x)) = -A(-x) \geq -p(-x) > -\epsilon,$$</p>
<p>where we used the fact that \(V\) is star-shaped, so \(x\in V\) implies \(-x\in V\). We have shown that  \(A(V) \subseteq (-\epsilon, \epsilon)\). \(\blacksquare\)</p>
{{</ math.inline >}}

## Zorn's lemma
{{< math.inline >}}
<p>In this section we'll state Zorn's lemma, which is a very useful tool in functional analysis (and not only) with numerous applications. Zorn's lemma can be proven using the <a href="https://en.wikipedia.org/wiki/Axiom_of_choice" target="_blank">axiom of choice</a> (in fact, it is equivalent to the axiom of choice).</p>

<p>We will state Zorn's lemma here without a proof. We will later use it to prove the Hahn-Banach theorem. Firstly, we need to state some definitions.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Definition 5 (Partial order).</strong> Let \(A\) be a nonempty set. A relation, \(\leq\), is a partial order on \(A\) if it satisfies the following properties</p>
<ol>
    <li>(Reflexivity) \(a \leq a\) for all \(a\in A\)</li>
    <li>(Antisymmetry) \(a \leq b\) and \(b \leq a\) implies \(a = b\) for all \(a, b\in A\)</li>
    <li>(Transitivity) \(a \leq b\) and \(b \leq c\) implies that \(a \leq c\) for all \(a, b, c \in A\)</li>
</ol>
</div>

<p>Note that for a given set \(A\) and a partial order \(\leq\) on \(A\) it is not necessary that either \(a\leq b\) or \(b\leq a\). For example, that the partial order \(\preceq\) on the set of symmetric matrices where \(A \preceq B\) means that \(B-A\) is positive semidefinite. There can be matrices \(A\) and \(B\) such that neither \(A \preceq B\) nor \(B \preceq A\).</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Definition 6 (Chain).</strong> Let \(A\) be a nonempty set equipped with a partial order \(\leq\). A set \(B\ subseteq A\) is said to be a chain if for every \(a,b\in B\), either \(a\leq b\) or \(b\leq a\).</p>
</div>

<p>As an example, take \(A={\rm I\! R}^n\) and for \(x,y \in {\rm I\! R}^n\) let \(x\leq y\) if and only if \(x_i \leq y_i\) for all \(i\). Take \(x_0 \in {\rm I\! R}^n\), \(x_0 \neq 0\). The set \(B={\rm I\! R} x_0 = \{\lambda x_0; \lambda \in {\rm I\! R}^n\}\) is a chain.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Definition 7 (Maximal element).</strong> Let \(A\) be a nonempty set equipped with a partial order \(\leq\). An element \(M \in A\) is said to be a maximal element of \(A\) if for all \(x\in A\),</p>
<p>$$m \leq x \Rightarrow x = m.$$</p>
</div>

<p>As an example, take again \(A={\rm I\! R}^n\) and for \(x,y \in {\rm I\! R}^n\) let \(x\leq y\) if and only if \(x_i \leq y_i\) for all \(i\). Take \(B\) to be the unit-ball of the Euclidean norm. Then any \(m \in {\rm I\! R}^n\) with \(\|m\|=1\) is a maximal element of \(B\). Note also that \(A\) does not have any maximal elements.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Definition 8 (Upper boun of a chain).</strong> Let \(A\) be a nonempty set equipped with a partial order \(\leq\) and let \(B\subseteq A\) be a chain. An element \(m \in A\) is said to be an upper bound of the chain if \(x \leq m\) for every \(x\in B\).</p>
</div>

<p>As a simple example, take \(A={\rm I\! R}\) with the standard order, \(\leq\), and the chain \(B = (0, 1)\). Then \(m=2\) is an upper bound; \(m=1\) is another upper bound of \(B\).</p>

<p>We will now state Zorn's lemma (without a proof).</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Theorem 8 (Zorn's lemma).</strong> Let \(A\) be a nonempty set equipped with a partial order \(\leq\) and every chain has an upper bound. Then, \(A\) has a maximal element.</p>
</div>
{{</ math.inline >}}





## The Hahn-Banach Theorem

<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>

## Minkowski functional

## Convex separating theorems 

### First (fundamental) separating theorem

### Second separating theorem

### Third separating theorem