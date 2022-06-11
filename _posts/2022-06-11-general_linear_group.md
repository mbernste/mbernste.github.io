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

Many curricula in linear algebra begin by introducing systems of linear equations. In my blog posts, I take an alternative pedogocial route that is a bit more abstract. Instead of starting with systems of linear equations, I start with [vector spaces](), [matrices](), and [linear transformations](). Advantages to this approach are 1) right from the start, we delve into the deep mathematical structures at the heart of linear algebra and 2) we keep everything abstract and thus, very generalizable to specific applications and problems. The disadvantages are 1) more intellectual demanding and 2) unmotivating because we have not tied many of these ideas to specific applications.

Here, we will take a step back and discuss the relationship between matrices and systems of linear equations. By doing so, we will introduce a set of important matrices called the _elementary matrices_ and discuss how the set of all invertible matrices, coupled with the elementary matrices, form an elegant mathematical structure called the _general linear group_. Before diving into the general linear group, we will first review the concept of a _group_ from _group theory_. Let's dig in!

Systems of linear equations
---------------------------

To review, a system of linear equation is a set of linear equations that all utilize the same set of variables, $x_1, x_2, \dots, x_n$, but each equation differs by the coefficients that multiply each variable. 

For example, say we have three variables, $x_1, x_2$, and $x_3$. A system of linear equations involving these three variables can be written as:

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$





