---
title: 'Matrix-vector multiplication'
date: 2020-12-19
permalink: /posts/matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
  - linear transformation
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

In a [previous post](https://mbernste.github.io/posts/matrices/), we discussed three ways one can view a matrix: as a table of values, as a list of vectors, and finally, as a function.  It is the third way of viewing a matrices that really gives matrices their power.  Here, we'll introduce an operation between matrices and vectors, called **matrix-vector multiplication**, which will enable us to use matrices as functions. 

Matrix-vector multiplication is an operation between a matrix and a vector that produces a new vector.  Notably, matrix-vector multiplication is only defined between a matrix and a vector where the length of the vector equals the number of columns of the matrix.  It is defined as follows:

<span style="color:#0060C6">**Definition 1 (Matrix-vector multiplication):** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$ and vector $\boldsymbol{x} \in \mathbb{R}^n$ the **matrix-vector multiplication** of $\boldsymbol{A}$ and $\boldsymbol{x}$ is defined as </span>

<center><span style="color:#0060C6">$$\boldsymbol{A}\boldsymbol{x} := x_1\boldsymbol{a}_{*,1} + x_2\boldsymbol{a}_{*,2} + \dots +  x_n\boldsymbol{a}_{*,n}$$ </span></center>

<span style="color:#0060C6">where $\boldsymbol{a}_{*,i}$ is the $i$th column vector of $\boldsymbol{A}$.</span>

Like most mathematical concepts, matrix-vector multiplication can be [viewed from multiple angles](), at various levels of abstraction. These views come in handy when we attempt to conceptualize the various ways in which we utilize matrix-vector multiplication to model real-world problems.  Below are three ways that I find useful for conceptualizing matrix-vector multiplication ordered from least to most abstract:

1. **As a "row-wise", vector-generating process:** Matrix-vector multiplication defines a process for creating a new vector using an existing vector where each element of the new vector is "generated" by taking a weighted sum of each row of the matrix using the elements of a vector as coefficients
2. **As taking a linear combination of the columns of a matrix:**  Matrix-vector multiplication is the process of  taking a linear combination of the column-space of a matrix using the elements of a vector as the coefficients
3. **As evaluating a function between vector spaces:** Matrix-vector multiplication allows a matrix to define a mapping between two vector spaces.

I find all three of the perspectives useful. The first two perspectives provide a way of understanding the *mechanism* of matrix-vector multiplication whereas the third perspective provides the *essence* of matrix-vector multiplication.  It is this third perspective of matrix-vector multiplication that enables us to view matrices as functions, as we discussed in the [previous post](https://mbernste.github.io/posts/matrices/).

Matrix-vector multiplication as a "row-wise", vector-generating process
------------

A useful way for viewing the mechanism of matrix-vector multiplication between a matrix $\boldsymbol{A}$ and a vector $\boldsymbol{x}$ is to see it as a sort of "process" (or even as a computer program) that constructs each element of the output vector in an iterative fashion where we iterate over each row of $A$. Specifically, for each row $i$ of $\boldsymbol{A}$, we take $\boldsymbol{x}$ and compute the dot product between $\boldsymbol{x}$ and the $i$th row of the matrix thereby producing the $i$th element of the output vector (See Theorem 1 in the Appendix to this post):

$$\boldsymbol{Ax} = \begin{bmatrix} \boldsymbol{a}_{1,*} \cdot \boldsymbol{x} \\ \boldsymbol{a}_{2,*}  \cdot \boldsymbol{x} \\ \vdots \\ \boldsymbol{a}_{m,*}  \cdot \boldsymbol{x} \\ \end{bmatrix}$$

where $\boldsymbol{a}_{i,*}$ is the $i$th row-vector in $\boldsymbol{A}$.  This process is illustrated schematically in Panel A of the figure below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_vec_mult_as_process.png" alt="drawing" width="700"/></center>

Matrix-vector multiplication as taking a linear combination of the columns of a matrix
------------

Matrix-vector multiplication between a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$ and vector $\boldsymbol{x} \in \mathbb{R}^m$ can be understood as taking a linear combination of the column vectors of $\boldsymbol{A}$ using the elements of $\boldsymbol{x}$ as the coefficients.  This is illustrated schematically below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_vec_mult_as_lin_comb.png" alt="drawing" width="700"/></center>

We can also view this geometrically:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_vec_mult_as_linear_comb_geom.png" alt="drawing" width="720"/></center>

In Panel A, we depict two column vectors of some matrix $\boldsymbol{A} \in \mathbb{R}^{3,2}$. In Panel B, we take a linear combination of the two column vectors of $$\boldsymbol{A}$$ according to the elements of some vector $\boldsymbol{x}$ thus producing the vector $\boldsymbol{Ax}$ (black vector) as shown in Panel C.

