---
author: "Pantelis Sopasakis"
title:  "Making sense of tensors and tensor products"
date: 2024-02-16
description: "Tensor products"
summary: "We are trying to make sense of tensors and the tensor product of vector spaces"
math: true
series: ["Mathematix"]
tags: ["Tensors", "Algebra"]
collapsible: true
---

<p>I was trying to make sense of tensor products; here are some notes on the topic.</p>

## As multilinear maps

<p>Let $(V, +, \cdot)$ be a vector space. Let $r$, $s$ be nonnegative integers. An $(r, s)$-tensor over $V$ - let us call it $T$ - is a multilinear map <sup>[<a href="#cite:1">1</a>]</sup>, <sup>[<a href="#cite:2">2</a>]</sup>, <sup>[<a href="#cite:3">3</a>]</sup></p>

<p>$$T:\underbrace{V^* \times \ldots \times V^*}_{r \text{ times}} \times \underbrace{V \times \ldots \times V}_{s \text{ times}} \to {\rm I\!R},$$</p>
<p>where $V^*$ is the dual vector space of $V$ - the space of covectors.</p>
<p>Before we explain what <em>multilinearity</em> is let's give an example.</p>
<p>Let's say $T$ is a $(1, 1)$-tensor. Then $T: V^* \times V \to {\rm I\!R}$, that is $T$ takes a covector and a vector and multilinearity means that for two covectors $\phi, \psi\in V^*$,</p>
<p>$$T(\phi+\psi, v) = T(\phi, v) + T(\psi, v),$$</p>
<p>and</p>
<p>$$T(\lambda \phi, v) = \lambda T(\phi, v),$$</p>
<p>for all $v\in V$, <em>and</em> it is also linear in the second argument, that is, </p>
<p>$$T(\phi, v+w) = T(\phi, v) + T(\phi, w),$$</p>
<p>and</p>
<p>$$T(\phi, \lambda v) = \lambda T(\phi, v).$$</p>
<p>Using these properties twice we can see that</p>
<p>$$T(\phi+\psi, v+w) = T(\phi, v) + T(\phi, w) + T(\psi, v) + T(\psi, w).$$</p>

<p><b>Example: A $(0, 2)$-tensor.</b> Let us denote the set of polynomials with real coefficients is denoted by $\mathsf{P}$. Define the map</p>
<p>$$g: (p, q) \mapsto g(p, q) \coloneqq \int_0^1 p(x)q(x){\rm d}x.$$</p>
<p>Then this is a $(0, 2)$-tensor,</p>
<p>$$g: \mathsf{P} \times \mathsf{P} \to {\rm I\!R},$$</p>
<p>and multilinearity is easy to check.</p>

<p>It becomes evident that an inner product is a $(0, 2)$-tensor. More precisely, an inner product is a bilinear symmetric positive definite operator $V\times V \to {\rm I\!R}$.</p>

<p><b>Example: Covectors as tensors.</b> It is easy to see that covectors, $\phi: V\to {\rm I\!R}$ are $(0, 1)$-tensors. Trivially. </p>

<p><b>Example: Vectors as tensors.</b> Given a vector $v\in V$ we can consider the mapping</p>
<p>$$T_v: V^* \ni \phi \mapsto T_v(\phi) = \phi(v) \in {\rm I\!R}.$$</p>
<p>This makes $T_v$ into a $(1, 0)$-tensor. </p>

<p><b>Example: linear maps as tensors.</b> We can see a linear map $\phi \in {\rm Hom}(V, V)$ as a $(1,1)$-tensor</p>
<p>$$T_\phi: V^* \times V \ni (\psi, v) \mapsto T_\phi(\psi, v) = \psi(\phi(v)) \in {\rm I\!R}.$$</p>


## Components of a tensor

<p>Let $T$ be an $(r, s)$-tensor over a finite-dimensional vector space $V$ and let $\{e_i\}_i$ be a basis for $V$. Let the dual basis, for $V^*$, be $\{\epsilon^i\}_i$. The two bases have the same cardinality.  Then define the $(r+s)^{\dim V}$ many numbers<p>
<p>$$T^{i_1, \ldots, i_r}_{j_1, \ldots, j_s} = T(\epsilon^{i_1}, \ldots, \epsilon^{i_r}, e_{j_1}, \ldots, e_{j_s}).$$</p>
<p>These are the components of $T$ with respect to the given basis.</p>

> This allows us to conceptualise a tensor as a multidimensional (multi-indexed) array. But maybe we shouldn't... This is as bad as treating vectors as sequences of numbers, or matrices as "tables" instead of elements of a vector space and linear maps respectively.

<p>Let's see how exactly this works via an example <sup>[<a href="#cite:4">4</a>]</sup>. Indeed, consider an $(2,3)$-tensor of the tensor space $\mathcal{T}^{2}_{3} = V^{\otimes 2} \otimes (V^*)^{\otimes 3}$ , which can be seen as a multilinear map</p>
<p>$$T:V^*\times V^*\times V \times V \times V \to {\rm I\!R}.$$</p>
<p>Yes, we have two $V^*$ and three $V$!</p>

<p>Take a basis $(e_i)_i$ of $V$ and a basis $(\theta^j)_j$ of $V^*$. Let us start with an example using a pure tensor of the form $e_{i_1}\otimes e_{i_2} \otimes e_{i_3} \otimes \theta^{j_1} \otimes \theta^{j_2},$ for some indices $i_1,i_2,i_3$ ,and $j_1, j_2$. This can be seen as a map $V^*\times V^*\times V \times V \times V \to {\rm I\!R}$, which is defined as</p>
<p>$$\begin{aligned}(\theta^{j_1} \otimes \theta^{j_2} \otimes e_{i_1}\otimes e_{i_2} \otimes e_{i_3})
(\bar{e}_1, \bar{e}_2, \bar{\theta}^1, \bar{\theta}^2, \bar{\theta}^3)
\\
{}={}
\langle \theta^{j_1}, \bar{e}_1\rangle
\langle \theta^{j_2}, \bar{e}_2\rangle
\langle e_{i_1}, \bar{\theta}^1\rangle
\langle e_{i_2}, \bar{\theta}^2\rangle
\langle e_{i_3}, \bar{\theta}^3\rangle,\end{aligned}$$</p>
<p>where $\langle {}\cdot{}, {}\cdot{}\rangle$ is the natural pairing between $V$ and its dual, so</p> 
<p>$$\begin{aligned}
(\theta^{j_1} \otimes \theta^{j_2} \otimes e_{i_1}\otimes e_{i_2} \otimes e_{i_3})
(\bar{e}_1, \bar{e}_2, \bar{\theta}^1, \bar{\theta}^2, \bar{\theta}^3)
\\{}={}
\theta^{j_1}(\bar{e}_1)
\theta^{j_2}(\bar{e}_2)
\bar{\theta}^1(e_{i_1})
\bar{\theta}^2(e_{i_2})
\bar{\theta}^3(e_{i_3}).\end{aligned}$$</p>
<p>More specifically, when the above tensor is applied to a basis vector $(e_{i_1'}, e_{i_2'}, \theta^{j_1'}, \theta^{j_2'}, \theta^{j_3'})$, then the result is</p>
<p>$$\begin{aligned}
&(\theta^{j_1} \otimes \theta^{j_2} \otimes e_{i_1}\otimes e_{i_2} \otimes e_{i_3})
(e_{i_1'}, e_{i_2'}, \theta^{j_1'}, \theta^{j_2'}, \theta^{j_3'})
\\
{}={}&
\theta^{j_1}(e_{i_1'})
\theta^{j_2}(e_{i_2'})
\theta^{j_1'}(e_{i_1})
\theta^{j_2'}(e_{i_2})
\theta^{j_3'}(e_{i_3})
\\
{}={}&
\delta_{i_1' j_1}
\delta_{i_2' j_2}
\delta_{i_1 j_1'}
\delta_{i_2 j_2'}
\delta_{i_3 j_3'}.
\end{aligned}$$</p>
<p>A <em>general</em> tensor of $\mathcal{T}^{2}_{3}$ has the form<p> 
<p>$$T 
{}={}
\sum_{
\substack{i_1, i_2, i_3 \\ j_1, j_2}
}
T_{j_1, j_2}^{i_1, i_2, i_3}
(\theta^{j_1} \otimes \theta^{j_2} \otimes e_{i_1}\otimes e_{i_2} \otimes e_{i_3}),$$</p>
<p>for some parameters (components) $T_{j_1, j_2}^{i_1, i_2, i_3}$. This can be seen as a mapping $T:V^*\times V^* \times V^* \times V  \times V \to {\rm I\!R}$ that acts on elements of the form</p>
<p>$$x 
{}={} 
\left(
\sum_{j_1}a^1_{j_1}\theta^{j_1}, 
\sum_{j_2}a^2_{j_2}\theta^{j_2}, 
\sum_{j_3}a^3_{j_3}\theta^{j_3},
\sum_{i_1}b^1_{i_1}e_{i_1},
\sum_{i_2}b^1_{i_2}e_{i_2},
\sum_{i_3}b^1_{i_3}e_{i_3}
\right),$$</p>
<p>and gives</p>
<p>$$\begin{aligned}
Tx 
{}={}& 
\sum_{
\substack{i_1, i_2, i_3 \\ j_1, j_2}
}
T_{j_1, j_2}^{i_1, i_2, i_3}
(e_{i_1}, e_{i_2}, e_{i_3}, \theta^{j_1}, \theta^{j_2})(x)
\\
{}={}&
\sum_{
\substack{i_1, i_2, i_3 \\ j_1, j_2}
}
T_{j_1, j_2}^{i_1, i_2, i_3}
\left\langle e_{i_1}, \sum_{j_1'}a^1_{j_1'}\theta^{j_1'}\right\rangle
\left\langle e_{i_2}, \sum_{j_2'}a^1_{j_2'}\theta^{j_2'}\right\rangle
\\
&\qquad\qquad\qquad\left\langle e_{i_3}, \sum_{j_3'}a^1_{j_3'}\theta^{j_3'}\right\rangle
\left\langle \theta_{j_1}, \sum_{i_1'}b^1_{i_1'}e^{i_1'}\right\rangle
\left\langle \theta_{j_2}, \sum_{i_2'}b^2_{i_2'}e^{i_2'}\right\rangle
\\
{}={}& 
\sum_{
\substack{i_1, i_2, i_3 \\ j_1, j_2}
}
T_{j_1, j_2}^{i_1, i_2, i_3}
a^1_{i_1}a^2_{i_2}a^3_{i_3}b^1_{j_1}b^1_{j_2}.
\end{aligned}$$</p>


## As a quotient on a huge space


<p>Here we construct a huge vector space and apply a quotient to enforce the axioms we expect tensors and tensor products to have. This huge space is a space of functions sometimes referred to as the "formal product" <sup>[<a href="#cite:5">5</a>]</sup>. See also this video <sup>[<a href="#cite:7">7</a>]</sup>.</p>

<p>We will define the tensor product of two vector spaces. Let $V, W$ be two vector spaces. We define a vector space $V*W$, which we will call the formal product of $V$ and $W$, as the linear space that has $V\times W$ as a Hamel basis.  This space is also known as the free vector space, $V*W = {\rm Free}(V\times W)$.</p>

<p>To make this more concrete, we can identify $V*W$ by the space of functions $\varphi: V\times W \to {\rm I\!R}$ with finite support. Representatives (and a basis) for this set are the functions</p>
<p>$$\delta_{v, w}(x, y) 
{}={} 
\begin{cases}
1, & \text{ if } (x,y)=(v,w)
\\
0,& \text{ otherwise}
\end{cases}$$</p>
<p>Indeed, every function $f:V\times W\to{\rm I\!R}$ with finite support (a function of $V*W$) can be written as a finite combination of such $\delta$ functions and each $\delta$ function is identified by a pair $(v,w)\in V\times W$.</p>

<p>Note that $V\times W$ is a vector space when equipped with the natural operations of function addition and scalar multiplication.</p>

<p>We consider the natural embedding, $\delta$, of $V\times W$ into $V*W$, which is naturally defined as</p>
<p>$$\delta:V\times W \ni (v_0, w_0) \mapsto \delta_{v_0, w_0} \in V * W.$$</p>
<p>Consider now the following subspace of $V*W$</p>
<p>$$M_0 {}={} \operatorname{span}
\left\{
\begin{array}{l}
\delta(v_1+v_2, w) - \delta(v_1, w) - \delta(v_2, w),
\\
\delta(v, w_1+w_2) - \delta(v, w_1) - \delta(v, w_2),
\\
\delta(\lambda v, w) - \lambda \delta(v, w),
\\
\delta(v, \lambda w) - \lambda \delta(v, w),
\\
v, v_1, v_2 \in V, w, w_1, w_2 \in W, \lambda \in {\rm I\!R}
\end{array}
\right\}$$</p>


> **Quotient space definition of tensor space.**
>
> We define the tensor product of $V$ with $W$ as 
> $$V\otimes W = \frac{V * W }{M_0}.$$
> This is called the tensor space of $V$ with $W$ and its elements are called tensors.


<p>This is the space we were looking for. Here's what we mean: we have already defined the mapping $\delta: V\times W \to V * W$. We also define the canonical embedding $\pi: V*W \to V \otimes M_0$. We then define the <em>tensor product</em> of $v\in V$ and $w\in W$ as</p>
<p>$$v\otimes w = (\pi {}\circ{} \delta)(v, w) = \delta_{v, w} {}+{} M_0.$$</p>
<p>It is a mapping $\otimes: V\times W \to V\otimes W$ and we can see that it is bilinear.</p>

> **Properties of $\otimes$.**
>
> The operator $\otimes$ is bilinear.

<p><em>Proof.</em> For $v\in V$, $w\in W$ and $\lambda \in {\rm I\!R}$ we have</p>
<p>$$\begin{aligned}
(\lambda v)\otimes w 
{}={}&
\delta_{\lambda v, w} + M_0
\\
{}={}& 
\underbrace{\delta_{\lambda v, w} - \lambda \delta_{v, w}}_{\in{}M_0} + \lambda \delta_{v, w} + M_0
\\
{}={}&
\lambda \delta_{v, w} + M_0
\\
{}={}&
\lambda (\delta_{v, w} + M_0)
\\
{}={}&
\lambda (v\otimes w).
\end{aligned}$$</p>
<p>Likewise, for $v_1, v_2 \in V$, $w\in W$, $\lambda \in {\rm I\!R}$,</p>
<p>$$\begin{aligned}
(v_1 + v_2)\otimes w 
{}={}&
\delta_{v_1+v_2, w} + M_0
\\
{}={}&
\underbrace{\delta_{v_1+v_2, w} - \delta_{v_1, w} -\delta_{v_2, w}}_{\in {} M_0} + \delta_{v_1, w} + \delta_{v_2, w} + M_0
\\
{}={}&
\delta_{v_1, w} + \delta_{v_2, w} + M_0
\\
{}={}&
(\delta_{v_1, w} + M_0) + (\delta_{v_2, w} + M_0)
\\
{}={}&
v_1\otimes w + v_2 \otimes w
\end{aligned}$$</p>
<p>The other properties are proved likewise. $\Box$</p>


## Universal property 

<p>Here's how I understand the universal property: Suppose we know that we have a function $f: V\times W \to{} ?$, which is <em>bilinear</em>. We can always think of the mysterious space $?$ as the tensor space $V\otimes W$ <sup>[<a href="#cite:5">5</a>]</sup>.</p>

<p>Let's look at Figure 1.</p>

<div id="fig1">
<img src="/tensor-product-universal-product.png" alt="Universal property of tensor product"  style="width: 45%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 1.</strong> Universal property of tensor product.</em></p>
</div>

<p>There is a unique <em>linear</em> function $\tilde{f}:V\otimes W \to{} ?$ such that</p>
<p>$$f(v, w) = \tilde{f}(v\otimes w).$$</p>
<p>Let us underline that $\tilde{f}$ is linear! This makes $\otimes$ a <em>prototype bilinear function</em> as any other bilinear function is a linear map of precisely this one.</p>






## Dimension

<p>Let $V$ and $W$ be finite dimensional. We will show that</p>

> **Dimension of tensor**
>
> $$\dim(V\otimes W) = \dim V \dim W.$$

<p><em>Proof 1.</em> To that end we use the fact that the dual vector space has the same dimension as the original vector space. That is, the dimension of $V\otimes W$ is the dimension of $(V\otimes W)^*.$</p>

<p>The space $(V\otimes W)^* = {\rm Hom}(V\otimes W, {\rm I\!R})$ is the space of bilinear maps $V\times W \to {\rm I\!R}$.</p>

<p>Suppose $V$ has the basis $\{e^V_1, \ldots, e^V_{n_V}\}$  and $W$ has the basis $\{e^W_1, \ldots, e^W_{n_W}\}$.</p>

<p>To form a basis for the space of bilinear maps $f:V\times W\to{\rm I\!R}$ we need to identify every such function with a sequence of scalars. We have</p>
<p>$$f(u, v) = f\left(\sum_{i=1}^{n_V}a^V_{i}e^V_{i}, \sum_{i=1}^{n_W}a^W_{i}e^W_{i}\right).$$</p>
<p>From the bilinearity of $f$ we have</p>
<p>$$f(u, v) = \sum_{i=1}^{n_V}\sum_{j=1}^{n_W} a^V_{i}a^W_{j} f(e^V_{i}, e^{W}_{j}).$$</p>
<p>The right hand side is a bilinear function and the coefficients $(a^V_i, a^W_j)$ suggest that the dimension if $n_V n_W$. $\Box$</p>

<p><em>Proof.</em> This is due to <sup>[<a href="#cite:22">22</a>]</sup>. We can write any $T \in V\otimes W$ as</p> 
<p>$$T = \sum_{k=1}^{n}a_k \otimes b_k,$$</p>
<p>for $a_k\in V$ and $b_k\in W$ and some finite $n$. If we take bases $\{v_i\}_{i=1}^{n_V}$ and $\{w_i\}_{i=1}^{n_W}$ we can write</p>
<p>$$a_k = \sum_{i=1}^{n_V}\alpha_{ki}v_i,$$</p>
<p>and</p>
<p>$$b_k = \sum_{j=1}^{n_W}\beta_{kj}w_j,$$</p>
<p>therefore,</p>
<p>$$\begin{aligned}T 
{}={}& 
\sum_{i=1}^{n}\left(\sum_{i=1}^{n_V}\alpha_{ki}v_i\right) \otimes\left(\sum_{j=1}^{n_W}\beta_{kj}w_j\right)
\\
{}={}&
\sum_{i=1}^{n} \sum_{i=1}^{n_V} \sum_{j=1}^{n_W} \alpha_{ki}\beta_{kj} v_i\otimes w_j.
\end{aligned}$$</p>
<p>This means that $\{v_i\otimes w_j\}$ is a basis of $V\otimes W$.</p>


## Tensor basis

<p>In the finite-dimensional case, the basis of $V\otimes W$ can be constructed from the bases of $V$ and $W$, $\{e^V_1, \ldots, e^V_{n_V}\}$  and $\{e^W_1, \ldots, e^W_{n_W}\}$ as the set</p>
<p>$$\mathcal{B}_{V\otimes W} = \{e^V_i \otimes e^{W}_j, i=1,\ldots, n_V, j=1,\ldots, n_W\}.$$</p>
<p>This implies that</p>
<p>$$\dim (V\otimes W) = \dim V \dim W.$$</p>

## Tensor products of spaces of functions

<p>We need first to define the function space $F(S)$ as in Kostrikin<sup>[<a href="#cite:2">2</a>]</sup>.</p>

<p>Let $S$ be any set. We define the set $F(S)$—we can denote it also as ${\rm Funct}(S, {\rm I\!R})$—as the set of all functions from $S$ to ${\rm I\!R}$. If $f\in F(S)$, then $f$ is a function $f:S\to{\rm I\!R}$ and $f(s)$ denotes the value at $s\in S$.</p>

<p>On $F(S)$ we define addition and scalar multiplication in a pointwise manner: For $f, g\in F(S)$ and $c\in {\rm I\!R}$,</p>
<p>$$\begin{aligned}
(f+g)(s) {}={}& f(s) + g(s),
\\
(cf)(s) {}={}& c f(s).
\end{aligned}$$</p>
<p>This makes $F(S)$ into a vector space. Note that $S$ is not necessarily a vector space.</p>

<p>If $S = \{s_1, \ldots, s_n\}$ is a finite set, $F(S)$ can be identified with ${\rm I\!R}^n$. After all, for every $f\in F(S)$ all you need to know is $f(s_1), \ldots, f(s_n)$.</p>

<p>Every element $s\in S$ is associated with the delta function</p>
<p>$$\delta_{s}(\sigma) = \begin{cases}
1, &\text{ if } \sigma = s,
\\
0, &\text{ otherwise}
\end{cases}$$</p>
<p>The function $\delta_s:S \to \{0,1\}$ is called <em>Kronecker's delta</em>.</p>

<p>If $S$ is finite, then every $f\in S$ can be written as</p>
<p>$$f = \sum_{s\in S} a_s \delta_s.$$</p>

<p>Let $S_1$ and $S_2$ be <em>finite<em> sets and let $F(S_1)$ and $F(S_2)$ be the corresponding function spaces. Then, there is a canonical identity of the form</p>
<p>$$\underbrace{F(\underbrace{S_1 \times S_2}_{\text{Finite set of pairs}})}_{\text{Has }\delta_{s_1, s_2}\text{ as basis}} = F(S_1) \otimes F(S_2),$$</p>
<p>which associates each function $\delta_{s_1, s_2}$ with $\delta_{s_1} \otimes \delta_{s_2}$.</p>

<p>If $f_1 \in F(S_1)$ and $f_2 \in F(S_2)$ then using the standard bases of $F(S_1)$ and $F(S_2)$</p>
<p>$$f_1 \otimes f_2 = 
\left(\sum_{s_1 \in S_1}f_1(s_1) \delta_{s_1}\right)
\otimes 
\left(\sum_{s_1 \in S_2}f_2(s_2) \delta_{s_2}\right).$$</p>

> <p><b>Isomorphism $(U\otimes V)^* \cong U^* \otimes V^*$.</b></p>
>
> We have the isomorphism of vector spaces $(U\otimes V)^* \cong U^* \otimes V^*$ with isomorphism map 
> <p>$$\rho:U^* \otimes V^* \to (U\otimes V)^*,$$</p>
> <p>where for $f\in U^*$ and $g\in V^*$,</p> 
> <p>$$\rho(f\otimes g)(u\otimes v) = f(u)g(v).$$</p>

<p>For short, we write $(f\otimes g)(u\otimes v) = f(u)g(v)$.</p>

<p>Roman <sup>[<a href="#cite:5">5</a>]</sup> in Theorem 14.7 proves that $\rho$ is indeed an isomorphism.</p>



## Associativity

<p>As Kostrikin notes <sup>[<a href="#cite:2">2</a>]</sup>, the spaces $(L_1\otimes L_2)\otimes L_3$ and $L_1 \otimes (L_2 \otimes L_3)$ do not coincide — they are spaces of different type. They, however, can be found to be isomorphic via a canonical isomorphism.</p>

<p>We will start by studying the relationship between $L_1 \otimes L_2 \otimes L_3$ and $(L_1 \otimes L_2) \otimes L_3$. </p>

<p>The mapping $L_1 \times L_2 \ni (l_1, l_2) \mapsto l_1 \otimes l_2 \in L_1 \otimes L_2$ is bilinear, so the mapping </p>

<p>$$L_1 \times L_2 \times L_2 \ni (l_1, l_2, l_3) \mapsto 
(l_1 \otimes l_2) \otimes l_2 \in (L_1 \otimes L_2) \otimes L_3$$</p>
<p>is trilinear, so it can be constructed via the unique linear map</p>
<p>$$L_1 \otimes L_2 \otimes L_3 \to (L_1 \otimes L_2) \otimes L_3,$$</p>
<p>that maps $l_1 \otimes l_2 \otimes l_3$ to $(l_1 \otimes l_2) \otimes l_3$. Using bases we can show that this map is an isomorphism.</p>


## Commutativity and the braiding map

> See [Wikipedia](https://en.wikipedia.org/wiki/Tensor_product#Commutativity_as_vector_space_operation).

<p>As a note, take $x = (x_1, x_2)$ and $y = (y_1, y_2)$. Then $x\otimes y$ and $y\otimes x$ look like</p>
<p>$$\begin{bmatrix}x_1y_1\\x_1y_2\\x_2y_1\\x_2y_2\end{bmatrix}, \begin{bmatrix}x_1y_1\\x_2y_1\\x_1y_2\\x_2y_2\end{bmatrix}$$</p>
<p>and we see that the two vectors contain the same elements in different order. In that sense,</p>
<p>$$V\otimes W \cong W \otimes V.$$</p>
<p>The corresponding map, $V\otimes V \ni v\otimes v' \mapsto v'\otimes v \in V\otimes V$ is called the <em>braiding map</em> and it induces an automorphism on $V\otimes V$.</p>

## Some key isomorphisms

### Result 1: Linear maps as tensors

> This is only true in the finite dimensional case.

<p>To prove this we build a natural isomorphism</p>
<p>$$\Phi:V^*\otimes W \to {\rm Hom}(V, W),$$</p>
<p>by defining</p>
<p>$$\Phi(v^*\otimes w)(v) = v^*(v)w.$$</p>
<p>Note that $v^*\otimes w$ is a <em>pure</em> tensor. A general tensor has the form</p>
<p>$$\sum_i v_i^*\otimes w_i,$$</p>
<p>and</p>
<p>$$\Phi\left(\sum_i v_i^*\otimes w_i\right)(v) = \sum_i v_i^*(v)w_i.$$</p>
<p>This is a linear map. Linearity is easy to see. See also this video <sup>[<a href="#cite:6">6</a>]</sup>.</p>

<p>Here is the statement:</p>

> <p>First isomorphism result: ${\rm Hom}(V, W) \cong V^* \otimes W$.</p>
>
> <p>In the finite-dimensional case, we have that ${\rm Hom}(V, W) \cong V^* \otimes W$ holds with isomorphism $\phi \otimes w \mapsto (v \mapsto \phi(v)w).$</p>

<p><em>Proof.</em> <sup>[<a href="#cite:10">10</a>]</sup> The proposed map, $\phi \otimes w \mapsto (v \mapsto \phi(v)w)$, is a linear map $V^*\otimes W\to {\rm Hom}(V, W)$. We will construct its inverse (and prove that it is the inverse). Let $(e_i)_i$ be a basis for $V$. Let $(e_i^*)_i$ be the naturally induced basis of the dual vector space, $V^*$. We define the mapping</p>
<p>$$g:{\rm Hom}(V, W) \ni \phi \mapsto \sum_{i}e_i^* \otimes \phi(e_i) \in V^*\otimes W.$$</p>
<p>We claim that $g$ is the inverse of $\Phi$ which we already defined to be the map $V^*\otimes W \to {\rm Hom}(V, W)$ given by $\Phi(v^*\otimes w)(v) = v^*(v)w.$ Indeed, we see that</p>
<p>$$\begin{aligned}
\Phi(g(\phi)) 
{}={}&
\Phi\left(\sum_{i=1}^{n}e_i^* \otimes \phi(e_i)\right)
&&\text{Definition of $g$}
\\
{}={}&
\sum_{i=1}^{n} \Phi\left(e_i^* \otimes \phi(e_i)\right)
&&\text{$\Phi$ is linear}
\\
{}={}&
\sum_{i=1}^{n}e_i^*({}\cdot{})\phi(e_i)
\\
{}={}&
\phi\left(\underbrace{e_i^*({}\cdot{})e_i}_{{\rm id}}\right) 
&&
\text{$\phi$ is linear}
\\
{}={}& \phi.
\end{aligned}$$</p>
<p>Conversely,</p>
<p>$$\begin{aligned}
g(\Phi(v^*\otimes w))
{}={}&
g(v^*(\cdot)w)
\\
{}={}&
\sum_{i=1}^{n}e_i^* \otimes v^*(e_i)w
\\
{}={}&
\left(\sum_{i=1}^{n}e_i^*  v^*(e_i)\right) \otimes w
\\
{}={}&
v^*\otimes w.
\end{aligned}$$</p>
<p>This completes the proof. $\Box$</p>



### Result 2: Dual of space of linear maps

<p>For two finite-dimensional spaces $V$ and $W$, it is </p>
<p>$$\begin{aligned}
{\rm Hom}(V, W)^* 
{}\cong{}
(V^*\otimes W)^*
{}\cong{}
V^{**}\otimes W^*
{}\cong{}
V\otimes W^*
{}\cong{}
{\rm Hom}(W, V).
\end{aligned}$$</p>

> It is ${\rm Hom}(V, W)^* {}\cong{} {\rm Hom}(W, V).$

<p>Some additional consequences of this are:</p>

<ol>
<li>${\rm Hom}({\rm Hom}(V,W),U)  \cong {\rm Hom}(V,W)^*\otimes U \cong (V^*\otimes W)^*\otimes U \cong V\otimes W^* \otimes U.$</li>
<li>$U\otimes V \otimes W \cong {\rm Hom}(U^*, V)\otimes W \cong {\rm Hom}({\rm Hom}(V,U^*),W)$</li>
<li>$V\otimes V^* \cong {\rm Hom}(V^*, V) \cong {\rm Hom}(V,V)$, where if $V$ is finite dimensional, $V^*\cong V$, so we see that $V^*\otimes V \cong {\rm End}(V)$ </li>
</ol>

> <p><b>Question:</b> How can we describe linear maps from ${\rm I\!R}^{m\times n}$ to ${\rm I\!R}^{p\times q}$ with sensors?</p>

<p>We are talking about the space ${\rm Hom}({\rm I\!R}^{m\times n}, {\rm I\!R}^{p\times q})$, but every matrix $A$ can be identified by the linear map $x\mapsto Ax$, so ${\rm I\!R}^{m\times n}\cong {\rm Hom}({\rm I\!R}^{n}, {\rm I\!R}^{m})$, so</p>
<p>$$\begin{aligned}
{\rm Hom}({\rm I\!R}^{m\times n}, {\rm I\!R}^{p\times q})
{}\cong{}&
{\rm Hom}({\rm Hom}({\rm I\!R}^n, {\rm I\!R}^m), {\rm Hom}({\rm I\!R}^q, {\rm I\!R}^p))
\\
{}\cong{}&
(({\rm I\!R}^n)^*\otimes {\rm I\!R}^m)^* \otimes ({\rm I\!R}^{q})^*\otimes {\rm I\!R}^p
\\
{}\cong{}&
{\rm I\!R}^n \otimes {\rm I\!R}^{m*} \otimes {\rm I\!R}^{q*} \otimes {\rm I\!R}^p
\end{aligned}$$</p>
<p>Such objects can be seen as multilinear maps ${\rm I\!R}^{n*} \times {\rm I\!R}^{m} \times {\rm I\!R}^{q} \times {\rm I\!R}^{p*} \to {\rm I\!R}$ , that is,</p>
<p>$$(x\otimes \phi \otimes \psi \otimes y)(\theta, s, t, \zeta) = \theta(x)\phi(s)\psi(t)\zeta(y).$$</p>
<p>Lastly,</p>
<p>$$\dim {\rm Hom}({\rm I\!R}^{m\times n}, {\rm I\!R}^{p\times q}) = \dim {\rm I\!R}^n \otimes {\rm I\!R}^{m*} \otimes {\rm I\!R}^{q*} \otimes {\rm I\!R}^p = nmpq.$$</p>


### Result 3: Tensor product of linear maps

> <p><b>Tensor product of linear maps.</b> Let $U_1, U_2$ and $V_1, V_2$ be vector spaces. Then</p>
> <p>$${\rm Hom}(U_1, U_2) \otimes {\rm Hom}(V_1, V_2) \cong {\rm Hom}(U_1\otimes V_1, U_2\otimes V_2)$$</p>
> <p>with isomorphism function</p>
> <p>$$(\phi\otimes\psi)(u\otimes v) = \phi(u) \otimes \psi(v).$$</p>


## Again, using the universal property

<p>We can define $V\otimes W$ to be the a space accompanied by a bilinear operation $\otimes: V\times W \to V \otimes W$ that has the universal property in the following sense: <sup>[<a href="#cite:5">5</a>]</sup></p>

> <p><b>Universal property.</b> If $f: V\times W \to Z$ is a bilinear function, then there is a unique linear function $\tilde{f}: V\otimes Z$ such that $f = \tilde{f} \circ \otimes$.</p>

<div id="universal-property-meme">
<img src="/boom.gif" alt="Universal property mind-blowing"  style="width: 40%; margin-left: auto;margin-right: auto;">
</div>

<p>The universal property says that every bilinear map $f(u, v)$ on a vector space $V$ is a linear function $\tilde{f}$ of the tensor product, $\tilde{f}(u\otimes v)$ <sup>[<a href="#cite:6">6</a>]</sup>.</p>

<p>See more about the uniqueness of tensor product via the universality-based definition as well as<sup>[<a href="#cite:8">8</a>]</sup>.</p>

## Making sense of tensors using polynomials

<p>This is based on<sup>[<a href="#cite:9">9</a>]</sup>. We can identify vectors $u=(u_0, \ldots, u_{n-1})\in{\rm I\!R}^n$ and $v\in{\rm I\!R}^m$ as polynomials over ${\rm I\!R}$ of the form</p>
<p>$$u(x) = u_0 + u_1x + \ldots + u_{n-1}x^{n-1}.$$</p>
<p>We know that a <em>pair</em> of vectors lives in the Cartesian product space ${\rm I\!R}^n\times {\rm I\!R}^m$. A pair of polynomials lives in a space with basis</p> 
<p>$$\mathcal{B}_{\rm prod} 
{}\coloneqq{}
\{(1, 0), (x, 0), \ldots, (x^{n-1}, 0)\} \cup \{(0, 1), (0, y), \ldots, (0, y^{n-1})\}.$$</p>
<p>But take now two polynomials $u$ and $v$ and multiply them to get</p>
<p>$$u(x)v(y) = \sum_{i}\sum_{j}c_{ij}x^iy^j.$$</p>
<p>The result is a polynomial of two variables, $x$ and $y$. This corresponds to the tensor product of $u$ and $v$.</p>

## Further reading

Lots of books on tensors for physicists are in <sup>[<a href="#cite:11">11</a>]</sup>. In <em>Linear Algebra Done Wrong</em> <sup>[<a href="#cite:12">12</a>]</sup> there is an extensive chapter on the matter. It would be interesting to read about tensor norms <sup>[<a href="#cite:13">13</a>]</sup>. These lecture notes <sup>[<a href="#cite:14">14</a>]</sup> <sup>[<a href="#cite:15">15</a>]</sup> <sup>[<a href="#cite:16">16</a>]</sup> seem worth studying too. These <sup>[<a href="#cite:18">18</a>]</sup> lectures notes on multilinear algebra look good, but are more theoretical and look a bit category-theoretical. A must-read book is <sup>[<a href="#cite:19">19</a>]</sup> and these lectures notes for MIT <sup>[<a href="#cite:20">20</a>]</sup>. A book that seems to explain things in an accessible way, yet rigorously is <sup>[<a href="#cite:21">21</a>]</sup>.

## References

<ol>
  <li id="cite:1">F. Schuller, <a target="_blank" href="https://www.youtube.com/watch?v=mbv3T15nWq0">Video lecture 3</a>, Accessed on 12 Sept 2023.</li>  
  <li id="cite:2">А. И. Кострикин, Ю.И.Манин, <a target="_blank" href="http://www.physics.uni-altai.ru/media/get.php?id=488">Линейная алгебра и геометрия<a>, Часть 4</li>  
  <li id="cite:3">Wikipedia, <a target="_blank" href="https://en.wikipedia.org/wiki/Tensor_product#As_a_quotient_space">tensor product</a> on Wikipedia, Accessed on 15 Sept 2023.</li>  
  <li id="cite:4">P. Renteln, Manifolds, Tensors, and Forms: An introduction for mathematicians and physicists, Cambridge University Press, 2014.</li>  
  <li id="cite:5">Steven Roman, Advanced Linear Algebra, Springer, 3rd Edition, 2010</li>  
  <li id="cite:6">Check out <a href="https://www.youtube.com/watch?v=qHuUazkUcnU">this guy</a> on YouTube (@mlbaker) gives a cool construction and explanation of tensors</li>  
  <li id="cite:7"> M. Penn's <a href="https://www.youtube.com/watch?v=K7f2pCQ3p3U&t=129s">video</a> "What is a tensor anyway?? (from a mathematician)" on YouTube</li>  
  <li id="cite:8">Proof: <a href="https://www.youtube.com/watch?v=VJJK2BoIaD8">Uniqueness of the Tensor Product</a>, YouTube video by Mu Prime Math</li>  
  <li id="cite:9">Prof Macauley on YouTube, Advanced Linear Algebra, Lecture 3.7: <a href="https://www.youtube.com/watch?v=T3N6qRIucQ0">Tensors</a>, accessed on 9 November 2023; see also his slides, <a href="http://www.math.clemson.edu/~macaule/classes/f20_math8530/slides/math8530_lecture-3-07_h.pdf">Lecture 3.7: Tensors</a>, lecture slides on tensors, some nice diagrams and insights.</li>  
  <li id="cite:10">Answer on <a href="https://math.stackexchange.com/a/679600/8357">MSE</a> on why ${\rm Hom}(V, W)$ is the same thing as $V^*\otimes W$, accessed on 9 November 2023</li>  
  <li id="cite:11">Lots of books on tensors, tensor calculus, and applications to physics can be found on <a href="https://github.com/JackieXie168/documents/tree/master/mathematics">this GitHub repo</a>, accessed on 9 November 2023</li>  
  <li id="cite:12">S. Treil, <a href="http://www.math.brown.edu/streil/papers/LADW/LADW_2017-09-04.pdf">Linear algebra done wrong</a>, Chapter 8: dual spaces and tensors, 2017</li>  
  <li id="cite:13">A. Defant and K. Floret, <em>Tensor norms and operator ideals</em> (<a href="https://github.com/JackieXie168/documents/blob/master/mathematics/Tensor%20Norms%20and%20Operator%20Ideals%20(North-Holland%20Mathematics%20Studies)%20(A.%20Defant%2C%20K.%20Floret)%200444890912.pdf">link</a>), North Holand, 1993</li>  
  <li id="cite:14">K. Purbhoo, Notes on Tensor Products and the Exterior Algebra for Math 245, <a href="https://www.math.uwaterloo.ca/~kpurbhoo/spring2012-math245/tensor.pdf">link</a></li>  
  <li id="cite:15">Lecture notes on tensors, Uni Berkeley, <a href="http://hitoshi.berkeley.edu/221A/tensorproduct.pdf">link</a></li>  
  <li id="cite:16">J. Zintl, Notes on tensor products, part 3, <a href="https://www.math.uni-tuebingen.de/user/zintl/MLA_Wi1819/MLA_Skript_%c2%a76.pdf">link</a></li>  
  <li id="cite:17">Rich Schwartz, <a href="https://www.math.brown.edu/reschwar/M153/tensor.pdf">Notes on tensor products</a></li>  
  <li id="cite:18">J. Zintl, Notes on multilinear maps, <a href="https://www.math.uni-tuebingen.de/user/zintl/MLA_Wi1819/MLA_Skript_%C2%A75.pdf">link</a></li>  
  <li id="cite:19">A Iozzi, <a href="https://www2.math.ethz.ch/education/bachelor/lectures/fs2016/other/mla/ma.pdf">Multilinear Algebra and Applications</a>. Concise (100 pages), very clear explanation.</li>  
  <li id="cite:20">MIT <a href="https://math.mit.edu/classes/18.952/spring2013/docs/book.pdf">Multilinear algebra lecture notes/book</a>, multilinear algebra, introduction (dual spaces, quotients), tensors, the <em>pullback operation</em>, alternating tensors, the space $\Lambda^k(V^*)$, the <em>wedge product</em>, the <em>interior product</em>, orientations, and more 👍 (must read)</li>  
  <li id="cite:21">JR Ruiz-Tolosa and E Castillo, From vectors to tensors, Springer, Universitext, 2005.</li>  
  <li id="cite:22">Elias Erdtman, Carl Jonsson, <a href="http://liu.diva-portal.org/smash/get/diva2:551672/FULLTEXT01.pdf">Tensor Rank</a>, Applied Mathematics, Linkopings Universite, 2012</li>  

</ol>




