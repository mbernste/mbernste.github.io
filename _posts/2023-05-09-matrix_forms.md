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

This is simply a dot product between $\boldsymbol{u}$ and $\boldsymbol{v}$, which can be interpretated as a weighted sum of $\boldsymbol{y}$ using the values in $\boldsymbol{x}$ as weights:

$$\boldsymbol{x}^T\boldsymbol{y} = \sum_{i=1}^N x_iy_i$$

It can also be interpreted as a weighted sum of $\boldsymbol{x}$ using the values in $\boldsymbol{y}$ as weights. 

2. $\boldsymbol{x}^T\boldsymbol{x}$

Building on the previous form, this is the dot product of a vector $\boldsymbol{x}$ with itself. We include this form separately because it has an additional interpretation: it is the square of the l2-norm of $\boldsymbol{x}$. That is,

$$\begin{align*}||\boldsymbol{x}||^2 &= \sqrt{\sum_{i=1}^n x_i^2}^2 \\ &= \sum_{i=1}^n x_ix_i \\ &= \boldsymbol{x}^T\boldsymbol{x}\end{align*}$$


