---
author: "Pantelis Sopasakis"
title:  "The Kalman Filter VIII: QR-based square root form"
date: 2023-02-13
description: "Square root form of the Kalman filter using QR decompositions"
summary: "Square root form of the Kalman filter"
math: true
series: ["Mathematix"]
tags: ["Estimation", "Kalman filter"]
collapsible: true
---

> <b>Previous post:</b> <a href="../kalman-7">Kalman Filter VII: Recursive maximum a posteriori</a><br>
> <b>Read next:</b> <a href="../kalman-9">The Kalman Filter IX: Information filter</a> (coming soon; expected: end of February)<br>

## About

<p>The big issue with the Kalman filter is that it involves the inverse of a matrix. When we update the covariance matrix, numerical issues may lead to covariances which are not positive semidefinite. Moreover, the condition number of the covariance can be very high. As a result the Kalman filter, in its <a href="../kalman-3">standard form</a> is not suitable for embedded applications with fixed-point arithmetic <a href="#ref::anderson">[1]</a>.</p>

<p>In this post we will present the square-root form of the Kalman filter by Tracy <a href="#ref::tracy">[2]</a> that uses only QR factorisations and we will give code snippets in Python.</p>

## Matrix factorisations

### Cholesky factorisation

<p>The Cholesky factorisation of a symmetric positive definite matrix can be thought of as a <em>square root</em> of the matrix. Every symmetric positive definite matrix, $M$, can be written as</p>
<p>$$M=U^\intercal U,\tag{1}$$</p>
<p>where $U$ is an upper diagonal matrix with positive diagonal entries. We introduce the notation $U = {\sf chol}(M)$.</p>


### QR factorisation

<p>Any $M\in{\rm I\!R}^{n\times n}$ can be written as</p>
<p>$$M = QR\tag{2}$$</p>
<p>where $Q$ is an orthogonal matrix - therefore, $QQ^\intercal=Q^\intercal{}Q=I$ - and $R$ is upper triangular. For convenience, let us define the operator ${\sf qr}$ that maps $M$ to such a pair $(Q, R)$. We write</p>
<p>$$(Q, R) = {\sf qr}(M).\tag{3}$$</p>

<p>The individual matrices $Q$ and $R$ will be denoted by ${\sf qr}_Q(M)$ and ${\sf qr}_R(M)$. We will not go into details regarding the <a href="https://www.math.purdue.edu/~kkloste/cs515fa14/qr-uniqueness.pdf" target="_blank">uniqueness</a> of the QR factorisation in this post.</p>


### Cholesky of sum of matrices

<p>The following lemma allows us to determine the Cholesky of the sum of two symmetric positive definite matrix matrices, $A+B$, from Cholesky factors or $A$ and $B$. We will see that this can be done at the cost of a QR factorisation.</p>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;padding-right:8px" id="LemmaVIII1">
<p><strong>Lemma VIII.1 (Cholesky of sum).</strong> It is </p>
<p>$${\sf chol}(A+B) = {\sf qr}_R\left(\begin{bmatrix}{\sf chol}(A) \\ {\sf chol}(B)\end{bmatrix}\right)^{\intercal}.\tag{4}$$</p>
</div>



<div style="width: 100%; padding: 5px 5px;" id="proofLemmaVIII1Container">
<p><em>Proof.</em> Let $U_A = {\sf chol}(A)$ and $U_B = {\sf chol}(B)$. Then</p>
</div>
<p>$$A + B = U_A^\intercal U_A + U_B^\intercal U_B = [U_A^\intercal ~~~ U_B^\intercal]
\begin{bmatrix}U_A \\ U_B\end{bmatrix}.\tag{5}$$</p>
<p>Then we perform the following QR factorisation</p>
<p>$$\begin{bmatrix}U_A \\ U_B\end{bmatrix} = QR,\tag{6}$$</p>
<p>so</p>
<p>$$A + B = [U_A^\intercal ~~~ U_B^\intercal]\begin{bmatrix}U_A \\ U_B\end{bmatrix} = R^\intercal Q^\intercal Q R = R^\intercal R,\tag{7}$$</p>
<p>therefore, $R^\intercal$ is the (upper triangular) Cholesky factor of $A+B$. $\Box$</p>

<p>We can write the result of <a href="#Lemma VIII.1">Lemma VIII.1</a> as follows</p>

<div style="border-style:dashed;border-width:1.5px;padding-left:10px;padding-right:8px" id="LemmaVIII1">
<p>Let $U$ and $V$ be upper triangular matrices. Then,</p>
<p>$$U^\intercal U + V^\intercal V = W^\intercal W,\tag{8a}$$</p>
<p>where</p>
<p>$$W = {\sf qr}_R\left(\begin{bmatrix}U \\ V\end{bmatrix}\right)^{\intercal}.\tag{8b}$$</p>
</div>
<br/>

<p>Here is an example of applying <a href="#LemmaVIII1">Lemma VIII.1</a> in Python.</p>

```python
import numpy as np

n = 3

def random_symm_posdef(n):
    W = np.random.rand(n, n)
    return W.T @ W + np.eye(n)

A = random_symm_posdef(n)
B = random_symm_posdef(n)

uA = np.linalg.cholesky(A).T
uB = np.linalg.cholesky(B).T

uAB = np.vstack((uA, uB))

_, r = np.linalg.qr(uAB)

error = r.T @ r - (A+B)
assert np.linalg.norm(error, np.inf) < 1e-12
```

### Solving linear systems 

<p>Both the Cholesky and the QR factorisations can be used to solve linear systems. For example, using the Cholesky factorisation of a symmetric positive definite matrix $A\in{\rm I\!R}^{n\times n}$, that is, $A = UU^\intercal$ we can solve the linear system</p>
<p>$$Ax = b \Leftrightarrow x = A^{-1}b = (UU^{\intercal})^{-1}b = U^{-\intercal}U^{-1}b.\tag{9}$$</p>
<p>Equivalently, the linear system $Ax = b$ is equivalent to solving</p>
<p>$$\begin{aligned}Uz =& b,\\U^\intercal x =& z.\end{aligned}$$</p>
<p>Since $U$ is triangular, the above two systems can be solved easily.</p>
<p>Likewise, for the QR factorisation, $A=QR$, we have</p>
<p>$$\begin{aligned}Ax = b 
\Leftrightarrow& (QR)^{-1}x = b
\\
\Leftrightarrow& R^{-1}Q^{-1}x = b
\\
\Leftrightarrow& R^{-1}Q^{\intercal}x = b,\end{aligned}$$</p>
<p>which can be solved easily.</p>
<p>Let us give an example in Python using <a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.linalg.solve_triangular.html" target="_blank"><code>scipy.linalg.solve_triangular</code></a>.</p>

```python
import numpy as np
import scipy.linalg as spla

A = np.array([[3, -1, 1],
              [5, 4, 2],
              [1, 2, -10]])
Q, R = np.linalg.qr(A)
b = np.array([[1, 2, 3]]).T
x = spla.solve_triangular(R, Q.T@b)
assert np.linalg.norm(A@x-b, np.inf) < 1e-12
```


## Square root form of the Kalman filter

<p>Tracy in <a href="#ref::tracy">[2]</a> presents a square-root Kalman filter that uses only QR decompositions. The idea is to formulate the measurement and time update steps of the Kalman filter in such a way that we update the Cholesky factorisation of the covariances. Hereafter we will assume that the system matrices, $A, G, Q,$ and $R$ are time-invariant.</p>

### Initialisation 

<p>We initialise the Kalman filter by setting $\hat{x}_{0\mid -1} = \tilde{x}_0$ and $\Sigma_{0\mid -1} = P_0$ as we did <a href="../kalman-3#eq:kf-updates">earlier</a>. Next we perform a Cholesky factorisation of $\Sigma_{0\mid -1}$. We define</p>
<p>$$F_{0\mid -1} {}={} {\sf chol}(\Sigma_{0\mid -1}).\tag{10}$$</p>
<p>We have that $\Sigma_{0\mid -1} = F_{0\mid -1}^{\intercal} F_{0\mid -1}$.</p>
<p>Moreover, we determine the Cholesky factorisations of $Q$ and $R$; we define</p>
<p>$$\begin{aligned}\Theta_Q ={}& {\sf chol}(Q),
\\
\Theta_R ={}& {\sf chol}(R).\end{aligned}$$</p>

### Measurement update

#### Measurement update of the state

<p>Recall that the measurement update equation for the state is</p>
<p>$$\hat{x}_{t{}\mid{}t}
      {}={}
      \hat{x}_{t{}\mid{}t-1}
      {}+{}
      {\color{blue}\Sigma_{t{}\mid{}t-1}C^\intercal
      (C\Sigma_{t{}\mid{}t-1}C^\intercal + R)^{-1}}(y_t - C\hat{x}_{t{}\mid{}t-1}).\tag{11}$$</p>
<p>The quantity of interest is the matrix in blue. Let us define</p>
<p>$$L_t = \Sigma_{t{}\mid{}t-1}C^\intercal
      (C\Sigma_{t{}\mid{}t-1}C^\intercal + R)^{-1}.\tag{12}$$</p>
<p>We have</p>
<p id="eq:13">$$
L_t {}={} F_{t{}\mid{}t-1}^{\intercal}  F_{t{}\mid{}t-1} C^\intercal
      (C F_{t{}\mid{}t-1}^{\intercal}  F_{t{}\mid{}t-1}  C^\intercal + \Theta_R^\intercal \Theta_R)^{-1}
\tag{13}$$</p>
<p>We can now invoke <a href="#LemmaVIII1">Lemma VIII.1</a> to factorise $C F_{t{}\mid{}t-1}^{\intercal}  F_{t{}\mid{}t-1}  C^\intercal + \Theta_R^\intercal \Theta_R$. It is</p>
<p>$$
C F_{t{}\mid{}t-1}^{\intercal}  F_{t{}\mid{}t-1}  C^\intercal + \Theta_R^\intercal \Theta_R = \Gamma_t^\intercal \Gamma_t,\tag{14}$$</p>
<p>where $\Gamma_t$ is the upper triangular matrix</p>
<p>$$\Gamma_t = {\sf qr}_R\left( 
    \begin{bmatrix}F_{t{}\mid{}t-1}  C^\intercal \\ \Theta_R\end{bmatrix}
    \right)^{\intercal}\tag{15}$$</p>
<p>So from Equation <a href="#3">(13)</a>, </p>
<p>$$L_t =  F_{t{}\mid{}t-1}^{\intercal}  F_{t{}\mid{}t-1} C^\intercal \Gamma_t^{-1} \Gamma_t^{-\intercal}.\tag{16}$$</p>
<p>Note that</p>
<p>$$L_t = (\Gamma_t^{-1}\Gamma_t^{-\intercal}CF_{t\mid t-1}^\intercal F_{t\mid t-1})^\intercal,\tag{17}$$</p>
<p>and the multiplication by $\Gamma_t^{-1}$ and $\Gamma_t^{-\intercal}$ amounts to solving a linear system with a triangular matrix, which can be done easily.</p>


#### Measurement update of the covariance

<p>Here we will use the <a href="../kalman-3#PropIII1">Joseph form</a> of the measurement update, that is</p>
<p>$$\begin{aligned}
\Sigma_{t\mid t} 
{}={}&
(I-L_tC)\Sigma_{t\mid t-1}(I-L_tC)^\intercal + L_t R L_t^\intercal
\\
{}={}&
(I-L_tC)\Sigma_{t\mid t-1}(I-L_tC)^\intercal + L_t \Theta_R^\intercal \Theta_R L_t^\intercal,
\end{aligned}\tag{18}$$</p>
<p>so from <a href="#LemmaVIII1">Lemma VIII.1</a>,</p>
<p>$$F_{t\mid t} {}={} {\sf qr}_R\left(
    \begin{bmatrix}F_{t\mid t-1}(I-L_tC) \\ \Theta_R L_t^\intercal\end{bmatrix}
    \right)^{\intercal}.\tag{19}$$</p>



### Time update
<p>The time update step of the state estimate, $\hat{x}_{t+1\mid t}$ remains the same, that is,</p>
<p>$$\hat{x}_{t+1\mid t} = A\hat{x}_{t\mid t}.\tag{20}$$</p>
<p>For the time update step of the covariance we have</p>
<p>$$\begin{aligned}
      \Sigma_{t+1{}\mid{}t}
      {}={}&
      A \Sigma_{t{}\mid{}t} A^\intercal + GQG^\intercal
      \\
      {}={}& A F_{t{}\mid{}t}^{\intercal} F_{t{}\mid{}t} A^\intercal + G\Theta_Q^{\intercal} \Theta_Q G^\intercal.
      \end{aligned}\tag{21}$$</p>
<p>From <a href="#LemmaVIII1">Lemma VIII.1</a>,</p>
<p>$$F_{t+1\mid t} {}={} {\sf qr}_R\left(
    \begin{bmatrix}
    F_{t\mid t} A^{\intercal}
    \\
    \Theta_{Q}G^{\intercal}
    \end{bmatrix}
    \right)^{\intercal}.\tag{22}$$</p>


### Putting it all together 

<p>... so we end up with the following update equations</p>

<p id="eq:kf-updates">$$\begin{aligned}
\text{Initial conditions} &
    \left[
    \begin{array}{l}
      \hat{x}_{0{}\mid{}-1}
      {}={}
      \tilde{x}_0
      \\
      F_{0{}\mid{}-1}
      {}={}
      {\sf chol}(P_0)
      \\
      \Theta_{Q}
      {}={}
      {\sf chol}(Q)
      \\
      \Theta_{R}
      {}={}
      {\sf chol}(R)
    \end{array}
    \right.
    \\
    \text{Measurement} &
      \left[
      \begin{array}{l}
      \Gamma_t = {\sf qr}_R\left( 
      \begin{bmatrix}F_{t{}\mid{}t-1}  C^\intercal \\ \Theta_R\end{bmatrix}
      \right)^{\intercal}
      \\
      e_t = y_t - C_t\hat{x}_{t{}\mid{}t-1}
      \\
      L_t = (\Gamma_t^{-1}\Gamma_t^{-\intercal}CF_{t\mid t-1}^\intercal F_{t\mid t-1})^\intercal
      \\
      \hat{x}_{t{}\mid{}t}
      {}={}
      \hat{x}_{t{}\mid{}t-1}
      {}+{}
      L_t e_t
      \\
      F_{t\mid t} 
      {}={}
      {\sf qr}_R\left(
    \begin{bmatrix}F_{t\mid t-1}(I-L_tC) \\ \Theta_R L_t^\intercal\end{bmatrix}
    \right)
    \end{array}
    \right.
    \\
    \text{Time update}        &
    \left[
    \begin{array}{l}
      \hat{x}_{t+1{}\mid{}t}
      {}={}
      A_t \hat{x}_{t{}\mid{}t}
      \\
      F_{t+1{}\mid{}t}
      {}={}
      {\sf qr}_R \left(
        \begin{bmatrix}
        F_{t\mid t}A^{\intercal} \\ \Theta_Q G^{\intercal}
        \end{bmatrix}
        \right)^{\intercal}
    \end{array}
    \right.
  \end{aligned}$$</p>

<p>We see that the measurement and time update steps involve three QR factorisations.</p>



## Example in Python 
<p>Here is a simple implementation of the above QR-based square root Kalman filter in Python</p>

```python
import numpy as np
import scipy.linalg as spla


class SquareRootKalmanFilter:

    def __init__(self, Q, R, A, C, G, x0, P0):
        # Initial covariances
        self.F_measurement_chol = None
        self.F_predicted_chol = np.linalg.cholesky(P0).T
        # System matrices
        self.A = A
        self.C = C
        self.G = G
        # Initialisation
        self.state_measurement = None
        self.state_predicted = x0
        self.theta_Q = np.linalg.cholesky(Q).T
        self.theta_R = np.linalg.cholesky(R).T

    @staticmethod
    def qrr(a, b):
        _, r = np.linalg.qr(np.vstack((a, b)))
        return r

    def time_update(self):
        self.state_predicted = self.A @ self.state_measurement
        self.F_predicted_chol = SquareRootKalmanFilter.qrr(
            self.F_measurement_chol @ self.A.T,
            self.theta_Q @ self.G.T)

    def measurement_update(self, y):
        nx = self.A.shape[0]

        # Compute Gamma_t
        gamma = SquareRootKalmanFilter.qrr(
            self.F_predicted_chol @ C.T,
            self.theta_R)

        # Compute the Kalman gain
        sigma_pred = self.F_predicted_chol.T @ self.F_predicted_chol
        c_sigma_pred = self.C @ sigma_pred
        l_temp = spla.solve_triangular(gamma, c_sigma_pred, lower=False, trans=1)
        kalman_gain = spla.solve_triangular(gamma, l_temp, lower=False).T

        # Compute the output error
        err = y - self.C @ self.state_predicted

        # State update
        self.state_measurement = self.state_predicted + kalman_gain @ err

        # Covariance update
        self.F_measurement_chol = SquareRootKalmanFilter.qrr(
            self.F_predicted_chol @ (np.eye(nx) - kalman_gain @ self.C).T,
            self.theta_R @ kalman_gain.T)
```


## References

<p><span id="ref::anderson">[1]</span> B.D.O. Anderson and J.B. Moore, Optimal Filtering, Dover Publications, 2005</p>

<p><span id="ref::tracy">[2]</span> K. Tracy, A square-root Kalman filter using only QR decompositions, arXiv: <a href="https://arxiv.org/abs/2208.06452" target="_blank">2208.06452</a>, 2022</p>

<br/><br/>

> <b>Previous post:</b> <a href="../kalman-7">Kalman Filter VII: Recursive maximum a posteriori</a><br>
> <b>Read next:</b> <a href="../kalman-9">The Kalman Filter IX: Information filter</a> (coming soon)<br>