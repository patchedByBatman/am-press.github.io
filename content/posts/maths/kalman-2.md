---
author: "Pantelis Sopasakis"
title:  "The Kalman Filter II: Conditioning"
date: 2023-02-01
description: "Conditioning multivariate normals"
summary: "We derive a useful formula that allows us to compute the conditional expectation of jointly normally distributed data; this result plays a central role in the development of the Kalman filter"
math: true
series: ["Mathematix"]
tags: ["Estimation", "Probability"]
collapsible: true
---

> <b>Read first:</b> <a href="../kalman-1">Kalman Filter I: The Gauss-Markov model</a><br>
> <b>Read next:</b> <a href="../kalman-3">Kalman Filter III: Measurement and time updates</a>

<p>In this post we present a result of central importance in the development of the Kalman filter.</p>

## Main result

<div style="border-style:dashed;border-width:1.5px;padding: 10px 10px 10px 10px; margin-bottom: 10px" id="thm:normal_conditioning"> 
 <p><b>Theorem II.1 (Conditioning of multivariate normal).</b> Let $X \sim \mathcal{N}(\mu, \Sigma)$ be an $n$-dimensional random vector. Let us partition $X$ into two random vectors $X_1$ and $X_2$ as follows</p>

<p>$$ X = \begin{bmatrix}X_1\\X_2\end{bmatrix},\tag{1}$$</p>

<p>with $X_1 \in \R^{n_1}$, $X_2 \in \R^{n_2}$ with $n = n_1 + n_2$. Let</p>

<p>$$ \mu=\begin{bmatrix}\mu_1\\\mu_2\end{bmatrix} \text{and } \Sigma = \begin{bmatrix}\Sigma_{11} & \Sigma_{12}\\\Sigma_{21} & \Sigma_{22}\end{bmatrix},\tag{2}$$</p>

<p>and assume that $\Sigma_{22}\in\mathbb{S}_{++}^{n_2}$.</p>

<p>Then, the conditional distribution of $X_1$ given that $X_2 = x_2$ is normal with mean</p>
<p>$${\rm I\!E}[X_1 {}\mid{} X_2 = x_2] {}={} \mu_1 + \Sigma_{12}\Sigma_{22}^{-1}(x_2 - \mu_2),\tag{3a}$$</p>
and
<p>$${\rm Var}[X_1{}\mid{} X_2 = x_2] {}={} \Sigma_{11} - \Sigma_{12}\Sigma_{22}^{-1} \Sigma_{21}.\tag{3b}$$</p>
</div>

<p>Theorem <a href="#thm:normal_conditioning">II.1</a> is discussed in the following video:</p>

<div id="youtube-video-conditioning">
<iframe alt="YouTube video on conditioning" style="margin:auto;display:block;" width="560" height="315" src="https://www.youtube.com/embed/h2sTS8cHkPM?start=456" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>

<p></p>
<p><em>Proof.</em> The proof hinges on <em>Schur's complement</em>. We define the Schur complement of $\Sigma$ (with respect to $\Sigma_{22}$) to be the following nonsingular matrix</p>
<p>$$\Sigma_* = \Sigma_{11} - \Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}.\tag{4}$$</p>
<p>Then, the inverse of $\Sigma$ is the matrix</p>
<p id="eq:schur_inverse">$$
  \Sigma^{-1} = \begin{bmatrix}
    \Sigma_{11}^*   & \Sigma_{12}^*
    \\
    \Sigma_{21}^{*} & \Sigma_{22}^{*}
  \end{bmatrix},\tag{5}$$</p>
<p>where $\Sigma_{11}^* = \Sigma_*^{-1}$, $\Sigma_{12}^*=-\Sigma_*^{-1}\Sigma_{12}\Sigma_{22}^{-1}$, $\Sigma_{21}^*=(\Sigma_{12}^*)^\intercal$ (since $\Sigma$ is symmetric) and $\Sigma_{22}^* = \Sigma_{22}^{-1} + \Sigma_{22}^{-1}\Sigma_{21}\Sigma_*^{-1}\Sigma_{12}\Sigma_{22}^{-1}$. We need to determine the pdf of $X_1$ conditional on $X_2$; we know that $p_{X_1\mid X_2}(x_1 {}\mid{} x_2)$ is <em>proportional to</em> $p_{X_1, X_2}(x_1, x_2)$. We denote this as</p>

<p id="eq:px1_cond_x2">$$p_{X_1\mid X_2}(x_1 {}\mid{} x_2) \propto p_{X_1, X_2}(x_1, x_2).\tag{6}$$</p>

<p>Since $(X_1, X_2)$ are jointly normal, we have that its pdf is</p>

<p id="eq:px1x2_proportional">$$p_{X_1, X_2}(x_1, x_2)
  {}\propto{}
  \exp\left(-\tfrac{1}{2}(x - \mu)^\intercal \Sigma^{-1}(x - \mu)\right),\tag{7}$$</p>

<p>where $x=(x_1, x_2)$ and $\mu = (\mu_1, \mu_2)$.</p> 

<p>The reader can use the block-inversion formula in Equation <a href="#eq:schur_inverse">(5)</a> to verify that we can write</p>

<p>$$\begin{aligned}
  (x - \mu)^\intercal \Sigma^{-1}(x - \mu)
  {}={}&
  (x_1 - \mu_*)^\intercal \Sigma_*^{-1}(x_1 - \mu_*)
  \\
  &\quad{}+{}
  (x_2 - \mu_2)^\intercal \Sigma_{22}^{-1}(x_2 - \mu_2),\tag{8}\end{aligned}$$</p>

<p>where $\mu_* = \mu_1 + \Sigma_{12}\Sigma_{22}^{-1}(x_2 - \mu_2)$. From Equations <a href="#eq:px1_cond_x2">(6)</a> and <a href="#eq:px1x2_proportional">(7)</a> we conclude that</p>

<p>$$p_{X_1\mid X_2}(x_1 {}\mid{} x_2)
  {}\propto{}
  \exp\left(-\tfrac{1}{2}(x_1 - \mu_*)^\intercal \Sigma_*^{-1}(x_1 - \mu_*)\right),\tag{9}$$</p>

<p>which proves that $X_1\mid X_2$ is normal with mean $\mu_*$ and variance $\Sigma_*$. $\Box$</p>

<p><b>Remark.</b> By Equation \eqref{eq:nrm:conditional_variance}, we have</p>

<p>$${\rm Var}[X_1{}\mid{} X_2 = x_2] {}={} \Sigma_{11} - \Sigma_{12}\Sigma_{22}^{-1} \Sigma_{21}.\tag{10}$$</p>

<p>Since \(\Sigma_{22} \succ 0\),  \(\Sigma_{12}\Sigma_{22}^{-1} \Sigma_{21} \succcurlyeq 0\),
therefore \(\Sigma_{11} - \Sigma_{12}\Sigma_{22}^{-1} \Sigma_{21} \preccurlyeq \Sigma_{11}\), i.e.,</p>

<p>$${\rm Var}[X_1{}\mid{} X_2 = x_2]  \preccurlyeq  {\rm Var}[X_1].\tag{11}$$</p>

<p>In other words, additional information <em>does not increase</em> (in the sense of $\preccurlyeq$) the uncertainty!}</p>



## Example 

<p>Suppose that $Z=(Z_1, Z_2, Z_3, Z_4)$ is a four-dimensional random variable that follow the normal distribution, $Z \sim \mathcal{N}(\mu, \Sigma)$ with $\mu=(1,2,3,4)$ and</p>

<p>$$
  \Sigma = \begin{bmatrix}
    1.0 & 0.35 & 0.32 & 0.39 \\ 0.35 & 0.84 & 0.3 & 0.26\\ 0.32 & 0.3 & 0.77 & 0.23\\ 0.39 & 0.26 & 0.23 & 0.83
  \end{bmatrix}.\tag{12}$$</p>

<p>The reader can verify that $\Sigma\in\mathbb{S}_{++}^4$. Suppose we measure $Z_3$ and $Z_4$ and we want to determine ${\rm I\!E}[Z_1, Z_2 {}\mid{} Z_3, Z_4]$. We will apply Theorem <a href="#thm:normal_conditioning">II.1</a> with $X_{1}=(Z_1, Z_2)$ and $X_{2}=(Z_3, Z_4)$. We have</p>

<p>$$
  \Sigma_{11} = \begin{bmatrix}1.0 & 0.35\\0.35 & 0.84\end{bmatrix},
  \Sigma_{12} = \begin{bmatrix}0.32 & 0.39\\0.3 & 0.26\end{bmatrix},
  \Sigma_{22} = \begin{bmatrix}0.77 & 0.23\\0.23 & 0.83\end{bmatrix}.$$</p>

<p>and $\mu_1 = (1,2)$, $\mu_2 = (3, 4)$. By Theorem <a href="#thm:normal_conditioning">II.1</a></p>

<p>$${\rm I\!E}\left[Z_1, Z_2 {}
  \left|\hspace{-0.2em}
  \begin{array}{l}
    Z_3 = z_3
    \\
    Z_4 = z_4
  \end{array}
  \hspace{-0.5em}
  \right.
  \right]
  {}={}
  \begin{bmatrix}1\\2\end{bmatrix}
  {+}
  \begin{bmatrix}0.32 & 0.39\\0.3 & 0.26\end{bmatrix}
  \begin{bmatrix}0.77 & 0.23\\0.23 & 0.83\end{bmatrix}^{-1}
  \left(
  \begin{bmatrix}
    z_3 \\z_4
  \end{bmatrix}
  {}-{}
  \begin{bmatrix}3\\4\end{bmatrix}
  \right),$$</p>
<p>and</p>
<p>$$\begin{aligned}
{\rm Var}\left[Z_1, Z_2 {}
  \left|
  \hspace{-0.2em}
  \begin{array}{l}
    Z_3 = z_3
    \\
    Z_4 = z_4
  \end{array}\hspace{-0.5em}
  \right.
  \right]
  {}={}&
  \begin{bmatrix}1.0 & 0.35\\0.35 & 0.84\end{bmatrix}
  \\&\quad{-}
  \begin{bmatrix}0.32 & 0.39\\0.3 & 0.26\end{bmatrix}
  \begin{bmatrix}0.77 & 0.23\\0.23 & 0.83\end{bmatrix}^{-1}
  \begin{bmatrix}0.32 & 0.3\\0.39 & 0.26\end{bmatrix}.\end{aligned}$$</p>

> <b>Read next:</b> <a href="../kalman-3">Kalman Filter III: Measurement and time updates</a>