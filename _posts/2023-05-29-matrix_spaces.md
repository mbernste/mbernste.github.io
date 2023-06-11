---
title: 'The spaces defined by matrices: column spaces, rows spaces, and null spaces'
date: 2023-05-29
permalink: /posts/matrixspaces/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------


Matrices are one of the fundamental objects studied in linear algebra. While on their surface they appear like simple tables of numbers, [as we have previously described](https://mbernste.github.io/posts/matrices/), there are many ways to view matrices that reveal them to be quite deep: Matrices are at once tables of numbers, sets of vectors, and perhaps most importantly, [linear functions between vector spaces](https://mbernste.github.io/posts/matrices_linear_transformations/). 

In this post, we will further dive into the deeper structures within matrices by showing three vector spaces that are implicitly defined by every matrix:
1. A column space
2. A row space
3. A null space

These spaces are not difficult to define; however the relationships between them are not so obvious. In this post, we will then discuss the properties of these spaces, their relationships to one another, and how their properties determine whether or not a matrix is [invertible or singular](https://mbernste.github.io/posts/inverse_matrices/). 

The column space and row space of a matrix
------------------------------------------

The **column space** of a matrix is simply the [vector space](https://mbernste.github.io/posts/vector_spaces/) [spanned](https://mbernste.github.io/posts/linear_independence/) by the column-vectors of a matrix. Likewise, the **row space** of a matrix is the vector space spanned by the row-vectors of a matrix. Specifically,

<span style="color:#0060C6">**Definition 1 (column space):** Given a matrix $\boldsymbol{A}$, the **column space** of $\boldsymbol{A}$, is the vector space that spans the column-vectors of $\boldsymbol{A}$</span>

<span style="color:#0060C6">**Definition 2 (row space):** Given a matrix $\boldsymbol{A}$, the **column space** of $\boldsymbol{A}$, is the vector space that spans the row-vectors of $\boldsymbol{A}$</span>

**Row space**

Let's use the following matrix as an example:

$$\begin{bmatrix}1 & 2 & 1 \\ 0 & 1 & -1\end{bmatrix}$$

This matrix can be thought about as a collection of two three-dimensional row vectors (The dotted lines are visualization guides. The colored dashed lines trace each vector to the $$z = 0$$ plane. The black dashed lines depict the difference between the two vectors on the $$z=0$$ plane.):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_row_vectors.png" alt="drawing" width="600"/></center>

The row space is then the vector space that is spanned by these two vectors. We see that in this case, the row space is a hyperplane:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_row_space.png" alt="drawing" width="350"/></center>

**Column space**

This example matrix can instead be thought about as a collection of three two-dimensional column vectors:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_column_vectors.png" alt="drawing" width="600"/></center>

The column space is then the vector space that is spanned by these three vectors. We see that in this case, the column space is all of $\mathbb{R}^2$ since we can form _any_ two-dimensional vector using a linear combination of these three vectors:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_column_space.png" alt="drawing" width="350"/></center>

For a more in depth discussion of the concept of **span**, see my [previous blog post](https://mbernste.github.io/posts/linear_independence/).


Rank: the intrinsic dimensionality of the column space and row space
--------------------------------------------------------------------

In the previous example matrix, we notice that the row space could be described by a hyperplane in $\mathbb{R}^3$ and thus, it's [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/) is only two. The column space spanned all of $\mathbb{R}^2$ and thus, it's intrinsic dimensionality is two as well. Even though there are three column-vectors, the dimensionality of the space spanned by these three vectors is only two. The intrinsic dimensionality of a set of vectors is given by the maximal number of linearly independent vectors in a set of vectors. With this in mind, we can form the following definitions:

<span style="color:#0060C6">**Definition 3 (column rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the **column rank** of $\boldsymbol{A}$ is the maximum sized subset of the columns of $\boldsymbol{A}$ that are linearly independent.</span>

<span style="color:#0060C6">**Definition 4 (row rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the **rank** of $\boldsymbol{A}$ is the maximum sized subset of the rows of $\boldsymbol{A}$ that are linearly independent.</span>

In this example, we saw that the column rank and the row rank are equal. Is this true for any matrix? It turns out that the anwswer is yes! *The intrinsic dimensionality of the row space and column space are always equal*. Moreover, we call the instrinsic dimensionality of the row space and column space as simply the **rank** of the matrix, without need of delineating whether we mean the row rank or the column rank. We can formalize this statement with the following theorem (proved in the Appendix to this post):

<span style="color:#0060C6">**Theorem 1 (row rank equals column rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, its row rank equals its column rank.</span>

The null space
--------------

Recall that a matrix, $\boldsymbol{A} \in \mathbb{R}^{m \times n}$ can be undestood to be a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/) from $\mathbb{R}^n$ to $\mathbb{R}^m$.

Nullity: the intrinsic dimensionality of the null space
-------------------------------------------------------

The null space is the orthogonal complement to the row space
------------------------------------------------------------

The spaces induced by invertible matrices
-----------------------------------------

Appendix
--------

<span style="color:#0060C6">**Theorem 1 (row rank equals column rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the row rank equals the column rank</span>

**Proof:**

Let $r_c$ be the column-rank of $\boldsymbol{A}$. Then, this means that there exists a set of basis vectors, $\{\boldsymbol{b}_1, \dots, \boldsymbol{b}_{r_c} \}$ that span the columns of $\boldsymbol{A}$. Let's encode these basis vectors into a matrix where each basis vector is a column-vector:

$$\boldsymbol{B} := \begin{bmatrix} \boldsymbol{b}_1 & \dots & \boldsymbol{b}_{r_c} \end{bmatrix}$$



$\square$


