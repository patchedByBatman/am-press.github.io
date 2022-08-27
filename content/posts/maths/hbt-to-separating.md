---
author: "Pantelis Sopasakis"
title: From Hahn-Banach to Separating Theorems
date: 2022-08-23
description: From the Hahn-Banach theorem to the three separating theorems
summary: From the Hahn-Banach theorem to the three separating theorems
math: true
series: ["Mathematix"]
tags: ["Convex Analysis", "Functional Analysis"]
showtoc: true
collapsible: true
---

## About

<p>In this post we will state and prove the Hahn-Banach theorem and the three separating theorems. All results will be stated for general topological vector spaces (normed spaces are a special case). All vector spaces in this post are taken over the field of real numbers.</p>

## Preliminaries

<p>We assume that the reader is familiar with the concept of a <a href="https://en.wikipedia.org/wiki/Topological_vector_space" target="_blank">topological vector space</a> (TVS).</p>

<p>Let \(X\) be a <abbr title="topological vector space">TVS</abbr>. Recall that a set \(A \subseteq X\) is said to be <a href="https://en.wikipedia.org/wiki/Balanced_set" target="_blank"><strong>balanced</strong></a> if \([-1, 1]A \subseteq A\). Of course \(0\in A\). Note that balanced sets are symmetric (\(-A = A\)).</p> 

<p>A set \(A\) is said to be <a href="https://en.wikipedia.org/wiki/Absorbing_set" target="_blank"><strong>absorbing</strong></a> if for every \(x\in X\) there is a \(c_0 > 0\) such that \(x \in cA\) for all \(c\in{\rm I\!R}\) with \(|c| \geq c_0\). In simple words, a set is absorbing if it can be inflated to include any point \(x\in X\) <em>and</em> once it absorbes \(x\) as we keep inflating it, it will keep containing \(x\).</p>

<p>We will recall a fact from the theory of <abbr title="topological vector space">TVS</abbr> that we will be using a lot in what follows. If \(X\) is a <abbr title="topological vector space">TVS</abbr>, the origin has a topological base of balanced and absorbing sets.</p>


## Positive sublinear functionals

<div style="border-style:solid;border-width:1.5px;padding:10px; margin-bottom: 10px">
<p><strong>Definition 1 (Positive sublinear functional).</strong> Let \(X\) be a vector space. A \(p:X\to{\rm I\!R}\) is called a positive sublinear functional (PSLF) if the following conditions are satisfied</p>
<ol>
    <li>\(p\) is nonnegative valued on \(X\)</li>
    <li>\(p\) is positively homogeneous on \(X\), that is, \(p(\lambda x) = \lambda p(x)\) for all \(\lambda\geq 0\) and \(x\in X\)</li>
    <li>\(p\) is sublinear, that is, \(p(x+y) \leq p(x) + p(y)\)</li>
</ol>
</div>
<p>Note that <abbr title="positive sublinear functionals">PSLFs</abbr> are not necessarily symmetrix (\(p(-x)\) is not equal to \(p(x)\)) and it is not necessary that \(x=0\) whenever \(p(x) = 0\).</p>

<p>Note that if \(p\) is an <abbr title="positive sublinear functional">PSLF</abbr> and \(\lambda < 0\), then \(p(x) \leq -p(-\lambda x).\)</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="prop2">
<p><strong>Proposition 2 (Continuity of <abbr title="positive sublinear functionals">PSLFs</abbr>).</strong> Let \(X\) be a <a href="https://en.wikipedia.org/wiki/Topological_vector_space" target="_blank">topological vector space</a> (TVS) and \(p:X\to{\rm I\!R}\) is an <abbr title="positive sublinear functional">PSLF</abbr>. Then, the following are equivalent</p>
<ol>
    <li>\(p\) is continuous</li>
    <li>\(p\) is continuous at \(0\)</li>
    <li>\(p\) is bounded in a neighbourhood of \(0\)</li>
</ol>
</div>

<button onclick="toggleCollapseExpand('proofProp2Button', 'proofProp2Container', 'Proof')" id="proofProp2Button">
  <i class="fa fa-cog fa-spin"></i> Click to reveal the proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px; " id="proofProp2Container">
<p><em>Proof.</em> It is obvious that 1 implies 2, which implies 3. We shall prove that 3 implies 2. Let \(V\) be a neighbourhood of \(0\) and \(p(V)\) is bounded, i.e., \(p(V) \subseteq (-M, M)\) for some \(M>0\). For \(x\in V\) we have that</p>
<p>$$p\left(\tfrac{\epsilon}{M}x\right){}={}\tfrac{\epsilon}{M} p(x) \in (-\epsilon, \epsilon),$$</p>
<p>which implies that</p>
<p>$$p\left(\tfrac{\epsilon}{M}V\right) \subseteq (-\epsilon, \epsilon),$$</p>
<p>so, \(p\) is continuous at \(0\).</p>

<p>Let us now show that 2 implies 1. Let \(p\) be continuous at \(0\) and \(x_0 \in X\). Let \(\epsilon > 0\). Then, there is \(V\), balanced neighbourhood of \(0\) such that \(p(V) \subseteq (-\epsilon, \epsilon)\). We will show that \(p(x_0 + V) \subseteq (p(x_0)-\epsilon, p(x_0) + \epsilon)\).</p>

<p>By taking \(v\in V\) we see that \(p(x_0 + v) \leq p(x_0) + p(v) < p(x_0) + \epsilon\). Likewise, \(p(x_0+v) = p(x_0 - (-v)) \geq p(x_0) - p(-v) > p(x_0) - \epsilon\). This completes the proof. \(\blacksquare\)</p>
</div>

<p></p>
<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px">
<p><strong>Proposition 3 (<abbr title="positive sublinear functionals">PSLFs</abbr> have convex sublevel sets).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(p:X\to{\rm I\!R}\) is an <abbr title="positive sublinear functional">PSLF</abbr>. Then, its sublevel sets, \(\{x: p(x) \leq a\}\), are convex.</p></div>

<p><em>Proof.</em> Straightforward. \(\blacksquare\)</p>

<p>Next, we will show that any linear functional that is bounded above by a continuous <abbr title="positive sublinear functional">PSLF</abbr>, is continuous.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="prop4">
<p><strong>Proposition 4 (Continuity of linear functionals).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr>,   \(p:X\to{\rm I\!R}\) is an <abbr title="positive sublinear functional">PSLF</abbr>,  \(A: X\to{\rm I\!R}\) is linear, and</p>
<p>$$A(x) \leq p(x),$$</p>
<p>for all \(x\in X\). If \(p\) is continuous, then \(A\) is continuous.</p>
</div>

<button onclick="toggleCollapseExpand('proofProp4Button', 'proofProp4Container', 'Proof')" id="proofProp4Button">
  <i class="fa fa-cog fa-spin"></i> Click to reveal the proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px; " id="proofProp4Container">
<p><em>Proof.</em> To show that \(A\) is continuous, it suffices to show that for every \(\epsilon > 0\), there is an open neighbourhood of \(0_X\) such that \(A(V) \subseteq (-\epsilon, \epsilon)\). Since \(p\) is continuous (at \(0\)), there is a balanced neighbourhood of \(0\) such that \(p(V) \subseteq (-\epsilon, \epsilon)\).</p>

<p>For \(x \in V\) we have </p>
<p>$$A(x) \leq p(x) < \epsilon.$$</p>
<p>Moreover,</p>
<p>$$A(x) = A(-(-x)) = -A(-x) \geq -p(-x) > -\epsilon,$$</p>
<p>where we used the fact that \(V\) is balanced, so \(x\in V\) implies \(-x\in V\). We have shown that  \(A(V) \subseteq (-\epsilon, \epsilon)\). \(\blacksquare\)</p>
</div>




## Zorn's lemma

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

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="zorn">
<p><strong>Lemma 9 (Zorn's lemma).</strong> Let \(A\) be a nonempty set equipped with a partial order \(\leq\) and every chain has an upper bound. Then, \(A\) has a maximal element.</p>
</div>





## The Hahn-Banach Theorem

<p>The Hahn-Banach theorem is without doubt one of the most important theorems in functional analysis with numerous applications the most notable of which are the separating theorems. The proof of the Hahn-Banach theorem is of remarkable elegance!</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="hahn-banach-thm">
<p><strong>Theorem 10 (Hahn-Banach Theorem).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(p: X \to {\rm I\!R}\) is an <abbr title="positive sublinear functionals">PSLFs</abbr>. Let \(Y\subseteq X\) be a subspace of \(X\) and a linear functional \(f:Y\to{\rm I\!R}\) is such that </p>
<p>$$f(y) \leq p(y),$$</p>
<p>for all \(y\in Y\). Then, there exists a linear functional \(\hat{f}: X \to {\rm I\!R}\) such that</p>
<ol>
    <li>\(\hat{f}\) extends \(f\), i.e., \(\hat{f}(y) = f(y)\) for all \(y\in Y\)</li>
    <li>\(\hat{f}(x) \leq p(x)\) for all \(x \in X\)</li>
</ol>
</div>

<button onclick="toggleCollapseExpand('proofHBButton', 'proofHBContainer', 'Proof')" id="proofHBButton">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px; " id="proofHBContainer">
<p><em>Proof.</em> We will prove the Hahn-Banach theorem using Zorn's lemma. Hereafter the notation "\(Y \sqsubseteq Z\) means "\(Y\) is a linear subspace of \(Z\)" (both \(Y\) and \(Z\)s are linear spaces). We start by defining the set</p>
<p>$$A = \left\{(Z, f_Z) : \begin{array}{l}Y \sqsubseteq 	 Z \sqsubseteq X,
\\
f_Z: \text{ linear},
\\
f_Z | Y = f,
\\
f_Z(z) \leq p(z), \forall z\in Z
\end{array}\right\}$$</p>

<p>We know that \((Y, f) \in A\). We introduce a partial order \(\leq\) on \(A\) where</a> 
<p>$$(Z, f_Z) \leq (Z', f_{Z'}),$$</p> 
<p>if and only if \(Z \sqsubseteq Z'\) and \(f_{Z} \leq f_{Z'}|Z \); that is, \(f_Z(x) \leq f_{Z'}(x)\) for all \(x\in Z\).</p>
<p>Let \(B = \{(Z_i, f_{Z,i})\}_{i\in I}\) be a chain in \(A\). The following element of \(A\) is an upper bound of \(B\):</p>
<p>$$\left(\bigcup_{i\in I}Z_i, \bigcup_{i\in I}f_{Z,i}\right),$$</p>
<p>where the union of functions is meant in the sense of the union of their graphs.</p>
<p>From <a href="#zorn">Zorn's lemma</a>, \(A\) has a maximal element, \((\bar{Z}, \bar{f})\). We will show tha that \(\bar{Z} = X\).</p>

<p>If not, there is a \(z_0 \in X \setminus \bar{Z}\) and we can extend \(\bar{Z}\) to a space \(\bar{Z}' = \bar{Z} \oplus {\rm I\!R}z_0\). Take \(x, y \in \bar{Z}\). Then,</p>
<p>$$\begin{aligned}&f_{\bar{Z}}(x-y) \leq p(x-y)\\
{}\Leftrightarrow{}&f_{\bar{Z}}(x) - f_{\bar{Z}}(y) \leq p(x-z_0) + p(z_0 - y)\\{}\Leftrightarrow{}&f_{\bar{Z}}(x) - p(x-z_0) \leq f_{\bar{Z}}(y) - p(z_0 - y),\end{aligned}$$</p>

<p>for all \(x, y \in \bar{Z}\). Now take a supremum on the <abbr title="left hand side">LHS</abbr> and an infimum on the <abbr title="right hand side">RHS</abbr></p>
<p>$$
\sup_{x\in \bar{Z}}f_{\bar{Z}}(x) - p(x-z_0) \leq \inf_{y\in \bar{Z}} f_{\bar{Z}}(y) - p(z_0 - y).
$$</p>

<p>Therefore, there is an \(a\) in between</p>
<p id="eq-star">$$
\sup_{x\in \bar{Z}}f_{\bar{Z}}(x) - p(x-z_0) \leq a \leq \inf_{y\in \bar{Z}} f_{\bar{Z}}(y) - p(z_0 - y).\tag{$*$}
$$</p>

<p>We can now extend \(\bar{f}\) (which is defined on \(\bar{Z}\)) to a \(\bar{f}'\) defined on \(\bar{Z}'\). All \(z' \in \bar{Z}'\) can be written as \(z' = z + \lambda z_0\) for some \(\lambda \in {\rm I\!R}\). We define</p>

<p>$$\bar{f}'(z') = \bar{f}'(z + \lambda z_0) = \bar{f}(z) + \lambda a.$$</p>

<p>It suffices to show that \(\bar{f}' \leq p\) on \(\bar{Z}'\). Equivalently, we need to show that</p>

<p id="eq1">$$\begin{aligned}\bar{f}'(z') \leq p(z') \Leftrightarrow{}& \bar{f}'(z+ \lambda z_0) \leq p(z + \lambda z_0) \\  \Leftrightarrow{}& \bar{f}(z) + \lambda a \leq p(z+\lambda  z_0),\tag{1}\end{aligned}$$</p>

<p>for all \(z\in \bar{Z}\) and \(\lambda \in {\rm I\!R}\).</p>

<p>We consider three cases. Firstly, if \(\lambda = 0\), the condition of Equation <a href="#eq1">(1)</a> is satisfied trivially (you can check). If \(\lambda > 0\), Equation <a href="#eq1">(1)</a> is equivalent to</p>

<p>$$\begin{aligned} a {}\leq{}&
 \tfrac{1}{\lambda}p(z+\lambda  z_0) - \tfrac{1}{\lambda}\bar{f}(z)
 \\
 {}={}& p\left(\frac{z}{\lambda}+ z_0\right) +\bar{f}\left(- \frac{z}{\lambda}\right),\end{aligned}$$</p>

<p>which is true due to Equation <a href="#eq-star">(\(*\))</a>.</p>

<p>Likewise, if \(\lambda < 0\) Equation <a href="#eq1">(1)</a> is equivalent to </p>
<p>$$a \geq -p\left(-\frac{z}{\lambda}-z_0\right) + \bar{f}\left(-\frac{z}{\lambda}\right),$$</p>
<p>which is true due to Equation <a href="#eq-star">(\(*\))</a>.</p>

<p>We have shown that \((\bar{Z}' ,\bar{f}')\) is an element of \(A\) and it is \((\bar{Z}' ,\bar{f}') > (\bar{Z}, \bar{f})\). This is a contradiction because \((\bar{Z}, \bar{f})\) is maximal.</p>

</p>This completes the proof. \(\blacksquare\)</p>
</div>

<p></p>
<p>Note that the linear functional \(\hat{f}\) of the Hahn-Banach theorem is guaranteed to be continuous by virtue of <a href="#prop4" title="Continuity of linear functionals">Proposition 4</a>.</p>

<p>Note that we could have stated the Hahn-Banach theorem on a linear space instead of a <abbr title="topological vector space">TVS</abbr>, but the topology is necessary to be able to talk about the continuity of \(\hat{f}\).</p>

## Minkowski functional

<p>We will now introduce the Minkowski functional. The Minkowski functional is an <abbr title="positive sublinear functional">PSLF</abbr> which is defined using a convex set. Let us give the definition.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="def11">
<p><strong>Definition 11 (Minkowski functional).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K\subseteq X\) is a convex set that contains zero in its interior (\(0 \in \mathrm{int}\; K\)). We define the Minkowski functional as</p>
<p>$$p_K(x) = \inf \left\{ \lambda > 0 : \frac{x}{\lambda} \in K\right\} = \inf \left\{ \lambda > 0 : x \in \lambda K\right\}.$$</p>
</div>

<p>Note that the set \(\{ \lambda > 0 : x / \lambda \in K\}\) is nonempty because every neighbourhood of the origin is absorbing, so \( \mathrm{int}\; K\) is an absrobing set, so \(K\) is also absorbing.</p>

<p>We will now show that the Minkowski functional of a \(K\) as in Definition <a href="#def11">11</a> is an <abbr title="positive sublinear functional">PSLF</abbr>.</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="prop12">
<p><strong>Proposition 12 (Minkowski functional is continuous PSLF).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K\subseteq X\) is a convex set that contains zero in its interior (\(0 \in \mathrm{int}\; K\)), and let \(p_K\) be the Minkowski functional of \(K\). Then \(p_K\) is a continuous <abbr title="positive sublinear functional">PSLF</abbr>.</p>
</div>

<button onclick="toggleCollapseExpand('proofProp12Button', 'proofProp12Container', 'proof')" id="proofProp12Button">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofProp12Container">
<p><em>Proof.</em> Clearly, \(p_K \geq 0\). We will show that \(p_K\) is positively homogeneous. Let \(c > 0\). Then</p>
<p>$$p_K(c x) = \inf\left\{\lambda > 0 : \frac{cx}{\lambda} \in K\right\} = \inf\left\{ \lambda > 0 : \frac{x}{\tfrac{\lambda}{c}}\right\} = \ldots = c p_K(x).$$</p>
<p>It is easy to see that \(p_K(0) = 0.\)</p>

<p>Next, we will show that \(p_K\) is sublinear. Take \(\epsilon > 0\) and choose \(\lambda_1, \lambda_2 > 0\) such that</p>
<p>$$\begin{aligned}p_K(x) < \lambda_1 < p_K(x) + \epsilon, \\ p_K(y) < \lambda_2 < p_K(y) + \epsilon.\end{aligned}$$</p>
<p>As a result we have that \(x/\lambda_1 \in K\) and \(y/\lambda_2 \in K\).</p>
<p>It suffices to show that \(p_K(x+y) \leq \lambda_1 + \lambda_2\). We have</p>
<p>$$\frac{x+y}{\lambda_1 + \lambda_2} = \frac{\lambda_1}{\lambda_1 + \lambda_2}\frac{x}{\lambda_1} + \frac{\lambda_2}{\lambda_1 + \lambda_2}\frac{y}{\lambda_2} \in K.$$</p>
<p>Therefore, \(p_K(x+y) \leq \lambda_1 + \lambda_2\) and taking \(\epsilon{}\to{}0\), it follows that \(p_K(x+y) \leq p_K(x) + p_K(y).\)</p>

<p>Lastly, we will show that \(p_K\) is continuous using <a href="#prop2" title="Continuity of PSLFs">Proposition 2</a>. For \(x\in K\), \(x/1 \in K\), so \(0 \leq p_K(x) \leq 1\), so it is bounded in \(\mathrm{int}\; K\), which is an open neighbourhood of zero, therefore, it is continuous. \(\blacksquare\)</p>
</div>

<p>The Minkowski functional of a convex set \(K\) allows us to obtain a complete understanding of the topological properties of \(K\). The following result allows us to use the Minkowski of \(K\) to determine the interior, closure and boundary of \(K\).</p>


<p>We will first introduce the following convenient notation:</p>

<p>$$\begin{aligned}[p_K < 1] {}={}& \{x\in X: p_K(x) < 1\}, \\ [p_K \leq 1] {}={}& \{x\in X: p_K(x) \leq 1\}, \\ [p_K = 1] {}={}& \{x\in X: p_K(x) = 1\}.\end{aligned}$$</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="prop13">
<p><strong>Proposition 13 (Topological properties of convex sets).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K\) is a convex set with \(0 \in \mathrm{int}\; K\) and let \(p_K\) be the Minkowski functional of \(K\). Then,</p>
<ol>
  <li>\(\mathrm{int}\; K = [p_K < 1]\)</li>
  <li>\(\mathrm{cl}\; K = [p_K \leq 1]\)</li>
  <li>\(\partial K = [p_K {}={} 1]\)</li>
</ol>
</div>

<button onclick="toggleCollapseExpand('proofProp13aButton', 'proofProp13aContainer', 'proof of No. 1')" id="proofProp13aButton">
  <i class="fa fa-cog fa-spin"></i> Expand proof of No. 1
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofProp13aContainer">
<p><em>Proof.</em> 1. We have that \([p_K < 1] = p_K^{-1}((-\infty, 1))\) and since \(p_K\) is continuous (<a href="#prop12" title="Minkowski functional is continuous PSLF">Prop 12</a>), it is <em>open</em>. Since \(K\) is convex and contains zero in its interior, \(\lambda K \subseteq K\) for all \(0<\lambda < 1\). This observation allows us to see that \([p_K < 1] \subseteq K\). Since \([p_K < 1]\) is an open set inside \(K\), we conclude that</p> 
<p>$$[p_K < 1] \subseteq \mathrm{int}\; K.$$</p> 
<p>The reason for this is that \(\mathrm{int}\; K\) is the <em>largest</em> open set inside \(K\). We then need to show that \([p_K < 1] \supseteq \mathrm{int}\; K\).</p>

<p>Take \(x_0 \in \mathrm{int}\; K\). We will use the fact that the scalar multiplication is continuous: the scalar multiplication maps</p>
<p>$${}\cdot{}: (1, x_0) \mapsto x_0 \in  \mathrm{int}\; K,$$</p>
<p>where \(\mathrm{int}\; K\) is open. From the continuity of the scalar multiplication, there is \(\epsilon > 0\) such that</p>
<p>$$(1-\epsilon, 1+\epsilon) x_0 \subseteq \mathrm{int}\; K.$$</p>
<p>Choosing</p>
<p>$$\lambda = \frac{1}{1+\tfrac{\epsilon}{2}},$$</p>
<p>we have \(x_0/\lambda \in K\), therefore, \(p_K(x_0) < 1\) \(\Box\).</p>
</div>

<br/>
<button onclick="toggleCollapseExpand('proofProp13bButton', 'proofProp13bContainer', 'proof of No. 2')" id="proofProp13bButton">
  <i class="fa fa-cog fa-spin"></i> Expand proof of No. 2
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofProp13bContainer">
<p>2. Firstly \([p_K \leq 1] = p_K^{-1}((-\infty, 1])\) is <em>closed</em> since it is the inverse image of the closed set \((-\infty, 1]\) through the continuous function \(p_K\). Next, if \(x\in K\),</p>
<p>$$p_K(x) = \inf\{\lambda>0 {}:{} x/\lambda \in K\} \leq 1,$$</p>
<p>so,</p> 
<p>$$K \subseteq \underbrace{[p_K \leq 1]}_{\text{closed}} \Rightarrow \mathrm{cl}\; K \subseteq [p_K \leq 1].$$</p>
<p>We will show that \([p_K \leq 1] \subseteq \mathrm{cl}\; K\). Take \(\tilde{x}\in [p_K \leq 1]\); equivalently \(p_{K}(\tilde{x}) \leq 1\). Take a sequence of scalars \((\lambda_{\nu})_{\rm I\!N}\) with \(0 < \lambda_\nu < 1\) and \(\lambda_\nu \to 1^{-}\). Then</p>
<p>$$\lambda_\nu \tilde{x} \in K,$$</p>
<p>for all \(\nu \in {\rm I\!N}\). So, \(\lim_\nu \lambda_\nu x = x \in  \mathrm{cl}\;K\). \(\Box\)</p>
</div>

<br/>
<button onclick="toggleCollapseExpand('proofProp13cButton', 'proofProp13cContainer', 'proof of No. 3')" id="proofProp13cButton">
  <i class="fa fa-cog fa-spin"></i> Expand proof of No. 3
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofProp13cContainer">
3. This is simply because \(\partial K = \mathrm{cl}\; K \setminus \mathrm{int}\; K = [p_K = 1].\) \(\Box\)
</div>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="prop14">
<p><strong>Proposition 14 (Minkowski functional of convex set).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K\) is a convex set with \(0 \in \mathrm{int}\; K\). Then,</p>
<p>$$p_{\mathrm{int}\; K} = p_{K} = p_{\mathrm{cl}\; K}.$$</p>
</div>

<button onclick="toggleCollapseExpand('proofProp14Button', 'proofProp14Container', 'proof')" id="proofProp14Button">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofProp14Container">
<p><em>Proof.</em> We will start by showing that \(p_{\mathrm{int}\; K} = p_{K}\). Since \(\mathrm{int}\; K \subseteq K\), we have \(p_{\mathrm{int}\; K} \geq p_{K}\). We will try to end up in a contradition by assuming that there is \(s\) such that</p> 
<p>$$p_{\mathrm{int}\; K}(x) > s > p_{K}(x)$$</p> 
<p>for some \(x\). Then, \(p_{\mathrm{int}\; K}(x/s) > 1\). However,</p>
<p>$$p_{K}\left(\frac{x}{s}\right) \Rightarrow \frac{x}{s} \in \mathrm{int}\; K \Rightarrow p_{\mathrm{int}\; K}\left(\frac{x}{s}\right) \leq 1,$$</p>
<p>which is a contradiction. Similary we can prove that \(p_{K} = p_{\mathrm{cl}\; K}.\) \(\blacksquare\)</p>
</div>


<p><br/>Using Propositions <a href="#prop13" title="Topological properties of convex sets">13</a> and <a href="#prop14" title="Minkowski functional of convex set">14</a> we can prove the following surprising topological result for convex sets.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="cor15">
<p><strong>Corollary 15 (Topological property of convex sets).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K\) is a convex set with \(0 \in \mathrm{int}\; K\). Then,</p>
<p>$$\mathrm{cl}\; \mathrm{int}\; K {}={} \mathrm{cl}\; K.$$</p>
</div>

<button onclick="toggleCollapseExpand('proofCorol15Button', 'proofCorol15Container', 'proof')" id="proofCorol15Button">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofCorol15Container">
<p><em>Proof.</em> We have</p>
<p>$$\mathrm{cl}\; \mathrm{int}\; K = [p_{\mathrm{int}\; K} \leq 1] = [p_K \leq 1] = \mathrm{cl}\; K,$$</p>
<p>which completes the proof. \(\blacksquare\)</p>
</div>

<p></p>
<p>Convexity is a necessary assumption of <a href="#cor15" title="Topological property of convex sets">Corollary 15</a>. As a counterexample, let \(X\) be a normed space, let \(\mathcal{B}\) be the unit norm ball, \(0 \neq x_0\in X\) and take \(K = \mathcal{B} \cup {\rm I\!R} x_0\), which is not convex. You can verify that \(\mathrm{cl}\; \mathrm{int}\; K {}\subsetneq{} \mathrm{cl}\; K.\)</p>


## Convex separating theorems 

<p>The Minkowski functional and the Hahn-Banach theorem allow us to prove the famous <em>separating theorems</em> or <em>separating hyperplane theorems</em> or <em>hyperplane separation theorems</em> for convex sets.</p> 

<p>We say that a nonzero continuous linear functional \(f: X \to {\rm I\!R}\) <em>separates</em> a set \(K\) and a point \(x_0\) if \(f(x) \leq f(x_0)\) for all \(x\in K\). Equivalently, we can write this as \(\sup f(K) \leq f(x_0)\). We say that \(f\) separates \(K\) and \(x_0\) <em>strictly</em> if the inequality is strict. Similarly, we say that \(f\) separates two sets \(K\) and \(L\) if \(\sup f(K) \leq \inf f(L)\).</p>

<p>We will state three separating theorems that assert the existence of such separating continuous linear functionals. The first separating theorem is about the separation of a <em>convex</em> set from a point. The second separating theorem is about the separation of two convex sets, and the third one is about the strict separation of two convex sets.</p>

### First separating theorem

<p>Let us state the first separating theorem that allows us to separate a point from a convex set using a linear function.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="first-sep-thm">
<p><strong>Theorem 16 (First separating theorem).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K\) is a convex set with a nonempty interior. Let \(x_0 \notin \mathrm{int}\; K\). Then there is a nonzero continuous linear functional, \(f: X \to {\rm I\!R}\), that separates \(x_0\) from \(K\), that is</p>
<p>$$\sup f(K) {}\leq{} f(x_0).$$</p>
</div>

<button onclick="toggleCollapseExpand('proofThm16aButton', 'proofThm16aContainer', 'proof')" id="proofThm16aButton">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofThm16aContainer">
<p><em>Proof.</em> Without loss of generality we shall assume that \(0\in \mathrm{int}\; K\). If not, we can simply take a point \(\bar{x}\) and use the change of variables \(x \mapsto x - \bar{x}\), i.e., to move the set so that zero is inside its interior.</p>
<p>Since \(x_0 \notin \mathrm{int}; K\), we have from <a href="#prop13" title="Topological properties of convex sets">Proposition 13</a> that \(p_K(x_0) \geq 1\).</p>
<p>On the space \(Y = {\rm I\!R}x_0\) we define the function</p>
<p>$$g(y) = g(\lambda x_0) = \lambda p_K(x_0).$$</p>
<p>It is easy to see that \(g(y) \leq p_K(y)\) for all \(y\in R\) and you see where this is going...</p>
<p>From the <a href="#hahn-banach-thm">Hahn-Banach theorem</a>, there is a linear functional, \(f\), that extends \(g\) to \(X\) such that \(f(x) \leq p_K(x)\) for all \(x\in X\).</p>
<p><a href="#prop4" title="Continuity of linear functionals">Proposition 4</a> implies that \(f\) is continuous on \(X\) since \(p_K\) is a continuous <abbr title="positive sublinear functional">PSLF</abbr> as we know from <a href="#prop12" title="Minkowski functional is continuous PSLF">Proposition 12</a>.</p>
<p>We have that</p>
<p>$$f(x_0){}={}g(x_0){}={}p_K(x_0)\geq 1,$$</p>
<p>so, \(f\) is a nonzero linear functional, and for all \(x\in K\), \(p_K(x) \leq 1\), therefore, \(f(x) \leq 1\).</p>
<p>This completes the proof.  \(\blacksquare\)</p>
</div>

<img src="/first-sep-thm.png" alt="First separating theorem"  style="width: 50%; margin-left: auto;margin-right: auto;"/>

<p><em><strong>Figure 1.</strong> We first define a linear function, \(g\), on \(Y = {\rm I\!R}x_0\) and use the Hahn-Banach theorem to extend it to the entire \(X\).</em></p>

<p>In the finite-dimensional case, \(X = {\rm I\!R}^n\), linear functions \(f: X \to {\rm I\!R}\) have the form of an inner product, that is, \(f(x) = c^\intercal x\) and the separation of a point \(x_0\in X\) from a convex set \(K\) with a nonempty interior reads</p>
<p>$$\sup_{x\in K} c^\intercal x \leq c^\intercal x_0 \Leftrightarrow \delta^*_K(c) \leq c^\intercal x_0,$$</p>
<p>where \(\delta^*_K\) is the <a href="../support-functions">support function</a> of \(K\).</p>

### Second separating theorem

<p>The second separating theorem allows us to separate two convex sets.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="second-sep-thm">
<p><strong>Theorem 17 (Second separating theorem).</strong> Let \(X\) be a <abbr title="topological vector space">TVS</abbr> and \(K, L\) be two convex sets, \(K\) has a nonempty interior and \(\mathrm{int}\; K \cap L = \emptyset\). Then there is a nonzero continuous linear functional, \(f: X \to {\rm I\!R}\), that separates \(K\) from \(L\), that is</p>
<p>$$\sup f(K) {}\leq{} \inf f(L).$$</p>
</div>

<img src="/second-sep-thm.png" alt="Second separating theorem" style="width: 50%; margin-left: auto;margin-right: auto;"/>

<p><em><strong>Figure 2.</strong> Second separating theorem.</em></p>

<button onclick="toggleCollapseExpand('proofThm17Button', 'proofThm17Container', 'proof')" id="proofThm17Button">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofThm17Container">
<p><em>Proof.</em> The set \(\mathrm{int}\; K - L\) is open because 
<p>$$\mathrm{int}\; K - L = \bigcup_{l \in L}(\mathrm{int}\; K - l),$$</p>
<p>so it is a union of open sets.</p>
<p>The set is convex because it is the Minkowski sum of two open sets, and \(0\notin \mathrm{int}\; K - L\). As a result, from the first separating theorem (<a href="#first-sep-thm">Theorem 16</a>), there is a nonzero continuous linear functional, \(f\), that separates \(0\) from \(\mathrm{int}\; K - L\), that is</p>
<p>$$\begin{aligned}&\sup f(\mathrm{int}\; K - L) \leq f(0) = 0\\\Rightarrow{}&\sup f(\mathrm{cl}\; \mathrm{int}\; K) \leq \inf f(L),\end{aligned}$$</p>
<p>but since \(K\) is convex, \(\mathrm{cl}\; \mathrm{int}\; K = K\), so</p>
<p>$$\sup f(K) \leq \inf f(L).$$</p>
<p>This completes the proof. \(\blacksquare\)</p>
</div>


### Third separating theorem

<p>For the third separating theorem we will need to assume that \(X\) is a <em>locally convex</em> <abbr title="topological vector space">TVS</abbr>. A <abbr title="topological vector space">TVS</abbr> is called locally convex if it has a basis of neighbourhoods of the origin consisting of convex sets.</p> 

<p>According to Proposition 4.1.12 in <a href="http://www.math.uni-konstanz.de/~infusino/TVS-WS18-19/Note2018.pdf" target="_blank">these lecture notes</a> by Maria Infusino (University of Konstanz), every locally convex <abbr title="topological vector space">TVS</abbr> has a basis of neighbourhoods of the origin consisting of open, absorbing, balanced, convex sets. </p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="third-sep-thm">
<p><strong>Theorem 18 (Third separating theorem).</strong> Let \(X\) be a locally convex <abbr title="topological vector space">TVS</abbr>, \(L\) is a nonempty closed convex set, \(K\) is a nonempty compact convex set and</p>
<p>$$K \cap L = \emptyset.$$</p>
<p>Then, there is a linear continuous functional \(f:X\to{\rm I\!R}\) that separates the two sets.</p>
</div>

<button onclick="toggleCollapseExpand('proofThm18Button', 'proofThm18Container', 'proof')" id="proofThm18Button">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofThm18Container">
<p><em>Proof.</em> Since \(K \cap L = \emptyset\), we have that \(0 \notin K - L\).</p> 

---

<p><strong>Claim.</strong> We will show that \(K-L\) is closed.</p>
<p>Equivalently, we will show that its complement is open. To that end, for \(x \notin K - L\) it suffices to find a neighbourhood of 0 which is symmetric (see the above remark) such that </p>
<p>$$\underbrace{(x+V)}_{\text{neigh. of } x} \cap (K - L) = \emptyset.$$</p>
<p>Equivalently, it suffices to find \(V\) such that</p>
<p>$$(K+V) \cap (x + L) = \emptyset.$$</p>
<p><em>Note:</em> in fact it should be \(K-V\), but \(V\) is symmetric.</p>
<p>Since \(K \cap (x+L) = \emptyset\) and \(x+L\) is closed, for all \(y \in K\) there is a neighbourhood of zero, \(V_y\), such that \((y+V_y) \cap (x + L) = \emptyset\). Then, we can determine \(U_y \ni 0\) such that \(U_y + U_y \subseteq V_y\). Now consider the following cover of \(K\)</p>
<p>$$K \subseteq \bigcup_{y \in K}(y + U_y).$$</p>
<p>Since \(K\) is compact, there is a finite subcover, i.e., there are \(y_1, \ldots, y_n\) such that</p>
<p>$$K \subseteq \bigcup_{i=1}^{n}(y_i + U_{y_i}).$$</p>
<p>Define the set</p>
<p>$$U = \bigcap_{i=1}^{n}U_{y_i},$$</p>
<p>which is an open set that contains \(0\). For every \(y\in K\) there is \(i\) such that \(y \in y_i + U_{y_i}\). Then,</p>
<p>$$y + U \subseteq y_i + U_i + U \subseteq y_i + U_i + U_i \subseteq y_i + V_{y_i}.$$</p>
<p>This means that \((y+U) \cap (x+L) \subseteq (y_i + V_{y_i}) \cap (x+L) = \emptyset.\) This proves the claim.</p>

---

<p>Since \(K-L\) is closed and \(0 \notin K-L\) there is a convex symmetric neighbourhood \(V\ni 0\) such that \(V \cap (K-L) = \emptyset\). Using <a href="#second-sep-thm" title="Second separating theorem">Theorem 17</a> we can separate \(V\) from \(K-L\), i.e., there is a nonzero linear continuous \(f: X \to {\rm I\!R}\) such that</p>
<p>$$\sup f(V) \leq \inf f(K-L) = \inf f(K) - \sup f(L).$$</p>
<p>The proof is completed by showing that \(\sup f(V) > 0\). There is an \(x\in X\) with \(f(x) > 0\). There is \(\lambda >0\) such that \(\lambda x \in V\) and \(f(\lambda x) = \lambda f(x) > 0\), so \(\sup f(V) > 0\). $\blacksquare$</p>
</div>

<p></p>
<p>Next we will show that every closed convex set in a locally convex <abbr title="topological vector space">TVS</abbr> can be written as an intersection of halfspaces. Recall that a halfspace is a set of the form</p>
<p>$$H = \{x \in X {}:{} f(x) \leq a\} = f^{-1}((-\infty, a]),$$</p>
<p>where \(f: X \to {\rm I\!R}\) is a continuous linear functional.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 0px 0px 10px; margin-bottom: 10px" id="intersection-halfspaces">
<p><strong>Proposition 19 (Representation of convex sets).</strong> Let \(X\) be a locally convex <abbr title="topological vector space">TVS</abbr>, and \(K\) is a nonempty closed convex set. Then \(K\) can be written as the intersection of a famiily of halfspaces.</p>
</div>

<button onclick="toggleCollapseExpand('proofThm19Button', 'proofThm19Container', 'proof')" id="proofThm19Button">
  <i class="fa fa-cog fa-spin"></i> Expand proof
</button>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofThm19Container">
<p><em>Proof.</em> Take \(x\notin K\). Since \(\{x\}\) is a compact and convex, from <a href="#third-sep-thm" title="Third separating theorem">Theorem 18</a>, there is a continuous linear operator, \(f_{x}\) such that \(\sup f_x(K) < s_x < f_x(x)\). Clearly</p>
<p>$$K \subseteq \bigcap_{x\notin K}f_{x}^{-1}((-\infty, s_x]).$$</p>
<p>To show that the above intersection is a subset of \(K\) it suffices to show that if \(x_0 \notin K\), then \(x_0 \notin \bigcap_{x\notin K}f_{x}^{-1}((-\infty, s_x])\), which is immediate. \(\blacksquare\)</p>
</div>
<p></p>

## Read next

- [From Separation Theorems to Farkas' Lemma](../farkas-separation)