---
title: 'Elementary matrices and the general linear group'
date: 2022-06-11
permalink: /posts/general_linear_group/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

Many curricula in linear algebra begin by introducing systems of linear equations. In my [blog posts on linear agebra](https://mbernste.github.io/posts/), I take an alternative pedogocial route that is a bit more abstract. Instead of starting with systems of linear equations, I start with [vector spaces](https://mbernste.github.io/posts/vector_spaces/), [matrices](https://mbernste.github.io/posts/matrices/), and [linear transformations](https://mbernste.github.io/posts/matrices_linear_transformations/). Advantages to this approach are 1) right from the start, we delve into the deep mathematical structures at the heart of linear algebra and 2) we keep everything abstract and thus, very generalizable to specific applications and problems. 

In this blog post, we will begin by taking a step back from the very abstract and discuss the relationship between matrices and systems of linear equations. This "backtracking" will only be a slight stepping stone back into the abstract. Specifically, we will discuss how all [invertible matrices](https://mbernste.github.io/posts/inverse_matrices/) are, in a particular sense, the same! 

Specifically, we will show how any invertible matrix can be converted to another invertible matrix by multiplying the matrix by some particular sequence of special matrices called **elementary matrices**. By doing so, we will reveal a very deep mathematical structure at the heart of linear algebra called the **general linear group**, thus describing a link between linear algebra and group theory!

Before we start, we will review a few important concepts. First, we will discuss the relationship between systems of linear equations and matrices. Second, we will review the definition of a **group** from group theory. Finally, we will describe the elementary row matrices and how they form the general linear group.

Let's dig in!

Systems of linear equations
---------------------------

To review, a system of linear equation is a set of linear equations that all utilize the same set of variables, $x_1, x_2, \dots, x_n$, but each equation differs by the coefficients that multiply each variable. 

For example, say we have three variables, $x_1, x_2$, and $x_3$. A system of linear equations involving these three variables can be written as:

$$\begin{align*}5 x_1 + -1 x_2 + x_3 &= 5 \\ 2 x_1 + -4 x_2 + 2 x_3 &= 6 \\ x_1 + x_2 + - x_3 &= -1 \end{align*}$$


$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

where $a_{1,1}, dots, a_{3,3}$ are the coefficients and are treated as fixed and $b_1, b_2,$ and $b_3$ are the 



