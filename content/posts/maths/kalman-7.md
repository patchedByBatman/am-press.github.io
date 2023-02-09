---
author: "Pantelis Sopasakis"
title:  "The Kalman Filter VII: Recursive maximum a posteriori"
date: 2023-02-09
description: "The Kalman filter is a recursive maximum a posteriori estimator"
summary: "We show that the Kalman filter is a recursive maximum a posteriori estimator. This "
math: true
series: ["Mathematix"]
tags: ["Estimation"]
collapsible: true
---

> <b>Previous post:</b> <a href="../kalman-6">Kalman Filter VI: Further examples</a><br>
> <b>Read next:</b> <a href="../kalman-8">The Kalman Filter VIII: Observer form, Steady state, Square root and Information form</a><br>

<p>Consider the dynamical system</p>

<p>$$\begin{aligned}
            x_{t+1} {}={} & Ax_t + w_t,
            \\
            y_t {}={}     & Cx_t + v_t,
        \end{aligned}$$</p>

<p>under the independence assumptions we stated <a href="../kalman-1#assumptions">earlier</a> and assuming that $w_t$, $v_t$, and $x_0$ are normally distributed, that is,</p>
<p>$$\begin{aligned}
            p_{w_t}(w) {}\propto{}   & \exp \left[-\tfrac{1}{2}\|w\|_{Q^{-1}}^2\right],
            \\
            p_{v_t}(v) {}\propto{}   & \exp \left[-\tfrac{1}{2}\|v\|_{R^{-1}}^2\right],
            \\
            p_{x_0}(x_0) {}\propto{} & \exp \left[-\tfrac{1}{2}\|x_0-\bar{x}_0\|_{P_{0}^{-1}}^{2}\right].
        \end{aligned}$$</p>

<p>Given a set of measurements $y_0, y_1, \ldots, y_{N-1}$ we need to estimate $x_0, x_1, \ldots, x_{N}$.</p>



## Useful results

<p>In what follows we use the convenient notation $x_{0:N}=(x_0, \ldots, x_N)$, and likewise we define $y_{0:N}$, $w_{0:N}$ and so on.</p>


<!-- Proposition VII.1: Joint distribution of states -->
<div style="border-style:dashed;border-width:1.5px;padding-left:10px;" id="PropVII-1">
<p><strong>Proposition VII.1 (Joint distribution of states).</strong> For any $N\in{\rm I\!N}$</p>
<p>$$p(x_{0:N})
        {}={}
        p(x_0)\prod_{t=0}^{N-1}p_{w_t}(x_{t+1} - Ax_{t}).$$</p>
</div>
<!-- END Proposition VII.1: Joint distribution of states -->

<!-- Proof of Proposition VII.1: Joint distribution of states -->
<button onclick="toggleCollapseExpand('proofPropVII1', 'proofPropVII1Container', 'proof')" id="proofPropVII1Button">
  <i class="fa fa-cog fa-spin"></i> Click to see the proof
</button>
<div style="margin-top:20px"></div>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofPropVII1Container">
<p><em>Proof.</em> It is</p>
<p>$$\begin{aligned}
p(x_{0:N}) {}={}& p(x_0)p(x_{1:N} \mid x_0)
\\
{}={}& p(x_0)p(x_1 \mid x_0) p(x_{2:N} \mid x_0,x_1)
\\
{}={}& p(x_0)p(x_1 \mid x_0) p(x_2 \mid x_{0}, x_{1})\cdot\ldots\cdot p(x_N \mid x_{0:N-1})
\end{aligned}$$</p>
<p>By the <a href="../kalman-1#markovianity-of-the-state-sequence">Markovianity of the sequence of states</a>,</p>
<p>$$\begin{aligned}
p(x_{0:N}) {}={}& p(x_0)p(x_1 \mid x_0) p(x_2 \mid x_{1})\cdot\ldots\cdot p(x_N \mid x_{N-1})
\\
{}={}& p(x_0) \prod_{t=1}^{N-1} p_{w_t}(x_{t+1} - f(x_t)),
\end{aligned}$$</p>
<p>where in the last step we used <a href="../kalman-1#propI1">Proposition I.1</a>. This completes the proof. $\Box$</p>
</div>
<!-- END Proof of Proposition VII.1: Joint distribution of outputs -->


<!--  
        Proposition VII.2: Joint distribution of states 
-->
<div style="border-style:dashed;border-width:1.5px;padding-left:10px;"  id="PropVII-2">
<p><strong>Proposition VI.2 (Joint distribution of outputs).</strong> Let $N\in{\rm I\!N}$. Then</p>
<p>$$p(y_{0:N})
        {}={}
        p(y_0)\prod_{t=1}^{N}p(y_t {}\mid{} y_{0:t-1}),$$</p>
<p>where $y_{0:t} = (y_0, \ldots, y_t)$.</p>
</div>

<br/>

<p><em>Proof.</em> Similar to the proof of <a href="#PropVII-1">Proposition VII.1</a>. $\Box$</p>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition VII.3 (Joint distribution of states and $w$'s).</strong> For any $N\in{\rm I\!N}$</p>
<p>$$\begin{aligned}p(x_{0:N}, w_{0:N-1})
        {}={}
        \begin{cases}
            0,                                         & \text{if not } x_{t+1} = Ax_t + w_t,
            \\
            p_{x_0}(x_0)\prod_{t=0}^{N-1}p_{w_t}(w_t), & \text{otherwise}
        \end{cases}\end{aligned}$$</p>
</div>

<br/>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;">
<p><strong>Proposition VI.4 (Joint distribution of states given outputs).</strong> For any $N\in{\rm I\!N}$</p>
<p>$$\begin{aligned}p(x_{0:N} {}\mid{} y_{0:N-1})
            {}\propto{}
            p_{x_0}(x_0)\prod_{t=0}^{N-1}p_{v_t}(y_t - Cx_t)p_{w_t}(x_{t+1}-Ax_t).\end{aligned}$$</p>
</div>



## The full information estimation problem 

<p>From <a href="PropVII-4">Proposition VII.4</a>, the log-likelihood (omitting the constant term) is </p>
<p>$$\begin{aligned}
         & \log p(x_0,\ldots, x_{N} {}\mid{} y_0, \ldots, y_{N-1})\\
         & \qquad{}={}
        \log p_{x_0}(x_0)
        {}+{}
        \sum_{t=1}^{N-1}\log p_{v_t}(y_t - Cx_t) + \log p_{w_t}(x_{t+1}-Ax_t)
         \\
         & \qquad{}={}
        -\tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^{2}
        + \tfrac{1}{2}\sum_{t=0}^{N-1}  -\|y_t - Cx_t\|_{R^{-1}}^{2} {}-{} \|x_{t+1}-Ax_t\|_{Q^{-1}}^{2}.
    \end{aligned}$$</p>
<p>Using the result of this exercise, we have the maximum <em>a posteriori</em> (MAP) estimate</p>
<p>$$\begin{aligned}
        (\hat{x}_t)_{t=0}^{N-1}
        {}={} &
        \argmax_{x_0,\ldots,x_{N-1}} p(x_0,\ldots, x_{N-1} {}\mid{} y_0, \ldots, y_{N})
        \\
        {}={} &
        \argmax_{x_0,\ldots,x_{N-1}} \log p(x_0,\ldots, x_{N-1} {}\mid{} y_0, \ldots, y_{N})
         \\
        {}={} &
        \argmax_{x_0,\ldots,x_{N-1}}
        -\tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^{2}
        + \tfrac{1}{2}\sum_{t=0}^{N-1}  -\|y_t - Cx_t\|_{R^{-1}}^{2} {}-{} \|x_{t+1}-Ax_t\|_{Q^{-1}}^{2}
        \\
        {}={} &
        \argmin_{x_0,\ldots,x_{N-1}}
        \tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^{2}
        + \tfrac{1}{2}\sum_{t=0}^{N-1}  \|y_t - Cx_t\|_{R^{-1}}^{2} {}+{} \|x_{t+1}-Ax_t\|_{Q^{-1}}^{2}.
    \end{aligned}$$</p>
    <p>In fact we can write it as</a>
    <p>$$(\hat{x}_t)_{t=0}^{N-1}
        {}={}
        \hspace{-1.5em}
        \argmin_{
        \substack{
        x_0,\ldots,x_{N},
        \\
        w_0, \ldots, w_{N-1},
        \\
        v_0, \ldots, v_{N-1},
        \\
        x_{t+1} = Ax_t + w_t, t\in{\rm I\!N}_{[0, N-1]}
        \\
        y_{t} = Cx_t + v_t, t \in {\rm I\!N}_{[0, N]}
        }
        }\hspace{-1em}
        \tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^{2}
        + \sum_{t=0}^{N-1}  \tfrac{1}{2}\|v_t\|_{R^{-1}}^{2} {}+{} \tfrac{1}{2}\|w_t\|_{Q^{-1}}^{2}.$$</p>

<p>We need to solve the problem</p>
<p>$$\begin{aligned}
            \operatorname*{minimise}_{
            \substack{
            x_0,\ldots,x_{N},
            \\
            w_0,\ldots, w_{N-1},
            \\
            v_0, \ldots, v_{N-1}
            }
            }\                  &
            \tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^{2}
            + \sum_{t=0}^{N-1}  \tfrac{1}{2}\|v_t\|_{R^{-1}}^{2} {}+{} \tfrac{1}{2}\|w_t\|_{Q^{-1}}^{2},
            \\
            \text{subject to: } & x_{t+1} = Ax_t + w_t, t\in{\rm I\!N}_{[0, N-1]},
            \\
                                & y_{t} = Cx_t + v_t, t \in {\rm I\!N}_{[0, N]},
        \end{aligned}$$</p>
<p>which is akin to a linear-quadratic optimal control problem. The key difference is the presence of an <em>arrival cost</em> instead of a <em>terminal cost</em> and the initial condition is not fixed. The problem can be written as follows:</p>

<p>$$\begin{aligned}
            \operatorname*{minimise}_{
            \substack{
            x_0,\ldots,x_{N},
            \\
            w_0,\ldots, w_{N-1}
            }
            }\                  &
            \underbrace{\tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^{2}}_{\ell_{x_0}(x_0)}
            + \sum_{t=0}^{N-1}  \underbrace{
            \tfrac{1}{2}\|y_t-Cx_t\|_{R^{-1}}^{2} {}+{} \tfrac{1}{2}\|w_t\|_{Q^{-1}}^{2}
            }_{\ell_t(x_t, w_t)},
            \\
            \text{subject to: } & x_{t+1} = Ax_t + w_t, t\in{\rm I\!N}_{[0, N-1]}.
        \end{aligned}$$</p>
    
<p>This is known as the <b>full information estimation</b> (FIE) problem. Later we will show that FIE is equivalent to the Kalman filter.</p>

## So what?

<p>Firstly, the full information estimation formulation allows us to interpret the Kalman filter as a Bayesian estimator and work in terms of prior and posterior distributions instead of conditional expectations as we did <a href="../kalman-3">earlier</a>. This way we can get a better understanding of how the Kalam filter works.</p>

<p>By looking at the cost function of the FIE problem we see that we are trying to minimise:</p>
<ol>
        <li>A penalty on the distance between the estimated initial state, $x_0$, and the expected initial state, $\bar{x}_0$, of our prior on $x_0$</li>
        <li>A penalty on the output error, $y_t - Cx_t$ (what we observe minus what we should be observing based on the estimated state)</li>
        <li>A penalty on the process noise (because we want to avoid an estimator that attributes everything to process noise)</li>
</ol>

<p>The above penalties are scaled by their corresponding variance-covariance matrices. This means that the "higher" a covariance, the "lower" the inverse covariance will be, entailing a lower penalty. For example, if we don't trust our sensors very much we will be having a "large" $R$, so a "small" $R^{-1}$, so a small penalty on $y_t - Cx_t$, thus allowing the estimator to predict states which lead to large observation errors.</p>

<p>Lastly, the Bayesian approach allows us to generalise to nonlinear systems. We can easily repeat the above procedure assuming we have nonlinear dynamics and/or a nonlinear relationship between states and outputs. This will lead to the moving horizon estimation method.</p>

## Forward dynamic programming


<p>The estimation problem becomes</p>

<p>$$\begin{aligned}
        \operatorname*{minimise}_{
        x_0,\ldots,x_{N-1}
        }\                  &
        \ell_{x_0}(x_0) + \sum_{t=0}^{N-1} \ell_t(x_t, w_t),
        \\
        \text{subject to: } & x_{t+1} = Ax_t + w_t, t\in\N_{[0, N-1]}.
\end{aligned}$$</p>
<p>We apply the DP procedure in a <em>forward</em> fashion:</p>
<p>$$\begin{aligned}
\widehat{V}_N^\star
{}={} &
\min_{\substack{x_0,\ldots,x_N \\w_0,\ldots,w_{N-1}}}
\left\{
\ell_{x_0}(x_0) + \sum_{t=0}^{N-1} \ell_t(x_t, w_t)
\left|
\begin{array}{l}
        x_{t+1} = Ax_t + w_t,
        \\
        t\in\N_{[0, N-1]}
\end{array}
\right.
\right\}
        \\
{}={} &
\min_{\substack{x_1,\ldots,x_N \\w_1,\ldots,w_{N-1}}}
\left\{
\underbrace{
        \min_{x_0, w_0}
        \left\{
        \ell_{x_0}(x_0) + \ell_0(x_0, w_0)
        {}\mid{}
        x_1 = Ax_0 + w_0
        \right\}
}_{V_1^{\star}(x_1)}
\rule{0cm}{1.1cm}\right.
                       \\&
\qquad\qquad\qquad
\left.
\rule{0cm}{1.1cm}
{}+{}
\sum_{t=1}^{N-1} \ell_t(x_t, w_t)\,
\left|
\begin{array}{l}
        x_{t+1} = Ax_t + w_t,
        \\
        t\in\N_{[1, N-1]}
\end{array}
\right.
\right\}
                       \\
{}={} &
\min_{\substack{x_1,\ldots,x_N \\w_1,\ldots,w_{N-1}}}
\left\{
V_1^{\star}(x_1)
{}+{}
\sum_{t=1}^{N-1} \ell_t(x_t, w_t)
\left|
\begin{array}{l}
        x_{t+1} = Ax_t + w_t,
        \\
        t\in\N_{[1, N-1]}
\end{array}
\right.
\right\}.
\end{aligned}$$</p>

<p>The <em>forward</em> dynamic programming procedure can be written as</p>
<p>$$\begin{aligned}
        V_0^\star(x_0) {}={}           & \ell_{x_0}(x_0),
        \\
        V_{t+1}^{\star}(x_{t+1}) {}={} & \min_{x_t, w_t}
        \left\{
        V_t^\star(x_t) + \ell_t(x_t, w_t) {}\mid{} x_{t+1} = Ax_t + w_t
        \right\},
        \\
        \widehat{V}_N^\star {}={}      & \min_{x_{N}}V_N^\star(x_N).
\end{aligned}$$</p>

<p>We shall prove that the solution of this problem yields the Kalman filter!</p>


## The Kalman Filter is a MAP estimator

To show that the <a href="#forward-dynamic-programming">forward DP</a> yields the Kalman Filter, we need two lemmata. Firstly, Woodbury's matrix inversion lemma which we state without a proof.


<!-- Lemma VII.5: Woodbury's identity -->
<div style="border-style:dashed;border-width:1.5px;padding-left:10px;" id="LemmaVII-5">
<p><strong>Lemma VII.5 (Woodbury's identity).</strong> The following holds</p>
<p>$$(S+UCV)^{-1} = S^{-1} - S^{-1}U(C^{-1} + VS^{-1}U)^{-1}VS^{-1}.$$</p>
</div>
<!-- END Lemma VII.5: Woodbury's identity -->

Secondly, we state and prove the following lemma.

<!-- Lemma VII.6: Factorisation of sum of quadratics -->
<div style="border-style:dashed;border-width:1.5px;padding-left:10px;" id="LemmaVII-6">
<p><strong>Lemma VII.6 (Factorisation of sum of quadratics).</strong> Let $Q_1\in\mathbb{S}_{++}^n$, $Q_2\in\mathbb{S}_{++}^m$, $F\in{\rm I\!R}^{m\times n}$, $b\in{\rm I\!R}^m$. Define</p>
<p>$$q(x) = \tfrac{1}{2}\|x-\bar{x}\|_{Q_1^{-1}}^{2} + \tfrac{1}{2}\|Fx-b\|_{Q_2^{-1}}^2.$$</p>
<p>Then for all $x\in{\rm I\!R}^n$,</p>
<p>$$q(x){}={}\tfrac{1}{2}\|x-x^{\star}\|_{W^{-1}}^2 + c,$$</p>
<p>where</p>
<p>$$\begin{aligned}
        x^\star {}={} & \bar{x} + Q_1F^\intercal S^{-1}(b-F\bar{x}),
        \\
        W {}={}       & Q_1 - Q_1F^\intercal S^{-1}F Q_1,
        \\
        c {}={}       & \tfrac{1}{2}\|F\bar{x}-b\|_{S^{-1}}^2,
\end{aligned}$$</p>
<p>and where $S = Q_2 + FQ_1F^\intercal.$ Moreover, </p>
<p>$$x^\star = \argmin_x q(x),$$</p>
<p>and</p>
<p>$$\min_x q(x) = c.$$</p>
</div>
<!-- END Lemma VII.6: Factorisation of sum of quadratics -->

<button onclick="toggleCollapseExpand('proofLemmaVII6', 'proofLemmaVII6Container', 'proof')" id="proofLemmaVII6Button">
  <i class="fa fa-cog fa-spin"></i> Click to see the proof
</button>
<div style="margin-top:20px"></div>

<div style="width: 100%; display: none; padding: 5px 5px;" id="proofLemmaVII6Container">
<p><em>Proof.</em> Since $q$ is a convex quadratic function, it has a minimiser, $x^\star$, which satisfies $\nabla q(x^\star) = 0$. The idea is that we can use Taylor's expansion to write $q$ as follows</p>
<p>$$\begin{aligned}
        q(x) {}={} & q(x^\star) + \nabla q(x^\star)^\intercal (x-x^\star) + \tfrac{1}{2}\|x-x^\star\|_{\nabla^2 q(x^\star)}^2
        \\
        {}={}      & q(x^\star) + \tfrac{1}{2}\|x-x^\star\|_{\nabla^2 q(x^\star)}^2,
\end{aligned}$$</p>
<p>It suffices to determine $x^\star$, $q(x^\star)$ and $\nabla^2 q(x^\star)$. Let us first determine $x^\star$. We have $\nabla q(x) {}={} Q_1^{-1}(x-\bar{x}) + F^\intercal Q_2^{-1}(Fx-b),$ and we need to solve $\nabla q(x^\star) = 0$, that is</p>
<p>$$Q_1^{-1}(x^\star-\bar{x}) + F^\intercal Q_2^{-1}(Fx^\star-b) {}={} 0,$$</p>
<p>from which</p>
<p>$$\begin{aligned}
        x^\star {}={} & (Q_1^{-1} + F^\intercal Q_2^{-1}F)^{-1}(Q_1^{-1}\bar{x} + F^\intercal Q_2^{-1}b)
        \\
        {}={}         &
        \textcolor{red}{\bar{x}}
        +
        (Q_1^{-1} + F^\intercal Q_2^{-1}F)^{-1}
        (Q_1^{-1}\bar{x} + F^\intercal Q_2^{-1}b
        {}\,{}
        \textcolor{red}{ {}-{} (Q_1^{-1} + F^\intercal Q_2^{-1}F)\bar{x}})
        \\
        {}={}         &
        \bar{x} + (Q_1^{-1} + F^\intercal Q_2^{-1}F)^{-1}F^\intercal Q_2^{-1}(b-F\bar{x})
        \end{aligned}$$</p>
<p>and now we apply Woodbury's matrix identity (<a href="#LemmaVII-5">Lemma VII.5</a>) to the term $(Q_1^{-1} + F^\intercal Q_2^{-1}F)^{-1}$</p>
<p>$$\begin{aligned}
        {}={}         &
        \bar{x} + \textcolor{blue}{(Q_1 - Q_1 F^\intercal (Q_2 + FQ_1F^\intercal)^{-1} FQ_1 )} F^\intercal Q_2^{-1}(b-F\bar{x})
        \\
        {}={}         &
        \bar{x} + Q_1 F^\intercal \left[
        I - (\underbrace{Q_2 + FQ_1F^\intercal}_{S})^{-1}\underbrace{FQ_1 F^\intercal}_{S - Q_2}
        \right]
        Q_2^{-1}(b-F\bar{x})
        \\
        {}={}         &
        \bar{x} + Q_1 F^\intercal S^{-1}(b-F\bar{x}),\end{aligned}$$</p>
<p>Next, let us determine $q(x^\star)$</p>

<p>$$\begin{aligned}
        q(x^\star)
        {}={} &
        \tfrac{1}{2}\|x^\star-\bar{x}\|_{Q_1^{-1}}^{2} + \tfrac{1}{2}\|Fx^\star-b\|_{Q_2^{-1}}^2
        \\
        {}={} &
        \tfrac{1}{2}\|Q_1 F^\intercal S^{-1} (b-F\bar{x})\|_{Q_1^{-1}}^{2}
        {}+{}
        \tfrac{1}{2}\|F\bar{x} - b + FQ_1F^\intercal S^{-1}(b-F\bar{x})\|_{Q_2^{-1}}^2\end{aligned}$$</p>

<p>$$\begin{aligned}{}={} &
        \tfrac{1}{2}\|Q_1 F^\intercal S^{-1} (b-F\bar{x})\|_{Q_1^{-1}}^{2}
        {}+{}
        \tfrac{1}{2}\| \left(I - FQ_1F^\intercal S^{-1}\right)(b-F\bar{x})\|_{Q_2^{-1}}^2
        \\
        {}={} &
        \tfrac{1}{2}\|Q_1 F^\intercal S^{-1} (b-F\bar{x})\|_{Q_1^{-1}}^{2}
        {}+{}
        \tfrac{1}{2}\| \left(I - (S-Q_2) S^{-1}\right)(b-F\bar{x})\|_{Q_2^{-1}}^2
        \\
        {}={} &
        \tfrac{1}{2}\|Q_1 F^\intercal S^{-1} (b-F\bar{x})\|_{Q_1^{-1}}^{2}
        {}+{}
        \tfrac{1}{2}\| Q_2 S^{-1}(b-F\bar{x})\|_{Q_2^{-1}}^2
        \\
        {}={} &
        \tfrac{1}{2}(b-F\bar{x})^\intercal S^{-1} FQ_1 F^\intercal S^{-1}(b-F\bar{x})
        \tfrac{1}{2}(b-F\bar{x})^\intercal S^{-1} Q_2 S^{-1} (b-F\bar{x})
        \\
        {}={} &
        \tfrac{1}{2}(b-F\bar{x})^\intercal S^{-1} (\underbrace{FQ_1 F^\intercal + Q_2}_{S}) S^{-1}(b-F\bar{x})
        \\
        {}={} &
        \tfrac{1}{2}(b-F\bar{x})^\intercal S^{-1} (b-F\bar{x}) = c.\end{aligned}$$</p>



<p>Lastly, it is easy to see that</p>
<p>$$\nabla^2 q(x) = Q_1^{-1} + F^\intercal Q_2^{-1} F = W^{-1},$$</p>
<p>where the second equality is due to <a href="#LemmaVII-5">Lemma VII.5</a>. This completes the proof. $\Box$</p>
</div>

<p>We can now state the main result of this section</p>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;" id="LemmaVII-6">
<p><strong>Theorem VII.7 (MAP Estimator = KF).</strong> Suppose that</p>
<p>$$\begin{aligned}
                    \ell_{x_0}(x_0) {}={}  & \tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^2,
                    \\
                    \ell_t(x_t, w_t) {}={} & \tfrac{1}{2}\|y_t-Cx_t\|_{R^{-1}}^2 + \tfrac{1}{2}\|w_t\|_{Q^{-1}}^2.
                \end{aligned}$$</p>
<p>Then, the <a href="#forward-dynamic-programming">forward DP</a> yields the KF equations.</p>
</div>

<br/>

<p>Indeed, the first step in the forward DP is</p>
<p>$$\begin{aligned}
V_{1}^{\star}(x_{1})
{}={} & \min_{x_0, w_0}
\left\{
V_0^\star(x_0) + \ell_0(x_0, w_0) {}\mid{} x_{1} = Ax_0 + w_0
\right\}
\\
{}={} & \min_{x_0, w_0}
\left\{
\tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^2 + \tfrac{1}{2}\|y_0-Cx_0\|_{R^{-1}}^2 + \tfrac{1}{2}\|w_0\|_{Q^{-1}}^2 {}\mid{} x_{1} = Ax_0 + w_0
\right\}
\\
{}={} & \min_{x_0}
\left\{
\tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^2 + \tfrac{1}{2}\|y_0-Cx_0\|_{R^{-1}}^2 + \tfrac{1}{2}\|x_1 - Ax_0\|_{Q^{-1}}^2
\right\}.
\end{aligned}$$</p>
<p>We can use <a href="#LemmaVII-6">Lemma VII.6</a> to write the sum of the first two terms as follows</p>
<p>$$\tfrac{1}{2}\|x_0 - \bar{x}_0\|_{P_0^{-1}}^2 + \tfrac{1}{2}\|y_0-Cx_0\|_{R^{-1}}^2
{}={}
\tfrac{1}{2}\|x_0-x_0^\star\|_{W_{0}^{-1}}^2 + \tfrac{1}{2}\|y_0 - Cx_0^\star\|_{S_0^{-1}}^2,$$</p>
<p>where</p>
<p>$$\begin{aligned}
        S_0 {}={}       & R + CP_0C^\intercal,
        \\
        W_0 {}={}       & P_0 - P_0 C^\intercal S_0^{-1} CP_0,
        \\
        x_0^\star {}={} & \bar{x}_0 + P_0C^\intercal S_0^\intercal (y_0 - C\bar{x}_0).
\end{aligned}$$</p>
<p>Note that $W_0 = \Sigma_{0\mid 0}$ and $x_0^\star = \hat{x}_{0\mid 0}$. Next, we have</p>
<p>$$V_1^\star(x_1)
{}={}
\underbrace{\tfrac{1}{2}\|y_0 - Cx_0^\star\|_{S_0^{-1}}^2}_{\text{constant}}
{}+{}
\min_{x_0}
\left\{
\tfrac{1}{2}\|x_0-x_0^\star\|_{W_{0}^{-1}}^2
{}+{}
\tfrac{1}{2}\|x_1 - Ax_0\|_{Q^{-1}}^2
\right\}.$$</p>
<p>From <a href="#LemmaVII-6">Lemma VII.6</a> we have</p>
<p>$$V_1^\star(x_1)
{}={}
\text{constant}
{}+{}
\tfrac{1}{2}\|x_1 - A\hat{x}_{0\mid 0}\|^2_{\overline{S}_{0}^{-1}},$$</p>
<p>where $\hat{x}_{1\mid 0} = A\hat{x}_{0\mid 0}$ and</p>
<p>$$\overline{S}_{0} = Q + AW_0A^\intercal = \Sigma_{1\mid 0},$$</p>
<p>(compare this the time update step of the Kalman filter).</p>
<p>Note that $V_1^\star$ has the same form as $V_1^\star$, so the same procedure can be repeated. This will yield the same iterates.</p>
