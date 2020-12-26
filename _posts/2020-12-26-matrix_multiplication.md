---
title: 'Matrix multiplication'
date: 2020-12-26
permalink: /posts/matrix_multiplication/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

At a very high level, matrix multiplication is an operation between two [matrices](https://mbernste.github.io/posts/matrices/) that creates a new matrix.  For students introduced to matrix multiplication, it can be puzzling to learn that matrix multiplication does not simply entail computing the product of the each pair of corresponding entries between the two matrices. Rather, matrix multiplication is much more complicated: given two matrices $\boldsymbol{A}$ and $\boldsymbol{B}$, each column of the product matrix $\boldsymbol{AB}$ is formed by multiplying $\boldsymbol{A}$ by each column of $\boldsymbol{B}$: 

<span style="color:#0060C6">**Definition 1 (Matrix multiplication):** The product of an $m \times n$ matrix $\boldsymbol{A}$ **matrix multiplied** by a $n \times p$ matrix $\boldsymbol{B}$ is given by</span>
 
<center><span style="color:#0060C6">$$\boldsymbol{AB} := \begin{bmatrix} \boldsymbol{A}\boldsymbol{B}_{*,1} & \boldsymbol{A}\boldsymbol{B}_{*,2} & \dots & \boldsymbol{A}\boldsymbol{B}_{*,n} \end{bmatrix}$$</span></center>

<span style="color:#0060C6">where $\boldsymbol{B}_{*,i}$ is the $i$th column of $\boldsymbol{B}$.</span>

Note that this definition requires that if we multiply an $m \times n$ matrix by a $n \times p$ matrix, the result will be an $m \times p$ matrix where the number of rows is determined by the first matrix and the number of columns is determined by the second matrix.  More succinctly:

$$\boldsymbol{A}_{m \times n} \ \boldsymbol{B}_{n \times p} = (\boldsymbol{AB})_{m \times p}$$

This complicated definition begs the question, what is the intuition behind matrix vector multiplication? And, why is it defined this way?

Three perspectives for understanding matrix multiplication
---------------

There are at least three perspectives for which one can view matrix multiplication each depending on the perspective taken on each of the matrix factors. Recall we can view a matrix [via a number of perspectives](https://mbernste.github.io/posts/matrices/):

1. As a list of column vectors
2. As a list of row vectors
3. As a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/)

Given these various ways of possibly viewing each matrix factor, $\boldsymbol{A} and $\boldsymbol{B}$, we can view their product, $\boldysmbol{AB}$, as follows, ordered from least abstract to most abstract:

1. **Matrix multiplication computes dot products for pairs of vectors:**
2. **Matrix multiplication computes a linear transformation on a set of vectors:**
3. **Matrix multiplication computes the composition of two linear transformation:**

