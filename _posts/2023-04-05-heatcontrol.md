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

A primary influence on the temperature of your home is the outdoor temperature, which we will assume to be constant, $H_o$. According to Newton's rate of cooling, your home will cool at a rate proportional to $x-H_o$. However, we can warm the home by, say, burning gas in a furnace at a rate $u(t)$. Our control system is then:

$$\dot x(t)=-k(x(t)-H_o)+u(t)$$

However we will make a substitution for simplicity $y=x-H_o$:

$$\dot y(t)=-ky(t)+u(t)$$

And our endpoint conditions are $x(0)=x(T)=H_i-H_o:=\Delta$. First, we note that we have a linear, homogeneous, autonomous system. Further, the coefficient on $u$ is nonzero so the system is controllable by the Kalman condition. In particular, at any time $T>0$, we can control the system to any state $y$. This means that, for example, no matter what temperature our house is before we get back, it can be controlled to our desired temperature in an infinitely small amount of time. 

Goal
------

Our goal is to minimize the total gas burned during our absence, which is:

$$C(u)=\int_0^T |u(t)|dt$$

where the Lagrangian is $L(u)=|u(t)|$. As mentioned before, the system is controllable at any positive time. Further, it can be shown that the total gas burned, $C$ can be made infinitely small by waiting longer and longer to heat the home back up (and doing so by burning a lot of gas $u$). This degenerate problem is not interesting, so we consider a constrained control, $u \in L^\infty([0,T],[0,U])$. In this case, we have to assume that $U/k>H_i>H_o$, meaning we can burn gas at a rate fast enough to achieve our desired temperature and that our desired temperature is warmer than the outside temperature.

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
  &= kp \\
  u(t) &= argmax_{v \in \Omega}
\end{align}
$$

