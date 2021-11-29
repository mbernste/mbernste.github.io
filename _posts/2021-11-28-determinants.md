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

When first learning linear algebra, I found the **determinant** to be one of the more confusing topics.  When introduced to determinants, one is taught that the the determinant of a matrix $\boldsymbol{A}$ is the "signed" area of the parallelepided formed by the columns of $\boldsymbol{A}$.  That is, the absolute value of the determinant is the volume of the parallelepided. 

For example, for a $2 \times 2$ matrix $\boldsymbol{A} := \begin{bmatrix}a & b \\ c & d\end{bmatrix}$, one can compute the determinant via the equation
$$\text{Det}(\boldsymbol{A}) := ad - bc$$.

We can verify that this equation gives us the area of the two-dimensional parallelogram pretty easily by drawing it out and seeing that the area can be obtained by computing the area of the rectangle that encompasses the parallelogram and subtracting the areas of the triangles around the parallelepided:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/TwoByTwoDeterminant.png" alt="drawing" width="700"/></center>

So far, this isn't too confusing, but things get more difficult when moving to matrices of higher dimensions. Unintuitively, the general definition of the determinant for a $m \times m$ matrix $\boldsymbol{A}$ is defined as

$$\text{Det}(\boldsymbol{A}) := \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) $$

where $\boldsymbol{A}_{-1, -i}$ denotes the matrix formed by deleting the first row and $i$th column of $\boldsymbol{A}$.

If you're like me, this equation is very opaque. How on earth does this equation calculate the volumne of an $m$-dimensional parallelepided? Moreover, why is it recursive? 

In this post, I am going to attempt to demystify this definition. To do so, we will begin with a set of axioms that seek to capture the notion of "volume" in an $m$-dimensional space. From this axiomization, we derive the equation for the determinant above!

Notation
--------

Before getting into the thick of it, let's define a bit of notation that we'll use in this blog post.  First, we note that the determinant, $\text{Det}$, is a function that maps square matrices to real numbers:

$$\text{Det} : \mathbb{R}^m \rightarrow \mathbb{R}$$ 

We will often represent the determinant of a matrix as a function with either a single matrix argument, $\text{Det}(\boldsymbol{A})$, or with multiple vector arguments $\text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,1})$ where $\boldsymbol{a}_{\*,1}, \dots, \boldsymbol{a}_{\*,1}$ are the columns of $\boldsymbol{A}$.

For other notation related to matrices that we will use in this post, see my [previous post on matrices](https://mbernste.github.io/posts/matrices/). 

Axioms for a determinant: abstracting the notion of geometric volume
--------------------------------------------------------------------

The definition of a determinant does not actually start with the calculation of of volume in the usual sense, but rather, we will begin by trying to abstract the fundamental properties of "geometric volume". 

**1. The determinant of the identity matrix is one**  

This makes intuitive sense: the parallelopided formed by the columns of the identity matrix form a hypercube in $m$-dimensional space. The volume of a cube is simply the product of the sides of the cube; in this case, they're all of length one so the volume should be one:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/DeterminantIdentityMatrix.png" alt="drawing" width="400"/></center>

That is, we have 

$$\text{Det}(\boldsymbol{I}) := 1$$

**2. If two columns of a matrix are equal, then its determinant is zero**  

If two columns of a matrix are equal, then the parallelapipde formed by their columns is flat. Intuitively, the volume of a flat parallelapided should be zero. To can visualize this intuition in three dimensions below:

Here we see that when two of the three column vectors are equal, the parallapided lies in a hyperplane. Clearly, its geometric volume is zero. We can generalize this to any dimensions by simply making this property an axiom of the determinant: if two colum vectors are equal, high-dimensional parallelapide is "flat" and thus has a volume of zero. 

**2. The determinant of a matrix is linear with respect to each column vector**

  

Deriving the formula for a determinant
--------------------------------------

What is meant by "signed volume"?
---------------------------------
