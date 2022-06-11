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

In this post, we discuss the relationship between [matrices](https://mbernste.github.io/posts/matrices/) and systems of linear equations. By doing so, we will introduce a set of important matrices called the _elementary matrices_ and discuss how the set of all [invertible matrices](https://mbernste.github.io/posts/inverse_matrices/), coupled with the elementary matrices, form an elegant mathematical structure called the _general linear group_. Before diving into the general linear group, we will first review the concept of a _group_ from _group theory_. 

In this blog post we will discuss some of the deep fundamental structures in linear algebra and show how all [invertible matrices](https://mbernste.github.io/posts/inverse_matrices/) are, in a particular sense, the same! Specifically, we will show how any invertible matrix can be converted to another invertible matrix by multiplying the matrix by some particular sequence of special matrices called **elementary matrices**. As a consequence, we will show that all invertible matrices can be constructed by multiplying the [identity matrix](https://mbernste.github.io/posts/matrices_as_functions/) by a particular sequence elementary matrices. In doing so, we will see that the elementary matrices form the "atoms" by which all invertible matfices are constructed. 

Finally, we will describe how the set of all invertible matrices, coupled with the set of elementary matrices, form a group called the **general linear group**. Thus, we will describe a fundamental link between linear algebra and group theory!

Before we start, we will review a few important concepts. First, we will discuss the relationship between systems of linear equations and matrices. Second, we will review the definition of a **group** from group theory. Finally, we will describe the elementary row matrices and how they form the general linear group.

Let's dig in!

Systems of linear equations
---------------------------

To review, a system of linear equation is a set of linear equations that all utilize the same set of variables, $x_1, x_2, \dots, x_n$, but each equation differs by the coefficients that multiply each variable. 

For example, say we have three variables, $x_1, x_2$, and $x_3$. A system of linear equations involving these three variables can be written as:

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$





