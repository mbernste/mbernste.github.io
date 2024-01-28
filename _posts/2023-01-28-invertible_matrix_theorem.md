---
title: 'The invertible matrix theorem'
date: 2024-01-28
permalink: /posts/invertible_matrix_theorem/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

Introduction
------------

Throughout many of my prior linear algebra posts, we have seen theorems of the form "A matrix has property X if and only if it is an invertible matrix". In this post, we will bring these theorems into one place, and introduce a few more, in order to form a set of statements that all can be used to define an invertible matrix. We will also show that each of these statements imply all of the rest of the statemetns. Put together, these statements form what is called the **invertible matrix theorem**. Not only does this theorem provide a [multi-angled perspective](https://mbernste.github.io/posts/understanding_3d/) into the nature of invertible matrices, it is also practically useful because if one has some matrix, $\boldsymbol{A}$, then one needs only to prove a single one of the statements in the invertible matrix theorem in order to learn that _all of the remaining statements_ of the invertible matrix theorem are also true of the matrix. 

The invertible matrix therorem
------------------------------

The invertible matrix theorem is stated as follows:

<span style="color:#0060C6">**Theorem 1**: A square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ is an invertible matrix if and only if _any_ of the following statements hold:</span>

<center><span style="color:#0060C6">1. There exists a square matrix $\boldsymbol{C} \in \in \mathbb{R}^{n \times n}$ such that $\boldsymbo{AC} = \boldsymbo{CA} = \boldsymbol{I}$</span></center>

<center><span style="color:#0060C6">2. The columns of $\boldsymbol{A}$ are linearly independent</span></center>

<center><span style="color:#0060C6">3. The rows of $\boldsymbol{A}$ are linearly independent</span></center>

<center><span style="color:#0060C6">4. The columns of $\boldsymbol{A}$ span all of $\boldsymbol{R}^n$</span></center>

<center><span style="color:#0060C6">5. The rows of $\boldsymbol{A}$ span all of $\boldsymbol{R}^n$</span></center>

<center><span style="color:#0060C6">6. $\boldsymbo{A}^T$  is an invertible matrix</span></center>

<center><span style="color:#0060C6">7. The rank of $\boldsymbol{A}$ is $n$</span></center>

<center><span style="color:#0060C6">8. The linear transformation $T(\boldsymbol{x}) := \boldsymbol{Ax}$ is one-to-one and onto.</span></center>

<center><span style="color:#0060C6">9. The equation $\boldsymbol{Ax} = \boldsymbol{0}$ has only the trivial solution $\boldsymbol{x} = \boldsymbol{0}$</span></center>

<center><span style="color:#0060C6">10. It is possible to use the row reduction algorithm to transform $\boldsymbol{A}$ into $\boldsymbol{I}$</span></center>

<center><span style="color:#0060C6">11. There exists a sequence of elementary matrices $\boldsymbol{E}_1, \boldsymbol{E}_2, \dots, \boldsymbol{E}_m$ such that $\boldsymbol{A}\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_m = \boldsymbol{I}$</span></center>

<center><span style="color:#0060C6">12. $\text{Det}(\boldsymbol{A}) > 0$</span></center>

Note: in different texts, the invertible matrix theorem can be written somewhat differently with some texts including some statements that others don't. The _essence_ of the invertible matrix theorem is that there are many seemingly different statements that all define an invertible matrix. Any of these statements imply all of the rest.

To prove that any one of these statements imply all of the rest, we will prove the following relationships between these statements:



