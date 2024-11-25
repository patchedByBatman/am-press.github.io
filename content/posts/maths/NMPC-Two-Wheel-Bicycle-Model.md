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
I have recently read a paper named "A Nonlinear Model Predictive Control Strategy for Autonomous Racing of Scale Vehicles" by Vittorio Cataffo et al., [1]. After reading the paper, I have decided to implement proposed system on my own and study it further by implementing it in a public road scenario, where road safety takes priority over minimum lap time. The purpose of this article is to showcase the formulation and simulation results of an NMPC controlled vehicle system. As a part of experimentation, I will be modifying the approach as I see fit and I will be updating this article by adding new sections accordingly.

## Section 1: Direct Implementation
This section showcases the simulation results of an NMPC controlled vehicle based bicycle model dynamics used in [1]. The results in this section are limited to implementation of vehicle dynamics and formulating an NMPC to drive it to a reference position on the xy-coordinate space and does not include autonomous navigation on a track. 

The two-wheel Bicycle model [1] is as follows:
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
with
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
where
$F_{r, x},\ F_{r, y},\ F_{f, x},\text{ and } F_{f, y} \in \R$ are the forces acting on the tires with $r$ and $f$ indicating rear and front tires respectively, and $x$ and $y$ indicating longitudinal and lateral component of forces in the local vehicle body xy-frame respectively. The constants $l_f,\text{ and }  l_r \in \R$ are the distances from the Centre of Gravity $(C_g)$ to front and rear wheels respectively. The control inputs $\tilde{d},\text{ and }  \delta \in \R$ are the normalised forward acceleration PWM control input and front wheel steering angle input in radians respectively. The states $p_x,\ p_y,\text{ and }  \psi \in \R$ are the vehicle's x position in meters, the y position in meters, and heading in radians in the global frame of reference respectively. The states $v_x,\ v_y,\text{ and }  \omega \in \R$ are the vehicle's x velocity in meters-per-second, the y velocity in meters-per-second, and the angular rotation rate around the z-axis in radians-per-second in the local body-fixed frame of reference respectively. These equations and their parameters are described in equations (1) through (4) in [1]. Throughout this article, the vehicle parameters are takes as described in Table 1 in [1]. They are given (estimated) as,

| Param    | Value            | Param    | Value              | Param    | value                             |
| -------- | ---------------- | -------- | ------------------ | -------- | --------------------------------- |
| $l_f$    | $0.178$ m        | $l_r$    | $0.147$ m          | $m$      | $5.6292$ kg                       |
| $J_z$    | $0.204$ kg m$^2$ | $B_f$    | $9.242$            | $B_r$    | $17.716$                          |
| $C_f$    | $0.085$          | $C_r$    | $0.133$            | $D_f$    | $134.585$ N                       |
| $D_r$    | $159.919$ N      | $C_{m1}$ | $20$ N             | $C_{m2}$ | $6.92 \times 10^{-7}$ kg s$^{-1}$ |
| $C_{m3}$ | $3.99$ N         | $C_{m4}$ | $0.67$ kg m$^{-1}$ | $M$      | $1674$                            |

## References
[1] Cataffo, Vittorio & Silano, Giuseppe & Iannelli, Luigi & Puig, Vicenç & Glielmo, Luigi. (2022). A Nonlinear Model Predictive Control Strategy for Autonomous Racing of Scale Vehicles. 10.1109/SMC53654.2022.9945279. 
