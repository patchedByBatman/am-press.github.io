---
author: "Pantelis Sopasakis"
title:  "Dual of p-norm via the KKT theorem"
date: 2022-09-17
description: "Dual of p-norm via the KKT theorem"
summary: "Dual of p-norm via the KKT theorem"
math: true
series: ["Mathematix"]
tags: ["Optimization", "Analysis", "Convex Analysis"]
collapsible: true
showtoc: false
---

<p>This is a short post about the dual p-norm, which is essentially defined by an optimisation problem. Recall that the p-norm of a vector $x\in{\rm I\!R}$ is defined as</p>
<p>$$\|x\|_p = \left(\sum_{i=1}^{n}|x_i|^p\right)^{\tfrac{1}{p}}.\tag{1}$$</p>
<p>We will show that the dual of $\|{}\cdot{}\|_p$ with $\|{}\cdot{}\|_q$, where $\tfrac{1}{p} + \tfrac{1}{q} = 1$. To do so, instead of using <a href="https://en.wikipedia.org/wiki/H%C3%B6lder%27s_inequality" target="_blank">Holder's inequality</a>, we will we use the KKT conditions of the optimisation problem that defines the dual norm.</p>
<p>The <a href="https://en.wikipedia.org/wiki/Dual_norm" target="_blank">dual norm</a> is defined as</p>
<p>$$\|z\|_{p,*} = \max_{\|y\|_{p} = 1} y^\intercal z = -\min_{\|y\|_{p}^{p} = 1} -y^\intercal z = -\min_{\|y\|_{p}^{p} = 1} y^\intercal z.\tag{2}$$</p>
<p>The dual norm is, therefore, defined via an equality-constrained optimisation problem. The Lagrangian function is</p>
<p>$$L(y, \lambda) = y^\intercal z + \lambda(\|y\|_{p}^{p} - 1),\tag{3}$$</p>
<p>and</p>
<p>$$\begin{aligned}\nabla_y L(y, \lambda) {}={}& z + \lambda (p|y_i|^{p-1} \mathrm{sign}(y_i) )_i,
\\
\tfrac{{\rm d}}{{\rm d} \lambda}L(y, \lambda) {}={}& \|y\|_{p}^{p} - 1.\tag{4}
\end{aligned}$$</p>
<p>We are looking for a KKT point, i.e., a point $(y^\star, \lambda^\star)$ such that $\nabla_y L(y^\star, \lambda^\star) = 0$ and $\nabla_y L(y^\star, \lambda^\star) = 0$, that is</p>
<p>$$\begin{aligned}z_i + \lambda^\star p|y^\star_i|^{p-1} \mathrm{sign}(y^\star_i) ={}& 0,
\\
\|y\|_{p}^{p} ={}& 1.\tag{5}
\end{aligned}$$</p>
<p>A first observation is that the only way for $\lambda^\star$ to vanish is if $z = 0$, so assuming $z\neq 0$, we have that $\lambda^\star \neq 0$. That said, if $z_i = 0$, then $y_i^\star = 0$. For those indices $i$ such that $z_i \neq 0$ we have</p>
<p>$$\frac{z_i}{\mathrm{sign}(y^\star_i) |y^\star_i|^{p-1}} = -\lambda^\star p,\tag{6}$$</p>
<p>which means that </p>
<p>$$\frac{z_1}{\mathrm{sign}(y^\star_1) |y^\star_1|^{p-1}} = \ldots = \frac{z_n}{\mathrm{sign}(y^\star_n) |y^\star_n|^{p-1}}.\tag{7}$$</p>
<p>Applying an absolute value to all terms and raising to the power $\tfrac{p}{p-1}$ we have</p>
<p>$$\frac{|z_1|^{\tfrac{p}{p-1}}}{|y^\star_1|^{p}} = \ldots = \frac{|z_n|^{\tfrac{p}{p-1}}}{|y^\star_n|^{p}}.\tag{8}$$</p>
<p>At the same time we have that $\|y^\star\|_p^p = 1$, or, what is that same</p>
<p>$$\sum_{i=1}^{n}|y_i^\star|^p = 1.\tag{9}$$</p>
<p>For convenience let us define $q=\tfrac{p}{p-1}$. By combining Equations (8) and (9) we have the linear system</p>
<p>$$\begin{bmatrix}
|z_2|^q & -|z_1|^q
\\
        &  \phantom{-}|z_3|^q & -|z_2|^q
\\[1em]
                &  & \ddots 
\\[0.7em]
&&& |z_{n-1}|^q & -|z_n|^q
\\
1 & 1 & \ldots & 1 & 1
\end{bmatrix}
\begin{bmatrix}
|y_1^\star|^p \\ |y_2^\star|^p \\ \vdots \\ |y_n^\star|^p
\end{bmatrix}
{}={}
\begin{bmatrix}
0\\0\\ \vdots \\ 1
\end{bmatrix}.\tag{10}$$</p>
<p>We can now solve this linear system to find that</p>
<p>$$|y_i^\star|^p = \frac{|z_i|^q}{\sum_{i=1}^{n}|z_i|^q}.\tag{11}$$</p>
<p>Detail: Note that if $z_i=0$ for some indices $i$, then the system of Equation (10) becomes underdetermined, but the $|y_i^\star|^p$ in Equation (11) are still a solution. From Equation (11), we have that</p>
<p>$$y_i^\star = \pm \left(\frac{|z_i|^q}{\sum_{i=1}^{n}|z_i|^q}\right)^{1/p},$$</p>
<p>where the $\pm$ means that for the time being we are not sure about the sign of $y_i^\star$. If we plug this into Equation (2) we have that</p>
<p>$$\|z\|_{p,*} = -\sum_{i=1}^{n}\pm \left(\frac{|z_i|^q}{\sum_{i=1}^{n}|z_i|^q}\right)^{1/p} z_i.$$</p>
<p>In order for $y^\star$ to be a solution of the <em>minimisation</em> problem in Equation (2), the sign of $y_i$ must be the same as the sign of $z_i$, in which case</p>
<p>$$\|z\|_{p,*} = \sum_{i=1}^{n} \left(\frac{|z_i|^q}{\sum_{i=1}^{n}|z_i|^q}\right)^{1/p} z_i = \frac{\sum_{i=1}^{n} |z_i|^{1 + \tfrac{p}{q}}}{\left(\sum_{i=1}^{n}|z_i|^q\right)^{\tfrac{1}{p}}},$$</p>
<p>and since $1 + \tfrac{p}{q} = q$, we have</p>
<p>$$\|z\|_{p,*} =  \frac{\sum_{i=1}^{n} |z_i|^{q}}{\left(\sum_{i=1}^{n}|z_i|^q\right)^{\tfrac{1}{p}}} = \left(\sum_{i=1}^{n}|z_i|^q\right)^{1-\tfrac{1}{p}} = \left(\sum_{i=1}^{n}|z_i|^q\right)^{\tfrac{1}{q}} = \|z\|_{q}.$$</p>
