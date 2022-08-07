---
title: 'Elementary matrices and the general linear group'
date: 2022-08-07
permalink: /posts/elementary_matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

In a [previous blog post](https://mbernste.github.io/posts/systems_linear_equations/), we showed how systems of linear equations can be represented as a matrix equation. For example, the system of linear equations,

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

can be represented succinctly as

$$\boldsymbol{Ax} = \boldsymbol{b}$$

where $\boldsymbol{A}$ is the matrix of coefficients $a_{1,1}, a_{1,2}, \dots, a_{3,3}$ and $\boldsymbol{b}$ is the matrix of coefficients of $b_1, b_2,$ and $b_3$.

Furthermore, we noted that this system will have exactly one solution if $\boldsymbol{A}$ is an [invertible matrix](https://mbernste.github.io/posts/inverse_matrices/). Now, a natural question is: how do we actually solve for this solution? In this post, we will show how we can represent the process of solving this system of linear equations using matrix multiplication by employing an important class of matrices called the **elementary matrices**. 

Reduced row echelon form
------------------------

Before digging into matrices, let's first discuss how one can go about solving a system of linear equations:

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

To solve such a system, our goal is perform simple algebraic operations on each of these equations until we convert the system to one with the following form:

$$\begin{align*}x_1 &= c_1 \\ x_2 &= c_2 \\ x_3 &= c_3 \end{align*}$$

where $c_1, c_2$, and $c_3$ are the solutions to the system -- that is, they are the values we can assign to $x_1, x_2$, and $x_3$ so that all of the equations in the system are valid.  Note that we can also write this final form of the system of linear equations as follows:

$$\begin{align*}1x_1 + 0x_2 + 0x_3 &= c_1 \\ 0x_1 + 1x_2 + 0x_3 &= c_2 \\ 0x_1 + 0x_2 + 1x_3 &= c_3 \end{align*}$$

Which in turn, can be written as a matrix equation, [as discussed previously](https://mbernste.github.io/posts/systems_linear_equations/):

$$\begin{bmatrix}1 && 0 && 0 \\ 0 && 1 && 0 \\ 0 && 0 && 1 \end{bmatrix}  \begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}c_1 \\ c_2 \\ c_3\end{bmatrix}$$

Or rather, simply as 

$$\boldsymbol{Ix} = \boldsymbol{c}$$

This form of the matrix equation is called **reduced row echolon form**.


Now, what kinds of algebraic operations can we perform on the equations of the system to solve it? There are three main categories:

1. **Scalar multiplication**: Simply multiply both sides of one of the equations by a scalar. 
2. **Row swap**: You can move one equation above or below another. Note, the order the equations are written is irrevalent to t


