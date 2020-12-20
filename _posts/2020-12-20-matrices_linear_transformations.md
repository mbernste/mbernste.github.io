---
title: 'Matrices as linear transformations'
date: 2020-12-21
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


Recall that we can view matrices as functions in the following sense: if we hold a matrix $\boldsymbol{A}  \in \mathbb{R}^{m \times n}$ as fixed, this matrix maps vectors in $\mathbb{R}^n$ to vectors in $\mathbb{R}^m$.  That is, we can define a function $T : \mathbb{R}^n \rightarrow \mathbb{R}^m$ as:

$$T(\boldsymbol{x}) := \boldsymbol{A}\boldsymbol{x}$$

Through this lense, let's look at a few common, "elementary" functions and determine their matrix:

**The identity matrix defines the identity function**

Recall an identity function $f$ for a set $S$ is the function $f(x) := x$ for all $x \in S$. In the context of a function $T$ over a vector space $\mathbb{R}^n$, the identity function $T(\boldsymbol{x}) := \boldsymbol{x}$ for all $\boldsymbol{x} \in \mathbb{R}^n$ is defined using the **identity matrix** for $\mathbb{R}^n$.  The identity matrix for $\mathbb{R}^n$, denoted $\boldsymbol{I}_n$ (or simply $\bold{I}$ if the dimensionality is implied by the context), is a square matrix of all zeros except for ones along the diagonal:  

<span style="color:#0060C6">**Definition (Identity matrix):** Each real-valued, Euclidean vector space $\mathbb{R}^n$ is associated with an **identity matrix**, denoted $\boldsymbol{I}_{n \times n}$ (or simply $\boldsymbol{I}$ if the dimensionality is implied by the context), which is a square matrix consisting of zeros in the off-diagonal entries and ones along the diagonal.</span>

For example, the identity matrix for $\mathbb{R}^3$ is defined as

$$\boldsymbol{I}_3 := \begin{bmatrix} 1 & 0  & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$  

It can easily be shown that applying matrix-vector multiplication using an identity matrix $\boldsymbol{I}_n$ with any vector $\boldsymbol{x} \in \mathbb{R}^n$ will result in the same vector $\bold{x}$.  Thus, a function $T(\bold{x}) := \bold{I}\bold{x}$ is the identity function for $\bold{R}^n$. 

**The zero matrix defines the zero function**

Recall a zero-function $f$ for a set $S$ is the function $f(x) := 0$ for all $x \in S$.  In the context of a function $T$ over a vector space $\mathbb{R}^n$, the zero function $T(\boldsymbol{x}) := \boldsymbol{0}$ for all $\boldsymbol{x} \in \mathbb{R}^n$ is defined using the **zero matrix** for $\mathbb{R}^n$.  The zero matrix for $\mathbb{R}^n$, denoted $\boldsymbol{0}_n$ is a square matrix of all zeros:

<span style="color:#0060C6">Each real-valued, Euclidean vector space $\mathbb{R}^n$ is associated with a **zero matrix**, denoted $\boldsymbol{0}_{n \times n}$, which is a square matrix consisting of all zeros.</span>

For example, the zero matrix for $\mathbb{R}^3$ is defined as
 $$\boldsymbol{0}_3 := \begin{bmatrix} 0 & 0  & 0\\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}$$
 
 It can easily be shown that applying matrix-vector multiplication using an identity matrix $\boldsymbol{0}_n$ with any vector $\boldsymbol{x} \in \mathbb{R}^n$ will result in the zero vector $\boldsymbol{0}$.  Thus, a function $T(\boldsymbol{x}) := \boldsymbol{0}_n\bold{x}$ is the zero function for $\mathbb{R}^n$. 


Linear transformations
---------

A linear transformation is a function that maps vectors from one vector space to vectors in another vector space such that it preserves scaler multiplication and vector addition. Specifically, a linear transformation is defined as follows:

<span style="color:#0060C6">**Definition 1 (Linear transformation):** Given vector spaces $(\mathcal{V}, \mathcal{F})$ and $(\mathcal{U}, \mathcal{F})$, a function $T : \mathcal{V} \rightarrow \mathcal{U}$ is a **linear transformation**, or is simply called **linear**, if for all $\boldsymbol{u}, \boldsymbol{v} \in \mathcal{V}$ and all scalars $c \in \mathcal{F}$,</span>

<center><span style="color:#0060C6">$$T(\boldsymbol{u} + \boldsymbol{v}) = T(\boldsymbol{u}) + T(\boldsymbol{v})$$</span></center>

<span style="color:#0060C6">and</span>

<center><span style="color:#0060C6">$$T(c\boldsymbol{u}) = cT(\boldsymbol{u})$$</span></center>

The figure below illustrates a linear transformation $T$ applied to three vectors (red, blue, and purple).  The vectors on the left are in $T$'s domain and the vectors on the right are in $T$'s range. The dotted lines connect each vector in the domain to its vector in the range as mapped by $T$.  Notice that the $T(\text{red}) + T(\text{blue}) = T(\text{red} + \text{blue})$.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_transform.png" alt="drawing" width="500"/></center>


Matrices perform linear transformations
----------



where $T$ uses the matrix $\boldsymbol{A}$ to performing the mapping.  As shown in Theorem 1 in the Appendix to this post, any function $T$ defined as a matrix multiplied by an input vector is a linear transformation.

Every linear transformation is characterized by a matrix
------------

Perhaps more interestingly, it turns out that *every* linear transformation between finite-dimensional vector spaces is defined by a unique matrix that performs the transformation.  That is, if I have two vector spaces in, say $\mathbb{R}^m$ and $\mathbb{R}^n$, and I have a linear transformation $T$ mapping vectors between them, then there exists a single unique matrix $\boldsymbol{A}$ that performs $T$'s mapping. That is, where $T(\boldsymbol{x}) = \boldsymbol{Ax}$. More specifically, $A$ is defined as:

$A := $

This matrix is called the **standard matrix** of $T$.  In fact, computing the standard matrix for $T$ is quite simple. It's simply:


The existence of the standard matrix for every $T$ is proven in Theorem 2 in the Appendix to this post.

This fact, that every linear transformation is characterized by a matrix, means that there is a one-to-one mapping between linear transformations and matrices.  Thus, in some sense, we can say that a matrix *is* is a linear transformation.

Common matrices viewed through the lense of functions
------------

Appendix
-----------

<span style="color:#0060C6">**Theorem (Matrices define linear transformations):** The function $T(\boldsymbol{x}) := \boldsymbol{Ax}$ is a linear transformation.</span>

**Proof:** We  show that for all $\boldsymbol{u}, \boldsymbol{v}$ in the domain of $T$ and for all scalars $c$, the following conditions hold:

1. $\boldsymbol{A}(\boldsymbol{u} + \boldsymbol{v}) = \boldsymbol{A}\boldsymbol{u} + \boldsymbol{A}\boldsymbol{v}$
2. $\boldsymbol{A}(c\boldsymbol{u}) = c(\boldsymbol{A}\boldsymbol{u})$

Proof of 1:

$$\begin{align*}\boldsymbol{A}(\boldsymbol{u} + \boldsymbol{v}) &= \boldsymbol{a}_{*,1}(u_1 + v_1) + \boldsymbol{a}_{*,2}(u_2 + v_2) + \dots + \boldsymbol{a}_{*,n}(u_n + v_n) \\ &= \boldsymbol{a}_{*,1}u_1 + \boldsymbol{a}_{*,1}v_1 + \boldsymbol{a}_{*,2}u_2 + \boldsymbol{a}_{*,2}v_2 + \dots + \boldsymbol{a}_{*,n}u_n + \boldsymbol{a}_{*,n}v_n \\ &= (\boldsymbol{a}_{*,1}u_1 + \boldsymbol{a}_{*,2}u_2 + \dots + \boldsymbol{a}_{*,n}u_n) + (\boldsymbol{a}_{*,1}v_1 + \boldsymbol{a}_{*,2}v_2 + \dots + \boldsymbol{a}_{*,n}v_n) \\ &= \boldsymbol{Au} + \boldsymbol{Av}\end{align*}$$

Proof of 2:

$$\begin{align*}\boldsymbol{A}(c\boldsymbol{u}) &= \boldsymbol{a}_{*,1}(cu_1) + \boldsymbol{a}_{*,2}(cu_2) + \dots + \boldsymbol{a}_{*,n}(cu_n) \\ &= c\boldsymbol{a}_{*,1}(u_1) + c\boldsymbol{a}_{*,2}(u_2) + \dots + c\boldsymbol{a}_{*,n}(u_n) \\ &= c(\boldsymbol{a}_{*,1}u_1 + \boldsymbol{a}_{*,2}u_2 + \dots + \boldsymbol{a}_{*,n}u_n) \\ &= c(\boldsymbol{Au})\end{align*}$$

