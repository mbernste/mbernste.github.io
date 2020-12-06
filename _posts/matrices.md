---
title: 'Introducing matrices'
date: 2020-11-24
permalink: /posts/matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Matrices are a fundamental concept in linear algebra and are ubiqutous across nearly every field of science and engineering.  In my opinion, matrices are introduced to students in a myopic way that hides the many ways that matrices are interpreted and utilized.  The problem, is that matrices can be thought about in multiple ways and each way is equally important.  I believe that in order to mitigate students' confusion, teachers often focus on only one way to view matrices when they are first introduced; however, at least for me, this method brought more confusion than it would have otherwise.  

Sometimes, matrices are introduced as simply, "a rectangular array of numbers," as is the case in the [Wikipedia entry on matrices]().  Personally, in my undergraduate linear algebra course, matrices were first introduced as a way to efficiently encode a system of linear equations. For example, the system of linear equations

$$\begin{align*}2x_1 + 4x_2 &= 6 \\ x_1 - 3x_2 &= 2\end{align*}$$

could be encoded as the *coefficient matrix*

$$\begin{align*}\begin{bmatrix}2 & 4 \\ 1 & 3\end{bmatrix}\end{align*}$$

or as the *augmented matrix*

$$\begin{align*}\begin{bmatrix}2 & 4 & 6 \\ 1 & 3 & 2\end{bmatrix}\end{align*}$$
