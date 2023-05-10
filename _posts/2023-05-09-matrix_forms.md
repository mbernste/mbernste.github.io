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

Analytical forms that include matrices and vectors can be challenging to interpret intuitively; however, there are certain common forms and patterns that arise across mathematical and scientific disciplines. In this post, we will catalogue and discuss some of these matrix forms.

1. $\boldsymbol{x}^T\boldsymbol{y}$

This is simply a dot product between $\boldsymbol{u}$ and $\boldsymbol{v}$, which can be interpretated as a weighted sum of $\boldsymbol{y}$ using the values in $\boldsymbol{x}$ as weights:

$$\boldsymbol{x}^T\boldsymbol{y} = \sum_{i=1}^N x_iy_i$$

It can also be interpreted as a weighted sum of $\boldsymbol{x}$ using the values in $\boldsymbol{y}$ as weights. 

2. $\boldsymbol{x}^T\boldsymbol{x}$

Building on the previous form, this is the dot product of a vector $\boldsymbol{x}$ with itself. 