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

Column spaces, row spaces, and null spaces of a matrix
------------------------------------------------------

**Row space**

The **row space** of a matrix is the vector space spanned by the row-vectors of a matrix. Specifically,

<span style="color:#0060C6">**Definition 1 (column space):** Given a matrix $\boldsymbol{A}$, the **column space** of $\boldsymbol{A}$, is the vector space that spans the column-vectors of $\boldsymbol{A}$</span>

Let's use the following matrix as an example:

$$\begin{bmatrix}1 & 2 & 1 \\ 0 & 1 & -1\end{bmatrix}$$

This matrix can be thought about as a collection of two three-dimensional row vectors (The dotted lines are visualization guides. The colored dashed lines trace each vector to the $$z = 0$$ plane. The black dashed lines depict the difference between the two vectors on the $$z=0$$ plane.):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_row_vectors.png" alt="drawing" width="600"/></center>

The row space is then the vector space that is spanned by these two vectors. We see that in this case, the row space is a hyperplane:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_row_space.png" alt="drawing" width="350"/></center>

**Column space**

The **column space** of a matrix is simply the [vector space](https://mbernste.github.io/posts/vector_spaces/) [spanned](https://mbernste.github.io/posts/linear_independence/) by the column-vectors of a matrix. Likewise,

<span style="color:#0060C6">**Definition 2 (row space):** Given a matrix $\boldsymbol{A}$, the **column space** of $\boldsymbol{A}$, is the vector space that spans the row-vectors of $\boldsymbol{A}$</span>

Using the previous example matrix, we can view it as a collection of three two-dimensional column vectors:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_column_vectors.png" alt="drawing" width="600"/></center>

The column space is then the vector space that is spanned by these three vectors. We see that in this case, the column space is all of $\mathbb{R}^2$ since we can form _any_ two-dimensional vector using a linear combination of these three vectors:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_visualize_column_space.png" alt="drawing" width="350"/></center>

For a more in depth discussion of the concept of **span**, see my [previous blog post](https://mbernste.github.io/posts/linear_independence/).


**Null space**

Recall that a matrix, $\boldsymbol{A} \in \mathbb{R}^{m \times n}$ can be undestood to be a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/) from $\mathbb{R}^n$ to $\mathbb{R}^m$. With this concept of a matrix in mind, we can define another space on a matrix: the space of all vectors that $\boldsymbol{A}$ maps to the zero vector. This space is called the **null space**. That is, any vector, $\boldsymbol{v} \in \mathbb{R}^m$ for which $\boldsymbol{Av} = \boldsymbol{0}$ is in the null space of $\boldsymbol{A}$.

<span style="color:#0060C6">**Definition 5 (null space):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the **null space** of $\boldsymbol{A}$ is the set of vectors, $\{\boldsymbol{v} \in \mathbb{R}^m \mid \boldsymbol{Av} = \boldsymbol{0}\}$</span>r

On its surface, the null space seems unrelated to the row space and column spaces of a matrix; however, there is indeed a key relationship between the null space and the row space of a matrix: the null space is the **orthogonal complement** to the row space. 

Before going further, let us define the orthogonal complement. Given a vector space $(\mathcal{V}, \mathcal{F})$, the orthogonal complement is another vector space $(\mathcal{V}', \mathcal{F})$ such that all vectors in $\mathcal{V}'$ are orthogonal to all vectors in $\mathcal{V}$.

<span style="color:#0060C6">**Definition 6 (orthogonal complement):** Given two vector spaces $(\mathcal{V}, \mathcal{F})$ and $(\mathcal{V}', \mathcal{F})$ that share the same scalar field, each is an **orthogonal complement** to the other if $\forall \boldsymbol{v} \in \mathcal{V}, \ \forall \boldsymbol{v}' \in \mathcal{V}' \ \langle \boldsymbol{v}, \boldsymbol{v}' \rangle = 0$</span>

With this concept in mind, we can see that the null space is the orthogonal complement to the row space. To see this, recall that we can view matrix-vector multiplication between a matrix $\boldsymbol{A}$ and a vector $\boldsymbol{x}$ as the process of taking a dot product of each row of $\boldsymbol{A}$ with $\boldsymbol{x}$:

$$\boldsymbol{Ax} := \begin{bmatrix} \boldsymbol{a}_{1,*} \cdot \boldsymbol{x} \\ \boldsymbol{a}_{2,*} \cdot \boldsymbol{x} \\ \vdots \\ \boldsymbol{a}_{m,*} \cdot \boldsymbol{x} \end{bmatrix}$$

If $\boldsymbol{x}$ is in the null space of $\boldsymbol{A}$ then this means that $\boldsymbol{Ax} = \boldsymbol{0}$, which means that ever dot product shown above is zero. That is,

$$\begin{align*}\boldsymbol{Ax} &= \begin{bmatrix} \boldsymbol{a}_{1,*} \cdot \boldsymbol{x} \\ \boldsymbol{a}_{2,*} \cdot \boldsymbol{x} \\ \vdots \\ \boldsymbol{a}_{m,*} \cdot \boldsymbol{x} \end{bmatrix} \\ &= \begin{bmatrix} 0 \\ 0  \\ \vdots \\ 0 \end{bmatrix} \\ &= \boldsymbol{0} \end{align*}$$

Recall, the dot product between two vectors is zero means that the two vectors are orthogonal. Thus we see that if $\boldsymbol{x}$ is in the null space of $\boldsymbol{A}$ it _has_ to be orthogonal to every row-vector of $\boldsymbol{A}$. This means that the null space is the orthogonal complement to the row space!

With the example matrix that we have been using, we can visualize the null space as being all of the vectors that point along the red vector shown below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/null_space_compliment_row_space_1.png" alt="drawing" width="350"/></center>

Notice, that this red vector is orthogonal to the hyperplane that spans the row-vectors of $\boldsymbol{A}$. To illustrate another example, let's use a different example matrix:

$$\begin{bmatrix}1 & 2 & 1 \\ 0 & -0.5 & 0.5\end{bmatrix}$$

Here, the two row-vectors point in the same directions and thus, span a line in $\mathbb{R}^m$. The null space now is a hyperplane that is orthogonal to this line that spans the row-vectors!

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/null_space_compliment_row_space_2.png" alt="drawing" width="350"/></center>





Rank: the intrinsic dimensionality of the column space and row space
--------------------------------------------------------------------

In the previous example matrix, we notice that the row space could be described by a hyperplane in $\mathbb{R}^3$ and thus, it's [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/) is only two. The column space spanned all of $\mathbb{R}^2$ and thus, it's intrinsic dimensionality is two as well. Recall, the intrinsic dimensionality of a set of vectors is given by the maximal number of linearly independent vectors in the set. With this in mind, we can form the following definitions:

<span style="color:#0060C6">**Definition 3 (column rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the **column rank** of $\boldsymbol{A}$ is the maximum sized subset of the columns of $\boldsymbol{A}$ that are linearly independent.</span>

<span style="color:#0060C6">**Definition 4 (row rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the **row rank** of $\boldsymbol{A}$ is the maximum sized subset of the rows of $\boldsymbol{A}$ that are linearly independent.</span>

In this example, we saw that the column rank and the row rank are equal. Is this true for any matrix? It turns out that the anwswer is yes! *The intrinsic dimensionality of the row space and column space are always equal*. Moreover, we call the instrinsic dimensionality of the row space and column space the **rank** of the matrix (no need to delinneate whether we mean the row rank or the column rank, since they are equal). We can formalize this statement with the following theorem (proved in the Appendix to this post):

<span style="color:#0060C6">**Theorem 1 (row rank equals column rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, its row rank equals its column rank.</span>



Nullity: the intrinsic dimensionality of the null space
-------------------------------------------------------



The spaces induced by invertible matrices
-----------------------------------------

Appendix
--------

<span style="color:#0060C6">**Theorem 1 (row rank equals column rank):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, the row rank equals the column rank</span>

**Proof:**

Let $r_c$ be the column-rank of $\boldsymbol{A}$. Then, this means that there exists a set of basis vectors, $\{\boldsymbol{b}_1, \dots, \boldsymbol{b}_{r_c} \}$ that span the columns of $\boldsymbol{A}$. Let's encode these basis vectors into a matrix where each basis vector is a column-vector:

$$\boldsymbol{B} := \begin{bmatrix} \boldsymbol{b}_1 & \dots & \boldsymbol{b}_{r_c} \end{bmatrix}$$



$\square$


