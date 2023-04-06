---
title: 'Optimal Control of Heating During Vacation'
date: 2023-04-05
permalink: /posts/2023/04/control-heat/
tags:
  - cool posts
---

What should your thermostat do when you are away from home? Say you keep the temperature of your home, $x(t)$, at a fixed temperature $H_i$ when you are around. Assume that you are going to be leaving for a winter vacation at time $t=0$, and you want the home to be the same temperature when you return at time $t=T$, but you don't care about the home's temperature when you are gone. We will use Pntryagin's maximum principle to achieve your desired final temperature, while minimize the amount of energy used in the meantime.

Acknowledgements
======

This post was inspired by the course Introduction to Control Theory and Optimal Control taught by [Nicolas Charon](https://www.cis.jhu.edu/~charon/) at Johns Hopkins University.

The Control System
======

A primary influence on the temperature of your home is the outdoor temperature, which we will assume to be constant, $H_o$. According to Newton's rate of cooling, your home will cool at a rate proportional to $x-H_o$. However, we can warm the home by, say, burning gas in a furnace at a rate $u(t) \in L^\infty([0,T])$. Our control system is then:

$$\dot x(t)=-k(x(t)-H_o)+u(t)$$

However we will make a substitution for simplicity $y=x-H_o$:

$$\dot y(t)=-ky(t)+u(t)$$

And our endpoint conditions are $x(0)=x(T)=H_i-H_o:=\Delta$. Our goal is to minimize the total gas burned during our absence, which is:

$$C(u)=\int_0^T |u(t)|dt$$

where the Lagrangian is $L(u)=|u(t)|$.

The Hamiltonian
======

Our Hamiltonian is:

$$H_\lambda(y,p,u)=p(u-ky)+\lambda |u|$$

And we can apply the strong Pontryagin maximum principle which is a necessary condition for an optimal control $u$, assuming one exists. The condition for optimality is in the following equations.

The evolution equations:

$$
\begin{align}
  \dot x &= \nabla_p H_\lambda \\
  &= u-ky \\
  \dot p &= -\nabla_y H_\lambda \\
  &= kp
\end{align}
$$