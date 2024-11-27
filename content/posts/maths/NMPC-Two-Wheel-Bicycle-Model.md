---
author: "NVS Chandra Mouli G"
title:  "Nonlinear Model Predictive Control (NMPC) for autonomous navigation of small scale cars"
date: 2024-11-24
description: "NMPC for autonomous navigation"
summary: "Discussion of design and simulation results of NMPC controlled small scale car."
math: true
series: ["Mathematix"]
tags: ["Nonlinear Control", "NMPC"]
collapsible: true
---
## Introduction
I have recently read a paper named "A Nonlinear Model Predictive Control Strategy for Autonomous Racing of Scale Vehicles" by Vittorio Cataffo et al., [1]. After reading the paper, I have decided to implement the proposed system in Python3 using OpEn. To study it further, I will be modifying the method to prioritize *road safe* features over minimum lap time. The purpose of this article is to showcase the formulation and simulation results of an NMPC controlled vehicle system that is *road safe* (at least in simulations). As a part of experimentation, I will be modifying the approach as the need arises and I will be updating this article by adding new sections accordingly.

### Write about OpEn, and other python3 requirements**

## Notation
| Symbol         | Expansion          | Comment                     |
|--------        |-----------         |---------                    |
$0_{n \times m}$ | $[0]_{n \times m}$ | An $n \times m$ null matrix.|

## Section 1: Initial Formulation
This section showcases the simulation results of an NMPC controlled vehicle based on bicycle model dynamics used in [1]. The results in this section are limited to the implementation of vehicle dynamics and formulating an NMPC to drive it to a reference position on the global xy-coordinate space and does not include autonomous navigation on a track and obstacle avoidance. 

The two-wheel Bicycle model in [1] is as follows:

<p>
$$
\begin{aligned}
&\dot{p}_x = v_x \cos{\psi} - v_y \cos{\psi}, \\
&\dot{p}_y = v_x \sin{\psi} + v_y \cos{\psi}, \\
&\dot{\psi} = \omega, \\
&m \dot{v}_x = F_{r, x} - F_{f, y} \sin{\delta} - F_{f, x} \cos{\delta} + m v_y \omega, \\
&m \dot{v}_y = F_{r, y} + F_{f, y} \cos{\delta} + F_{f, x} \sin{\delta} - m v_x \omega, \\
&J_z \dot{\omega} = l_f F_{f, y} \cos{\delta} + l_f F_{f, x} \sin{\delta} - l_r F_{r, y}.
\end{aligned}
$$
</p>

with

<p>
$$
\begin{aligned}
&\alpha_f = - \arctan\left(\frac{\omega l_f + v_y}{v_x}\right) + \delta, \\
&\alpha_r = \arctan\left(\frac{\omega l_r - v_y}{v_x}\right), \\
&F_{f, y} = D_f \sin(C_f \arctan(B_f \alpha_f)), \\
&F_{r, y} = D_r \sin(C_r \arctan(B_r \alpha_r)), \\
&F_{f, x} = F_{r, x} = F_x, \\
&F_x = (C_{m1} - C_{m2} v_x)\tilde{d} - C_{m3} - C_{m4} v^2_x.
\end{aligned}
$$
</p>

where
$F_{r, x},\ F_{r, y},\ F_{f, x},\text{ and } F_{f, y} \in \R$ are the forces acting on the tires with $r$ and $f$ indicating rear and front tires respectively, and $x$ and $y$ indicating longitudinal and lateral component of forces in the local vehicle body xy-frame respectively. The constants $l_f,\text{ and }  l_r \in \R$ are the distances from the Centre of Gravity $(C_g)$ to front and rear wheels respectively. The control inputs $\tilde{d},\text{ and }  \delta \in \R$ are the normalised forward acceleration PWM duty-cycle control input and front wheel steering angle input in radians respectively. The states $p_x,\ p_y,\text{ and }  \psi \in \R$ are the vehicle's x position in meters, the y position in meters, and the heading in radians in the global frame of reference respectively. The states $v_x,\ v_y,\text{ and }  \omega \in \R$ are the vehicle's x velocity in meters-per-second, the y velocity in meters-per-second, and the angular rotation rate around the z-axis in radians-per-second in the local body-fixed frame of reference respectively. These equations and their parameters are described in equations (1) through (4) in [1]. Now the dynamics can be written as,

<p>
$$
\begin{aligned}
&\dot{\mathbf{z}}(t) = \mathbf{g}(\mathbf{z}(t),\ \mathbf{u}(t)), \\
\text{with}\\
&\mathbf{z}(t) = [p_x(t),\ p_y(t),\ \psi(t),\ v_x(t),\ v_y(t),\ \omega(t)]^\mathsf{T} \text{ as the state vector}, \\
&\mathbf{u}(t) = [\tilde{d}(t),\ \delta(t)]^\mathsf{T} \text{ as the input vector}, \\
&\mathbf{g} : \R^{n_x} \times \R^{n_u} \rightarrow \R^{n_x}.
\end{aligned}
$$
</p>

Using forward Euler method, the discretised system for some small sampling time $T \in \R_{>0}$ can be written as,

<p>
$$
\mathbf{z}(k + 1) = \mathbf{z}(k) + T \cdot \mathbf{g}(\mathbf{z}(k), \mathbf{u}(k)), \ k \in \Z^+.
$$
</p>

Throughout this article, the vehicle parameters are taken as described in Table 1 in [1]. They are given (estimated) as,

| Param    | Value            | Param    | Value              | Param    | value                             |
| -------- | ---------------- | -------- | ------------------ | -------- | --------------------------------- |
| $l_f$    | $0.178$ m        | $l_r$    | $0.147$ m          | $m$      | $5.6292$ kg                       |
| $J_z$    | $0.204$ kg m$^2$ | $B_f$    | $9.242$            | $B_r$    | $17.716$                          |
| $C_f$    | $0.085$          | $C_r$    | $0.133$            | $D_f$    | $134.585$ N                       |
| $D_r$    | $159.919$ N      | $C_{m1}$ | $20$ N             | $C_{m2}$ | $6.92 \times 10^{-7}$ kg s$^{-1}$ |
| $C_{m3}$ | $3.99$ N         | $C_{m4}$ | $0.67$ kg m$^{-1}$ | $M$      | $1674$                            |

The goal is to formulate an NMPC that minimises the distance between the desired final position $\mathbf{p}_d = [p_x^d,\ p_y^d]^\mathsf{T}$ and the position of the vehicle $\mathbf{p}_N = [p_x^N,\ p_y^N]^\mathsf{T}$ after $N$ (prediction horizon) time steps. This can also be interpreted as asking the MPC controller to take the system as close as possible to the desired final position with in a given time of $N \cdot T$ seconds. Whilst doing so, the controller shall ensure the system obeys the state and input (safety) constraints, given as

<p>
$$
\begin{aligned}
&v_x \in \bm{\gamma} = [0,\ 5], \\
&\begin{bmatrix} \ \tilde{d} \ \\ \ \delta \ \end{bmatrix}  \in \bm{\mu} = [0,\ 1] \times \left[-\frac{\pi}{6},\ \frac{\pi}{6}\right]. \\
%&\delta \in \left[-\frac{\pi}{6},\ \frac{\pi}{6}\right].
\end{aligned}
$$
</p>

It should also be of priority that the system is not subjected to violently arbitrary accelerations and steering angles. This can be formulated as aiming for a minimum *jerk* trajectory and can be modeled as minimising the distance between successive input vectors. With this, the NMPC formulation takes the following form,

<p>
$$
\begin{aligned}
\mathbb{P}^i_N(\mathbf{z}^i(0)) :\ &\underset{\mathbf{u}^i}{\text{minimise}}\ \|\mathbf{p}^i_N - \mathbf{p}^i_d\|_{\mathbf{Q}_{1}}^2 + \sum_{k=0}^{N-1} \|\mathbf{u}^i(k) - \mathbf{u}^i(k-1)\|_{\mathbf{Q}_2}^2 \\
\text{s.t.}\ & \mathbf{z}^i(0) = \mathbf{z}^{i-1}(N), \\
\ &\mathbf{u}^i(-1) = \mathbf{u}^{i-1}(N-1), \\
\ &\mathbf{z}^i(k+1) = \mathbf{g}(\mathbf{z}^i(k), \mathbf{u}^i(k)),\ k \in \Z_{[0, N-1]}, \\
\ &\mathbf{u}^i(k) \in \bm{\mu},\ k \in \Z_{[0, N-1]}, \\
\ &v_x^i(k) \in \bm{\gamma},\ k \in \Z_{[0, N-1]}, \\
\ &\mathbf{Q}_1 \in \mathbb{S}^{2}_{++}, \\
\ &\mathbf{Q}_2 \in \mathbb{S}^{n_u}_{++}, \text{ and}\\
\ &i \in \Z_{[0, \bm{S}]}.
\end{aligned}
$$
</p>
**Note:** The $i$ in the superscript of $\mathbb{P}^i_N$ is indicative of a formulation that can change over iterations, which will be addressed in the coming sections.

Where, $i$ is the number of the iteration in $\bm{S}$ simulation steps, with $\mathbf{u}^0(-1)$ being the input that the system began with i.e., the input at $t=-1$. The idea of NMPC is to begin with iteration number $i=0$ at $t=0$ and solve $\mathbb{P}^0_N(\mathbf{z}^0(0))$ for ${}^\star \mathbf{U}^{0}$, where ${}^\star \mathbf{U}^i = \underset{\mathbf{u}^i}{\text{argmin}}\ \mathbb{P}^i_N(\mathbf{z}^i(0))$. Then, take the first computed input ${}^\star\mathbf{u}^0(0)$, apply it to the system and take a measurement of the resulting state ${}^\star\mathbf{z}^0(1)$. With $\mathbf{u}^1(-1) = {}^\star\mathbf{u}^0(0) \text{ and } \mathbf{z}^1(0) = {}^\star\mathbf{z}^0(1)$, proceed to iteration $i=1$ at $t=T$ to solve $\mathbb{P}^1_N(\mathbf{z}^1(0))$, obtain ${}^\star\mathbf{u}^1(0)$, apply it to the system to get ${}^\star\mathbf{z}^1(1)$ and move on to iteration $i=2$ at $t = 2T$. This procedure is repeated till $i=\bm{S}$.

**Note:** The reader might notice that this iterative method only works assuming that the computation of ${}^\star \mathbf{U}^i$ takes less than $T$ seconds during each iteration. It is indeed the case and it is not clear what happens if each computation takes longer than $T$ seconds. This hurts the confidence on the designed system, as it might produce unexpected results. Thus, the selection of $T$ shall be of careful consideration owing to the trade off between the accuracy of the discrete approximation and computational limitations. 

This setup is implemented and simulated in Python3 with $N=50,\ \bm{S} = 300,\ \mathbf{z}^0(0) = 0_{n_x \times 1} \text{ and }\mathbf{p}^i_d = [5, 5]^\mathsf{T}\ \forall\ i \in \Z_{[0, \bm{s}]}$. The following GIF shows the simulation results.

<!-- <div>
<img width="640" height="480" controls>
  <source src="/mpc_car_st_slope_no_brake.gif" type="image/gif">
</img>
</div> -->
<img src="/mpc_car_st_slope_no_brake.gif" alt="Simulation results" width="640" height="400">


As it can be seen in the GIF, the NMPC controlled vehicle indeed drove towards (close to) the destination $[5, 5]^\mathsf{T}$, but it didn't converge. It could have been a matter of tuning $\mathbf{Q}_1$ and $\mathbf{Q}_2$, but before tuning them, the vehicle dynamics need to be modified to add a braking system. Remember, the end goal is to have an NMPC controlled autonomous vehicle that is *road safe*. These preliminary results are good enough for now as the weight matrices $\mathbf{Q}_1$ and $\mathbf{Q}_2$ might need retuning when the dynamics have changed.

## Section 2: Let's Brake $_{(\textit{or rather not})}$ the system

This section discusses the addition of a braking system to the vehicle dynamics. In the end, a simulation result is provided for the modified system under the same scenario as in Section 1. The dynamics shall be modified with caution, as it might end up with a broken (*unsolvable*) system.  Going further, the GIF playback will be slowed down when necessary to help with tracking changes in the states and control inputs.

In the equation of $F_x$ in the dynamics, the term $C_{m3}$ might act as the initial resistance of static friction between the tires and the road, and the term $C_{m4}v^2_x$ acts as the force due to air drag as the vehicle starts to move. Though, this captures the initial and forward moving dynamics, this model only works for $\tilde{d} > 0$. Leave $\tilde{d} = 0$, then at $t=0$, $F_x = -C_{m3}$, which makes $v_x < 0$. Since, $v_x^2 > 0$, the negative x-force on the vehicle increases quadratically as $F_x = -C_{m3} - C_{m3}v_x^2$. Also, when the vehicle starts moving i.e., $|v_x| > 0$, the term $C_{m3}$ should vanish, or should switch to rolling fictional force between the tires and the road. It would also make sense to make $\text{sign}(C_{m4}) = \text{sign}(v_x)$ to properly model air drag. These will require additional modifications in the dynamics, which will be addressed in a later section.

Due to the above reasons, moving forward it is assumed that the simulation results are valid as long as $\tilde{d} > 0$ and $v_x > 0$ (this is also the lower bound of $v_x$ in our formulation) and any part of the simulation that violates these conditions (even when $v_x = 0$) shall be considered inaccurate.

With these conditions under consideration, the addition of the braking system can be done by the following modifications to the system dynamics,

<p>
$$
\begin{aligned}
&F_\text{brake} = \mu_{KF}\tilde{b}, \\
&\tilde{b} \in [0, 1], \\
&\mu_{KF} \in \R_+, \\
&F_x = (C_{m1} - C_{m2} v_x)\tilde{d} - C_{m3} - C_{m4} v^2_x - F_\text{brake}
\end{aligned}
$$
</p>

It should be noted that the $\text{sign}(F_\text{brake})$ is only valid if $v_x > 0$. With these modifications to the dynamics, starting from $\mathbf{z}^0(0) = 0_{n_x \times 1}$, the modified system is simulated in Python3 with $N=50,\ \bm{S} = 300,\  \text{ and }\mathbf{p}^i_d = [5, 5]^\mathsf{T}\ \forall\ i \in \Z_{[0, \bm{s}]}$ and the results are shown in the following GIF.

<img src="/mpc_car_st_slope_with_brake.gif" alt="Simulation results" width="640" height="400">

As it can be seen from the results, indeed the vehicle reaches $z_d = [5, 5, 0, 0, 0, 0]^\mathsf{T}$ i.e., $\mathbf{p}_d = [5, 5]^\mathsf{T}$. While this is a good result, it should also be noted that between $t=2.25$ and $t=3.5$, the controller is applying acceleration PWM $(\tilde{d})$ and brake input $(\tilde{b})$ simultaneously. The fix for this undesirable usage of $\tilde{d}$ and $\tilde{b}$ will be discussed in the next section i.e., Section 3.

## References
[1] Cataffo, Vittorio & Silano, Giuseppe & Iannelli, Luigi & Puig, Vicenç & Glielmo, Luigi. (2022). A Nonlinear Model Predictive Control Strategy for Autonomous Racing of Scale Vehicles. 10.1109/SMC53654.2022.9945279. 
