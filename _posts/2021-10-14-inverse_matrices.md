---
title: 'Invertible matrices'
date: 2021-10-13
permalink: /posts/inverse_matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
------------

As we have discussed in depth, matrices can viewed [as functions](https://mbernste.github.io/posts/matrices_as_functions/) between vector spaces. In this post, we will discuss matrices that represent **invertible functions**. Such matrices are called **invertible matrices** and their corresponding inverse function is characterized by an **inverse matrix**. 

More rigorously, the inverse matrix of a matrix $\boldsymbol{A}$ is defined as follows:

<span style="color:#0060C6">**Definition 1 (Inverse matrix):** Given a square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, it's **inverse matrix** is the matrix $\boldsymbol{C}$ that when either left or right multiplied by $\boldsymbol{A}$, yields the identity matrix. That is, if for a matrix $\boldsymbol{C}$ it holds that $$\boldsymbol{AC} = \boldsymbol{CA} = \boldsymbol{I}$$, then $\boldsymbol{C}$ is the inverse of $\boldsymbol{A}$. This inverse matrix, $\boldsymbol{C}$ is commonly denoted as $\boldsymbol{A}^{-1}$.</span>
  
This definition might seem a bit of opaque, so in the remainder of this blog post we will explore a number of  [complimentary perspectives](https://mbernste.github.io/posts/understanding_3d/) for viewing inverse matrices.

Intuition behind invertible matrices
------------------------------------

Here are three ways to understand invertible matrices:

1. An invertible matrix characterizes an invertible linear transformation 
2. An invertible matrix preserves the dimensionality of transformed vectors 
3. An invertible matrix computes a change of coordinates for a vector space 

Below we will explore each of these.

**1. An invertible matrix characterizes an invertible linear transformation**

Any matrix $\boldsymbol{A}$ for which there exists an inverse matrix $\boldsymbol{A}^{-1}$ characterizes an invertible linear transformation. That is, given an invertible matrix $\boldsymbol{A}$, the linear transformation $$T(\boldsymbol{x}) := \boldsymbol{Ax}$$ has an inverse linear transformation $T^{-1}(\boldsymbol{x})$ defined as $T^{-1}(\boldsymbol{x}) := \boldsymbol{A}^{-1}\boldsymbol{x}$. 

Recall, for a function to be invertible it must be both [onto](https://en.wikipedia.org/wiki/Surjective_function) and [one-to-one](https://en.wikipedia.org/wiki/Injective_function). We show in the Appendix to this blog post that if $\boldsymbol{A}$  is invertible, then $T(\boldsymbol{x})$ defined using an invertible matrix $\boldsymbol{A}$ is both onto (Theorem 2) and one-to-one (Theorem 3).

At a more intuitive level, the inverse of a matrix $\boldsymbol{A}$ is the matrix that "reverts" vectors transformed by $\boldsymbol{A}$ back to their original vectors:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_inverse.png" alt="drawing" width="500"/></center>

Thus, since matrix multiplication encodes a composition of the matrices' linear transformations, it follows that a matrix multiplied by its inverse yields the identity matrix $\boldsymbol{I}$, which characterizes the linear transformation that maps vectors back to themselves. This observation allows us to rigorously define the inverse of a matrix $\boldsymbol{A}$ as the matrix that when multiplied by $\boldsymbol{A}^{-1}$ yields the identity matrix.


**2. A singular matrix collapses vectors into a lower-dimensional subspace**

A singular matrix "collapses" or "compresses" vectors into an intrinsically lower dimensional space whereas an invertible matrix preserves their [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/) of the vectors.

This follows from the fact that a matrix is invertible if and only if its columns are linearly independent (Thoerem XXXXX in the Appendix). Recall a set of $n$ linearly independent vectors $$S := \{ \boldsymbol{x}_1, \dots, \boldsymbol{x}_n \}$$ spans a space with an intrinsic dimensionality of $n$ because in order to specify any vector $\boldsymbol{b}$ in the vector space, one must specify the coefficients $c_1, \dots, c_n$ such that 

$$\boldsymbol{b} = c_1\boldsymbol{x}_1 + \dots + c_n\boldsymbol{x}_n$$ 

However, if $S$ is not linearly independent, then we can throw away "redundant" vectors in $S$ that can be constructed from the remaining vectors. Thus, the intrinsic dimensionality of a linearly dependent set $S$ is the maximum sized subset of $S$ that is linearly independent.

When a matrix $\boldsymbol{A}$ is singular, its columns are linearly dependent and thus, the vectors that constitute the column space of the matrix is inherently of lower dimension than the number of columns. Thus, when $\boldsymbol{A}$ multiplies a vector $\boldsymbol{x}$, it transforms $\boldsymbol{x}$ into this lower dimensional space. Once transformed, there is no way to transform it back to its original vector because certain dimensions of the vector were "lost" in this transformation.

To make this more concrete, an example is shown in below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_inverse_lin_ind.png" alt="drawing" width="1000"/></center>

In Panel A of this figure, we show the column vectors of a matrix $\boldsymbol{A} \in \mathbb{R}^{3 \times 3}$ that span a plane. In Panel B, we show the solution to the equation $\boldsymbol{Ax} = \boldsymbol{b}$. In Panel C, we show another solution to $\boldsymbol{Ax} = \boldsymbol{b}$. Notice that there are multiple vectors in $\mathbb{R}^3$ that $$\boldsymbol{A}$$ maps to $\boldsymbol{b}$. Thus, there does not exist an inverse mapping and therefore no inverse matrix to $\boldsymbol{A}$. These multiple mappings from $\mathbb{R}^3$ to $\boldsymbol{b}$ arise directly from the fact that the columns of $\boldsymbol{A}$ are linearly dependent.

Also notice that this singular matrix maps vectors in $\mathbb{R}^3$ to vectors that lie on the plane in $\mathbb{R}^3$ that are spanned by its column vectors. All vectors on a plane in $\mathbb{R}^3$ are of intrinsic dimensionality of two rather than three because we only need to specify coefficients for two of the column vectors in $\boldsymbol{A}$ to specify a point on the plane. We can throw away the third. Thus, we see that this singular matrix collapses points from the full 3-dimensional space $\mathbb{R}^3$ to the 2-dimensional space on the plane spanned by the columns of $\boldsymbol{A}$.


**3. An invertible matrix computes a change of coordinates for a vector space**

A vector $\boldsymbol{x} \in \mathbb{R}^n$ can be viewed as the coordinates for a point in a coordinate system. That is, for each dimension $i$, the vector $\boldsymbol{x}$ provides a value along each dimension -- that is, $x_i$ is the value along dimension $i$. The coordinate system we use is, in a mathematical sense, arbitrary. To see why it's arbitrary, notice in the figure below that we can specify locations in $\mathbb{R}^2$ using either the grey coordinate system or the blue coordinate system:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/coordinate_change.png" alt="drawing" width="600"/></center>

We see that there is a one-to-one and onto mapping between coordinates in each of these two alternative coordinate systems. The point $\boldsymbol{x}$ is located at $[-4, -2]$ in the grey coordinate system and as $[-1, 1]$ in the blue coordinate system.

Thus we see that all coordinate systems are able to provide an unambiguous location for points in the space and thus, there is a one-to-one and onto mapping between them. Nonetheless, it often helps to have some coordinate system that acts as a reference to every other coordinate system. This reference coordinate system is usually defined by the standard basis vectors ${\boldsymbol{e}_1, \dots, \boldsymbol{e}_n }$ where $\boldsymbol{e}_i$ consists of all zeros except for a one at index $i$.

All coordinate systems can then be constructed from the coordinate system defined by the standard basis vectors. This is depicted in the previous figure in which the reference coordinate system is depicted by the grey grid and is constructed by the orthonormal basis vectors $\boldsymbol{e}_1$ and $\boldsymbol{e}_2$. An alternative coordinate system is depicted by the blue grid and is constructed from the basis vectors $\boldsymbol{a}_1$ and $\boldsymbol{a}_2$.

Now, how do invertible matrices enter the picture? Well, an invertible matrix $\boldsymbol{A} := [\boldsymbol{a}_1, \dots, \boldsymbol{a}_n]$ can be viewed as an operator that converts vectors described in terms of some set of basis vectors ${\boldsymbol{a}_1, \dots, \boldsymbol{a}_n}$ back to a description in terms of the standard basis vectors ${\boldsymbol{e}_1, \dots, \boldsymbol{e}_n }$. 

That is, if we have some vector $\boldsymbol{x'} \in \mathbb{R}^n$, then $\boldsymbol{Ax'}$ can be understood to be the vector in the standard basis *if* $\boldsymbol{x'}$ was described according to the basis formed by the columns of $\boldsymbol{A}$. Another way to think about this is that if we have some vector $\boldsymbol{x} \in \mathbb{R}^n$ described according to the standard basis, then we can describe $\boldsymbol{x}$ in terms of an alternative basis $\boldsymbol{a}_1, \dots, \boldsymbol{a}_n$ by multiplying $\boldsymbol{x}$ by the inverse of the matrix $\boldsymbol{A} := [ \boldsymbol{a}_1, \dots, \boldsymbol{a}n]$. That is $$\boldsymbol{x}\boldsymbol{A} := \boldsymbol{A}^{-1}\boldsymbol{x}$$ is the representation of $\boldsymbol{x}$ in terms of the basis columns of $\boldsymbol{A}$.

Properties
----------
 
Below we discuss several properties of invertible matrices that provide more intuition into how they behave and also provide algebraic rules that can be used in derivations.

1. **The columns of an invertible matrix are linearly independent** (Theorem~\ref{thrm:cols_inverse_lin_ind}). 
2. **Taking the inverse of an inverse matrix gives you back the original matrix**  (Theorem~\ref{thrm:inv_of_inv_mat}). Given an invertible matrix $\bold{A}$ with inverse $\bold{A}^{-1}$, it follows from Definition~\ref{def:inverse_matrix}, that $\bold{A}^{-1}$ is also invertible with inverse $\bold{A}$.  That is, 
$$(\bold{A}^{-1})^{-1} = \bold{A}$$
This also follows from the fact that the inverse of an inverse function $f^{-1}$ is simply the original function $f$.
3. **The result of multiplying invertible matrices is invertible** (Theorem~\ref{thrm:comp_inv_matrices}). Given two matrices $\bold{A}, \bold{B} \in \mathbb{R}^{n \times n}$, the matrix that results from their multiplication is invertible. That is, $\bold{AB}$ is invertible and its inverse is given by 
$$(\bold{AB})^{-1} = \bold{B}^{-1}\bold{A}^{-1}$$
Recall the result of matrix multiplication results in a matrix that characterizes the composition of the linear transformations characterized by the factor matrices. That is, $\bold{ABx}$ first transforms $\bold{x}$ with $\bold{B}$ and then transforms the result with $\bold{A}$.  It follows that in order to invert this composition of transformations, one must first pass the vector through $\bold{B}^{-1}$ and then through $\bold{A}^{-1}$.

\begin{figure}[htbp]
\centering
\includegraphics[scale=0.4]{inverse_matrix_mult.png}  
\caption{Demonstrating schematically why $(\bold{AB})^{-1} = \bold{B}^{-1}\bold{A}^{-1}$. The matrix $\bold{AB}$ first applies the mapping by $\bold{B}$ and then applies the mapping by $\bold{A}$.  The inverse of this function would thus entails applying the inverse of $\bold{A}$ followed by the inverse of $\bold{B}$.}
\label{fig:inverse_matrix}
\end{figure} 

Appendix
--------

<span style="color:#0060C6">**Theorem 1 (Null space of an invertible matrix):** The null space of an invertible matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ consists of only the zero vector $\boldsymbol{0}$.</span>

**Proof:**

We must prove that
 
$$\boldsymbol{Ax} = \boldsymbol{0}$$
 
has only the trivial solution $\boldsymbol{x} := \boldsymbol{0}$.
 
$$\begin{align*}\boldsymbol{Ax} &= \boldsymbol{0} \\ \implies \boldsymbol{A}^{-1}\boldsymbol{Ax} &= \boldsymbol{A}^{-1}\boldsymbol{0} \\ \implies \boldsymbol{x} &= \boldsymbol{0} \end{align*}$$

$\square$

<span style="color:#0060C6">**Theorem 2 (Invertible matrices characterize onto functions):** An invertible matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ characterizes an onto linear transformation. </span>

**Proof:**

Let $\boldsymbol{x}$, $\boldsymbol{b} \in \mathbb{R}^n$.  Then, there exists a vector, $\boldsymbol{x} \in \mathbb{R}^n$ such that
$$\boldsymbol{Ax} = \boldsymbol{b}$$
This solution is precisely 

$$\boldsymbol{x} := \boldsymbol{A}^{-1}\boldsymbol{b}$$

as we see below:

$$\begin{align*}&\boldsymbol{A}(\boldsymbol{A}^{-1}\boldsymbol{b}) = \boldsymbol{b} \\ \implies & (\boldsymbol{AA}^{-1})\boldsymbol{b} = \boldsymbol{b} && \text{associative law} \\ \implies & \boldsymbol{I}\boldsymbol{b} = \boldsymbol{b} && \text{definition of inverse matrix} \\ \implies & \boldsymbol{b} = \boldsymbol{b} \end{align*}$$

$\square$
 
<span style="color:#0060C6">**Theorem 3 (Invertible matrices characterize one-to-one functions):** A an invertible matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ characterizes a one-to-one linear transformation.</span>

**Proof:**

For the sake of contradiction assume that there exists two vectors $\boldsymbol{x}$ and $\boldsymbol{x}'$ such that $\boldsymbol{x} \neq \boldsymbol{x}'$ and that 
 $$\boldsymbol{Ax} = \boldsymbol{b}$$
 and
 $$\boldsymbol{Ax}' = \boldsymbol{b}$$
 where $b \neq \boldsymbol{0}$.  Then,

 $$\begin{align*} \boldsymbol{Ax} - \boldsymbol{Ax}' &= \boldsymbol{0} \\ \implies \boldsymbol{A}(\boldsymbol{x} - \boldsymbol{x}') = \boldsymbol{0}\end{align*}$$
 
 By Theorem 1, it must hold that 
 
 $$\boldsymbol{x} - \boldsymbol{x}' = \boldsymbol{0}$$
 
which implies that $\boldsymbol{x} = \boldsymbol{x}'$. This contradicts our original assumption. Therefore, it must hold that there does not exist two vectors $\boldsymbol{x}$ and $\boldsymbol{x}'$ that map to the same vector via the invertible matrix $\boldsymbol{A}$.  Therefore, $\boldsymbol{A}$ encodes a one-to-one function.

$\square$



<span style="color:#0060C6">**Theorem 4 (Column vectors of invertible matrices are linearly independent):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$,
$\boldsymbol{A}$ is invertible if and only if $\{ \boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,n} \}$ are linearly independent. </span>

**Proof:**

We first prove the $\implies$ direction: we assume that $\boldsymbol{A}$ is invertible and show that under this assumption, the only solution to
$$\boldsymbol{a}_{*,1}x_1 + \dots + \boldsymbol{a}_{*,n}x_n = \boldsymbol{0}$$
is $\boldsymbol{x} := \boldsymbol{0}$, which is the condition for linear independence.

$$\begin{align*}\boldsymbol{a}_{*,1}x_1 + \dots + \boldsymbol{a}_{*,n}x_n &= \boldsymbol{0} \\ \implies \boldsymbol{Ax} &= \boldsymbol{0} \\ \implies \boldsymbol{A}^{-1}\boldsymbol{Ax} &= \boldsymbol{A}^{-1}\boldsymbol{0} \\ \implies \boldsymbol{x} &= \boldsymbol{0} \end{align*}$$

We now prove the $\impliedby$ direction: we assume the columns of $\boldsymbol{A}$ are linearly independent and show that under this assumption there exists a matrix $\boldsymbol{C}$ such that

$$\boldsymbol{CA} = \boldsymbol{AC} = \boldsymbol{I}$$

Since the columns of $\boldsymbol{A}$ are linearly independent, then the reduced row echelon form of $\boldsymbol{A}$ has a pivot in every column. This means that there exists a sequence of elementary row matrices $\boldsymbol{E}_1, \dots, \boldsymbol{E}_k$ such that when multiplied by $\boldsymbol{A}$, they produce the identity matrix. That is,
$$(\boldsymbol{E}_1\dots\boldsymbol{E}_k)\boldsymbol{A} = \boldsymbol{I}$$

Though not proven formally, it can be seen that elementary row matrices are invertible.  That is, you can always ``undo" the transformation imposed by an elementary row matrix (e.g. for an elementary row matrix that swaps rows, you can always swap them back). Furthermore, since the product of invertible matrices is also invertible, $(\boldsymbol{E}_1\dots\boldsymbol{E}_k)$ is invertible. Thus,

$$\begin{align*} & (\boldsymbol{E}_1\dots\boldsymbol{E}_k)\boldsymbol{A} = \boldsymbol{I} \\ \implies & (\boldsymbol{E}_1\dots\boldsymbol{E}_k)^{-1} (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)\boldsymbol{A} = (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1}\boldsymbol{I} \\ \implies & \boldsymbol{A} = (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1} \boldsymbol{I} \\ \implies & \boldsymbol{A} = \boldsymbol{I}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1} \\ \implies & \boldsymbol{A}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k) = \boldsymbol{I}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k) \end{align*}$$ 

Hence, $\boldsymbol{C} := (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)$ is the matrix for which $\boldsymbol{AC} = \boldsymbol{CA} = \boldsymbol{I}$ and is thus $\boldsymbol{A}$'s inverse.

$\square$








