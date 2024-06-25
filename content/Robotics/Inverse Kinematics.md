---
title: Inverse Kinematics
draft: false
tags:
  - robotics
  - Lie_Group
  - Manifold
---
## Overview
Inverse Kinematics is one of the fundamental tools in robotics, it accepts trajectories in cartesian space and generate trajectories in general coordinate. In this note, inverse kinematics is demonstrated with a bit of Lie group theory to ease the concept and bring in more insight of the computation.

## Problem Statement
With kinematics function $f$ which satisfies
$$
\begin{aligned}
x=f(q)
\end{aligned}
$$
where $x\in SE(3)$, $q\in \mathcal{S}$ belongs to a valid set of generalized coordinate. Find the corresponding $q$ for a given $x_d$. 

## Numerical Algorithm and Computation on SE(3)
Initialize a generalized coordinate $q_0$, take the Taylor expansion of it
$$
\begin{aligned}
f(q_d)=f(q_0)+J_{q_0}(q_d-q_0)
\end{aligned}
$$
Rearrange we have

$$
\begin{aligned}
\Delta q=J_{q_0}^{-1}\Big(f(q_d)-f(q_0)\Big)
\end{aligned}
$$

We could do integration with a time parameter $\text{dt}$

$$
\begin{aligned}
\dot{q}=\Delta q\ \text{dt} 
\end{aligned}
$$

Now we have an iterative algorithm, but how to calculate it, because $f(q)\in SE(3)$ involves translation and rotation. Lie group would help! Consider $f(q_d)=\mathcal{X}_d$, and $f(q_0)=\mathcal{X}_0$, we could do $$
\begin{aligned}
\Delta q=J_{q_0}^{-1}\text{Log}(\mathcal{X}_d-\mathcal{X}_0)
\end{aligned}
$$ which becomes a 6D vector in cartesian space. Note that here $-$ means the right subtraction because the Jacobian is define in the local frame. 

The idea behind is inverse kinematics is actually use the error on the $SE(3)$ manifold as a searching direction, aka a velocity, then map it back to the configuration space. Because
$$
\begin{aligned}
\dot{x}=J_q(q)\dot{q}
\end{aligned}
$$
Ideally we have to use the $\text{Exp}$ operator in configuration space to map $\dot{q}$ to $q$, but if we ignore the joint limit and velocity limit, the tangent space $\dot{q}$ share the same manifold with the configuration space $q$. 

Of course, there are a lot of details when implement the algorithm, e.g. 
- The inverse, usually pseudo inverse is used;
- You could also used the left subtraction in here, but then the Jacobian must in global coordinate defined on Lie algebra;

## Reference
- [A micro Lie theoy for state estimation in robotics](https://arxiv.org/pdf/1812.01537)
