---
title: 'Matrices linear transformations'
date: 2020-12-20
permalink: /posts/matrices_linear_transformations/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - linear transformation
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
-----------
In a [previous post](https://mbernste.github.io/posts/matrix_vector_mult/), we discussed the definition of matrix-vector multiplication enables us to view matrices as functions between vector spaces. As we'll show in this post, matrices represent a very specific type of function: a **linear transformation**.


Definition
---------

A linear transformation is a function that maps vectors from one vector space to vectors in another vector space such that it preserves scaler multiplication and vector addition. Specifically, a linear transformation is defined as follows:

<span style="color:#0060C6">**Definition 1 (Linear transformation):** Given vector spaces $(\mathcal{V}, \mathcal{F})$ and $(\mathcal{U}, \mathcal{F})$, a function $T : \mathcal{V} \rightarrow \mathcal{U}$ is a \textbf{linear transformation}, or \textbf{linear}, if for all $\boldsymbol{u}, \boldsymbol{v} \in \mathcal{V}$ and all scalars $c \in \mathcal{F}$,</span>

<center><span style="color:#0060C6">$$T(\boldsymbol{u} + \boldsymbol{v}) = T(\boldsymbol{u}) + T(\boldsymbol{v})$$</span></center>

<span style="color:#0060C6">and</span>

<center><span style="color:#0060C6">$$T(c\boldsymbol{u}) = cT(\boldsymbol{u})$$</span></center>
