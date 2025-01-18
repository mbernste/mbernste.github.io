---
title: 'A zoo of matrix forms'
date: 2023-05-07
permalink: /posts/matrixforms/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

Equations that include matrices and vectors can be challenging to interpret intuitively; however, there are certain forms and patterns that commonly arise. Understanding these subpatterns of matrix forms within equations helps to interpret the full equation. In this post, we will catalogue and discuss some of these matrix forms.

1. $\boldsymbol{x}^T\boldsymbol{y}$

This is simply a dot product between $\boldsymbol{x}$ and $\boldsymbol{y}$. Thus, if you ever see an equation like $\boldsymbol{x}^T\boldsymbol{y} = 0$, this means that $\boldsymbol{x}$ is orthogonal to $\boldsymbol{y}$. 

This form can also be interpretated in a more granular way as a weighted sum of $\boldsymbol{y}$ using the values in $\boldsymbol{x}$ as weights (or conversely as a weighted sum of $\boldsymbol{x}$ using the values in $\boldsymbol{y}$ as weights):

$$\boldsymbol{x}^T\boldsymbol{y} = \sum_{i=1}^N x_iy_i$$

2. $\boldsymbol{x}^T\boldsymbol{x}$

Building on the previous form, this is the dot product of a vector $\boldsymbol{x}$ with itself. We include this form separately because it has an additional interpretation: it is the square of the l2-norm of $\boldsymbol{x}$. That is,

$$\begin{align*}||\boldsymbol{x}||^2 &= \left(\sqrt{\sum_{i=1}^n x_i^2}\right)^2 \\ &= \sum_{i=1}^n x_ix_i \\ &= \boldsymbol{x}^T\boldsymbol{x}\end{align*}$$

Thus, if you ever see an equation like $\boldsymbol{x}^T\boldsymbol{x} = 1$, this is saying that the square of $\boldsymbol{x}$'s norm is 1, which means that the norm itself is one. This equation is simply saying that $\boldsymbol{x}$ is a unit vector!

3. $\boldsymbol{x}\boldsymbol{y}^T$

While this looks like Form 1, it is quite different. It actually computes a full matrix of size $n \times n$ where element $i$, $j$ is $x_iy_j$. 

4. $\boldsymbol{D}\boldsymbol{X}\boldsymbol{D}$

Given a square diagonal matrix $\boldsymbol{D}$ and a square matrix $\boldsymbol{X}$, this formula will compute the matrix where each element $i$, $j$ is given by $x_{i,j}d_{i,i}d_{j,j}$. That is:

$$\boldsymbol{D}\boldsymbol{X}\boldsymbol{D} = \begin{bmatrix}x_{1,1}d_{1,1}d_{1,1} & x_{1,2}d_{1,1}d_{2,2} & \dots  & x_{1,n}d_{1,1}d_{n,n} \\  x_{2,1}d_{2,2}d_{1,1} & x_{2,2}d_{2,2}d_{2,2} & \dots  & x_{2,n}d_{2,2}d_{n,n} \\ \vdots & \vdots & \ddots & \vdots \\  x_{n,1}d_{n,n}d_{1,1} & x_{n,2}d_{n,n}d_{2,2} & \dots  & x_{n,n}d_{n,n}d_{n,n} \end{bmatrix}$$

   


