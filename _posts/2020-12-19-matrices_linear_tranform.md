---
title: 'Matrix-vector multiplication'
date: 2020-12-19
permalink: /posts/matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
  - linear transformation
---

As we briefly mentioned in a [previous post]() on how to think about matrices, we discussed three ways one can view a matrix: as a table of values, as a list of vectors, and finally, as a function.  It is the third way of viewing a matrices that really gives matrices their power.  Here, we'll introduce an operation between matrices and vectors, called **matrix-vector multiplication**, which will enable us to use matrices as functions. 

Matrix-vector multiplication is an operation between a matrix and a vector that produces a new vector.  Notably, matrix-vector multiplication is only defined between a matrix and a vector where the length of the vector equals the number of columns of the matrix.  It is defined as follows:

<span style="color:#0060C6">**Definition 1 (Matrix-vector multiplication):** Given a matrix $\bold{A} \in \mathbb{R}^{m \times n}$ and vector $\bold{x} \in \mathbb{R}^n$ the \textbf{matrix-vector multiplication} of $\bold{A}$ and $\bold{x}$ is defined as </span>

<center><span style="color:#0060C6">$$\bold{A}\bold{x} := x_1\bold{a}_{*,1} + x_2\bold{a}_{*,2} + \dots +  x_n\bold{a}_{*,n}$$ </span></center>

<span style="color:#0060C6">where $\bold{a}_{*,i}$ is the $i$th column vector of $\bold{A}$.</span>





