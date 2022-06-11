---
title: 'Systems of linear equations'
date: 2022-06-11
permalink: /posts/systems of linear equations/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

Many curricula in linear algebra begin by introducing systems of linear equations. In my [blog posts on linear agebra](https://mbernste.github.io/posts/), I take an alternative pedogocial route that is a bit more abstract. Instead of starting with systems of linear equations, I start with [vector spaces](https://mbernste.github.io/posts/vector_spaces/), [matrices](https://mbernste.github.io/posts/matrices/), and [linear transformations](https://mbernste.github.io/posts/matrices_linear_transformations/). Advantages to this approach are 1) right from the start, we delve into the deep mathematical structures at the heart of linear algebra and 2) we keep everything abstract and thus, very generalizable to specific applications and problems. 

In this blog post, we will begin by taking a step back from the very abstract and discuss the relationship between matrices and systems of linear equations. Specifically, we will show how many ideas we have discussed so far, such as invertible matrices, relate to description of solutions to systems of linear equations.

Let's dig in!

How matrices can represent systems of linear equations
------------------------------------------------------

To review, a system of linear equation is a set of linear equations that all utilize the same set of variables, $x_1, x_2, \dots, x_n$, but each equation differs by the coefficients that multiply each variable. 

For example, say we have three variables, $x_1, x_2$, and $x_3$. A system of linear equations involving these three variables can be written as:

$$\begin{align*}3 x_1 + 2 x_2 - x_3 &= 1 \\ 2 x_1 + -2 x_2 + 4 x_3 &= -2 \\ -x_1 + 0.5 x_2 + - x_3 &= 0 \end{align*}$$

A **solution** to this system of linear equations is an assignment to the variables $x_1, x_2, x_3$, such that all of the equations are simultaneously true. In our case, a solution would be given by $(x_1, x_2, x_3) = (1, -2, -2)$.

More abstractly, we could write a system of linear equations as 

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

where $a_{1,1}, \dots, a_{3,3}$ are the coefficients and $b_1, b_2,$ and $b_3$ are the constant terms, all treated as fixed.

Notice, we can can write this system of linear equations much more succinctly using [matrix-vector](https://mbernste.github.io/posts/matrix_vector_mult/) multiplication. That is,

$$\begin{bmatrix}a_{1,1} && a_{1,2} && a_{1,3} \\ a_{2,1} && a_{2,2} && a_{2,3} \\ a_{3,1} && a_{3,2} && a_{3,3} \end{bmatrix}  \begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}b_1 \\ b_2 \\ b_3\end{bmatrix}$$

This is the first important point: any system of linear equations can be written succintly as an equation using matrix-vector multiplication!

The relationship between invertible matrices and the solutions to systems of linear equations
--------------------------------------------------------------------------------------------

Now, a natural question to ask is, given a system of linear equations, how many solutions does it have? 

In some cases, the system could have one solution as in the example described previously; however, in other cases, it could have an infinitely large number of solutions. For example, the system below has an infinite number of solutions:

In still other cases, the system could have no solutions at all! That is, 





