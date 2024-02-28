---
author: "Pantelis Sopasakis"
title:  "Tensor product via universality"
date: 2024-02-28
description: "Tensor products and universality"
summary: "Here we look at the universality-based definition of the tensor product"
math: true
series: ["Mathematix"]
tags: ["Tensors", "Algebra"]
collapsible: true
---


<p>We start by defining the <a href="/posts/maths/tensor-product">tensor product</a> of two vector spaces $V$ and $W$ via the universal property. Recall the definition of the tensor product of two vector spaces using the approach of universality<sup>[<a href="#cite:1">1</a>]</sup> <sup>[<a href="#cite:2">2</a>]</sup> <sup>[<a href="#cite:3">3</a>]</sup>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="defn">
    <p><strong>Definition: tensor product.</strong> Let $V$ and $W$ be two vector spaces. The tensor product of $V$ and $W$ is a vector space $T$ along with a bilinear map $\tau:V\times W \to T$ such that for every bilinear map </p>
    <p>$$f:V\times W \to U,$$</p>
    <p>where $U$ is a vector space, there is a unique <em>linear</em> map $\tilde{f}:T\to U$ such that</p>
    <p>$$\tilde{f} \circ \tau = f,$$</p>
    <p>i.e., the following diagram commutes</p>
    <div id="fig1">
        <img src="/tensor-product-commutative-1.png" alt="Commutative diagram demonstrating the universal property"  style="width: 55%; margin-left: auto;margin-right: auto;">
        <p><em><strong>Figure 1.</strong> Commutative diagram demonstrating the universal property.</em></p>
    </div>
</div>

<p>The mysterious vector space $T$ is called the tensor product of $V$ and $W$ and can be denoted by $T = V\otimes W$. The bilinear map $\tau$ is called the tensor product bilinear map, or just <em>tensor product</em> of two vectors; we also denote $\tau(u, v) = u \otimes v$.</p>

<p>Note that a tensor product is a <em>pair</em> of a vector space, $V\otimes W$ and a bilinear map, $\tau: V\times W \to V\otimes W$.</p>

We prove the following<sup>[<a href="#cite:2">2</a>]</sup>


<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="defn">
    <p><strong>Uniqueness up to isomorphism.</strong> Tensor products are unique up to isomorphism, i.e., given two tensor products $(T_1, \tau_1)$ and $(T_2, \tau_2)$, </p>
    <p>$$T_1\cong T_2.$$</p>
</div>

<p><em>Proof.</em> We apply the definition of the tensor product with $\tau_2$ in place of the bilinear map $f$ and using the tensor product space $T_1$ as in the following graph</p>
<div id="fig2">
        <img src="/tensor-product-commutative-2.png" alt="Commutative diagram 2."  style="width: 45%; margin-left: auto;margin-right: auto;">
        <p><em><strong>Figure 2.</strong> Commutative diagram.</em></p>
</div>

<p>From Figure 2 we see that</p>
<p>$$\tau_2 = \phi_{12} \circ \tau_1.\tag{1}$$</p>
<p>Next, we swap $T_1$ and $T_2$...</p>
<div id="fig3">
        <img src="/tensor-product-commutative-3.png" alt="Commutative diagram 3."  style="width: 45%; margin-left: auto;margin-right: auto;">
        <p><em><strong>Figure 3.</strong> Commutative diagram.</em></p>
</div>

<p>We see that</p>
<p>$$\tau_1 = \phi_{21}\circ \tau_2.\tag{2}$$</p>

<p>From Equations (1) and (2),</p>
<p>$$\tau_1 = \phi_{21}\circ \phi_{12}\circ \tau_1.\tag{3}$$</p>
<p>This makes us suspect that $\phi_{12} = \phi_{21}^{-1}$. To prove this, we put $T_1$ in both places in the commutative diagram as follows:</p>
<div id="fig4">
        <img src="/tensor-product-commutative-4.png" alt="Commutative diagram 4."  style="width: 45%; margin-left: auto;margin-right: auto;">
        <p><em><strong>Figure 4.</strong> Commutative diagram with $T_1$ and $T_1$ (twice).</em></p>
</div>


<p>By the uniqueness of the linear map $T_1\to T_1$ and since ${\rm id}_{T_1}:T_1\to T_1$ does the job we conclude that only ${\rm id}_{T_1}$ is such that ${\rm id}_{T_1} \circ \tau_1 = \tau_1$, so in Equation (3) we have</p> 
<p>$$\phi_{12}\circ \phi_{21} = {\rm id}_{T_1}.\tag{4}$$</p>
<p>Likewise, we can show that</p>
<p>$$\phi_{21}\circ \phi_{12} = {\rm id}_{T_{2}}.\tag{5}$$</p>
<p>The map $\phi_{12}:T_1 \to T_2$ is a vector space isomorphism, which completes the proof. $\Box$</p>


### Existence

<p>The existence of the tensor product is established constructively using the concept of the free vector space. The above definition of course does not prove that the tensor product exists, and neither does the uniqueness statement above.</p>

### Example: trace

<p>The mapping $\langle {}\cdot{}, {}\cdot{}\rangle: V^*\times V\to \R$ defined as $\langle f, v\rangle = f(v)$ is the natural pairing of $V$ and its dual map. It is easy to see that it is bilinear. Then, we know that there exists a <em>linear</em> map $V^*\otimes V\to \R$ which we call <em>trace</em> and is defined as</p> 
<p>$${\rm tr}(f\otimes v) = \langle f, v\rangle = f(v).$$</p>
<div id="fig5">
        <img src="/tensor-product-commutative-5.png" alt="Trace definition using universal property"  style="width: 45%; margin-left: auto;margin-right: auto;">
        <p><em><strong>Figure 5.</strong> Trace definition using universal property.</em></p>
</div>


## References

<ol>
    <li id="cite:1">Proof: <a href="https://www.youtube.com/watch?v=VJJK2BoIaD8">Uniqueness of the Tensor Product</a>, YouTube video by Mu Prime Math</li>  
    <li id="cite:2">Lecture notes on <a href="https://www-users.cse.umn.edu/~garrett/m/algebra/notes/27.pdf">tensor products</a> , accessed on 8 November 2023</li>  
    <li id="cite:3">Joel Kamnitzer, <a href="http://www.math.toronto.edu/~jkamnitz/courses/mat247/tensorproducts2.pdf">lecture notes on tensor products</a>, accessed on 8 November 2023</li>
</ol>


