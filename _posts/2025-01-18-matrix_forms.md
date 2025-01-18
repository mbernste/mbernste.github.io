---
title: 'A zoo of matrix forms'
date: 2025-01-18
permalink: /posts/matrixforms/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

Equations that include matrices and vectors can be challenging to interpret intuitively; however, there are certain forms and patterns that commonly arise. Understanding these patterns within equations helps to interpret the full equation. In this post, we will catalogue and discuss some of these matrix forms. This post is designed to form a sort of "reference manual" for quickly reviewing common matrix forms. I hope to add new common matrix forms to this blog post as I confront them in my self-teaching and professional work.

1\. $\boldsymbol{x}^T\boldsymbol{y}$
------------------------------------

This is simply a dot product between $\boldsymbol{x}$ and $\boldsymbol{y}$. Thus, if you ever see an equation like $\boldsymbol{x}^T\boldsymbol{y} = 0$, this means that $\boldsymbol{x}$ is orthogonal to $\boldsymbol{y}$. 

This form can also be interpretated in a more granular way as a weighted sum of $\boldsymbol{y}$ using the values in $\boldsymbol{x}$ as weights (or conversely as a weighted sum of $\boldsymbol{x}$ using the values in $\boldsymbol{y}$ as weights):

$$\boldsymbol{x}^T\boldsymbol{y} = \sum_{i=1}^N x_iy_i$$

2\. $\boldsymbol{x}^T\boldsymbol{x}$
------------------------------------

Building on the previous form, this is the dot product of a vector $\boldsymbol{x}$ with itself. We include this form separately because it has an additional interpretation: it is the square of the l2-norm of $\boldsymbol{x}$. That is,

$$\begin{align*}||\boldsymbol{x}||^2 &= \left(\sqrt{\sum_{i=1}^n x_i^2}\right)^2 \\ &= \sum_{i=1}^n x_ix_i \\ &= \boldsymbol{x}^T\boldsymbol{x}\end{align*}$$

Thus, if you ever see an equation like $\boldsymbol{x}^T\boldsymbol{x} = 1$, this is saying that the square of $\boldsymbol{x}$'s norm is 1, which means that the norm itself is one. This equation is simply saying that $\boldsymbol{x}$ is a unit vector!

3\. $\boldsymbol{x}\boldsymbol{y}^T$
------------------------------------

While this looks like Form 1, it is quite different. It computes a full matrix of size $n \times n$ where element $i$, $j$ is $x_iy_j$. This operation is called the [outer product](https://en.wikipedia.org/wiki/Outer_product):

$$\boldsymbol{x}\boldsymbol{y}^T = \begin{bmatrix}x_1y_1 & x_1y_2 & \dots & x_1y_n \\ x_2y_1 & x_2y_2 & \dots & x_2y_n \\ \vdots & \vdots & \ddots & \vdots \\ x_ny_1 & x_ny_2 & \dots & x_ny_n \end{bmatrix}$$

4\. $\boldsymbol{Ax}$
--------------------

This is standard [matrix-vector multiplication](https://mbernste.github.io/posts/matrix_vector_mult/). As we discussed in a [prior post](https://mbernste.github.io/posts/matrix_vector_mult/), there are three main ways to veiw this operation:

* As a row-wise vector-generating process:
  
$$\boldsymbol{Ax} = \begin{bmatrix} \boldsymbol{a}_{1,*} \cdot \boldsymbol{x} \\ \boldsymbol{a}_{2,*}  \cdot \boldsymbol{x} \\ \vdots \\ \boldsymbol{a}_{m,*}  \cdot \boldsymbol{x} \\ \end{bmatrix}$$

* As taking a linear combination of the rows of $\boldsymbol{A}$ using the values of $\boldsymbol{x}$ as weights:

$$\boldsymbol{A}\boldsymbol{x} := x_1\boldsymbol{a}_{*,1} + x_2\boldsymbol{a}_{*,2} + \dots +  x_n\boldsymbol{a}_{*,n}$$

* As [transforming](https://mbernste.github.io/posts/matrices_linear_transformations/)  the vector $\boldsymbol{x}$ via a linear transformation characterized by the matrix $\boldsymbol{A}$, denoted $T$:

$$\boldsymbol{Ax} = T(\boldsymbol{x})$$

5\. $\boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x}$
--------------------------------------------------

This is a [quadratic form](https://en.wikipedia.org/wiki/Quadratic_form) that reduces a scalar computed by the following formula:

$\boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x} = \sum_{i=1}^n\sum_{j=1}^n a_{i,j}x_ix_j$

This is a quadratic form because it specifies an equation in which all possible pairs of elements in $\boldsymbol{x}$ are multiplied together. Moreover, each pair is scaled by a specific value in $\boldsymbol{A}$. When $i = j$, the form will have a squared term, $a_{i,i}x_i^2$, and thus, this is a quadratic equation.

6\. $\boldsymbol{D}\boldsymbol{A}\boldsymbol{D}'$
------------------------------------------------

Let $\boldsymbol{D}$ and $\boldsymbol{D}'$ be two square diagonal matrices. Let $\boldsymbol{A}$ be an arbitrary square matrix. The formular $\boldsymbol{D}\boldsymbol{A}\boldsymbol{D}'$ will compute the matrix where each element $i$, $j$ is given by $a_{i,j}d_{i,i}{d'}_{j,j}$. That is:

$$\boldsymbol{D}\boldsymbol{A}\boldsymbol{D}' = \begin{bmatrix}a_{1,1}d_{1,1}{d'}_{1,1} & a_{1,2}d_{1,1}{d'}_{2,2} & \dots  & a_{1,n}d_{1,1}{d'}_{n,n} \\  a_{2,1}d_{2,2}{d'}_{1,1} & x_{2,2}d_{2,2}d_{2,2} & \dots  & a_{2,n}d_{2,2}{d'}_{n,n} \\ \vdots & \vdots & \ddots & \vdots \\  a_{n,1}d_{n,n}{d'}_{1,1} & a_{n,2}d_{n,n}{d'}_{2,2} & \dots  & a_{n,n}d_{n,n}{d'}_{n,n} \end{bmatrix}$$

   


