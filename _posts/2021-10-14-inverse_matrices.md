---
title: 'Invertible Matrices'
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

<span style="color:#0060C6">**Definition 1 (Inverse matrix):** Given a square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, it's **inverse matrix** is the matrix $\boldsymbol{C}$ that when either left or right multiplied by $\boldsymbol{A}$, yields the identity matrix. That is, if for a matrix $\boldsymbol{C}$ it holds that $$\boldsymbol{AC} = \boldsymbol{CA} = \boldsymbol{I}$$, then $\boldsymbol{C}$ is the inverse of $\boldsymbol{A}$.</span>
  
This definition might seem a bit of opaque, so in the remainder of this blog post we will explore a number of  [complimentary perspectives](https://mbernste.github.io/posts/understanding_3d/) for viewing inverse matrices: 

1. An invertible matrix characterizes an invertible linear transformation 
2. An invertible matrix preserves information 
3. An invertible matrix preserves the dimensionality of transformed vectors 
4. An invertible matrix computes a change of coordinates for a vector space 

An invertible matrix characterizes an invertible linear transformation
-----------------------------------------------------------------------

Any matrix $\boldsymbol{A}$ for which there exists an inverse matrix $\boldsymbol{A}^{-1}$ characterizes an invertible linear transformation. That is given an invertible matrix $\boldsymbol{A}$, the linear transformation $$T(\boldsymbol{x}) := \boldsymbol{Ax}$$ has an inverse linear transformation $T^{-1}(\boldsymbol{x})$. Recall, for a function to be invertible it must be both [onto](https://en.wikipedia.org/wiki/Surjective_function) and [one-to-one](https://en.wikipedia.org/wiki/Injective_function). We show in the Appendix to this blog post that $T(\boldsymbol{x})$ defined using an invertible matrix $\boldsymbol{A}$ is both onto (Theorem 2) and one-to-one (Theorem 3).

At a more intuitive level, the inverse of a matrix $\boldsymbol{A}$ is the matrix that ``reverts" vectors transformed by $\boldsymbol{A}$ back to their original vectors (Figure~\ref{fig:inverse_matrix}). Thus, since matrix multiplication encodes a composition of the matrices' linear transformations, it follows that a matrix multiplied by its inverse yields the identity matrix $\boldsymbol{I}$, which characterizes the linear transformation that maps vectors back to themselves. This observation allows us to rigorously define the inverse of a matrix $\boldsymbol{A}$ as the matrix that when multiplied by $\boldsymbol{A}^{-1}$ yields the identity matrix.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_inverse.png" alt="drawing" width="500"/></center>

An invertible matrix preserves information
------------------------------------------

The transformation carried out by an invertible matrix $\boldsymbol{A}$ can be ``reverted." That is, let $\boldsymbol{b}$ be the vector that results from transforming $\boldsymbol{x}$ with $\boldsymbol{A}$. We can recover the original $\boldsymbol{x}$ by multiplying $\boldsymbol{b}$ by $\boldsymbol{A}^{-1}$: 

$$\begin{align*} \boldsymbol{b} := \boldsymbol{Ax} \\ \implies \boldsymbol{A}^{-1}\boldsymbol{b} = \boldsymbol{A}^{-1}\boldsymbol{Ax} \\ \implies \boldsymbol{x} = \boldsymbol{A}^{-1}\boldsymbol{b} \end{align*}$$

Inherently, $\boldsymbol{A}$ preserves all of the information of $\boldsymbol{x}$ in $\boldsymbol{b}$ as evidenced by the fact that we can recover $\boldsymbol{x}$ from $\boldsymbol{b}$ via $\boldsymbol{A}^{-1}$. If, on the other hand, $\boldsymbol{A}$ is singular, then we cannot recover $\boldsymbol{x}$ from $\boldsymbol{b}$. Intuitively, information about $\boldsymbol{x}$ is lost in the transformation into $\boldsymbol{b}$.


A singular matrix collapses vectors into a lower-dimensional subspace
---------------------------------------------------------------------

The loss of information described in the previous section can be viewed geometrically by the fact that a singular matrix "collapses" or "compresses" vectors into an intrinsically lower dimensional space. That is, a singular matrix reduces the [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/) of the vectors. The loss of these dimensions constitutes the "loss of information" discussed in the previous section.

A matrix is invertible if and only if its columns are linearly independent (See Thoerem XXXXX in the Appendix to this post). Recall a set of $n$ linearly independent vectors $$S := {\boldsymbol{x}_1, \dots, \boldsymbol{x}_n}$$ spans a space with an intrinsic dimensionality of $n$ because in order to specify any vector $\bold{b}$ in the vector space, one must specify the coefficients $c_1, \dots, c_n$ such that $$\boldsymbol{b} = c_1\boldsymbol{x}_1 + \dots + c_n\boldsymbol{x}_n$$ However, if $S$ is not linearly independent, then we can throw away ``redundant" vectors in $S$ that can be constructed from the remaining vectors. Thus, the intrinsic dimensionality of a linearly dependent set $S$ is the maximum sized subset of $S$ that is linearly independent.

When a matrix $\boldsymbol{A}$ is singular, its columns are linearly dependent and thus, the vectors that constitute the column space of the matrix is inherently of lower dimension that the number of columns. Thus, when $\boldsymbol{A}$ multiplies a vector $\boldsymbol{x}$, it transforms $\boldsymbol{x}$ into this lower dimensional space. Once transformed, there is no way to transform it back to its original vector because certain dimensions of the vector were ``lost" in this transformation.

To make this more concrete, an example of this phenomenon can be seen in Figure~\ref{fig:inverse_matrix}. In Figure~\ref{fig:inverse_matrix}, a singular matrix $\bold{A} \in \mathbb{R}^{3 \times 3}$ maps vectors in $\mathbb{R}^3$ to vectors that lie on a plane in $\mathbb{R}^3$. All vectors on a plane in $\mathbb{R}^3$ are of intrinsic dimensionality of two rather than three because we only need to specify coefficients for two of the column vectors in $\mathbb{A}$ to specify a point on the plane. We can throw away the third. Thus, we see that this singular matrix collapses points from the full 3-dimensional space $\mathbb{R}^3$ to the 2-dimensional space on the plane spanned by the columns of $\mathbb{A}$.

\begin{figure}[htbp] \centering \includegraphics[scale=0.3]{matrix_inverse_lin_ind.png}
\caption{(A) The column vectors of a matrix $\bold{A} \in \mathbb{R}^{3 \times 3}$. (B) One solution to the equation $\bold{Ax} = \bold{b}$. (C) Another solution to $\bold{Ax} = \bold{b}$. That is, there are multiple $\bold{x} \in \mathbb{R}^3$ that map to $\bold{b}$. Thus, there does not exist an inverse mapping and therefore no inverse matrix to $\bold{A}$. These multiple constructions of mappings from $\mathbb{R}^3$ to $\bold{b}$ arise directly from the fact that the columns of $\bold{A}$ are linearly dependent.} \label{fig:inverse_matrix} \end{figure}


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

 $$\begin{align*} \boldsymbol{Ax} - \boldsymbol{Ax}' &= \boldsymbol{0} \\ \implies \boldsymbol{A}(\boldsymbol{x} - \boldsymbol{x}') = 0\end{align*}$$
 
 By Theorem 1, it must hold that 
 
 $$\boldsymbol{x} - \boldsymbol{x}' = \boldsymbol{0}$$
 
which implies that $\boldsymbol{x} = \boldsymbol{x}'$. This contradicts our original assumption. Therefore, it must hold that there does not exist two vectors $\boldsymbol{x}$ and $\boldsymbol{x}'$ that map to the same vector via the invertible matrix $\boldsymbol{A}$.  Therefore, $\boldsymbol{A}$ encodes a one-to-one function.

$\square$









\subsubsection*{An invertible matrix computes a change of coordinates for a vector space}

A vector $\bold{x} \in \mathbb{R}^n$ can be viewed as the coordinates for a point in a coordinate system. That is, for each dimension $i$, the vector $\bold{x}$ provides a value along each dimension (e.g. $x_i$ is the value along dimension $i$). Of course, the coordinate system we use can be arbitrary. In Figure~\ref{fig:coordinate_change}, we can specify locations in $\bold{R}^2$ using either the grey coordinate system or the blue coordinate system. Furthermore, there is a one-to-one and onto mapping between coordinates in each of these two alternative coordinate systems. The point $\bold{x}$ located at $[-4, -2]$ in the grey coordinate system can be described as $[-1, 1]$ according to the blue coordinate system.

All coordinate systems are, in some sense, equivalent in that each is able to provide an unambiguous location for points in the space. Nonetheless, it often helps to have some coordinate system that acts as a reference to every other coordinate system. This reference coordinate system is the defined by the standard basis vectors ${\bold{e}_1, \dots, \bold{e}_n }$. All other coordinate systems can then be constructed from this reference coordinate system. In Figure~\ref{fig:coordinate_change}, the reference coordinate system is depicted by the grey grid and is constructed by the orthonormal basis vectors $\bold{e}_1$ and $\bold{e}_2$. An alternative coordinate system is depicted by the blue grid and is constructed from the basis vectors $\bold{a}_1$ and $\bold{a}_2$.

An invertible matrix $\bold{A} := [\bold{a}_1, \dots, \bold{a}_n]$ can be viewed as an operator that converts vectors described in terms of the basis vectors ${\bold{a}_1, \dots, \bold{a}_n}$ back to a description in terms of the standard basis vectors ${\bold{e}_1, \dots, \bold{e}_n }$. That is, if we have some vector $\bold{x'} \in \mathbb{R}^n$, then $\bold{Ax'}$ can be understood to be the vector in the standard basis \textit{if} $\bold{x'}$ was described according to the basis formed by the columns of $\bold{A}$. Another way to think about this is that if we have some vector $\bold{x} \in \mathbb{R}^n$ described according to the standard basis, then we can describe $\bold{x}$ in terms of an alternative basis $\bold{a}_1, \dots, \bold{a}_n$ by multiplying $\bold{x}$ by the inverse of the matrix $\bold{A} := [ \bold{a}_1, \dots, \bold{a}n]$. That is $$\bold{x}\bold{A} := \bold{A}^{-1}\bold{x}$$ is the representation of $\bold{x}$ in terms of the basis columns of $\bold{A}$.

\begin{figure}[htbp] \centering \includegraphics[scale=0.3]{coordinate_change.png}
\caption{Here we have a vector $\bold{x} \in \mathbb{R}^2$. Using the standard basis vectors $\bold{e_1}, \bold{e_2}$, the vector $\bold{x}$ is given by $[-4, -2]$. Using the column vectors $\bold{a}1$ and $\bold{a}2$ of matrix $\bold{A}$ as a basis, this vector $\bold{x}{\bold{A}}$ is given by $[-1,1]$. The matrix $\bold{A}$ maps $\bold{x}\bold{A}$ to $\bold{x}$.} \label{fig:coordinate_change} \end{figure}
