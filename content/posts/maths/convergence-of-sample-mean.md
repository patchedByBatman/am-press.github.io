---
author: "Pantelis Sopasakis"
title:  "Reading Vershynin's HDP I"
date: 2023-06-29
description: "A result on the convergence of sample mean"
summary: "<p>We show that the sample mean converges to the true mean at a rate of 1 / sqrt(k)</p>"
math: true
series: ["Mathematix"]
tags: ["Probability", "Vershynin"]
collapsible: true
draft: false
---

<p>These are my notes on Ronan Vershynin's "High dimensional probability", Chapters 1 and 2 [<a href="#cite:ver19" title="Vershynin, HDP">1</a>] and some solved exercises.</p>

## Preliminaries

<!-- EXERCISE 1.1.3 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex113">
<p><strong>Exercise 1.1.3.</strong> Let \(X_1, X_2, \ldots\) be a sequence of iid random variables with mean \(\mu\) and a finite variance. Show that</p>
<p>$${\rm I\!E}\left|\frac{1}{N}\sum_{i=1}^{N}X_i - \mu\right| {}={} O\left(\frac{1}{\sqrt{N}}\right).$$</p>
</div>

<p><em>Solution.</em> Without loss of generality we shall assume that $\mu=0$.</p> <p>Firstly, we will get rid of that annoying absolute value as follows: Let us define</p>
<p>$$\bar{X}_N = \frac{1}{N}\sum_{i=1}^{N}X_i.$$</p>
<p>Then,</p>
<p>$${\rm I\!E}|\bar{X}_N| = {\rm I\!E} \sqrt{\bar{X}_N^2} \leq \sqrt{{\rm I\!E}[\bar{X}_N^2]},$$</p>
<p>where we used <a href="https://en.wikipedia.org/wiki/Jensen%27s_inequality" target="_blank">Jensen's inequality</a> (using the fact that the square root is a concave function).</p>

<p>Now for ${\rm I\!E}[\bar{X}_N^2]$ we have</p>
<p>$${\rm I\!E}[\bar{X}_N^2] = \frac{1}{N^2} {\rm I\!E}\left(\sum_{i=1}^{N}X_i\right)^2 = \frac{1}{N^2} {\rm I\!E}\left[\sum_{i=1}^{N}X_i^2\right] =\frac{1}{N^2} N\sigma^2 = \frac{\sigma^2}{N}.$$</p>

<p>In the second equality we used the assumption of independence.</p>

<p>As a result</p>
<p>$${\rm I\!E}\left|\frac{1}{N}\sum_{i=1}^{N}X_i\right| {}\leq{} \sqrt{{\rm I\!E}[\bar{X}_N^2]} = \frac{\sigma}{\sqrt{N}}.$$</p>

<p>This completes the proof. $\Box$</p>


<p>Let us juxtapose the above result to the classical Lindeberg-Lévy central limit theorem (CLT):</p>

<!-- LL-CLT -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ll-clt">
<p><strong>Theorem 1 (Lindeberg-Lévy CLT).</strong> Let \(X_1, X_2, \ldots\) be a sequence of iid random variables with mean \(\mu\) and a finite variance \(\sigma^2\). Define $S_N = \sum_{i=1}^{N}X_i$ and</p>
<p>$$Z_N = \frac{S_N - {\rm I\!E[S_N]}}{\sqrt{{\rm Var}[S_N]}} = \frac{1}{\sigma\sqrt{N}}\sum_{i=1}^{N}(X_i - \mu).$$</p>
<p>Then, as \(N\to\infty\)</p>
<p>$$Z_N \overset{d}{\to} N(0, 1),$$</p>
<p>where \(\overset{d}{\to}\) means "convergence in distribution."</p>
</div>

<p><em>Proof.</em> See [<a href="#cite:scholz19">2</a>].</p>

<p>We see that the Lindeberg-Lévy CLT also gives a \(1/\sqrt{N}\) type convergence result, but in the sense of convergence in distribution and it also gives us that "limit distribution", which is a normal.</p>

## Tails of the normal distribution

<!-- EXERCISE 2.1.4 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex214">
<p><strong>Exercise 2.1.4. (Truncated normal distribution)</strong> Let \(g\sim\mathcal{N}(0,1)\). Show that for all $t\geq 1$, we have</p>
<p>$$\begin{aligned}{\rm I\!E}[g^2 1_{g>t}] ={}& t \tfrac{1}{\sqrt{2\pi}}e^{-\tfrac{t^2}{2}} + {\rm P}[g > t] \\  \leq{}& \left(t+\tfrac{1}{t}\right)\tfrac{1}{\sqrt{2\pi}} e^{-\tfrac{t^2}{2}}.\end{aligned}$$</p>
</div>

<p><em>Solution.</em> We have</p>
<p>$$\begin{aligned}{\rm I\!E}[g^2 1_{g>t}] 
={}& 
\int_t^\infty x^2 e^{-\tfrac{x^2}{2}}\tfrac{1}{\sqrt{2\pi}} {\rm d}x
\\
{}={}& 
\tfrac{1}{\sqrt{2\pi}} \int_t^\infty x^2 e^{-\tfrac{x^2}{2}} {\rm d}x
\\
{}={}& 
\tfrac{1}{\sqrt{2\pi}} \int_t^\infty - x \left(e^{-\tfrac{x^2}{2}}\right)' {\rm d}x
\\
{}={}& 
-\tfrac{1}{\sqrt{2\pi}} \left[ \left.x e^{-\tfrac{x^2}{2}}\right|_{t}^{\infty} - \int_t^\infty e^{-\tfrac{x^2}{2}} {\rm d}x\right]
\\
{}={}& 
-\tfrac{1}{\sqrt{2\pi}} \left[ -te^{-\tfrac{t^2}{2}} -  \int_t^\infty e^{-\tfrac{x^2}{2}}{\rm d}x\right]
\\
{}={}&
\tfrac{1}{\sqrt{2\pi}}  te^{-\tfrac{t^2}{2}} + {\rm P}[g > t]
\end{aligned}$$</p>
<p>We now invoke Proposition 2.1.2 in [<a href="#cite:ver19" title="Vershynin, HDP">1</a>] according to which</p>
<p>$${\rm P}[g > t] \leq \tfrac{1}{t} \tfrac{1}{\sqrt{2\pi}} e^{-\tfrac{t^2}{2}}.$$</p>
<p>This completes the proof. $\Box$</p>






## A quick brush-up on probability inequalities

<p>Let us start with Markov's inequality, which is one of the most fundamental probability inequalities. Many other well-known inequalities are derived from this.</p>

<!-- MARKOV -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="markov-ineq">
<p><strong>Theorem 2 (Markov's inequality).</strong> Let \(X\) be a nonnegative random variable and \(t>0\). Then</p>
<p>$${\rm P}[X \geq t] \leq \frac{{\rm I\!E[X]}}{t}.$$</p>
</div>

<p>Chebyshev's inequality is a corollary of Markov's inequality.</p>

<!-- CHEBSHEV'S INEQUALITY -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="cheby-ineq">
<p><strong>Corollary 3 (Chebyshev's inequality).</strong> Let \(X\) be a random variable with mean $\mu$ and variance $\sigma^2$ and \(t>0\). Then</p>
<p>$${\rm P}[|X-\mu| \geq t] \leq \frac{\sigma^2}{t^2}.$$</p>
</div>

<p><em>Proof.</em> The left-hand side of Chebyshev's inequality is ${\rm P}[|X-\mu| \geq t] = {\rm P}[(X-\mu)^2 \geq t^2]$. The random variable $Y=(X-\mu)^2$ is nonnegative, so we can apply Markov's inequality:</p>
<p>$${\rm P}[(X-\mu)^2 \geq t^2] \leq \frac{{\rm I\!E}[(X-\mu)^2 ]}{t^2} = \frac{\sigma^2}{t^2}.$$</p>
<p>This completes the proof. $\Box$</p>




<div id="fig1">
<img src="/prob-inequalities.png" alt="Probability inequalities"  style="width: 90%; margin-left: auto;margin-right: auto;">

<p><em><strong>Figure 1.</strong> The Markov, Chebyshev, and Hoeffding inequalities.</em></p>
</div>



## Hoeffding's inequality and more

<p>Let us start by stating Hoeffding's inequality for independent symmetric Bernoulli random variables. Recall that the symmetric Bernoulli distribution - <em>aka</em> the Rademacher distribution - takes the values \(-\tfrac{1}{2}\) and \(\tfrac{1}{2}\) with equal probability.</p>

<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="cheby-ineq">
<p><strong>Theorem 4 (Hoeffdings's inequality for symmetric Bernoulli).</strong> Let \(X_1, \ldots, X_N\) be independent symmetric Bernoulli random variables, and \(a{}\in{}{\rm I\!R}^N\). Then, for any \(t\geq 0\),</p>
<p id="eq:h1">$${\rm P}\left[\sum_{i=1}^{N}a_i X_i \geq t\right] \leq \exp\left(- \frac{t^2}{2\|a\|_2^2}\right).\tag{H1}$$</p>
</div>

<p><em>Proof.</em> The proof is given in [<a href="#cite:ver19" title="Vershynin, HDP">1</a>], but a couple of things are left to the reader as an exercise.</p>

<p>Firstly, we assume without loss of generality that $\|a\|_2=1$. Let's see why: suppose we have proven (<a href="#eq:h1">H1</a>) with $\|a\|_2=1$, that is</p>
<p>$${\rm P}\left[\sum_{i=1}^{N}a_i X_i \geq t\right] \leq \exp\left(- \frac{t^2}{2}\right).\tag{\text{H1'}}$$</p>
<p>Then, if \(\|a\|\neq 1\) (and \(\|a\|\neq 0\)), we define $a_i' = a_i / \|a\|_2$ and we have</p>
<p>$${\rm P}\left[\sum_{i=1}^{N}a_i X_i \geq t\right] = {\rm P}\left[\sum_{i=1}^{N}\frac{a_i}{\|a\|_2} X_i \geq \frac{t}{\|a\|_2}\right] \overset{H1'}{\leq} \exp\left(- \frac{t^2}{2\|a\|_2^2}\right).$$</p>

<p>Now the trick is to use Markov's inequality after we apply the function $\exp(\lambda \cdot)$, where $\lambda > 0$, on both sides of the inequality inside the probability</p>
<p>$$\begin{aligned}{\rm P}\left[\sum_{i=1}^{N}a_i X_i \geq t\right] ={}& {\rm P}\left[\exp\left(\lambda\sum_{i=1}^{N}a_i X_i\right) \geq \exp(\lambda t)\right] \\ {}\leq{}& e^{-\lambda t} {\rm I\!E}\left[ \exp \left( \lambda \sum_{i=1}^{N}a_i X_i\right)\right].\end{aligned}$$</p>

<p>In the last step we applied Markov's inequality (<a href="#markov-ineq">Theorem 2</a>). Next we have that</p>

<p>$$\begin{aligned}{\rm I\!E}\left[ \exp \left( \lambda \sum_{i=1}^{N}a_i X_i\right)\right] {}={}& {\rm I\!E}\left[ \prod_{i=1}^{N} \exp(\lambda a_i X_i)\right] \\ {}={}& \prod_{i=1}^{N} {\rm I\!E} \exp(\lambda a_i X_i)\end{aligned}$$</p>

<p>Then it is not difficult to see that ${\rm I\!E} \exp(\lambda a_i X_i) = \cosh(\lambda a_i).$ And here comes this exercise:</p>

<!-- EXERCISE 2.2.3 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex223">
<p><strong>Exercise 2.2.3. (Bounding the hyperbolic cosine)</strong> Show that for all $x\in{\rm I\!R}$</p>
<p>$$\cosh (x) \leq \exp(x^2/2).$$</p>
</div>

<p><em>Solution.</em> We want to prove that $\ln \cosh x \leq \tfrac{1}{2}x^2$. Define $f(x)=\ln \cosh x - \tfrac{1}{2}x^2$. Then $f'(x) = \tanh x - x$ and $f''(x) = -\tanh^2(x) \leq 0$, so $f$ is concave. The only solution of $f'(x)=0$ is $x=0$ and $f(0) = 0$, so $f$ has a maximum at $x=0$ and $f(x)\leq 0$ for all $x\in{\rm I\!R}$. $\Box$</p>

<p>Back to the proof of Hoeffding's inequality, we have</p>
<p>$$\begin{aligned}{\rm P}\left[\sum_{i=1}^{N}a_i X_i \geq t\right] {}\leq{}& e^{-\lambda t} \prod_{i=1}^{N}  \exp(\lambda^2 a_i^2 / 2) \\ {}={}& \exp\left(-\lambda t + \tfrac{\lambda^2}{2}\sum_{i=1}^{N}a_i^2\right) \\ {}={}& \exp\left(-\lambda t + \tfrac{\lambda^2}{2}\right).\end{aligned}$$</p>

<p>Taking the minimum with respect to $\lambda > 0$, which is attained at $\lambda = t$, we prove Hoeffding's inequality. $\Box$</p>


<p><b>Remark.</b> In the proof of the above version of Hoeffding's inequality we used the <a href="https://en.wikipedia.org/wiki/Moment-generating_function" target="_blank"><em>moment generating function</em></a> (MGF) of a random variable $X$ which is defined as $M_X(\lambda) = {\rm I\!E}\exp(\lambda X)$. The MGF is a function that shows up all the time in such probability inequalities. The same argument as above is used to prove the <a href="https://en.wikipedia.org/wiki/Chernoff_bound" target="_blank">Chernoff bound</a>.</p>


<p>Hoeffding's inequality can be generalised to general bounded variables.</p>

<!-- THEOREM 5 -->
<div style="border-style:solid;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="cheby-ineq">
<p><strong>Theorem 5 (Hoeffdings's inequality for bounded random varibles).</strong> Let \(X_1, \ldots, X_N\) be independent random variables, bounded in $[m_i, M_i]$ for all $i$. Then, for any \(t > 0\),</p>
<p id="eq:h2">$${\rm P}\left[\sum_{i=1}^{N} (X_i - {\rm I\!E}[X_i]) \geq t\right] \leq \exp\left(- \frac{2t^2}{\sum_{i=1}^{N}(M_i - m_i)^2}\right).\tag{H2}$$</p>
</div>

<p><em>Proof.</em> See [<a href="#cite:Duchi">3</a>].</p>

<!-- EXERCISE 2.2.8 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex228">
<p><strong>Exercise 2.2.8. (Boosting randomised algorithms)</strong> We have an algorithm for solving some decision problem, which makes a (binary) decision at random and returns the correct answer with probability \(\tfrac{1}{2}+\delta\), for some \(\delta > 0\), which is a little better than a random guess. We run the algorithm \(N\) times and take the majority vote. Show that for any \(\epsilon \in (0, 1)\), the answer is correct with probability \(1 - \epsilon\), as long as \(N \geq \tfrac{1}{2} \delta^{-2} \ln \epsilon^{-1}\).</p>
</div>

<p><em>Solution.</em> Let $X_i$ be the outcome of the $i$-th run of the algorithm where $X_i=0$ corresponds to a correct decision, and $X_i$ corresponds to a wrong decision. Then ${\rm I\!E}[X_i] = \tfrac{1}{2}-\delta$ and $X_i$ is bounded in $[0, 1]$. By Hoeffding's inequality we see that</p>

<p>$$\begin{aligned}&{}{\rm P}\left[\sum_{i=1}^{N}(X_i - (\tfrac{1}{2}-\delta)) \geq t\right] \leq \exp\left(-\frac{2t^2}{N}\right) \\ \Leftrightarrow & {\rm P}\left[\sum_{i=1}^{N}X_i - N(\tfrac{1}{2}-\delta) \geq t\right]  \leq \exp\left(-\frac{2t^2}{N}\right).\end{aligned}$$</p>


<p>The probability of the randomised algorithm (based on majority vote) to give the wrong answer is</p>
<p>$$\begin{aligned}P_{\rm err} ={}& {\rm P}\left[\sum_{i=1}^{N}X_i \geq \frac{N}{2}\right] \\ {}={}& \left[\sum_{i=1}^{N}X_i - N(\tfrac{1}{2}-\delta) \geq \frac{N}{2}- N(\tfrac{1}{2}-\delta)\right] \\ {}={}& \left[\sum_{i=1}^{N}X_i - N(\tfrac{1}{2}-\delta) \geq N\delta\right] \\ {}\leq{}& \exp\left(-\frac{2}{N}N^2\delta^2\right) = \exp(-2N\delta^2).\end{aligned}$$</p>

<p>To have $P_{\rm err} \leq \epsilon$ it suffices that</p>
<p>$$\exp(-2\delta^2 N) \leq \epsilon \Leftrightarrow N \geq \frac{1}{2\delta^2}\ln \tfrac{1}{\epsilon}.$$</p>
<p>This proves the assertion. $\Box$</p>


<!-- EXERCISE 2.2.10 -->
<div style="border-style:dashed;border-width:1.5px;padding: 10px 15px 0px 10px; margin-bottom: 10px" id="ex2210">
<p><strong>Exercise 2.2.10. (Small ball probabilities)</strong> Let \(X_1, \ldots, X_N\) be nonnegative independent continuous random variables. Suppose that the <span title="probability density function"><u style="text-decoration:underline dotted">pdf</u></span> of $X_i$ are uniformly bounded by $1$. Then</p>
<ol>
    <li>Show that ${\rm I\!E}[-tX_i] \leq 1/t$ for all $t > 0$</li>
    <li>Deduce that
        <p>$${\rm P}\left[\frac{1}{N}\sum_{i=1}^{N}X_i \leq \epsilon\right] \leq (e\epsilon)^N.$$</p>
    </li>
</ol>
</div>

<p><em>Solution.</em> (1): Using the law of the unconscious statistician,</p>
<p>$${\rm I\!E}[e^{-tX_i}] = \int_{0}^{\infty} e^{-tx}p_{X_i}(x){\rm d}x \leq \int_0^\infty e^{-tx}{\rm d}x = \tfrac{1}{t}.$$</p>
<p>(2): We have</p>
<p>$$\begin{aligned}
    {\rm P}\left[\frac{1}{N}\sum_{i=1}^{N}X_i \leq \epsilon\right]
    {}={}&
    {\rm P}\left[\sum_{i=1}^{N}-\frac{X_i}{\epsilon} \leq -N\right]
    \\
    {}\overset{\text{Ber.}}{=}{}&
    {\rm P}\left[\exp \left(\lambda \sum_{i=1}^{N}-\frac{X_i}{\epsilon}\right) \leq \exp(-\lambda N)\right]
    \\
    {}\overset{\text{Mar.}}{\leq}{}&
    e^{\lambda N} {\rm I\!E}\left[ \exp\left(-\lambda \sum_{i=1}^{N}\frac{X_i}{\epsilon}\right)\right]
    \\
    {}\overset{\text{Ind.}}{=}{}&
    e^{\lambda N} \prod_{i=1}^{N}  {\rm I\!E} [-\lambda X_i / \epsilon] \leq e^{\lambda N}(\epsilon/\lambda)^N.
\end{aligned}$$</p>
<p>Above, "Ber." stands for Bernstein's trick, "Mar." stands for Markov inequality, and "Ind." refers to the independence of $X_i$. The above inequality holds for $\lambda=1$, and the assertion follows. $\Box$</p>



## References 

<ol>
  <li id="cite:ver19">R. Vershynin, High Dimensional Probabiltiy: an introduction with applications in data science, Cambridge University Press, 2019</li>
  <li id="cite:scholz19">F.W. Scholz, Central Limit Theorems and Proofs, Lecture Notes, Math/Stat 394, University of Washington, Winter 2019 (<a href="https://faculty.washington.edu/fscholz/DATAFILES394_2019/CLT.pdf" target="_blank">pdf</a>)</li>
  <li id="cite:Duchi">John Duchi, CS229 Supplemental Lecture notes: Hoeffding's inequality, Lecture Notes, CS229, Stanford (<a href="http://cs229.stanford.edu/extra-notes/hoeffding.pdf" target="_blank">pdf</a>)</li>
</ol>
