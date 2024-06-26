---
title: Inverse Kinematics
draft: false
tags:
  - robotics
  - Lie_Group
  - Manifold
---
## Overview
Inverse Kinematics is one of the fundamental tools in robotics, it accepts trajectories in cartesian space and generate trajectories in generalized coordinates. In this note, inverse kinematics is demonstrated with a bit of Lie group theory to ease the concept and bring in more insight of the computation.

## Problem Statement
With kinematics function $f$ which satisfies
$$
\begin{aligned}
x=f(q),
\end{aligned}
$$
where $x\in \mathbb{R}^6$ include the translation and rotation, $q\in \mathcal{S}$ belongs to a valid set of generalized coordinate. The target is finding the corresponding $q$ for a given $x_d$. 
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
\dot{q}=\Delta q\ \text{dt}.
\end{aligned}
$$
Now we have an iterative algorithm, but how to calculate it, because $f(q)\in \mathbb{R}^6$ involves translation and rotation. Lie group would help! Consider $\mathcal{X}_d$ and $\mathcal{X}_0$, which are the $SE3$ representation of $x_d$ and $x_0$, respectively. We could then do 

$$
\begin{aligned}
\Delta q=J_{q_0}^{-1}\text{Log}(\mathcal{X}_d-\mathcal{X}_0)
\end{aligned}
$$

where $\text{Log}(\mathcal{X}_d-\mathcal{X}_0)$ is a 6D vector in cartesian space. Note that here $-$ means the right subtraction because the Jacobian is define in the local frame. 

The idea behind is inverse kinematics use the difference of $\mathcal{X}_d$ and $\mathcal{X}_0$ on the $SE(3)$ manifold as a search direction, then map it back to the generalized coordinates. Because
$$
\begin{aligned}
\dot{x}=J_q(q)\dot{q}
\end{aligned},
$$
ideally we have to use the $\text{Exp}$ operator in configuration space to do integration. But since the tangent space $\dot{\mathcal{Q}}$ of $\dot{q}$ and the generalized coordinate $\mathcal{Q}$ of $q$ both belongs to $\mathbb{R}^n$, we only need to do simple Euler integration.

Of course, there are a lot of details when implement the algorithm, e.g. 
- How to calculate the inverse of Jacobian, usually pseudo inverse is used;
- You could also used the left subtraction, but then the Jacobian must in global coordinate defined on Lie algebra;

For implementation, one can check the code here, implemented with pinocchio [pinocchio inverse kinematics](https://gepettoweb.laas.fr/doc/stack-of-tasks/pinocchio/master/doxygen-html/md_doc_b-examples_i-inverse-kinematics.html). 

## Reference
- [A micro Lie theoy for state estimation in robotics](https://arxiv.org/pdf/1812.01537)
