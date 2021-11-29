---
title: 'Demystifying determinants'
date: 2021-11-28
permalink: /posts/determinants/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

In introductory linear algebra, one is taught that the the **determinant**, $\text{Det}$, is a function that maps square [matrices](https://mbernste.github.io/posts/matrices/) to real numbers:

$$\text{Det} : \mathbb{R}^m \rightarrow \mathbb{R}$$ 

More specifically, the the absolute value of a matrix's determinant is the area of the parallelepided formed by its columns. While conceptually, this is fairly straightforward, the analytical form of the determinant is quite confusing. Specifically, the determinant of an $m \times m$ matrix is defined as:

$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$

where $\boldsymbol{A}_{-1, -i}$ denotes the matrix formed by deleting the first row and $i$th column of $\boldsymbol{A}$. Note that this is a [recursive definition](https://en.wikipedia.org/wiki/Recursive_definition) where the base case is a $2 \times 2$ matrix. 

Somehow this formula calculates the volume of an $m$-dimensional parallelepided. If you're like me, this is not at all obvious. How on earth does this equation calculate volume? Moreover, why is it recursive?

In this post, I am going to attempt to demystify this definition. We will start with the base case of a $2 \times 2$ matrix, verify that it indeed computes the volume of the parallelogram formed by the columns of the matrix, and then move on to the determinant for larger matrices. 

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

Now what about for $m > 2$? For this, the definition of the determinant states that

$$\text{Det}(\boldsymbol{A}) := \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i})$$

How on earth does this formula calculate volume? 

The easiest way to see how this formula calculates volume, is to first begin by formulating, in a very abstract sense, a set of three axioms that attempt to capture our notion of "geometric volume". Then, we can show that the formula above is the only formula that satisfies these axioms! These axioms are as follows:

**1. The determinant of the identity matrix is one**  

The first axiom states that

$$\text{Det}(\boldsymbol{I}) := 1$$

This makes intuitive sense: the parallelopided formed by the columns of the identity matrix form a hypercube in $m$-dimensional space. We know that the volume of a cube is simply the product of the sides of the cube. in this case, they're all of length one so the volume should be one:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/DeterminantIdentityMatrix.png" alt="drawing" width="400"/></center>


**2. If two columns of a matrix are equal, then its determinant is zero**  

If two columns of a matrix are equal, then the parallelapipde formed by their columns is flat. Intuitively, the volume of a flat parallelapided should be zero. To can visualize this intuition in three dimensions below:

Here we see that when two of the three column vectors are equal, the parallapided lies in a hyperplane. Clearly, its geometric volume is zero. We can generalize this to any dimensions by simply making this property an axiom of the determinant: if two colum vectors are equal, high-dimensional parallelapide is "flat" and thus has a volume of zero. 

**2. The determinant of a matrix is linear with respect to each column vector**



Note, for the remainder of this blog post, we will often represent the determinant of a matrix as a function with either a single matrix argument, $\text{Det}(\boldsymbol{A})$, or with multiple vector arguments $\text{Det}(\boldsymbol{a}_{\*,1}, \dots, \boldsymbol{a}_{\*,1})$ where $\boldsymbol{a}_{\*,1}, \dots, \boldsymbol{a}_{\*,1}$ are the columns of $\boldsymbol{A}$.





Deriving the formula for a determinant
--------------------------------------

What is meant by "signed volume"?
---------------------------------
