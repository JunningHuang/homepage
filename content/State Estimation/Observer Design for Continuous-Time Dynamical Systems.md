---
title: Observer Design for Continuous-Time Dynamical Systems
draft: false
tags:
  - observer
  - state_estimation
  - survey
---
> This note is based on Pauline Bernard's survey paper [observer Design for continuous-Time dynamical systems](https://minesparis-psl.hal.science/hal-03337138/document). I highly recommend everyone who is working in the field of observer design, state estimation to read this extremely beautiful paper. She is one of the leading figures in the field of observer design and my favorite researcher in observer design.
## Overview
Observer design 

## Problem Statement
There are three ways to define a real-time state estimation problem, given a dynamical system:
$$
\begin{aligned}
\dot{x}=f(x),\ \ y=h(x)
\end{aligned}
$$
- Open loop estimation based on simulation
	In a probabilistic manner, $\text{argmax}_{x_0} P(x_0|y_{0:t},u_{0:t})$, estimate the initial state or current state via simulation assuming the model is known. In a stochastic sense it's doing inference, while in a deterministic manner, it's like interval estimation.
- Open loop estimation based on optimization, moving horizon optimization
	$\hat{x}=\text{argmin}_{\hat{x}_f}\int_{t-\bar{t}}^t|Y(\hat{x}_f,t;\tau)-y(\tau)|^2d\tau$, $\bar{t}\in[0,t]$ is a window parameter.
- Closed loop estimation based on dynamical systems
	a dynamical system $\dot{\hat{z}}=\mathcal{F}(\hat{z},y,t),\ \ \hat{x}=\mathcal{T}(\hat{z},y,t)$, which verifies $\lim_{t\to\infty}|\hat{x}(t)-x(t)|=0$. Here $\hat{z}=T(\hat{x})$ and $\mathcal{T}$ is the left-inverse of the transformation $T$
 
>**Remark**
>- The first and second approaches are possibly equivalent in the lens of inference as optimization, note that any inference problem can be rewrite as an optimization problem.
>- The third approach has some connection to the optimization perspective, because the Lyapunov function can be cast as a cost function. But the mechanism under the hood is very different because an observer include the transformation from one coordinate to another and transform it back.

## Detectability, Observability and Normal Forms

Distinguishability



## Reference
- [observer Design for continuous-Time dynamical systems](https://minesparis-psl.hal.science/hal-03337138/document)





