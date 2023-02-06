---
author: "Pantelis Sopasakis"
title:  "The Kalman Filter V: It's BLUE!"
date: 2023-02-04
description: "The Kalman filter is BLUE"
summary: "In this post we will show that the Kalman filter is BLUE: a best linear unbiased estimator"
math: true
series: ["Mathematix"]
tags: ["Estimation"]
collapsible: true
---

> <b>Read first:</b> <a href="../kalman-4">Kalman Filter IV: Application to position estimation</a><br>
> <b>Read next:</b> <a href="../kalman-6">Kalman Filter VI: Further examples</a><br>

## Minimum variance estimators 

<p>Firstly, we will show that the conditional expectation is a minimum variance estimator.</p>

<div id="thm:v1" style="border-style:dashed;border-width:1.5px;padding-left:10px;padding-top:15px">
<p><strong>Theorem V.1.</strong>  Suppose $X$ and $Y$ are jointly distributed continuous real-valued random variables and we measure $Y=y$. Let $\hat{x}=\hat{x}(y)$ be a minimiser of the problem. </p>
<p>$$\operatorname*{minimise}_{z}{\rm I\!E}[\|X-z\|^2 {}\mid{} Y=y],$$</p>
<p>that is, $\hat{x}$ is a <em>minimum variance estimate</em> of $X$ given $Y=y$. Then, $\hat{x}$ is unique and</p>
<p>$$\hat{x} = {\rm I\!E}[X {}\mid{} Y=y].$$</p>
</div>
<p></p>

<p>Does this theorem look too good to be true? Well... it is. We <a href="../kalman-2#thm:normal_conditioning">know</a> that if $(X, Y)$ are jointly normally distributed and we know their mean and variance, we can compute the conditional expectation of $X$ given $Y=y$. However, in practice we often encounter cases where the random variables are not normally distributed. But even when they are approximately jointly normal, we won't know their means and variances.</p>

<p>In the context of the Kalman filter, it makes sense that if the noises ($w$ and $v$) are not normally distributed, the Kalman filter will not be the best estimation methodology. The good news is that the Kalman filter remain the best linear filter in any case!</p>


<iframe alt="YouTube video: the Kalman filter is BLUE" style="margin:auto;display:block;"  width="560" height="315" src="https://www.youtube.com/embed/JJNLfZG1J-o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## KF is BLUE

<p>In this section we will drop the normality assumptions. The Kalman filter is a linear (affine) estimator.
By combining the measurement and time updates of the Kalman filter, we can see that</p>

<p>$$
    \hat{x}_{t+1{}\mid{}t}
    {}={}
    \underbrace{A_t \hat{x}_{t{}\mid{}t-1}}_{\text{system dynamics}}
    {}+{}
    K_t\underbrace{(y_t - C_t\hat{x}_{t{}\mid{}t-1})}_{\text{prediction error}},$$</p>

<p>where $K_t{}={}A_t\Sigma_{t{}\mid{}t-1}C_t^\intercal (C_t\Sigma_{t{}\mid{}t-1}C_t^\intercal + R_t)^{-1}.$ The Kalman filter is an <em>affine filter</em>. It is in fact the <em>best</em> affine filter (will explain). Recall that, by definition, $\hat{x}_{t+1{}\mid{}t} {}={} {\rm I\!E}[x_{t+1} {}\mid{} y_0,\ldots,y_t]$, therefore, the KF is <em>unbiased</em>, i.e.,</p>

<p>$${\rm I\!E}[\hat{x}_{t+1{}\mid{}t}{}-{}x_{t+1}]
    {}={}
    {\rm I\!E}[{\rm I\!E}[x_{t+1} {}\mid{} y_0, \ldots, y_t]-x_{t+1}]
    {}={}
    0.$$</p>


<p>The conditional expectation of a random variable $X$ given $Y=y$ minimises the following function</p>

<p>$$f(z; y)
    {}={}
    {\rm I\!E}\left[\|X - z\|^2 {}\mid{} Y=y\right].$$</p>

<p>This means that</p>

<p>$$f\left({{\rm I\!E}[X{}\mid{}Y=y]}; y\right)
    {}\leq{}
    f(z; y),$$</p>

<p>for all estimators $z(y)$.</p>

<p>Moreover, define the function
$F(z; y) {}={} {\rm I\!E}[(X-z)(X-z)^\intercal {}\mid{}Y=y].$ Then,</p>

<p>$$F\left({{\rm I\!E}[X{}\mid{}Y=y]}; y\right)
        {}\preccurlyeq{}
        F(z; y),$$</p>

<p><em>However</em>, ${\rm I\!E}[X{}\mid{}Y=y]$ can be difficult to determine (without the normality assumption); in general, it is a <em>nonlinear</em> function of $y$.</p>

<p><b>Question:</b> What is the best <em>linear</em> (affine) estimator we can construct?</p>


<p>Suppose that $X$ and $Y$ are jointly distributed. Then the <em>best</em> (minimum variance) estimator of $X$ given $Y=y$ is ${\rm I\!E}[X{}\mid{}Y=y]$. What is the best <em>affine</em> estimator?</p>

<p><b>Problem statement:</b> Without assuming that $X$ and $Y$ are (jointly) normally distributed,
suppose we are looking for estimators of the form $\widehat{X}(y)=A y+b$, i.e., <em>affine</em> estimators. We seek to determine $A=A^\star$ and $b=b^\star$ so that $\widehat{X}(y)=A^\star y+b^\star$ is the <em>best affine estimator</em>, i.e., the best estimator among all affine ones, i.e.,</p>

<p>$$
    {\rm I\!E}\left[\|X - A^\star y + b^\star\|^2\right]
    {}\leq{}
    {\rm I\!E}\left[\|X - Ay + b\|^2\right],$$</p>

<p>for any $A$ and $b$, and its conditional counterpart</p>

<p>$${\rm I\!E}\left[\|X - \left(A^\star y + b^\star\right)\|^2 {}\mid{} Y {}={} y\right]
    {}\leq{}
    {\rm I\!E}\left[\|X - \left(A y + b\right)\|^2 {}\mid{} Y {}={} y\right],$$</p>

<p>also holds for any $A$ and $b$.</p>

<div id="thm:kf-is-blue" style="border-style:dashed;border-width:1.5px;padding-left:10px;padding-top:15px;padding-right:3px">
<p><strong>Theorem V.2 (KF is BLUE).</strong>
        Suppose that $(X, Y)$ are jointly distributed with means ${\rm I\!E}[X]=m_x$,
        ${\rm I\!E}[Y]=m_y$ and covariance matrix</p>
        <p>$${\rm Var}\begin{bmatrix}X\\Y\end{bmatrix}
            {}={}
            \begin{bmatrix}
                \Sigma_{xx} & \Sigma_{xy}
                \\
                \Sigma_{yx} & \Sigma_{yy}
            \end{bmatrix},$$</p>
        <p>with $\Sigma_{yy} {}\succ{} 0$. The best affine estimator of $X$ given $Y$ is $\widehat{X}(Y) = A^\star Y + b^\star$ with</p>
        <p>$${A^\star {}={} \Sigma_{xy}\Sigma_{yy}^{-1}},
            \text{ and }
            {b^\star = m_x - A^\star m_y}.$$</p>
        <p>In particular, ${\rm I\!E}\left[\|X-\widehat{X}(Y)\|^2\right] {}\leq{} {\rm I\!E}\left[\|X-(AY+b)\|^2\right],$ for any parameters $A$ and $b$.</p>
</div>

<p></p>

<p><b>Remarks:</b> The estimator can be written as $\widehat{X}(Y) = m_x + A^\star(Y-m_y)$. The Kalman filter is the best affine filter in the sense that it minimises the <em>mean square error</em>, ${\rm I\!E}[\|X-\widehat{X}\|^2].$ Theorem <a href="#thm:kf-is-blue">2</a> does not require that $X$ or $Y$ be Gaussian.
We can prove a similar result for the covariance matrix ${\rm I\!E}[(X-\widehat{X})(X-\widehat{X})^\intercal]$ (guess what...). Later we will show that KF is the <em>best affine</em> filter.</p>


<p><em>Before the Proof.</em> We will use the following observations: for an $n$-dimensional random variable $Z$:</p>
<p>$${\rm I\!E}[\|Z\|^2]
    {}={}
    {\rm I\!E}[Z^\intercal Z]
    {}={}
    {\rm I\!E}[{\rm trace}(ZZ^\intercal)]
    {}={}  {\rm trace} {\rm I\!E}[ZZ^\intercal].$$</p>

<p>Secondly, \({\rm Var}[Z] = {\rm I\!E}[ZZ^\top] - {\rm I\!E}[Z]{\rm I\!E}[Z]^\intercal\), so ${\rm I\!E}[ZZ^\top] = {\rm Var}[Z] + {\rm I\!E}[Z]{\rm I\!E}[Z]^\intercal,$
therefore,</p>

<p>$${\rm I\!E}[\|Z\|^2]
    {}={}
    {\rm trace} {\rm I\!E}[ZZ^\top]
    {}={}  {\rm trace} {\rm Var}[Z] + {\rm trace} \left({\rm I\!E}[Z]{\rm I\!E}[Z]^\intercal\right).$$</p>

<p>Note also that ${\rm I\!E}[X-AY-b] = m_x - Am_y - b.$</p>

<p><em>Proof.</em> It is</p>

<p>$$\begin{aligned}
        {\rm I\!E}[\|X-AY-b\|^2]
         & \quad {}={}
        {\rm trace} {\rm Var} [X-AY-b] + {\rm trace}({\rm I\!E}[X-AY-b]({}\cdot{})^\intercal)
           \\
         & \quad {}={}
        {\rm trace} {\rm Var} [X-AY-b] + \|m_x - Am_y - b\|^2,
    \end{aligned}$$</p>
<p>where</p>

<p>$$\begin{aligned}
        {\rm Var}(X-AY-b)
        {}={} &
        {\rm I\!E}[(X-m_x-A(Y-m_y))({}\cdot{})^\intercal]
                      \\
        {}={} &
        {\rm I\!E}[(X-m_x)(X-m_x)^\intercal]
        {}+{}
        {\rm I\!E}[A(Y-m_y)(Y-m_y)^\intercal{}A^\intercal]
                       \\
              & \qquad {}-{}
        A(Y-m_y){\rm I\!E}[X-m_x]^\intercal
        {}-{}
        {\rm I\!E}[X-m_x](Y-m_y)^\intercal A^\intercal
                      \\
        {}={} &
        \Sigma_{xx} + A\Sigma_{yy}A^\intercal - A\Sigma_{yx} - \Sigma_{xy}A^\intercal,
    \end{aligned}$$</p>
<p>therefore,</p>
<p>$${\rm I\!E}[\|X-AY-b\|^2]
        {}={}
        {\rm trace}
        \left[
        \Sigma_{xx}
        {}+{}
        A\Sigma_{yy}A^\intercal - A\Sigma_{yx} - \Sigma_{xy}A^\intercal
        \right]
        {}+{}
        \|m_x-Am_y-b\|^2.$$</p>
<p>Now observe that</p>
<p>$$(A-\Sigma_{xy}\Sigma_{yy}^{-1}) \Sigma_{yy} (A-\Sigma_{xy}\Sigma_{yy}^{-1})^\intercal
        {}={}
        {
        A\Sigma_{yy}A^\intercal
        -\Sigma_{xy}A^\intercal
        -A\Sigma_{yx}
        }
        {}+{} \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}.$$</p>
<p>The mean square error can be written as</p>
<p>$$\begin{aligned}
        {\rm I\!E}[\|X-AY-b\|^2]
        {}={}&
        \underbrace{
            {\rm trace}[\Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}]
        }_{\text{independent of } A \text{ and } b}
        \\
        &\quad{}+{}
        {\rm trace}[(A-\Sigma_{xy}\Sigma_{yy}^{-1}) \Sigma_{yy} (A-\Sigma_{xy}\Sigma_{yy}^{-1})^\intercal]
        \\
        &\qquad{}+{}
        \|m_x - Am_y - b\|^2.\end{aligned}$$</p>

<p>All terms are nonnegative. The term $\Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}$ is the Schur complement of $\Sigma$, so it is positive semidefinite. The first term is independent of $A$ and $b$. The second term can be made $0$ by taking $A = \Sigma_{xy}\Sigma_{yy}^{-1}$ and the third term vanishes if we take $b = m_x - Am_y$. $\Box$</p>


## Exercises

<p><b>Exercise V.1.</b> Suppose that $(X, Y)$ are jointly distributed with means ${\rm I\!E}[X]=m_x$,
${\rm I\!E}[Y]=m_y$ and covariance matrix</p>
<p>$${\rm Var}\begin{bmatrix}X\\Y\end{bmatrix}
    {}={}
    \begin{bmatrix}
        \Sigma_{xx} & \Sigma_{xy}
        \\
        \Sigma_{yx} & \Sigma_{yy}
    \end{bmatrix},$$</p>
<p>with $\Sigma_{yy} {}\succ{} 0$. Show that the best affine estimator of $X$ given $Y$ is $\widehat{X}(Y) = A^\star Y + b^\star$ with</p>
<p>$${A^\star {}={} \Sigma_{xy}\Sigma_{yy}^{-1}},
    \text{ and }
    {b^\star = m_x - A^\star m_y},$$</p>
<p>in the sense that</p>
<p>$${\rm I\!E}\left[(X-\widehat{X}(y))(X-\widehat{X}(y))^\intercal\right]
    {}\preccurlyeq{}
    {\rm I\!E}\left[(X-Ay-b)(X-Ay-b)^\intercal\right],$$</p>
<p>for any parameters $A$ and $b$.</p>

<p><em>Hint:</em> follow the steps of the proof of the theorem we just stated, omitting the trace.</p>

<p><b>Exercise V.2 (Estimator bias and variance).</b>  Show that the best linear estimator, $\widehat{X}(Y)= A^\star{}Y + b^\star$, with</p>
<p>$$\begin{aligned}
    A^\star {}={} & \Sigma_{xy}\Sigma_{yy}^{-1}, \\
    b^\star {}={} & m_x - A^\star m_y.
\end{aligned}$$</p>
<p>is <em>unbiased</em>, i.e., ${\rm I\!E}[X-\widehat{X}(Y)]=0$ and its variance (the variance of the estimator error, $X-\widehat{X}(Y)$) is</p>
<p>$${\rm Var}[X-\widehat{X}(Y)]
    {}={}
    \Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}.$$</p>


## Recovering the Kalman Filter

<p><b>Assumptions:</b> $x_0$, $(w_t)_t$ and $(v_t)_t$ are mutually independent random variables
(not necessarily Gaussian) with ${\rm I\!E}[w_t]=0$, ${\rm I\!E}[v_t]=0$, ${\rm I\!E}[x_0] = \tilde{x}_0$, and ${\rm Var}[w_t] = Q_t$, ${\rm Var}[v_t] = R_t$, ${\rm Var}[x_0] = P_0$. Then \((x_0, y_0)\) is jointly distributed with mean</p>
<p>$${\rm I\!E}
    \begin{bmatrix}
        x_0 \\ y_0
    \end{bmatrix}
    {}={}
    \begin{bmatrix}
        {\tilde{x}_0}
        \\
        {C_0\tilde{x}_0}
    \end{bmatrix},$$</p>
<p>and variance-covariance matrix</p>
<p>$${\rm Var}
    \begin{bmatrix}
        x_0 \\ y_0
    \end{bmatrix}
    {}={}
    \begin{bmatrix}
        {P_0}    & {P_0C_0^\intercal}
        \\
        {C_0P_0} & {C_0P_0C_0^\intercal + R_0}
    \end{bmatrix}.$$</p>
<p>By Theorems <a href="#thm:v1">V.1</a> and <a href="#thm:kf-is-blue">V.2</a>, the best affine estimator of $x_0$ given $y_0$ is</p>
<p>$$\hat{x}_{0}(y_0)
    {}={}
    {\tilde{x}_0}
    {}+{}
    {P_0C_0^\intercal}
    ({C_0P_0C_0^\intercal + R_0})^{-1}
    (y_0 - {C_0\tilde{x}_0}).$$</p>
<p>and the error covariance is</p>
<p>$${\rm Var}[x_0 - \hat{x}_{0}(y_0)]
    {}={}
    P_0
    {}-{}
    {P_0C_0^\intercal}
    ({C_0P_0C_0^\intercal + R_0})^{-1}
        {C_0P_0}.$$</p>
<p>These are the same formulas as in the Kalman filter!</p>

<p>We can easily show recursively that the Kalman filter is the <b>Best</b> (minimum variance, minimal covariance matrix) <b>Linear</b> (actually affine) <b>Unbiased Estimator</b> (BLUE).
"Best linear" means that it is the best among all linear estimators - however, <b>there may be some nonlinear estimator that leads to a lower variance</b>. Without the normality assumption, the Kalman filter is not a minimum variance estimator.</p>

> <b>Read next:</b> <a href="../kalman-6">Kalman Filter VI: Further examples</a><br>