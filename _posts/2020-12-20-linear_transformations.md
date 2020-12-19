---
title: 'Intuiting linear transformations'
date: 2020-12-20
permalink: /posts/linear_transformations/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - linear transformation
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
-----------
In a [previous post](), we discussed how when we define matrix-vector multiplication, matrices can be viewed as functions between vector spaces. In fact, matrices represent a very specific type of function: a **linear transformation**.

So what exactly is a linear transformation? As we'll soon see, linear transformations have a pretty simply definition, but think this definition does not do well at illuminating what linear transformations really do geometrically.  In this post, we will define linear transformations and show that linear transformations are capable of stretching and rotating objects, but they are incapable of "warping" objects.  Hopefully this makes more sense as we dig into the details.

Definition
---------

A linear transformation is a function that maps vectors from one vector space to vectors in another vector space such that it preserves scaler multiplication and vector addition. Specifically, a linear transformation is defined as follows:

<span style="color:#0060C6">**Definition 1 (Linear transformation):** Given vector spaces $(\mathcal{V}, \mathcal{F})$ and $(\mathcal{U}, \mathcal{F})$, a function $T : \mathcal{V} \rightarrow \mathcal{U}$ is a \textbf{linear transformation}, or \textbf{linear}, if for all $\bold{u}, \bold{v} \in \mathcal{V}$ and all scalars $c \in \mathcal{F}$,</span>

<center><span style="color:#0060C6">$$T(\bold{u} + \bold{v}) = T(\bold{u}) + T(\bold{v})$$</span></center>

<span style="color:#0060C6">and</span>

<center><span style="color:#0060C6">$$T(c\bold{u}) = cT(\bold{u})$$.</span></center>
