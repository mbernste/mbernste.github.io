---
title: 'Demystifying determinants'
date: 2023-04-23
permalink: /posts/determinants/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

In introductory linear algebra, one is taught that the the **determinant**, $\text{Det}$, is a function that maps square [matrices](https://mbernste.github.io/posts/matrices/) to real numbers,

$$\text{Det} : \mathbb{R}^{m \times m} \rightarrow \mathbb{R}$$ 

for which the absolute value of a matrix's determinant is the area of the parallelepided formed by its columns. 

While conceptually, this is fairly straightforward, the analytical formula for the determinant is quite confusing. Specifically, the determinant of an $m \times m$ matrix is defined as:

$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$

where $\boldsymbol{A}_{-1, -i}$ denotes the matrix formed by deleting the first row and $i$th column of $\boldsymbol{A}$. Note that this is a [recursive definition](https://en.wikipedia.org/wiki/Recursive_definition) where the base case is a $2 \times 2$ matrix. 

When one is usually first taught determinants, they are supposed to take it as a given that this formula calculates the volume of an $m$-dimensional parallelepided; however, if you're like me, this is not at all obvious. How on earth does this formula calculate volume? Moreover, why is it recursive?

In this post, I am going to attempt to demystify this definition. We will start with the base case of a $2 \times 2$ matrix, verify that it indeed computes the volume of the parallelogram formed by the columns of the matrix, and then move on to the determinant for larger matrices. We will conclude with several fundamental properties of determinants and their intuition.

$2 \times 2$ matrices
---------------------

Let's first only look at the $m = 2$ case and verify that this equation computes the area of the parallelogram formed by the matrix's columns. Let's say we have a matrix

$$\boldsymbol{A} := \begin{bmatrix}a & b \\ c & d\end{bmatrix}$$

Then we see that the area can be obtained by computing the area of the rectangle that encompasses the parallelogram and subtracting the areas of the triangles around it:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/TwoByTwoDeterminant.png" alt="drawing" width="700"/></center>

Simplifying the equation above we get

$$\text{Det}(\boldsymbol{A}) = ad - bc$$

which is exactly the definition for the $2 \times 2$ determinant.  So far so good. 

Defining the determinant for $m \times m$ matrices: abstracting the notion of geometric volume
----------------------------------------------------------------------------------------------

Moving on to $m > 2$, the definition of the determinant is

$$\text{Det}(\boldsymbol{A}) := \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i})$$

Before understanding this equation, we must first ask ourselves what we even mean by "volume" in $m$-dimensional space. In fact, it is through answering this very question that will arrive at the equation above. Specifically, we will formulate a set of three axioms that attempt to capture our notion of "geometric volume" in a very abstract way. Then, we will show that the only formula that satisfies these axioms is the formula for the determinant shown above! 

These axioms are as follows:

**1. The determinant of the identity matrix is one**  

The first axiom states that

$$\text{Det}(\boldsymbol{I}) := 1$$

Why do we want this to be an axiom? First, we note that the parallelepided formed by the columns of the identity matrix, $\boldsymbol{I}$, is a hypercube in $m$-dimensional space:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/DeterminantIdentityMatrix.png" alt="drawing" width="400"/></center>

We would like our notion of "geometric volume" to match our common intuition that the volume of a cube is simply the product of the sides of the cube. In this case, they're all of length one so the volume, and thus the determinant, should be one.


**2. If two columns of a matrix are equal, then its determinant is zero**  

For a given matrix $\boldsymbol{A}$, if any two columns $\boldsymbol{a}\_{\*,i}$ and $\boldsymbol{a}\_{\*,j}$ are equal, then the determinant of $\boldsymbol{A}$ should be zero.

Why do we want this to be an axiom? We first note that if two columns of a matrix are equal, then the parallelapipde formed by their columns is flat. For example, here's a depiction of a parallelepided formed by the columns of a $3 \times 3$ matrix with two columns that are equal:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/FlatParallelepiped.png" alt="drawing" width="400"/></center>

We see that the parallelepided is flat and lies within a hyperplane.

We would like our notion of "geometric volume" to match our common intuition that the volume of a flat object is zero. Thus, when any two columns of a matrix are equal, we would like the determinant to be zero.

**3. The determinant of a matrix is linear with respect to each column vector**

Note, for the remainder of this blog post, we will often represent the determinant of a matrix as a function with either a single matrix argument, $\text{Det}(\boldsymbol{A})$, or with multiple vector arguments $\text{Det}(\boldsymbol{a}\_{\*,1}, \dots, \boldsymbol{a}\_{\*,n})$ where $\boldsymbol{a}\_{\*,1}, \dots, \boldsymbol{a}\_{\*,n}$ are the $n$ columns of $\boldsymbol{A}$.

Now, using this notation, the final axiom for the determinant is that $\text{Det}$ is a [linear function](https://mbernste.github.io/posts/matrices_linear_transformations/) with respect to each argument vector. For $\text{Det}$ to be linear with respect to each argument is to imply two conditions. First, for a given constant $k$, it holds that,

$$\forall j \in [n], \ \text{Det}(\boldsymbol{a}_{*,1}, \dots, k\boldsymbol{a}_{*,j}, \dots  \boldsymbol{a}_{*,n}) = k\text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j}, \dots  \boldsymbol{a}_{*,n})$$

and second, that

$$\forall j \in [n], \ \text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j} + \boldsymbol{v}, \dots  \boldsymbol{a}_{*,n}) = \text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j}, \dots  \boldsymbol{a}_{*,n}) + \text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{v}, \dots  \boldsymbol{a}_{*,n})$$

Why do we wish the linearity of $\text{Det}$ to be an axiom? Because it turns out that the volume of a two-dimensional parallelogram is linear with respect to the vectors that form its sides. To show this, let's start with a parallelogram defined by the columns of the following matrix:

$$\boldsymbol{A} := \begin{bmatrix}a & b \\ c & d\end{bmatrix}$$

Let's say we multiply one of the column vectors by k to form $\boldsymbol{A}'$:

$$\boldsymbol{A}' := \begin{bmatrix}ka & b \\ kc & d\end{bmatrix}$$

Its determinant is 

$$\begin{align*}\text{Det}(\boldsymbol{A}') &:= kad - bkc \\ &= k(ad - bc) \\ &= k\text{Det}(\boldsymbol{A})\end{align*}$$

Now let's consider another matrix formed by taking the first column or $\boldsymbol{A}$ and adding a vector $\boldsymbol{v}$:

$$\boldsymbol{A}' := \begin{bmatrix}a + v_1 & b \\ c + v_2 & d\end{bmatrix}$$

Its determinant is 

$$\begin{align*}\text{Det}(\boldsymbol{A}') &:= (a + v_1)d - b(c + v_2) \\ &= ad + v_1d - bc - bv_2 \\ &= (ad -  bc) + (v_1d - bv_2) \\ &= \text{Det}\left(\begin{bmatrix}a & b \\ c & d\end{bmatrix}\right) + \text{Det}\left(\begin{bmatrix}v_1 & b \\ v_2 & d\end{bmatrix} \right) \end{align*}$$

We would like the generalized definition of a determinant to also be linear with respect to the vectors that form its sides. 

Deriving the formula for a determinant
--------------------------------------

In the previous section, we outlined three axioms that define fundamental ways in which the volume of a parallelogram is related to the vectors that form its sides. We will show that there is only one analytica formula for the determinant that satisfies these axioms. That formula is:

$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$

For now, we will assume that there exists a function $\text{Det}: \mathbb{R}^{m \times m} \rightarrow \mathbb{R}$ that satisfies our three axioms and will subsequently prove a series of theorems and lemmas that will build up to this final formula. Many of these theorems/lemmas will make heavy use of the fact that [invertible matrices can be decomposed into the product of elementary matrices](https://mbernste.github.io/posts/row_reduction/).

<span style="color:#0060C6">**Theorem 1:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if we exchange any two column-vectors of $\boldsymbol{A}$ to form a new matrix $\boldsymbol{A}'$, then $\text{Det}(\boldsymbol{A}') = -\text{Det}(\boldsymbol{A})$</span>

<span style="color:#0060C6">**Lemma 1:** Given an elementary matrix that represents row-scaling, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$, where $\boldsymbol{E}$ scales the $j$th row of a system of linear equations by $k$, its determinant is simply $k$.</span>

<span style="color:#0060C6">**Lemma 2:** Given an elementary matrix that represents row-swapping, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that swaps the $i$th and $j$th rows of a system of linear equations, its determinant is simply -1.</span>

<span style="color:#0060C6">**Lemma 3:** Given an elementary matrix that represents a row-sum, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that multiplies row $j$ by $k$ times row $i$, its determinant is simply 1.</span>

<span style="color:#0060C6">**Theorem 2:** Given a square matrix $\boldsymbol{A}$, it holds that $\text{Det}(\boldsymbol{A}) = \text{Det}(\boldsymbol{A}^T).</span>

<span style="color:#0060C6">**Theorem 3:** Given matrices $\boldsymbol{A}, \boldsymbol{B} \in \mathbb{R}^{m \times m}$, it holds that $\text{Det}(AB) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{B})</span>

**Proof:**

We will start with a simpler case where $\boldsymbol{A}$ is an [elementary matrix](https://mbernste.github.io/posts/row_reduction/). We thus, must consider the three scenarios where $\boldsymbol{A}$ is either a row-scaling matrix, row-swapping matrix, or a row-sum matrix. First, let's consider the case where $\boldsymbol{A}$ is a row-scaling matrix that scales the $j$th row of an [system of linear equations](https://mbernste.github.io/posts/row_reduction/) by a constant $k$. Because we are scaling 







<span style="color:#0060C6">**Lemma 2:** Given an upper-triangular matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, its determinant can be computed by multiplying its diagonal entries.</span>

**Proof:**


If determinants capture the notion of volume, then why can it be negative?
--------------------------------------------------------------------------

The relationship between determinants and the invertability of a matrix
-----------------------------------------------------------------------

The determinant of a matrix product
-----------------------------------

Appendix
--------

<span style="color:#0060C6">**Lemma 1:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if we exchange any two column-vectors of $\boldsymbol{A}$ to form a new matrix $\boldsymbol{A}'$, then $\text{Det}(\boldsymbol{A}') = -\text{Det}(\boldsymbol{A})$</span>

**Proof:**

Let columns $i$ and $j$ be the columns that we exchange within $\boldsymbol{A}$. For ease of notation, let us define 

$$\text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j}) := \text{Det}_{i,j}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m})$$

to be the determinant of $\boldsymbol{A}$ as a function of only the $i$th and $j$th column-vectors of $\boldsymbol{A}$ where the other column-vectors are held fixed. Then, we see that

$$\begin{align*} \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j}) &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j})  + \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i}) && \text{Axiom 2} \\ &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) - \text{Det}_{i,j}(\boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 2} \\ &= \text{Det}_{i,j}(-\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= -\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= -(\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i}) - \text{Det}_{i,j}(\boldsymbol{a}_{*,j},\boldsymbol{a}_{*,j})) && \text{Axiom 3} \\ &=  -\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i}) && \text{Axiom 2}\end{align*}$$

$\square$



<span style="color:#0060C6">**Theorem 2:** Given an elementary matrix that represents row-scaling, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$, where $\boldsymbol{E}$ scales the $j$th row of a system of linear equations by $k$, its determinant is simply $k$.</span>

**Proof:**

Such a matrix would be a diagonal matrix with all ones along the diagonal except for the $j$th entry, which would be $k$. For example, a $4 \times 4$ row-scaling matrix that scales the second row by $4$ would look as follows:

$$\boldsymbol{A} := \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & k & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1\end{bmatrix}$$

Note that this is a triangular matrix and thus, its determinant is given by the product along its diagonals, which is simply $k$. 

$\square$



<span style="color:#0060C6">**Theorem 2:** Given an elementary matrix that represents row-swapping, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that swaps the $i$th and $j$th rows of a system of linear equations, its determinant is simply -1.</span>

**Proof:**

A row-swapping matrix that swaps the $i$th and $j$th rows of a system of linear equations can be formed by simply swapping the $i$th and $j$th column vectors of the identity matrix.  For example, a $4 \times 4$ row-scaling matrix that swaps the second and third rows would look as follows:

$$\boldsymbol{A} := \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1\end{bmatrix}$$

Axiom 1 for the definition of the determinant states that the determinant of the identity matrix is 1. According to Theorem XXXXX, if we swap two column-vectors of a matrix, its determinant is multiplied by -1. Here we are swapping two column-vectors of the identity matrix yielding a determinant of -1.

$\square$



