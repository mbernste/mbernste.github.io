---
title: 'The Eigenvalues of Symmetric Matrices'
date: 2023-05-07
permalink: /posts/eigensym/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

We may ask, which unit vector is stretched the most under a symmetric matrix $\boldsymbol{S} \in \mathbb{R}^m$. That is, we want to solve:

$$\text{arg max}_\boldsymbol{u} \boldsymbol{Su}$$

such that 

$$\boldsymbol{u}^T\boldsymbol{u} = 1$$

The Spectral Theorem tells us that because $\boldsymbol{S}$ is symmetric it is _orthogonally diagonalizable_, meaning that we can decompose $\boldsymbol{S}$ as:
