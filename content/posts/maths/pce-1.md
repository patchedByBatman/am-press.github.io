---
author: "Pantelis Sopasakis"
title:  "Polynomial chaos expansions: Part I"
date: 2022-09-06
description: "Kosambi-Karhunen-Loève theorem, orthogonal polynomials"
summary: "An introduction to polynomial chaos expansions"
math: true
series: ["Mathematix"]
tags: ["Probability", "Statistics"]
collapsible: true
---

<p>In this introductory post we will present some fundamental results that will pave the way towards polynomial chaos expansions. This will be done in a series of blog posts.</p>

## 0. Introduction 


### 0.1. Preliminaries
<p>Mercer's theorem is a fundamental theorem in reproducing kernel Hilbert space<sup>[<a href="https://arxiv.org/pdf/1408.0952.pdf" target="_blank">ref</a>]</sup>. Before we proceed we need to state a few definitions. Note certain authors use different notation and definitions. We start with the definition of a symmetric function.</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="symmetric">
<p><strong>Definition 1 (Symmetric).</strong> A function \(K:[a,b]\times[a,b] \to {\rm I\!R}\) symmetric if $K(x, y) = K(y, x)$ for all $x,y\in[a,b]$.</p>
</div>

<p>Next we give the definition of a positive definite function \(K:[a,b]\times[a,b] \to {\rm I\!R}\).</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="posef">
<p><strong>Definition 2 (Positive definite function).</strong> A function \(K:[a,b]\times[a,b] \to {\rm I\!R}\) is called <em>nonnegative definite</em> if \(\sum_{i,j=1}^{n} f(x_i) f(x_j) K(x_i,x_j) \geq 0\), for all \((x_i)_{i=1}^{n}\) in \([a,b]\), all \(n\in\N\) and all functions \(f:[a, b] \to {\rm I\!R}\).</p>
</div>

<button onclick="toggleCollapseExpand('remarkPosdefButton', 'remarkPosdefContainer', 'Remark')" id="remarkPosdefButton">
  <i class="fa fa-cog fa-spin"></i> Remark on definition of nonnegative definiteness
</button>

<div style="width: 100%; display: none; padding: 5px 5px; " id="remarkPosdefContainer">
<p>Some authors<sup>[<a href="#references">1, 2</a>]</sup> use the following definition of nonnegative definiteness: A function \(K:[a,b]\times[a,b] \to {\rm I\!R}\) is called <em>nonnegative definite</em> if \(\sum_{i,j=1}^{n} c_i c_j K(x_i,x_j) \geq 0\), for all \((x_i)_{i=1}^{n}\) in \([a,b]\), all $c_i, c_j \in {\rm I\!R}$ and all \(n\in\N\). This definition implies that $K(x,x) = 0$ for all $x\in[a,b]$, whereas Definition 2 only implies that $K(x, x) \geq 0$.</p>
</div>

<p></p>
<p>We can now give the definition of a kernel.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="kernel">
<p><strong>Definition 3 (Kernel).</strong> A function \(K:[a,b]\times[a,b] \to {\rm I\!R}\) is called a <em>kernel</em> if it is (i) continuous, (ii) symmetric, and (iii) nonnegative definite.</p>
</div>

<p>Some examples of kernels are (for $x,y\in [a, b]$)</p>
<ol>
    <li>Linear, $K(x, y) = x y$</li>
    <li>Polynomial, $K(x, y) = (x y + c)^d$, with $c\geq 0$</li>
    <li>Radial basis function, $K(x, y) = \exp(-\gamma (x-y)^2)$</li>
    <li>Hyperbolic tangent, $K(x, y) = \tanh(xy + c)$</li>
</ol>

<!-- <div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="kernel">
<p><strong>Definition 4 (Integral nonnegative definite).</strong> A kernel \(K:[a,b]\times[a,b] \to {\rm I\!R}\) is said to be <em>integral nonnegative definite</em> if</p>
<p>$$\int_a^b \int_a^b K(x, t)\phi(s)\phi(t)\mathrm{d}s\mathrm{d}t \geq 0,$$</p>
<p>for all continuous functions $\phi:[a,b]\to{\rm I\!R}$.</p>
</div> -->




### 0.2. Hilbert-Schmidt integral operators


<p>We give the definition of the Hilbert-Schmidt integral operator of a kernel.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="hs-integral-operator">
<p><strong>Definition 4 (HS integral operator).</strong> Let \(K\) be a kernel. The <em>Hilbert-Schmidt integral operator</em> is defined as a $T_K : \mathcal{L}^2([a,b]) \to \mathcal{L}^2([a,b])$ that maps a function $\phi \in \mathcal{L}^2([a,b])$ to the function</p>
<p>$$T_K \phi = \int_{a}^{b}K({}\cdot{}, s)\phi(s)\mathrm{d} s.$$</p>
<p>which is an $\mathcal{L}^2([a,b])$-function.</p>
</div>

<p>The Hilbert-Schmidt integral operator of a kernel is linear, bounded, and compact. Moreover, $T_K\phi$ is continuous for all $\phi\in\mathcal{L}^2([a,b])$. We also have that $T_K$ is <em>self adjoint</em>, that is, for all $g\in\mathcal{L}^2([a,b])$,<p>
<p>$$\langle T_K \phi, g\rangle = \langle \phi, T_K g\rangle.$$</p>


</p>Recall that given a linear map $A:U\to U$ on a real linear space $U$, an eigenvalue-eigenvector pair $(\lambda, \phi)$, with $\lambda\in\mathbb{C}$ and $\phi\in U$ is one that satisfies $A\phi = \lambda \phi$.</p>

<p>For the Hilbert-Schmidt integral operator of a kernel</p>
<ol>
    <li>There is at least one eigenvalue-eigenfunction pair</p>
    <li>The set of its eigenvalues is countable</li>
    <li>Its eigenvalues are (real and) nonnegative</li>
    <li>Its eigenfunctions are continuous</li>
    <li>Its eigenfunctions span $\mathcal{L}^2([a,b])$</li>
</ol>
<p>From the spectral theorem for linear, compact, self-adjoint operators, there is an orthonormal basis of $\mathcal{L}^2([a,b])$ consisting of eigenvectors of $T_K$. </p>



### 0.3. Mercer's Theorem
<p>We can now state Mercer's theorem.</p>
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="mercer-thm">
<p><strong>Theorem 5 (Mercer's theorem).</strong> Let \(K\) be a kernel. Then, there is an orthonormal basis \((e_i)_{i}\) of $\mathcal{L}^2([a,b])$ of eigenfunctions of $T_K$, and corresponding (nonnegative) eigenvalues \((\lambda_i)_i\) so that</p>
<p>$$K(s,t) = \sum_{j=1}^{\infty} \lambda_j e_j(s)e_j(t),$$</p>            
<p>where convergence is absolute and uniform in \([a,b]\times [a,b]\).</p>
</div>

<p>The fact that $(\lambda_i, e_i)$ is an eigenvalue-eigenfunction pair of $T_K$ means that $T_K e_i = \lambda_i e_i$, that is,</p>
<p>$$\int_a^b K(t, s)e_i(s)\mathrm{d}s = \lambda_i e_i(t).$$</p>
<p>This is a Fredholm integral equation of the second kind.</p>

## 1. The Kosambi–Karhunen–Loève Theorem
<p>We can now state the Kosambi–Karhunen–Loève (KKL) theorem<sup>[<a href="#references">3</a>]</sup>. The Kosambi–Karhunen–Loève Theorem is a special case of the class of polynomial chaos expansions we will discuss later. It is a consequence of Mercer's Theorem.</p>



<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="kkl">
<p><strong>Theorem 6 (KKL Theorem).</strong><sup>[<a href="#references">3</a>]</sup> Let \((X_t)_{t\in [a,b]}\) be a centred, continuous stochastic process on \((\Omega, \mathcal{F}, \mathrm{P})\) with a covariance function $R_X(s,t) = {\rm I\!E}[X_s X_t]$. Then, for $t\in[a, b]$</p>
<p id="eq1">\[
        X_t(\omega) = \sum_{i=1}^{\infty}Z_i(\omega) e_i(t),\tag{1}
\]
</p>
<p>with</p>
<p>\[
        Z_i(\omega) = \int_{T}X_t(\omega)e_i(t) \mathrm{d}t, \tag{2}
\]</p>
<p>where $e_i$ are eigenfunctions of the Hilbert-Schmidt integral operator of $R_X$ and form an orthonormal basis of $\mathcal{L}^2(\Omega, \mathcal{F}, \mathrm{P})$.</p>
</div>

<p>Since $(Z_i)_i$ is an orthonormal basis, \({\rm I\!E}[Z_i Z_j] = 0\) for \(i\neq j\). Moreover, \({\rm I\!E}[Z_i]=0\). The variance of $Z_i$ is ${\rm I\!E}[Z_i^2] = \lambda_i$ — the corresponding eigenvalue to $Z_i$.</p>

<p>In Equation (<a href="#eq1">1</a>), the series converges in the mean-square sense to $X_t$, uniformly in $t\in[a,b]$.</p>


<p>What is more, \((e_i)_i\) and \((\lambda_i)_i\) are eigenvectors and eigenvalues of the Hilbert-Schmidt integral operator \(T_{R_X}\) of the auto-correlation function \(R_X\) of the random process, that is, they satisfy the Fredholm integral equation of the second kind</p>
<p>\[
        T_{R_X}e_i = \lambda_i e_i
\]</p>
<p>or equivalently</p>
<p>\[
        \int_{a}^{b} R_X(s,t) e_i(s) \mathrm{d} s = \lambda_i e_i(t),
\]</p>
<p>for all $i\in\N$.</p>

<p>Let \((X_t)_{t\in T}\), \(T=[a,b]\), be a stochastic process which satisfies the requirements of the Kosambi-Karhunen-Loève theorem. Then, there exists a basis \((e_i)_i\) of \(\mathcal{L}^2(T)\) such that for all \(t\in T\)</p>
<p>\[
X_t(\omega) = \sum_{i=1}^{\infty} \sqrt{\lambda_i}\xi_i(\omega)e_i(t),
\]</p>
<p>in \(\mathcal{L}^2(\Omega, \mathcal{F}, \mathrm{P})\), where \(\xi_i\) are centered, mutually uncorrelated random variables with unit variance and are given by</p>
<p>\[\xi_i(\omega) = \tfrac{1}{\sqrt{\lambda_i}}\int_{a}^{b} X_{\tau}(\omega) e_i(\tau) \mathrm{d} \tau.\]</p>

## 2. Orthogonal polynomials

<p>Let \(\mathsf{P}_N([a,b])\) denote the space of polynomials \(\psi:[a,b]\to{\rm I\!R}\) of degree no larger than \(N\in\N\).</p>

<p>Consider the space \(\mathcal{L}^2([a,b])\) and a positive continuous random variable with pdf $w$ (or, in general, a positive function $w:[a, b] \to [0, \infty)$). For two functions \(\psi_1,\psi_2: [a,b] \to {\rm I\!R}\), we define the scalar product</p>
<p>\[
        \left\langle\psi_1, \psi_2\right\rangle_{w} = \int_{a}^{b} w(\tau) \psi_1(\tau) \psi_2(\tau) \mathrm{d} \tau.
\]</p>
<p>and the corresponding norm \( \|f\|_w = \sqrt{\left\langle f,f\right\rangle_w}\). Define the space</p>
<p>\[
        \mathcal{L}^2_w([a,b]) = \{f:[a,b]\to{\rm I\!R} {}:{} \|f\|_w < \infty\}.
\]</p>

<p>For a random variable \(\Xi \in \mathcal{L}^2(\Omega, \mathcal{F}, \mathrm{P}; {\rm I\!R})\) with PDF \(p_\Xi>0\), we define</p>
<p>\[
        \left\langle\psi_1, \psi_2\right\rangle_{\Xi} {}\coloneqq{} \left\langle\psi_1, \psi_2\right\rangle_{p_{\Xi}}.
\]</p>

<p>If the random variable $\Xi$ is not continuous (so, it does not have a pdf), then given its distribution $F_{\Xi}(\xi) = \mathrm{P}[\Xi \leq \xi]$, we can define the inner product as </p>
<p>$$\langle \psi_1, \psi_2\rangle_{\Xi} {}={} \int_{a}^{b}\psi_1 \psi_2 \mathrm{d}F_{\Xi}.$$</p>

<p>Let $\Xi$ be a real-valued random variable with probability density function $p_\Xi$. Let \(\psi_1,\psi_2:\Omega\to{\rm I\!R}\) be two polynomials. We say that \(\psi_1,\psi_2\) are orthogonal with respect to (the pdf of) \(\Xi\) if \(\left\langle\psi_1, \psi_2\right\rangle_{\Xi} = 0\).</p> 

<p>The random variable $\Xi$ the induces the above inner product and norm is often referred to as the <strong>germ</strong>.</p>

<p>Let \(\psi_0, \psi_2,\ldots\), with \(\psi_0=1\), be a sequence of orthogonal polynomials with respect to the above inner product. Then,</p>
<p>\[
        0 = \left\langle \psi_0, \psi_1 \right\rangle_\Xi
        = \int_{-\infty}^{\infty} \psi_{1}(s)
        p_{\Xi}(s) \mathrm{d} s
        = {\rm I\!E}[\psi_1(\Xi)],
\]</p>
<p>by virtue of LotUS. Likewise, \({\rm I\!E}[\psi_i(\Xi)] = 0\) for all \(i\).</p>




### 2.1. Popular polynomial bases

<p>(<strong>Hermite polynomials</strong>). Let \(\Xi\) be distributed as \(\mathcal{N}(0,1)\). Then, its pdf is</p>
<p>$$p_{\Xi}(s) = \frac{1}{\sqrt{2\pi}}e^{-\frac{x^2}{2}}.$$</p> 
<p>and the polynomials \(\psi_0,\psi_1,\ldots\) are the Hermite polynomials, the first few of which are \(H_0(x)=1\), \(H_1(x)=x\), \(H_2(x)=x^2-1\), \(H_3(x) = x^3 - 3x\). These are orthogonal with respect to \(\Xi\), that is</p>
<p>\[
        \left\langle{}H_i, H_j\right\rangle_\Xi = \int_{-\infty}^{\infty}H_i(s) H_j(s) e^{-\frac{s^2}{2}}\mathrm{d} s = 0,
\]</p>
<p>for \(i\neq j\).</p>


<p>(<strong>Legendre polynomials</strong>). If \(\Xi\sim U([-1,1])\), then \(\psi_0,\psi_1,\ldots\) are the
Legendre polynomials. If, instead, \(\Xi\sim U([-1,1])\), the coefficients of the
Legendre polynomials can be modified.</p>

<p>(<strong>Laguerre polynomials</strong>). If the germ is an exponential random variable on \([0,\infty)\),
then \(\psi_0,\psi_1,\ldots\) are the Laguerre polynomials.</p>


### 2.2. Projection and Best Approximation
<p>On a normed space $X$, let us recall that the projection of a point $x \in X$ on a closed set $H\subseteq X$ is defined as</p>
<p>$$\Pi_H(x) = \argmin_{y\in H}\|y-x\|.$$</p>
<p>In other words,</p>
<p>$$\|\Pi_H(x) - x\| \leq \|y-x\|, \text{ for all } y\in H.$$</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="projection1">
<p><strong>Proposition 7 (Projection on subspace).</strong> Let $X$ be an inner product space and $H \subseteq X$ is a linear subspace of $X$. Let $x\in X$. The following are equivalent</p>
<ol>
<li>$x^\star = \Pi_{H}(x)$</li>
<li>$\|x^\star - x\| \leq \|y-x\|$, for all $y\in H$</li>
<li>$x^\star - x$ is orthogonal to $y$ for all $y\in H$</li>
</ol>
</div>

<p><em>Proof.</em> (1 $\Leftrightarrow$ 2) is immediate from the definition of the projection.</p>
<p>(1 $\Leftrightarrow$ 3) The optimisation problem that defines the projection can be written equivalently as</p>
<p>$$\operatorname*{Minimise}_{y}\tfrac{1}{2}\|y-x\|^2 + \delta_H(y).$$</p>
<p>So the optimality conditions are $0 \in \partial(\tfrac{1}{2}\|x^{\star}-x\|^2 + \delta_H(x^{\star}))$. Equivalently</p>
<p>$$0 \in x^{\star}-x + N_H(x^{\star}) \Leftrightarrow x^{\star}-x \in H^{\perp},$$</p>
<p>and this completes the proof. $\Box$</p>


<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="projection2">
<p><strong>Proposition 8 (Projection on subspace).</strong> Let $X$ be an inner product space and $H \subseteq X$ is a finite-dimensional linear subspace of $X$ with an orthogonal basis $\{e_1, \ldots, e_n\}$*. Then,</p>
<p>$$\Pi_H(x) = \sum_{i=1}^{n}c_i e_i,$$</p>
<p>where</p>
<p>$$c_i = \frac{\langle x, e_i \rangle}{\|e_i\|^2},$$</p>
<p>for all $i=1,\ldots, n$.</p>
</div>

<p>* If the basis is not orthogonal, we can produce an orthogonal basis using the Gram-Schmidt orthogonalisation procedure<sup>[<a href="https://en.wikipedia.org/wiki/Gram%E2%80%93Schmidt_process" target="_blank">ref</a>]</sup></p>
<p><em>Proof.</em> It suffices to show that Condition 3 of <a href="#projection1" title="Projection on subspace">Proposition 7</a> is satisfied. Equivalently, it suffices to show that</p>
<p>$$\left\langle \sum_{i=1}^{n} \frac{\langle x, e_i \rangle}{\|e_i\|^2}e_i - x, e_j\right\rangle=0,$$</p>
<p>for all $j=1,\ldots,n$. This is true because $\langle e_i, e_j\rangle = \delta_{ij}\|e_j\|^2$. $\Box$</p>

<p>Let $\{\psi_0, \ldots, \psi_N\}$ be an orthogonal basis of the set of polynomials on $[a, b]$ with degree up to $N$. This is denoted by $\mathsf{P}_N([a, b])$. Orthogonality is meant with respect to an inner product \(\left\langle{}\cdot{}, {}\cdot{}\right\rangle_w\). Suppose that the $\psi_i$ are unitary, i.e., $\|\psi_i\|_w = 1$.</p>
<p>Following <a href="#projection2">Proposition 8</a>, the projection operator onto \(\mathsf{P}_N([a, b])\) is</p>
<p>\[
        \Pi_N:\mathcal{L}^2_w([a, b]) \ni f \mapsto \Pi_N f \coloneqq \sum_{j=0}^{N}\hat{f}_j \psi_j \in \mathsf{P}_N,
\]</p>
<p>where $\hat{f}_j = \left\langle{}f, \psi_j\right\rangle_w.$</p>


<p>For  \(f\in\mathcal{L}^2_w([a, b])\), define \(f_N = \Pi_N f\). Then,</p>
<p>\[
        \lim_{N\to\infty}\|f - f_N\|_{w} = 0.
\]</p>


### 2.3. Example
<p>Here we will approximate the function </p>
<p>$$f(x) = \sin(5x) \exp(-2x^2),$$</p>
<p>over $[-1, 1]$ using Legendre polynomials<sup>[<a href="https://en.wikipedia.org/wiki/Legendre_polynomials">ref</a>]</sup>. The Legendre polynomials, $L_0, L_1, \ldots$ are orthogonal with respect to the standard inner product of $\mathcal{L}^2([-1, 1])$. The first four Legendre polynomials are</p>
<p>$$\begin{aligned}
L_0(x) {}={}& 1,
\\
L_1(x) {}={}& x,
\\
L_2(x) {}={}& \tfrac{1}{2}(3x^2 - 1),
\\
L_3(x) {}={}& \tfrac{1}{2}(5x^3 - 1).
\end{aligned}$$</p>
<p>Using <a href="#projection2">Proposition 8</a>, we can compute the coefficients of the approximation $f \approx \Pi_N f$. In <a href="#fig1">Figure 1</a> we see a comparison of $f_5$, $f_7$ and $f_9$ with $f$. We see that as $N$ increases, the approximation comes closed to $f$.</p>
<div id="fig1">
<img src="/pol-approx-1.jpg" alt="Approximation of f with Legendre polynomials"  style="width: 97%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 1.</strong> Approximation of $f(x) = \sin(5x) \exp(-2x^2)$ using Legendre polynomials.</em></p>
</div>

<div id="fig2">
<img src="/pol-approx-1-error.jpg" alt="Approximation L2-norm-error against N"  style="width: 65%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 2.</strong> Plot of $\|f-f_N\|_{\mathcal{L}^2([-1, 1])}$ against $N$. As $N\to\infty$, the approximation error goes to zero.</em></p>
</div>

<p>Is this better compared to the Taylor expansion? TL;DR: Yes! Big time! Taylor's approximation is a <em>local</em> approximation.</p>

### 2.4. Focused approximation

<p>Let's take the same function as in the example of <a href="#23-example">Section 2.3</a>, but now suppose we want to focus more close to $-1$ and less so close to $1$. We want to treat errors close to $-1$ as more important and errors closer to $1$ as less important. To that end, we use the weight function</p>
<p>$$w(x) = (1-x)^a(1+x)^b,$$</p>
<p>with $a=2$ and $b=0.1$.</p>

<div id="fig3">
<img src="/pol-jacobi.jpg" alt="Approximation using  Jacobi polynomials"  style="width: 65%; margin-left: auto;margin-right: auto;">
<p><em><strong>Figure 3.</strong> Approximation of $f(x) = \sin(5x) \exp(-2x^2),$ with polynomials which are orthogonal with respect to $w$.</em></p>
</div>


<p>The Jacobi polynomials<sup>[<a href="https://en.wikipedia.org/wiki/Jacobi_polynomials" target="_blank">ref</a>]</sup> are orthogonal with resepct to $w$.</p>



## Read next

- <p><a href="../pce-2">Polynomial chaos expansions: Part II</a></p>



## References 

1. G.E. Fasshauer, <a href="http://amadeus.csam.iit.edu/~fass/PDKernels.pdf" target="_blank">Positive Definite Kernels: Past, Present and Future</a>, 2011
2. Marco Cuturi, <a href="https://arxiv.org/pdf/0911.5367.pdf" target="_blank">Positive Definite Kernels in Machine Learning</a>, 2009
3. R.B. Ash, Information Theory, Dover Books on Mathematics, 2012
4. D. Xiu, Numerical methods for stochastic computations: a spectral method approach, Princeton University Press, 2010

