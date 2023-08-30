---
author: "Pantelis Sopasakis"
title:  "Reading Vershynin's HDP II: Subgaussianity"
date: 2023-06-29
description: "Subgaussianity"
summary: "We study the class of sub-Gaussian random variables: those random variables whose tails are dominated by a Gaussian. Such random variables satisfy Hoeffding-type bounds and possess several interesting properties. We also define the sub-Gaussian norm and study its properties."
math: true
series: ["Mathematix"]
tags: ["Probability", "Vershynin"]
collapsible: true
draft: false
---

> See first: <a href="../vershynin-hdp-1">Reading Vershynin's HDP I: Markov, Chernoff, Hoeffding</a>

> See next: <a href="../vershynin-hdp-3">Reading Vershynin's HDP III: Subexponential random variables</a>


<p>We ask what is the class of random variables that satisfy a Hoeffding-type bound, which for $N=1$ gives</p>
<p>$${\rm P}[|X| > t] \leq e^{-ct^2}.$$</p>
<p>This inequality says that the <b>tails</b> of $X$ are <b>sub-Gaussian</b>.</p>
<p>Many random variables fall into this category: the normal, and all bounded distributions.</p> 

## Some notable properties of the Gaussian

<p>Some properties of the normal are inherited by all random variables. Let us firstly look at how $\|X\|_{L^p}$ scales with $p$ for $X\sim\mathcal{N}(0, 1)$.</p>

<!-- EXERCISE 2.5.1 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex251">
<p><strong>Exercise 2.5.1. (Moments of the normal distribution)</strong> Show that for each $p \geq 1$, the random variable $X\sim\mathcal{N}(0, 1)$ satisfies</p>
<p>$$\|X\|_{L^p} = \sqrt{2} \left(\frac{\Gamma\left(\frac{p+1}{2}\right)}{\Gamma(\frac{1}{2})}\right)^{1/p},$$</p>
<p>and</p>
<p>$$\|X\|_{L^p} = O(\sqrt{p}), \text{ as } p \to \infty.$$</p>
</div>

<p><em>Solution.</em> We have</p>
<p>$$\begin{aligned}
\|X\|_{L^p}^p {}={}& {\rm I\!E}[|X|^p] {}={} 
\int_{-\infty}^{\infty}|x|^p\frac{1}{\sqrt{2\pi}}e^{-\frac{x^2}{2}} {\rm d}x
\\
{}={}& 2 \int_{0}^{\infty}x^p\frac{1}{\sqrt{2\pi}}e^{-\frac{x^2}{2}} {\rm d}x
\\
{}={}& \frac{2}{\sqrt{2\pi}} \int_{0}^{\infty}x^pe^{-\frac{x^2}{2}} {\rm d}x
\\
{}={}& \frac{\sqrt{2}}{\sqrt{\pi}} \int_{0}^{\infty}x^pe^{-\frac{x^2}{2}} {\rm d}x
\end{aligned}$$</p>
<p>We now turn our attention to the integral</p>
<p>$$\begin{aligned}
I {}={}& \int_{0}^{\infty}x^pe^{-\frac{x^2}{2}} {\rm d}x
\\
{}={}& \int_{0}^{\infty} x x^{p-1}e^{-\frac{x^2}{2}} {\rm d}x
\end{aligned}$$</p>
<p>We define $y = x^2/2$; then ${\rm d}y = x{\rm d}x$ and $x^{p-1} = (2y)^{(p-1)/2}$. We have</p>
<p>$$\begin{aligned}
I {}={}&  \int_{0}^{\infty} (2y)^{\frac{p-1}{2}}e^{-y} {\rm d}y 
\\
{}={}& 2^{\frac{p-1}{2}} \int_{0}^{\infty} y^{\left(\frac{p-1}{2} + 1\right) - 1}e^{-y} {\rm d}y 
\\
{}={}& 2^{\frac{p-1}{2}} \Gamma\left(\frac{p+1}{2}\right).
\end{aligned}$$</p>
<p>As a result, and using the fact that $\sqrt{\pi} = \Gamma(1/2)$,</p>
<p>$$\begin{aligned}
\|X\|_{L_p}^{p} = \frac{\sqrt{2}}{\Gamma(\frac{1}{2})} 2^{\frac{p-1}{2}} \Gamma\left(\frac{p+1}{2}\right),
\end{aligned}$$</p>
<p>and the assertion follows by raising to the power $p$. The asymptotic result follows by Stirling's approximation formula</p>
<p>$$\begin{aligned}\Gamma(z) \sim \sqrt{2\pi} z^{z-\frac{1}{2}}e^{-z}, \text{ as } z \to \infty.\end{aligned}$$</p>
<p>This proves the assertion. $\Box$</p>

<p>As we will see below, this asymptotic property fully characterises the class of sub-Gaussian random variables.</p>


<!-- EXERCISE 2.5.1b -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex251b">
    <p><strong>Exercise 2.5.1/b. (MGF of normal distribution)</strong> Show that the moment generating function (MGF) of the random variable $X\sim\mathcal{N}(0, 1)$ is</p>
    <p>$$M_X(\lambda) = \exp(\lambda^2/2),$$</p>
    <p>for $\lambda \in {\rm I\!R}$.</p>
</div>

<p><em>Solution.</em> This can be seen by direct computation. By the definition of <u style="text-decoration:underline dotted" title="moment generating function">mgf</u>,</p>

<p>$$\begin{aligned}M_X(\lambda) = {\rm I\!E}[e^{\lambda X}] = \int_{-\infty}^{\infty}e^{\lambda x}\frac{1}{\sqrt{2\pi}}e^{-x^2/2}{\rm d}x = \ldots = \exp(\lambda^2/2).\end{aligned}$$</p>

## Characterisation of sub-Gaussianity

The following proposition characterises the property of sub-Gaussianity (this is Proposition 2.5.2 in [<a href="#cite:ver19" title="Vershynin, HDP">1</a>]).

<!-- PROPOSITION 1: Characterisation of subGaussianity -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="subGaussianityProp">
    <p><strong>Proposition 1 (Sub-Gaussian properties).</strong> Let $X$ be a random variable. Then the following properties are equivalent</p>
    <ol>
        <li id="subGaussianityProp:1">The tails of $X$ satisfy ${\rm P}[|X| \geq t] \leq 2 \exp(-t^2/K_1^2)$, for all $t\geq 0$, for some constant $K_1 > 0$</li>
        <li id="subGaussianityProp:2">The moments of $X$ satisfy $\|X\|_{L^p} \leq K_2 \sqrt{p}$, for all $p\geq 1$, for some constant $K_2$</li>
        <li id="subGaussianityProp:3">The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $X^2$ satisfies ${\rm I\!E}[\exp(\lambda^2X^2)] \leq \exp(K_3^2 \lambda^2)$, for all $\lambda$ such that $|\lambda|\leq 1/K_3$</li>
        <li id="subGaussianityProp:4">The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $X^2$ is bounded at some point, namely, ${\rm I\!E}[\exp(X^2/K_4^2)] \leq 2$</li>
    </ol>
    <p>Moreover, if ${\rm I\!E}[X] = 0$ the above properties are also equivalent to</p>
    <ol start=5>
        <li id="subGaussianityProp:5">The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $X$ satisfies ${\rm I\!E}[\lambda X] \leq \exp(K_5^2 \lambda^2)$ for all $\lambda \in {\rm I\!R}$</li>
    </ol>
    <p>Lastly, there is a constant $C$ so that for any two constants $K_i$, $K_j$, $i,j=1,\ldots, 5$, we have $K_j \leq C K_i$.</p>
</div>

<p><em>Note.</em> The constants $K_1, \ldots, K_5$ depend on $X$. In fact, they depend on the <em>sub-Gaussian norm</em> of $X$, that we will introduce later.</p>

<!-- Proof 1/2 Button -->
<button onclick="toggleCollapseExpand('proofSubgaussianity12', 'proofSubgaussianity12Container', 'Proof')" id="proofSubgaussianity12Button">
  <i class="fa fa-cog fa-spin"></i> Proof <a href="#subGaussianityProp:1">1.</a> $\Rightarrow$ <a href="#subGaussianityProp:2">2.</a>
</button>

<!-- Proof of Prop1, 1. => 2. -->
<div style="width: 100%; display: none; padding: 5px 5px; " id="proofSubgaussianity12Container">
    <p>Directly,</p>
    <p>$$\begin{aligned}{\rm I\!E}[|X|^p] 
    {}={}&
    \int_0^\infty {\rm P}[|X|^p \geq u] {\rm d}u
    \\
    {}\overset{u = t^p}{=}{}& \int_0^\infty {\rm P}[|X|^p \geq t^p] {\rm d}t^p
    \\
    {}={}&
    \int_0^\infty {\rm P}[|X|^p \geq t^p] p t^{p-1} {\rm d}t
    \\
    {}\overset{\text{1.}}{=}{}& \int_0^\infty 2 \exp(-t^2/K_1^2) p t^{p-1}{\rm d}t
    \end{aligned}$$</p>
    <p>By defining $\xi = t/K_1$,</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[|X|^p] 
    {}\leq{}& 
    \int_0^\infty 2 \exp(-\xi^2)p K_1^{p-1}\xi^{p-1}K_1 {\rm d}\xi
    \\
    {}={}&
    K_1^p \int_0^\infty 2 e^{-\xi^2}p \xi^{p-1} {\rm d}\xi
    \\
    {}={}& K_1 p \int_0^\infty e^{-\xi^2} (\xi^2)^{\frac{p}{2}-1}{\rm d}\xi^2
    \\
    {}={}&
    K_1 p \Gamma\left(\frac{p}{2}\right) 
    \leq
    K_1 p \left(\frac{p}{2}\right)^{\frac{p}{2}},
    \end{aligned}$$</p>
    <p>where the last inequality is because $\Gamma(x) \leq x^x$ for all $x>0$. We conclude that</p>
    <p>$$\begin{aligned}\|X\|_{L^p} \leq K_1^{1/p} p^{1/p} \left(\frac{p}{2}\right)^{\frac{1}{2}}.\end{aligned}$$</p>
    <p>The quantity $p^{1/p}$ is bounded, that is, there is an $M>0$ such that $p^{1/p} \leq M$ for all $p\geq 1$; in fact $M\approx 1.445$. </p>
    <p>$$\begin{aligned}\|X\|_{L^p} \leq K_1^{1/p} M \left(\frac{p}{2}\right)^{\frac{1}{2}} \leq \max\{K_1, 1\} M \left(\frac{p}{2}\right)^{\frac{1}{2}},\end{aligned}$$</p>
    <p>so, property <a href="#subGaussianityProp:2">2.</a> is satisfies with $K_2 = \max\{K_1, 1\} M / \sqrt{2}$.  $\Box$</p>
</div><br>

<!-- Proof 2/3 Button -->
<button onclick="toggleCollapseExpand('proofSubgaussianity23', 'proofSubgaussianity23Container', 'Proof')" id="proofSubgaussianity23Button">
  <i class="fa fa-cog fa-spin"></i> Proof <a href="#subGaussianityProp:2">2.</a> $\Rightarrow$ <a href="#subGaussianityProp:3">3.</a>
</button>

<!-- Proof of Prop1, 2. => 3. -->
<div style="width: 100%; display:none; padding: 5px 5px;" id="proofSubgaussianity23Container">
    <p>By homogeneity, it suffices to show this, <u style="text-decoration:underline dotted" title="without loss of generality">wlog</u>, for $K_2 = 1$. Suppose $\|X\|_{L^p} \leq \sqrt{p}$ for all $p\geq 1$. Then, we expand the <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of $X^2$ using Taylor's expansion,</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[\exp(\lambda^2 X^2)]
    {}={}&
    {\rm I\!E}\left[ 1 + \sum_{p=1}^{\infty} \frac{(\lambda^2 X^2)^p}{p!} \right]
    \\
    {}={}&
    1 + \sum_{p=1}^{\infty} \frac{\lambda^{2p} {\rm I\!E}[X^{2p}]}{p!} 
    \end{aligned}$$</p>
    <p>We have that ${\rm I\!E}[X^{2p}] = \|X\|_{L^{2p}}^{2p} \leq \sqrt{2p}^{2p} = (2p)^p$, so</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[\exp(\lambda^2 X^2)]
    {}\leq{}&    
    1 + \sum_{p=1}^{\infty} \frac{\lambda^{2p} (2p)^p}{p!} .
    \end{aligned}$$</p>
    <p>Next we use the fact that $p! \geq (p/e)^p$, so</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[\exp(\lambda^2 X^2)]
    {}\leq{}&    
    1 + \sum_{p=1}^{\infty} \frac{\lambda^{2p} (2p)^p}{\left(\frac{p}{e}\right)^p}
    {}={} 
    1 + \sum_{p=1}^{\infty} \frac{(2\lambda^2 p)^p}{\left(\frac{p}{e}\right)^p}
    \\
    {}={}&
    \frac{1}{1 - 2e\lambda^2},
    \end{aligned}$$</p>
    <p>provided that $2e\lambda^2 < 1$.</p>
    <p>We now use the fact that $(1-x)^{-1} \leq e^{2x}$ for $x\in[0, 1/2]$, so</p>
    <p>$${\rm I\!E}[\exp(\lambda^2 X^2)] \leq \exp(4e\lambda^2),$$</p>
    <p>for all $\lambda$ with $|\lambda| \leq \frac{1}{2\sqrt{e}}$, which is <a href="#subGaussianityProp:3">3.</a> with $K_3 = 2\sqrt{e}$.  $\Box$</p>
</div><br>

<!-- Proof 3/4 Button -->
<button onclick="toggleCollapseExpand('proofSubgaussianity34', 'proofSubgaussianity34Container', 'Proof')" id="proofSubgaussianity34Button">
  <i class="fa fa-cog fa-spin"></i> Proof <a href="#subGaussianityProp:3">3.</a> $\Rightarrow$ <a href="#subGaussianityProp:3">4.</a>
</button>

<!-- Proof of Prop1, 3. => 4. -->
<div style="width: 100%; display:none; padding: 5px 5px;" id="proofSubgaussianity34Container">
    <p>It can be seen that for $K_4 = K_3/\ln 2$, Property <a href="#subGaussianityProp:3">3.</a> implies <a href="#subGaussianityProp:3">4.</a>  $\Box$</p>
</div><br>



<!-- Proof 4/1 Button -->
<button onclick="toggleCollapseExpand('proofSubgaussianity41', 'proofSubgaussianity41Container', 'Proof')" id="proofSubgaussianity41Button">
  <i class="fa fa-cog fa-spin"></i> Proof <a href="#subGaussianityProp:4">4.</a> $\Rightarrow$ <a href="#subGaussianityProp:1">1.</a>
</button>


<!-- Proof of Prop1, 4. => 1. -->
<div style="width: 100%; display:none; padding: 5px 5px;" id="proofSubgaussianity41Container">
    <p>Without loss of generality, take $K_4=1$. Then,</p>
    <p>$$\begin{aligned}{\rm P}[|X| \geq t] {}={}& {\rm P}[e^{X^2} \geq e^{t^2}]
    \\
    {}\leq{}& 
    {\rm E}[\exp(X^2)]e^{-t^2}
    \\
    {}\leq{}&
    2\exp(-t^2),\end{aligned}$$</p>
    <p>where the first inequality is because of <a href="../vershynin-hdp-1#markov-ineq" target="_blank">Markov's inequality</a>, and the second is from Property <a href="#subGaussianityProp:3">4.</a>  $\Box$</p>
</div><br>

<!-- Proof 3/5 Button -->
<button onclick="toggleCollapseExpand('proofSubgaussianity35', 'proofSubgaussianity35Container', 'Proof')" id="proofSubgaussianity35Button">
  <i class="fa fa-cog fa-spin"></i> (Zero-mean assumption) Proof <a href="#subGaussianityProp:3">3.</a> $\Rightarrow$ <a href="#subGaussianityProp:5">5.</a>
</button>


<!-- Proof of Prop1, 3. => 5. -->
<div style="width: 100%; display:none; padding: 5px 5px;" id="proofSubgaussianity35Container">
    <p>Without loss of generality, take $K_3=1$. For all $x\in{\rm I\!R}$ we have $e^x \leq x + e^{x^2}$. Then,</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[\exp(\lambda X)] 
    {}\leq{}& 
    {\rm I\!E}[\lambda X + e^{\lambda^2 X^2}]
    {}={}
    {\rm I\!E}[e^{\lambda^2 X^2}] \leq e^{\lambda^2},
    \end{aligned}$$</p>
    <p>for $|\lambda| \leq 1$. To prove Property <a href="#subGaussianityProp:5">5.</a> for $|\lambda| \geq 1$, we use the fact that $2\lambda x \leq \lambda^2 + x^2$. Then,</p>
    <p>$$\begin{aligned}
    {\rm I\!E}[\exp(\lambda X)] \leq e^{\lambda^2/2}{\rm I\!E}[e^{X^2/2}] \leq e^{\lambda^2/2}e^{1/2} \leq e^{\lambda^2}.~\Box
    \end{aligned}$$</p>    
</div><br>


<!-- Proof 5/1 Button -->
<button onclick="toggleCollapseExpand('proofSubgaussianity51', 'proofSubgaussianity51Container', 'Proof')" id="proofSubgaussianity51Button">
  <i class="fa fa-cog fa-spin"></i> (Zero-mean assumption) Proof <a href="#subGaussianityProp:5">5.</a> $\Rightarrow$ <a href="#subGaussianityProp:1">1.</a>
</button>

<!-- Proof of Prop1, 5. => 1. -->
<div style="width: 100%; display:none; padding: 5px 5px;" id="proofSubgaussianity51Container">
    <p>Without loss of generality, take $K_5=1$. We use Bernstein's trick:</p>
    <p>$$\begin{aligned}
    {\rm P}[X > t] 
    {}={}& 
    {\rm P}[e^{\lambda X} > e^{\lambda t}] 
    \\
    {}\leq{}&
    {\rm I\!E}e^{\lambda X}e^{-\lambda t} \leq e^{-\lambda t}e^{\lambda^2} = e^{-\lambda t + \lambda^2}.
    \end{aligned}$$</p>    
    <p>For $\lambda = t/2$, it is ${\rm P}[X > t] \leq e^{-t^2/4}$, so ${\rm P}[|X| > t] \leq 2e^{-t^2/4}$.  $\Box$</p>
</div><br>



<!-- EXERCISE 2.5.5 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px; margin-top:10px" id="ex255">
<p><strong>Exercise 2.5.5. (Regarding Proposition 1, Item <a href="#subGaussianityProp:3">3</a>)</strong></p>
<ol>
    <li>Suppose $X\sim\mathcal{N}(0,1)$. Show that the function $\lambda \mapsto {\rm I\!E}[\exp(\lambda^2 X^2)]$ is finite <em>only</em> in some neighbourhood of zero.</li>
    <li>Suppose that some random variable $X$ satisfies ${\rm I\!E}[\exp(\lambda^2 X^2)] \leq \exp(K\lambda^2)$ for all $\lambda \in {\rm I\!R}$ for some constant $K$. Show that $X$ is an essentially bounded random variable.</li>
</ol>
</div>

<p><em>Solution.</em> 1. For $X\sim\mathcal{N}(0,1)$ we have</p>
<p>$$\begin{aligned}{\rm I\!E}[\exp(\lambda^2 X^2)] {}={}& \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}e^{\lambda^2x^2}e^{-\frac{x^2}{2}}{\rm d}x = \frac{2\sqrt{\pi}}{\sqrt{2 - 4\lambda}},\end{aligned}$$</p>
<p>and the integral converges only for $|\lambda| < 1/2$.</p>
<p>2. It suffices to determine a value $N$ such that ${\rm P}[|X| \geq N] = 0$. Take $z\in{\rm I\!R}$. Then,</p>
<p>$$\begin{aligned}
{\rm P}[|X| \geq z] 
{}={}& 
{\rm P}[\exp(\lambda^2 X^2) \geq \exp(\lambda^2 z^2)]
\\
{}\leq{}& 
\exp(-\lambda^2 z^2){\rm I\!E}\exp(K\lambda^2)
\\
{}={}\exp[\lambda^2 (K-z^2)].
\end{aligned}$$</p>
<p>Choose $N \geq \sqrt{K}$. Then,</p>
<p>$$\begin{aligned}{\rm P}[|X| \geq N] \leq \exp(\lambda^2 (\underbrace{K-N^2}_{\lneq 0})),\end{aligned}$$</p>
<p>and take $\lambda \to \infty$ to see that ${\rm P}[|X| \geq N] = 0$. $\Box$</p>

<!-- <p>$$\begin{aligned}\end{aligned}$$</p> -->
<!-- <p>$$\begin{aligned}\end{aligned}$$</p> -->

## The sub-Gaussian norm

<p>A random variable that satisfies any of the properties of Proposition <a href="#subGaussianityProp">1</a> is called a sub-Gaussian random variable. We define the sub-Gaussian norm of $X$ to be the smallest value of $K_4$ in property <a href="#subGaussianityProp:4">4</a> and we denote this as </p>

<p>$$\begin{aligned}\|X\|_{\psi_2} = \inf\{t > 0 : {\rm I\!E}\exp(X^2/t^2) \leq 2\}.\end{aligned}$$</p>

<p>More specifically, this is the <em>Orlisz norm</em> of $X$ generated by the function $\Phi(u) = e^{u^2} - 1$ (more on this later).</p>

<p>From the definition, it follows that ${\rm I\!E}[e^{X^2/\|X\|_{\psi_2}}] \leq 2,$
and if there is a $K$ such that
${\rm I\!E}[e^{X^2/K}] \leq 2,$
then $K \geq \|X\|_{\psi_2}.$</p>


> <p><b>Note:</b> We could define a norm $\|X\|' = \sup_{p \geq 1} \|X\|_{L^p}/\sqrt{p}$. This would be equal to $\|X\|_{\psi_2}$ times an absolute constant.</p>

<!-- EXERCISE 2.5.7 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex257">
<p><strong>Exercise 2.5.7. ($\|{}\cdot{}\|_{\psi_2}$ is a norm)</strong> Show that $\|{}\cdot{}\|_{\psi_2}$ is indeed a norm on the space of sub-Gaussian random variables.</p>
</div>

<p><em>Solution.</em> It is easy to show nonnegativity and homogeneity, so we will move on to subadditivity. Let $X$ and $Y$ be two sub-Gaussian random variables. We have<p>
<p>$$\begin{aligned}
\|X+Y\|_{\psi_2}
{}={}&
\inf\left\{t>0 {}:{} {\rm I\!E}\exp\frac{(X+Y)^2}{t^2} \leq 2\right\}
\\
{}={}&
\inf\left\{t=t_1+t_2, t_1, t_2>0 {}:{} {\rm I\!E}\exp\frac{(X+Y)^2}{(t_1 + t_2)^2} \leq 2\right\}
\\
{}={}&
\inf\left\{t=t_1+t_2, t_1, t_2>0 {}:{} {\rm I\!E}\exp\left(\frac{t_1 \frac{X}{t_1}+t_2 {Y}{t_2}}{t_1 + t_2}\right)^2  \leq 2\right\}
\\
{}={}&
\inf\left\{t=t_1+t_2, t_1, t_2>0 {}:{} {\rm I\!E}\exp\left(\frac{t_1}{t_1+t_2} \frac{X}{t_1} + \frac{t_2}{t_1+t_2} \frac{Y}{t_2}\right)^2  \leq 2\right\}.
\end{aligned}$$</p>
<p>We have managed to conjure up a convex combination. We define the convex function $g(s) = \exp s^2$ (easy to check). By the convexity property of $g$, we have</p>

<p>$$\begin{aligned}
{\rm I\!E}\exp\left(\frac{t_1}{t_1+t_2} \frac{X}{t_1} + \frac{t_2}{t_1+t_2} \frac{Y}{t_2}\right)^2
\leq 
\frac{t_1}{t_1+t_2} {\rm I\!E}\exp (X/t_1)^2
{}+{} 
\frac{t_2}{t_1+t_2} {\rm I\!E}\exp (Y/t_2)^2,
\end{aligned}$$</p>
<p>so,</p>
<p>$$\begin{aligned}
\|X+Y\|_{\psi_2}
{}\leq{}&
\inf \Big\{ 
    t=t_1+t_2, t_1, t_2>0 {}:{}
    \\
    &\qquad 
    \frac{t_1}{t_1+t_2} {\rm I\!E}\exp (X/t_1)^2
{}+{} 
\frac{t_2}{t_1+t_2} {\rm I\!E}\exp (Y/t_2)^2 \leq 2
    \Big\},
\\
{}\leq{}&
\inf \Big\{ 
    t=t_1+t_2, t_1, t_2>0 {}:{}
    \\
    &\qquad 
    {\rm I\!E}\exp (X/t_1)^2 \leq 2, \text{ and }
    {\rm I\!E}\exp (Y/t_2)^2 \leq 2 \Big\}
\\
{}={}&
\inf \left\{ t_1 > 0 {}:{} {\rm I\!E}\exp (X/t_1)^2 \leq 2 \right\}
\\
&\qquad{}+{}
\inf \left\{ t_2 > 0 {}:{} {\rm I\!E}\exp (Y/t_2)^2 \leq 2 \right\}
\\
{}={}& \|X\|_{\psi_2} + \|Y\|_{\psi_2}.
\end{aligned}$$</p>

<p>Lastly, we need to show that if $\|X\|_{\psi_2} = 0$, then $X=0$ almost surely. From the definition of the sub-Gaussian norm and <a href="#subGaussianityProp">Proposition 1</a>, there is a $C$ such that $\|X\|_{L_p} \leq C \|X\|_{\psi_2}\sqrt{p}$, for all $p\geq 1$. This means that if $\|X\|_{\psi_2} = 0$, then $\|X\|_{L_p}=0$, so $X=0$ a.s. $\Box$</p>

<!-- PROPOSITION 1: Characterisation of subGaussianity -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="subGaussianNormProperties">
    <p><strong>Proposition 2 (Properties of $\|{}\cdot{}\|_{\psi_2}$).</strong> Let $X$ be a sub-Gaussian random variable with sub-Gaussian norm $\|X\|_{\psi_2}$. Then, there exist constants $C, c > 0$ such that</p>
    <ol>
        <li id="subGaussianityNormProp:1">${\rm P}[|X| \geq t] \leq 2 \exp(-ct^2/\|X\|_{\psi_2})$, for all $t\geq 0$</li>
        <li id="subGaussianityNormProp:2">$\|X\|_{L^p} \leq C \|X\|_{\psi_2} \sqrt{p}$ for all $p\geq 1$</li>
        <li id="subGaussianityNormProp:3">${\rm I\!E}\exp(X^2 / \|X\|_{\psi_2}^2) \leq 2$</li>
        <li id="subGaussianityNormProp:4">If ${\rm I\!E}[X] = 0$, then ${\rm I\!E}\exp(\lambda X) \leq \exp(C\lambda^2 \|X\|_{\psi_2}^2)$, for all $\lambda \in {\rm I\!R}$</li>
    </ol>    
</div>

<p>Regarding the first property, we have that</p>
<p>$$\begin{aligned}{\rm P}[|X| > t] {}={}& {\rm P}[X^2 > t^2] \\
{}={}&
{\rm P}\left[\exp\left(\frac{X}{\|X\|_{\psi_2}}\right) > \exp\left(\frac{t^2}{\|X\|_{\psi_2}}\right)\right]
\\
{}\leq{}&
\exp\left(-\frac{t^2}{\|X\|_{\psi_2}}\right) {\rm I\!E}\left[\exp\frac{X}{\|X\|_{\psi_2}}\right]
\\
{}={}& 2 \exp\left(-\frac{t^2}{\|X\|_{\psi_2}}\right),
\end{aligned}$$</p>
<p>which proves the first property. Note that in the first inequality we used <a href="../vershynin-hdp-1#markov-ineq" target="_blank">Markov's inequality</a>.</p>

## An alternative expression for the sub-Gaussian norm

<p>An alternative expression for the sub-Gaussian norm can be produced by <a href="#subGaussianityProp">Proposition 1</a> and, in particular, the equivalence between <a href="#subGaussianityProp:2">2.</a> and <a href="#subGaussianityProp:4">4.</a>. We have</p>
<p>$$\begin{aligned}
\|X\|_{\psi_2} 
{}={}&
\inf \{t>0 {}:{} {\rm I\!E}[\exp(X^2/t^2)] \leq 2\}
\\
{}={}& \inf\{t > 0 {}:{} \|X\|_{p} \leq Ct\sqrt{p}, \text{ for all } p \geq 1\}.
\end{aligned}$$</p>
<p>for some constant $C > 0$. We can now set $s=Ct > 0$, so $t=s/C$, and write</p>
<p>$$\begin{aligned}
\|X\|_{\psi_2} 
{}={}& \frac{1}{C}\inf\{s > 0 {}:{} \|X\|_{p} \leq s\sqrt{p}, \text{ for all } p \geq 1\}
\\
{}={}& \frac{1}{C}\inf\{s > 0 {}:{} \frac{\|X\|_{p}}{\sqrt{p}} \leq s, \text{ for all } p \geq 1\}
\\
{}={}& \frac{1}{C}\sup_{p\geq 1} \frac{\|X\|_{p}}{\sqrt{p}}.
\end{aligned}$$</p>
<p>Along the same lines and using item <a href="#subGaussianityProp:5">5.</a> we can show that a zero-mean random variable has the following sub-Gaussian norm</p>

<p>$$\begin{aligned}\|X\|_{\psi_2} {}={}&
\frac{1}{C}\inf\{K > 0 {}:{} {\rm I\!E}[\exp(\lambda X)] \leq \exp(K^2\lambda^2),  \lambda \in {\rm I\!R}\}
\\
{}={}&
\frac{1}{C}\inf\{K > 0 {}:{} \log {\rm I\!E}[\exp(\lambda X)] \leq K^2\lambda^2,  \lambda \in {\rm I\!R}
\}\end{aligned}$$</p>
<p>The natural logarithm of the <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> is known as the <a href="https://en.wikipedia.org/wiki/Cumulant">cumulant generating function</a>, $\kappa_X$. We can write</p>
<p>$$\begin{aligned}\|X\|_{\psi_2} {}={}&
\frac{1}{C}\inf\{K > 0 {}:{} \kappa_X(\lambda) \leq K^2\lambda^2,  \text{ for all } \lambda \in {\rm I\!R}\}
\\
{}={}&
\frac{1}{C} \sup_{\lambda}\frac{\kappa_X(\lambda)}{\lambda^2}
\end{aligned}$$</p>
<p>Cool! Let's put these in a box...</p>

<!-- PROPOSITION 3 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="thm:psi2-norm-alternative">
<p><strong>Proposition 3. ($\|{}\cdot{}\|_{\psi_2}$ norm)</strong> The sub-Gaussian norm of a sub-Gaussian random variable $X$ can be written as</p>
<p>$$\|X\|_{\psi_2} {}={} \frac{1}{C}\sup_{p\geq 1} \frac{\|X\|_{p}}{\sqrt{p}}$$</p>
<p>for an absolute constant $C$. If $X$ is a zero-mean variable, then</p>
<p>$$\|X\|_{\psi_2} {}={} \frac{1}{C} \sup_{\lambda}\frac{\kappa_X(\lambda)}{\lambda^2}.$$</p>
</div>



## Maximum of sub-Gaussians

### First attempt 

<p>We will first show an upper bound on the expectation of the maximum of finitely many sub-Gaussian random variables which is of the form $O(\log N)$.</p>

<p>Suppose that $X_1, \ldots, X_N$ are sub-Gaussian random variables. In this section we shall study $\max_i |X_i|$ and try to establish uppper bounds. To that end, we will work with the <u style="text-decoration:underline dotted" title="moment generating function">mgf</u>s of $X_i$.</p>
<p>Firstly, we observe that</p>
<p>$$\begin{aligned}\exp(t {\rm I\!E}\max_{i=1,\ldots, N}|X_i|)
{}={}&
\exp ({\rm I\!E}[t \max_{i=1,\ldots, N}|X_i|])
\\
{}\overset{\text{Jensen}}{=}{}& {\rm I\!E} \exp(t \max_{i=1,\ldots, N}|X_i|)
\\
{}={}& {\rm I\!E} \max_{i=1,\ldots, N} \exp(t|X_i|)
\\
{}\leq{}& {\rm I\!E} \max_{i=1,\ldots, N} (e^{tX_i} + e^{-tX_i})
\\
{}={}& {\rm I\!E} \sum_{i=1}^{N} e^{tX_i} + e^{-tX_i}
\\
{}={}&
\sum_{i=1}^{N} {\rm I\!E}e^{tX_i} + {\rm I\!E}e^{-tX_i}.
\end{aligned}$$</p>
<p>Now if we assume that ${\rm I\!E}[X_i] = 0$ for all $i$, we have</p>
<p>$$\begin{aligned}{\rm I\!E}e^{tX_i} \leq \exp(K_5^2 t^2),\end{aligned}$$</p>
<p>for all $t\in{\rm I\!R}$, so from the above inequality,</p>
<p>$$\begin{aligned}\exp(t {\rm I\!E}\max_{i=1,\ldots, N}|X_i|)
\leq 2 \exp(K_5^2 t^2)N,\end{aligned}$$</p>
<p>therefore,</p>
<p>$$\begin{aligned}{\rm I\!E}\max_{i=1,\ldots, N}|X_i| \leq \frac{1}{t}\log(2N) + K_5^2 t,\end{aligned}$$</p>
<p>for all $t>0$. By taking $t = \log(2N)/K_5^2$, we obtain,</p>
<p>$$\begin{aligned}{\rm I\!E}\max_{i=1,\ldots, N}|X_i| \leq  K_5^2 + \log(2N).\end{aligned}$$</p>


### Vershynin's result

<p>We will show the following result, which is Exercise 2.5.10 in [<a href="#cite:ver19" title="Vershynin, HDP">1</a>].</p>

<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex113">
<p><strong>Exercise 2.5.10.</strong> Let $X_1, X_2, \ldots, X_N$ be a sequence of sub-Gaussian random variables, not necessarily independent, with $K_{\max} = \max_i \|X_i\|_{\psi_2}$. Show that</p>
<p>$${\rm I\!E}\max_{i} \frac{|X_i|}{\sqrt{1+\log i}} \leq C  K_{\max}.$$</p>
<p>Then, deduce that for $N\geq 2$,</p>
<p>$${\rm I\!E}\max_{i=1,\ldots,N} |X_i|\leq C  K_{\max} \sqrt{\log N}.$$</p>
</div>

<p><em>Solution.</em> For notational convenience let us define $Y_i = X_i / \sqrt{1 + \log i}$. The key idea is to express the expectation in terms of tail probabilities. We have</p>
<p>$$\begin{aligned}
{\rm I\!E}\left[\max_{i=1,\ldots, N}Y_i\right] 
{}={}&
\int_0^\infty {\rm P}\left[\max_{i=1,\ldots, N}Y_i \geq t\right] {\rm d}t
\\
{}\leq{}&
\int_0^\infty \sum_{i=1}^{N}{\rm P}\left[Y_i \geq t\right] {\rm d}t
\\
{}={}&
\sum_{i=1}^{N} \int_0^\infty {\rm P}\left[Y_i \geq t\right] {\rm d}t
\\
{}={}&
\sum_{i=1}^{N} \int_0^\infty {\rm P}\left[|X_i| \geq t\sqrt{1+\log i}\right] {\rm d}t
\end{aligned}$$</p>
<p>Now define $u = t\sqrt{1+\log i}$, so</p>
<p>$$\begin{aligned}
{\rm I\!E}\left[\max_{i=1,\ldots, N}Y_i\right] 
{}\leq{}&
\sum_{i=1}^{N} \frac{1}{\sqrt{1+\log i}} \int_0^\infty {\rm P}\left[|X_i| \geq u\right] {\rm d}u
\\
{}={}&
\sum_{i=1}^{N} \frac{1}{\sqrt{1+\log i}} \int_0^\infty \exp(-cu^2/\|X_i\|_{\psi_2}) {\rm d}u
\\
{}\leq{}&
\sum_{i=1}^{N} \frac{1}{\sqrt{1+\log i}} \int_0^\infty \exp(-cu^2/K_{\max}) {\rm d}u
\end{aligned}$$</p>
<p>The proof is concluded with a trick that can be found <a href="https://math.stackexchange.com/a/3302080/8357" target="_blank">here</a>.</p>

<!-- <p>$$\begin{aligned}\end{aligned}$$</p> -->


## Sum of sub-Gaussians

<p>Here we will show that the sum of independent sub-Gaussians is sub-Gaussian too.</p>

<!-- PROPOSITION 4 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="subGaussianityProp">
    <p><strong>Proposition 4. (Sub of sub-Gaussians)</strong> Let $X_1, \ldots, X_N$ be <em>independent</em> sub-Gaussian random variables with zero-mean. Then,</p>
    <p>$$\left\|\sum_{i=1}^N X_i\right\|_{\psi_2}^2 {}\leq{} C \sum_{i=1}^{N} \|X_i\|_{\psi_2}^2$$</p>
    <p>where $C$ is an absolute constant.</p>
</div>

<p><em>Proof.</em> The <u style="text-decoration:underline dotted" title="moment generating function">mgf</u> of the sum is</p>
<p>$$\begin{aligned}
{\rm I\!E}\left[\exp\left(\lambda \sum_{i=1}^{N}X_i\right)\right]
{}={}&
\prod_{i=1}^{N} {\rm I\!E}[\exp(\lambda X_i)]
\\
{}\leq{}& \prod_{i=1}^N \exp (C_0\lambda^2 \|X_i\|_{\psi_2}^2)
\\
{}={}&
\exp\left(\lambda^2 C_0 \sum_{i=1}^N \|X_i\|_{\psi_2}^2\right).
\end{aligned}$$</p>
<p>Given that $\sum_i X_i$ is a zero-mean RV, it follows from Proposition 1, Item <a href="#subGaussianityProp:5">5</a>, that it is sub-Gaussian and $K_5^2 = C_0 \sum_{i=1}^N \|X_i\|_{\psi_2}^2.$ There is a constant $\bar{C}$ such that $K_1 \leq \bar{C}K_5 = \bar{C}C_0 \sum_{i=1}^N \|X_i\|_{\psi_2}^2$. This completes the proof. $\Box$</p>


> See next: <a href="../vershynin-hdp-3">Reading Vershynin's HDP III: Subexponential random variables</a>

## References 

<ol>
  <li id="cite:ver19">R. Vershynin, High Dimensional Probabiltiy: an introduction with applications in data science, Cambridge University Press, 2019</li>  
</ol>