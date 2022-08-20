---
author: "Pantelis Sopasakis"
title: Generalised directional derivatives
date: 2022-08-20
description: Generalised directional derivatives and examples
summary: Examples on the Dini, Clarke and Michel-Penot directional derivatives
math: true
series: ["Mathematix"]
tags: ["Convex Analysis"]
---

<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  table-layout: fixed
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
  width: 25%
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


{{< math.inline >}}
<p>In the previous post on the <a href="../rayleigh-quotient">Rayleigh quotient</a> we defined the directional derivative of a function \(f: \mathbb{R}^n \to \overline{\mathbb{R}}\) as</p>

$$\begin{aligned}f'(x; h) = \lim_{t \downarrow 0} \frac{f(x+th)-f(x)}{t},\end{aligned}$$

<p>provided that the limit exists.</p> 

<p>It turns out that all convex functions are directionally differentiable on the interior (actually, the core) of their domains and \(f'(x; \cdot)\) is sublinear. However, the sublinearity property may fail when working with nonconvex functions. This motivates the definition of generalised directional derivatives which will hopefully be accompanied by some good calculus rules.</p>
{{</ math.inline >}}




## 1. Generalised Directional Derivative

### 1.1. Dini Directional Derivative

{{< math.inline >}}
<p>The Dini directional derivative of a function \(f: \mathbb{R}^n \to \overline{\mathbb{R}}\) at a point \(x\) along a direction \(h\) is a generalised derivative given by </p>

<p>$$\begin{aligned}f^-(x; h) = \liminf_{t \downarrow 0} \frac{f(x+th)-f(x)}{t}.\end{aligned}$$</p>

<p>However, as we will see later, the Dini directional derivative is not always sublinear.</p>
{{</ math.inline >}}




### 1.2. Clarke Directional Derivative

{{< math.inline >}}
<p>We also define the Clarke directional derivative of \(f\)  at \(x\) for \(h\) is given by</p>

<p>$$\begin{aligned}f^\circ(x; h) {}={}& \limsup_{y \to x, t \downarrow 0} \frac{f(y+th)-f(y)}{t} \\ {}={}& \inf_{\delta>0}\, \sup_{\substack{\|y-x\|\leq \delta \\ t \in (0,\delta)}} \frac{f(y+th)-f(y)}{t}.\end{aligned}$$</p>

<p>We can show that</p>

<div style="border-style:solid;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition 1.</strong> The Clarke directional derivative is positive homogeneous and <em>sublinear</em>, i.e.,</p>
<p>$$\begin{aligned}f^\circ(x; u + v) \leq f^\circ(x; u) + f^\circ(x; v),\end{aligned}$$</p>
<p>for all \(x, u, v\).</p>
</div>

<p><em>Proof.</em> To show that \(f^\circ(x; {}\cdot{})\) is positively homogeneous, take \(\lambda > 0\). We have </p>

<p>$$\begin{aligned}f^\circ(x; \lambda h) {}={}& \limsup_{y\to x, t\downarrow 0}\frac{f(y+\lambda t h) - f(y)}{t}\\{}\overset{\eta = \lambda t}{=}{}& \limsup_{y\to x, \eta\downarrow 0}\frac{f(y+\eta h) - f(y)}{\tfrac{1}{\lambda}\eta} = \lambda f^\circ(x; h).\end{aligned}$$</p>

<p>We need to show that \(f^\circ(x; h+h') \leq f^\circ(x; h) + f^\circ(x; h')\). We have</p>

<p>$$\begin{aligned}f^\circ(x; h+h') {}={}& \limsup_{y\to x, t\downarrow 0}\frac{f(y+th+th') - f(y)}{t}\\{}={}& \limsup_{y\to x, t\downarrow 0}\frac{f(y+th+th') - f(y+th') + f(y+th') - f(y)}{t} \\ {}\leq{}&  \limsup_{y\to x, t\downarrow 0}\frac{f(y+th+th') - f(y+th') }{t} \\ &\qquad+  \limsup_{y\to x, t\downarrow 0}\frac{f(y+th') - f(y)}{t}\end{aligned}$$</p>

<p>Now in the first limsup let us define \(\tilde{y} = y+th\) and see that \(\tilde{y} \to x\) as \(y \to x\) and \(t \downarrow 0\), therefore the first limsup is equal to \(f^\circ(x; h)\). \(\blacksquare\)</p>

<p>Observe that the Clarke directional derivative majorises the Dini derivative \(f^-(x; h) \leq f^\circ(x; h)\). This is easy to prove - if not, please write a comment here below and I will elaborate.</p>

{{</ math.inline >}}



### 1.3. Michel-Penot Directional Derivative

{{< math.inline >}}
<p>The Michel-Penot directional derivative is defined as</p>

<p>$$\begin{aligned}f^\#(x; h) {}={}& \sup_{u\in\mathbb{R}^n} \limsup_{t \downarrow 0} \frac{f(x+t(h+u))-f(x+th)}{t}.\end{aligned}$$<p>

<div style="border-style:solid;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition 2.</strong> The Michel-Penot directional derivative is sublinear, i.e.,</p>
<p>$$\begin{aligned}f^\#(x; u + v) \leq f^\#(x; u) + f^\#(x; v),\end{aligned}$$</p>
<p>for all \(x, u, v\).</p>
</div><br/>

<p><em>Proof.</em> Coming soon.</p>

<p>Observe that</p>

<p>$$\begin{aligned}f^-(x; h) \leq f^\#(x; h) \leq f^\circ(x; h).\end{aligned}$$</p>

<p>To prove the second inequality, \(f^\#(x; h) \leq f^\circ(x; h)\), fix \(u\) and observe that</p>

<p>$$\begin{aligned}f^\circ(x; h) = \limsup_{y\to x, t\downarrow 0} \frac{f(y+th) - f(y)}{t} \geq \limsup_{\substack{y=x+tu,\\ t\downarrow 0}} \frac{f(x+tu+th) - f(x+tu)}{t},\end{aligned}$$</p>

<p>and take the supremum with respect to \(u\) on both sides.</p>

{{</ math.inline >}}

## 2. Examples

### 2.1. Absolute value
{{< math.inline >}}
<p>Let us first see how the above three derivatives behave on a nonsmooth convex function. Consider the function \(f(x) = |x|\), with \(x \in \mathbb{R}\). The Dini derivative of \(f\) at \(x=0\) for \(h\) is</p>

<p>$$\begin{aligned}f^-(x; h) = \liminf_{t\downarrow 0} \frac{|th|}{t} = |h|.\end{aligned}$$</p>

<p>For the Clarke derivative we have that </p>

<p>$$\begin{aligned}f^\circ(0; h) = \limsup_{y\to 0, t\downarrow 0} \frac{|y+th|-|y|}{t} \leq \limsup_{y\to 0, t\downarrow 0} \frac{|y| + |th| - |y|}{t} = |h|,\end{aligned}$$</p>

<p>using the triangle inequality. By choosing the sequences \(y_\nu = \tfrac{1}{\nu^2}\) and \(t_\nu = \tfrac{1}{\nu}\) we have that </p>

<p>$$\begin{aligned}f^\circ(0; h) {}={}& \limsup_{y\to 0, t\downarrow 0} \frac{|y+th|-|y|}{t} \\ {}\geq{}& \lim_{\nu} \frac{|y_\nu + t_\nu h|-|y_\nu|}{t_\nu} = |h|,\end{aligned}$$</p>

<p>therefore, \(f^\circ(0; h) = |h|\). Since the Michel-Penot directional derivative is between the Dini and Clarke derivatives, we conclude that \(f^\#(0; h) = |h|\) (however, it can be easily determined using the definition).</p>
{{</ math.inline >}}

### 2.2. Negative Absolute value
{{< math.inline >}}
<p>Consider the function \(f(x) = -|x|\) with \(x \in \mathbb{R}\). This is a nonsmooth concave function. The Dini derivative of \(f\) at \(x=0\) along the direction \(h\) is </p>

<p>$$\begin{aligned}f^-(0; h) {}={}& \liminf_{t\downarrow 0} \frac{-|th|}{t} = -|h|.\end{aligned}$$</p>

<p>The Michel-Penot derivative is</p>

<p>$$\begin{aligned}f^\#(0; h) {}={}& \sup_{u\in\mathbb{R}}\limsup_{t\downarrow 0} \frac{-|th + tu|+|tu|}{t} = \sup_u |u| - |h+u| = -|h|.\end{aligned}$$</p>

<p>The last equality is because (i) \(\sup_u |u| - |h+u| \geq |0| - |h+0| = -|h|\) and (ii) by the triangle inequality \(\sup_u |u| - |h+u| \leq -|h|\).</p>

<p>Lastly, the Clarke derivative of \(f(x) = -|x|\) at 0 is</p>

<p>$$\begin{aligned}f^\circ(0; h) {}={} \limsup_{y \to 0, t\downarrow 0} \frac{|y+th|-|y|}{t} {}\leq{} |h|,\end{aligned}$$</p>

<p>by using the triangle inequality. By following the same procedure as with \(|x|\) in Example 1, we conclude that \(f^\circ(0; h) = |h|\).</p>

<p>We can state the following result that gives the Clarke derivative of \(-f\) in terms of that of \(f\).</p>


<div style="border-style:solid;border-width:1.5px;padding-left:10px;padding-top:15px">
<p>
<strong>Proposition 3.</strong> It is \((-f)^\circ(x; h) = f^\circ(x; -h)\).
</p></div><br/>

<p><em>Proof.</em> We have</p>

<p>$$\begin{aligned}f^\circ(x; -h) {}={} \limsup_{y \to x, t\downarrow 0} \frac{f(y-th)-f(y)}{t},\end{aligned}$$</p>

<p>Define \(z = y + th\) and observe that as \(t \downarrow 0\) and \(y \to x\), \(z \to x\). Additionally, \(y = z + th\). Therefore we have </p>

<p>$$\begin{aligned}f^\circ(x; -h) {}={} \limsup_{y \to x, t\downarrow 0} \frac{f(y-th)-f(y)}{t} = \limsup_{z\to x, t \downarrow 0} \frac{f(z) - f(z+th)}{t} = -f^\circ(x; h),\end{aligned}$$</p>

<p>which completes the proof. \(\blacksquare\)</p>

<p>Note that the property of Proposition 3 does not hold for the Dini derivative, but the Michel-Penot derivative satisfies \(f^\#(x; -h) = (-f)^\#(x; h)\).</p>

<p>It is also easy to prove that</p>

<div style="border-style:solid;border-width:1.5px;padding-left:10px;padding-top:15px">
<p><strong>Proposition 4.</strong> It is \((\lambda f)^\circ(x; h) = \lambda f^\circ(x; h)\), for \(\lambda \geq 0\).</p>
</div>
<br/>

<p>Proposition 4 holds for the Michel-Penot derivative too.</p>
{{</ math.inline >}}


### 2.3. An interesting case

{{< math.inline >}}
<p>Consider the following function</p>

<p>$$\begin{aligned}f(x) = \begin{cases}x^2 \sin\tfrac{1}{x}, & \text{ for } x \neq 0 \\ 0, &\text{ for } x=0\end{cases}\end{aligned}$$</p>

<p>This is how the graph of this function looks like:</p>

<img src="https://mathematix.files.wordpress.com/2021/10/weird_function_v4.jpg" alt="interesting function; is this differentiable?"/>

<p>and if we look closer, this is what we'll see</p>

<img src="https://mathematix.files.wordpress.com/2021/10/weird_function_v2.jpg" alt="interesting function zoom in around zero"/>

<p>and then if we zoom in even more, this is what we see </p>

<img src="https://mathematix.files.wordpress.com/2021/10/weird_function_v3.jpg" alt="interesting function further zoom in"/>

<p>This function is not differentiable at zero; this is its derivative:</p>

<img src="https://mathematix.files.wordpress.com/2021/10/d_weird_function_v2.jpg" alt="derivative at zero"/>

<p>We are interested in the (generalised) derivatives at \(x=0\). The Dini derivative is</p>

<p>$$\begin{aligned}f^-(x; h) {}={} \liminf_{t \downarrow 0}\frac{t^2h^2 \sin\tfrac{1}{th}}{t}=\liminf_{t \downarrow 0} th^2 \sin\tfrac{1}{th}=0.\end{aligned}$$</p>

<p>In order to determine the Clarke derivative we use the fact that the function is continuously differentiable at all \(y \neq 0\), therefore, by Taylor's approximation theorem,</p>

<p>$$ \begin{aligned}f(y + th) {}={} y(t) + f'(y)th + o(|th|),\end{aligned}$$</p>

<p>for adequately small \(t\), and for \(y \neq 0\),</p>

<p>$$\begin{aligned}f'(y) {}={} 2y\sin\tfrac{1}{y} - \cos\tfrac{1}{y}.\end{aligned}$$</p>

<p>Then, for any fixed \(h\),</p>

<p>$$\begin{aligned}f^\circ(0; h) {}={}& \limsup_{y\to 0, t \downarrow 0}\frac{f'(y)th + o(|th|)}{t} \\ {}={}& \limsup_{y\to 0, t \downarrow 0} f'(y)|h| + \frac{o(|th|)}{t} = |h|.\end{aligned}$$</p>

<p>The Michel-Penot derivative is<p>

<p>$$\begin{aligned}f^\#(0; h) {}={}& \sup_u\limsup_{t \downarrow 0}\frac{(th+tu)^2\sin\frac{1}{th+tu} - t^2u^2\sin\frac{1}{tu}}{t} \\ {}={}& \sup_u \limsup_{t \downarrow 0} t \left[ (h+u)^2\sin\frac{1}{th+tu} - u^2\sin\frac{1}{tu}\right] = 0.\end{aligned}$$<p>


{{</ math.inline >}}



### 2.4. An even more interesting example

{{< math.inline >}}
<p>Consider the function</p>

<p>$$\begin{aligned}f(x) {}={} \begin{cases}3^n, & \text{ if } 3^n \leq x \leq 2(3^n), n \in \mathbb{Z} \\ 2x - 3^{n+1}, &\text{ if } 2(3^n) \leq x \leq 3^{n+1} \\ 0, & \text{ if } x \leq 0\end{cases}\end{aligned}$$</p>

<img src="https://mathematix.files.wordpress.com/2021/10/weirder_function.jpg?w=1024" alt="wow! what a function!"/>

<p>The Dini derivative of \(f\) at 0 for a negative direction \( h < 0\) is clearly equal to 0. For \( h>0\), by definition</p>

<p>$$\begin{aligned}f'(0; h) = \liminf_{t \downarrow 0}\frac{th}{t} = \lim_{\epsilon \downarrow 0} \inf_{0 < t < \epsilon}\frac{f(th)}{t} = \frac{h}{2},\end{aligned}$$</p>

<p>so, overall \( f'(0; h) = \max\{0, \tfrac{h}{2}\}.\)</p>

<p>The liminf of the Dini derivative with \( h>0\) is illustrated below:</p>

<img src="https://mathematix.files.wordpress.com/2021/10/dini.gif?w=1024" alt="demonstration of liminf of the Dini derivative"/>

<p>For the Clarke derivative with \( h>0\) it is convenient to use the following expression:</p>

<p>$$\begin{aligned}f^\circ(0; h) ={}& \limsup_{y\to 0, t \downarrow 0}\frac{f(y+th) - f(y)}{t} \\ {}={}& \lim_{\epsilon \downarrow 0} \underbrace{\sup_{\substack{|y| < \epsilon \\ 0 < t < \epsilon}} \frac{f(y+th) - f(y)}{t}}_{2} = 2h,\end{aligned}$$</p>

<p>whereas for \( h < 0\) we have \( f^\circ(0; h) = 0\), so overall \( f^\circ(0; h) = \max\{0, 2h\}\).</p>


<img src="https://mathematix.files.wordpress.com/2021/10/clarke-1.gif?w=1024" alt="demonstration of liminf of the Dini derivative"/>

<p>Lastly, the Michel-Penot derivative at 0 along a direction \( h<0\) is equal to zero because it is bounded between the Dini and Clarke derivatives, which vanish for \( h<0\). For \( h > 0\) the Michel-Penot derivative is \( f^\#(0; h) = 2h\) and the optimal u in the supremum is \( u = 2\). Overall \( f^\#(0; h) = \max\{0, 2h\}\).</p>

<p>Below you can see an animation showing the convergence of the limsup in the definition of the Michel-Penot derivative for \( h=1\) and for different values of \( u\) (\( u=1,\tfrac{1}{2},2\)).</p>

<img src="https://mathematix.files.wordpress.com/2021/10/michel-penot.gif?w=1024" alt="illustration of the Michel Penot derivative"/>

{{</ math.inline >}}



### 2.5. Summary

{{< math.inline >}}
<table>
  <tr>
    <th>Function</th>
    <th>Dini, \(f'(0; h)\)  </th>
    <th>Michel-Penot \(f^\#(0; h)\) </th>
    <th>Clarke \(f^\circ(0; h)\)</th>
  </tr>
  <tr>
    <td>\(f(x) = |x|\)</td>
    <td>\(|h|\)</td>
    <td>\(|h|\)</td>
    <td>\(|h|\)</td>
  </tr>
  <tr>
    <td>\(f(x) = -|x|\)</td>
    <td>\(-|h|\)</td>
    <td>\(-|h|\)</td>
    <td>\(|h|\)</td>
  </tr>
  <tr>
    <td><a href="#23-an-interesting-case">Example 2.3</a></td>
    <td>\(0\)</td>
    <td>\(0\)</td>
    <td>\(|h|\)</td>
  </tr>
  <tr>
    <td><a href="#24-an-even-more-interesting-example">Example 2.4</a></td>
    <td>\(\max\{0, \tfrac{h}{2}\}\)</td>
    <td>\(\max\{0, 2h\}\)</td>
    <td>\(\max\{0, 2h\}\)</td>
  </tr>
</table>
{{</ math.inline >}}

## Bibliographic notes

[1] The examples given here are the solutions of Exercise 1 in Section 6.1 (Generalized derivatives) of the book: JM Borwein and AS Lewis, Convex Analysis and Nonlinear Optimization, Canadian Mathematical Society, Second Edition, Springer, 2010 (p. 127-128).

[2] FH Clarke, Optimization and Nonsmooth Analysis, SIAM Classics in Applied Mathematics, Wiley, 1983: A great book to understand the concept of Clarke's generalised derivative.