---
title: 'Demystifying the determinant'
date: 2023-07-08
permalink: /posts/determinantsformula/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_Much of my understanding of this material comes from [these lecture notes](http://faculty.fairfield.edu/mdemers/linearalgebra/documents/2019.03.25.detalt.pdf) by Mark Demers re-written in my own words._

Introduction
------------

In introductory linear algebra, one is taught that the the **determinant**, $\text{Det}$, is a function that maps square [matrices](https://mbernste.github.io/posts/matrices/) to real numbers,

$$\text{Det} : \mathbb{R}^{m \times m} \rightarrow \mathbb{R}$$ 

for which the absolute value of a matrix's determinant is the area of the parallelepided formed by its columns.

While conceptually, this is fairly straightforward, the analytical formula for the determinant is quite confusing. Specifically, the determinant of an $m \times m$ matrix is defined as:

$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$

where $\boldsymbol{A}_{-1, -i}$ denotes the matrix formed by deleting the first row and $i$th column of $\boldsymbol{A}$. Note that this is a [recursive definition](https://en.wikipedia.org/wiki/Recursive_definition) where the base case is a $2 \times 2$ matrix. 

When one is usually first taught determinants, they are supposed to take it as a given that this formula calculates the volume of an $m$-dimensional parallelepided; however, if you're like me, this is not at all obvious. How on earth does this formula calculate volume? Moreover, why is it recursive? 

In this post, I am going to attempt to demystify this definition. We will start with the base case of a 2×2
 matrix, verify that it indeed computes the volume of the parallelogram formed by the columns of the matrix, and then move on to the determinant for larger matrices. We will then discuss what the volume of the parallelepided formed by a matrix's columns informs us about the linear transformation described by that matrix. We will conclude by discussing how to interpret the sign (whether it's positive or negative) of a matrix's determinant. 
 

$2 \times 2$ matrices
---------------------

Let's first only look at the $m = 2$ case and verify that this equation computes the area of the parallelogram formed by the matrix's columns. Let's say we have a matrix

$$\boldsymbol{A} := \begin{bmatrix}a & b \\ c & d\end{bmatrix}$$

Then we see that the area can be obtained by computing the area of the rectangle that encompasses the parallelogram and subtracting the areas of the triangles around it:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/TwoByTwoDeterminant.png" alt="drawing" width="700"/></center>

Simplifying the equation above we get

$$\text{Det}(\boldsymbol{A}) = ad - bc$$

which is exactly the definition for the $2 \times 2$ determinant.  So far so good. 

Defining the determinant for $m \times m$ matrices: a generalization of geometric volume
----------------------------------------------------------------------------------------

Moving on to $m > 2$, the definition of the determinant is

$$\text{Det}(\boldsymbol{A}) := \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i})$$

Before understanding this equation, we must first ask ourselves what we really mean by "volume" in $m$-dimensional space. In fact, it is through the process of answering this very question that we bring us to the equation above. Specifically, we will formulate a set of three axioms that attempt to capture the notion of "geometric volume" in a very abstract way that applies to higher dimensions. Then, we will show that the only formula that satisfies these axioms is the formula for the determinant shown above! 

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

Before digging into this final axiom, let us define some notation to make our discussion easier. Specifically, for the remainder of this post, we will often represent the determinant of a matrix as a function with either a single matrix argument, $\text{Det}(\boldsymbol{A})$, or with multiple vector arguments $\text{Det}(\boldsymbol{a}\_{\*,1}, \dots, \boldsymbol{a}\_{\*,n})$ where $\boldsymbol{a}\_{\*,1}, \dots, \boldsymbol{a}\_{\*,n}$ are the $n$ columns of $\boldsymbol{A}$.

Now, the final axiom for the determinant is that $\text{Det}$ is a [linear function](https://mbernste.github.io/posts/matrices_linear_transformations/) with respect to each argument vector. For $\text{Det}$ to be linear with respect to each argument is to imply two conditions. First, for a given constant $k$, it holds that,

$$\forall j \in [n], \ \text{Det}(\boldsymbol{a}_{*,1}, \dots, k\boldsymbol{a}_{*,j}, \dots  \boldsymbol{a}_{*,n}) = k\text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j}, \dots  \boldsymbol{a}_{*,n})$$

and second, that

$$\forall j \in [n], \ \text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j} + \boldsymbol{v}, \dots  \boldsymbol{a}_{*,n}) = \text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j}, \dots  \boldsymbol{a}_{*,n}) + \text{Det}(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{v}, \dots  \boldsymbol{a}_{*,n})$$

Why do we wish the linearity of $\text{Det}$ to be an axiom? Because it turns out that the volume of a two-dimensional parallelogram is linear with respect to the vectors that form its sides. We can prove this both algebraically as well as geometrically. Let's start with the algebraic proof starting with a parallelogram defined by the columns of the following matrix:

$$\boldsymbol{A} := \begin{bmatrix}a & b \\ c & d\end{bmatrix}$$

Let's say we multiply one of the column vectors by k to form $\boldsymbol{A}'$:

$$\boldsymbol{A}' := \begin{bmatrix}ka & b \\ kc & d\end{bmatrix}$$

Its determinant is 

$$\begin{align*}\text{Det}(\boldsymbol{A}') &:= kad - bkc \\ &= k(ad - bc) \\ &= k\text{Det}(\boldsymbol{A})\end{align*}$$

Now let's consider another matrix formed by taking the first column or $\boldsymbol{A}$ and adding a vector $\boldsymbol{v}$:

$$\boldsymbol{A}' := \begin{bmatrix}a + v_1 & b \\ c + v_2 & d\end{bmatrix}$$

Its determinant is 

$$\begin{align*}\text{Det}(\boldsymbol{A}') &:= (a + v_1)d - b(c + v_2) \\ &= ad + v_1d - bc - bv_2 \\ &= (ad -  bc) + (v_1d - bv_2) \\ &= \text{Det}\left(\begin{bmatrix}a & b \\ c & d\end{bmatrix}\right) + \text{Det}\left(\begin{bmatrix}v_1 & b \\ v_2 & d\end{bmatrix} \right) \end{align*}$$

To provide more intuition about why this linearity property holds, let's look at it geometrically. As a preliminary observation, notice how if we skew one of the edges of a parallelogram along the axis of the other edge, then the area remains the same. We can see this in the figure below by noticing that the area of the yellow triangule is subtracted from the first paralellogram, but is added to the second:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/DeterminantSkewParallogramAxis.png" alt="drawing" width="500"/></center>

With this observation in mind, we can now show why the determinant is linear from a geometric perspective. Let's start with the first axiom that says if we scale one of the sides of a parallelogram by $k$, then the area of the parallelogram is scaled by $k$. Below, we show a parallelogram where we scale one of the vectors, $\boldsymbol{v}$, by $k$. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/Determinant_linearity_axiom1_part1.png" alt="drawing" width="500"/></center>

We see that we can skew both sides of the parallelogram to be orthogonal to one another forming a rectangle that preserves the area of the parallelogram. This rectangle has sides of length $a$ and $b$ and thus an area of $ab$. When we skew the enlarged parallelogram in the same way, we form a rectangle with sides of length $a$ and $kb$ and thus an area of $kab$ We know the sides of the enlarged parallelogram are of length $a$ and $kb$ by observing that the two shaded triangles shown below are [similar](https://www.mathsisfun.com/geometry/triangles-similar.html):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/Determinant_linearity_axiom1_part2.png" alt="drawing" width="500"/></center>

The second axiom of linearity states that if we break apart one of the vectors that forms an edge of the parallelogram into two vectors, we can show that they form two "sub-parallelograms" whose total area equals the area of the original parallelogram.  This is shown in the following "visual proof":

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/Determinant_linearity_axiom2.png" alt="drawing" width="800"/></center>


Deriving the formula for a determinant
--------------------------------------

In the previous section, we outlined three axioms that define fundamental ways in which the volume of a parallelogram is related to the vectors that form its sides. It turns out that the _only_ formula that satisfies these axioms is the following:

$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$

We will start by assuming that there exists a function $\text{Det}: \mathbb{R}^{m \times m} \rightarrow \mathbb{R}$ that satisfies our three axioms and will subsequently prove a series of theorems that will build up to this final formula. Many of these theorems/lemmas will make heavy use of the fact that invertible matrices can be decomposed into the product of elementary matrices. For an in-depth discussion of elementary matrices, [see my previous post](https://mbernste.github.io/posts/row_reduction/). 

The Theorems required to derive this formula are outlined below. and their proofs are described in the Appendix to this post

<span style="color:#0060C6">**Theorem 1:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if we exchange any two column-vectors of $\boldsymbol{A}$ to form a new matrix $\boldsymbol{A}'$, then $\text{Det}(\boldsymbol{A}') = -\text{Det}(\boldsymbol{A})$</span>

<span style="color:#0060C6">**Theorem 2:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if if it's column-vectors are [linearly dependent](https://mbernste.github.io/posts/linear_independence/), then its determinant is zero.</span>

<span style="color:#0060C6">**Theorem 3:** Given a triangular matrix, $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, its determinant can be computed by multiplying its diagonal entries.</span>

<span style="color:#0060C6">**Theorem 4:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, adding a multiple of one column-vector of $\boldsymbol{A}$ to another column-vector does not change the determinant of $\boldsymbol{A}$.</span>

<span style="color:#0060C6">**Theorem 5:** Given an [elementary matrix](https://mbernste.github.io/posts/row_reduction/) that represents row-scaling, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$, where $\boldsymbol{E}$ scales the $j$th row of a system of linear equations by $k$, its determinant is simply $k$.</span>

<span style="color:#0060C6">**Theorem 6:** Given an [elementary matrix](https://mbernste.github.io/posts/row_reduction/) that represents row-swapping, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that swaps the $i$th and $j$th rows of a system of linear equations, its determinant is simply -1.</span>

<span style="color:#0060C6">**Theorem 7:** Given an [elementary matrix](https://mbernste.github.io/posts/row_reduction/) that represents a row-sum, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that multiplies row $j$ by $k$ times row $i$, its determinant is simply 1.</span>

<span style="color:#0060C6">**Theorem 8:** Given matrices $\boldsymbol{A}, \boldsymbol{B} \in \mathbb{R}^{m \times m}$, it holds that $\text{Det}(AB) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{B})$</span>

<span style="color:#0060C6">**Theorem 9:** Given a square matrix $\boldsymbol{A}$, it holds that $\text{Det}(\boldsymbol{A}) = \text{Det}(\boldsymbol{A}^T)$.</span>

With these theorems in hand we can derive the final formula for the determinant:

<span style="color:#0060C6">**Theorem 10:** Tbe determinant of matrix is linear with respect to the row vectors of the matrix</span>

<span style="color:#0060C6">**Theorem 11:** Let $\text{Det} : \mathbb{R}^{n \times n} \rightarrow \mathbb{R}$ be a function that satisfies the following three properties:</span>

<span style="color:#0060C6">1. $\text{Det}(\boldsymbol{I}) = 1$</span>

<span style="color:#0060C6">2. Given $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, if any two columns of $\boldsymbol{A}$ are equal, then $\text{Det}(\boldsymbol{A}) = 0$</span>

<span style="color:#0060C6">3. $\text{Det}$ is linear with respect to the column-vectors of its input.</span>

<span style="color:#0060C6">Then $\text{Det}$ is given by</span>

<span style="color:#0060C6">$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$</span>

Again, this proof is left to the Appendix of this post. A sketch of how all of these theorems lead up to Theorem 10 is shown below:


The determinant describes how much a matrix grows or shrinks space
-------------------------------------------------------------------

We have now shown how the determinant of a matrix, $\boldsymbol{A}$, captures the volume of the parallelepiped formed by $\boldsymbol{A}$'s columns. However, what is the significance of this quantity? Recall, that a powerful way to [view a matrix](https://mbernste.github.io/posts/matrices/) is as a characterizing a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/) between vector spaces. That is, given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times n}$, we can form a function $T$ that maps vectors in $\mathbb{R}^n$ to $\mathbb{R}^m$ using [matrix-vector multirplication](https://mbernste.github.io/posts/matrix_vector_mult/):

$$T(\boldsymbol{x}) := \boldsymbol{Ax}$$

It turns out that the determinant tells us something fundamental about this linear transformation: it tells us how much the linear transformation "grows" or "shrinks" space. To see why this is, we will first examine what happens to the volume of a rectangle/hyperrectangle when it is transformed by an invertible matrix.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/determinant_scales_circle.png" alt="drawing" width="700"/></center>


Interpreting the sign of the determinant
----------------------------------------

So far, we have discussed how the absolute value of the determinant of a matrix captures the volume of the parallelopiped formed by that matrix's columns; however, we have glossed over the fact that this interpretation of the determinant requires taking its absolute value. What does the sign of the determinant capture? If determinants capture volume, then how can it be negative (intuitively, volume is only a positive quantity)? 

It turns out that the sign of the determinant captures something else about a matrix's linear transformation other than how much it grows or shrinks space: it captures whether or not a matrix "inverts" space. That is, a matrix with a positive determinant will maintain the orientation of vectors in the original space relative to one another, but a matrix with a negative determinant will invert their orientation. 

As an example, let us consider the matrix $\boldsymbol{A} := \begin{bmatrix}0 & 1 \\ 1 & 0\end{bmatrix}$. The determinant of $\boldsymbol{A}$ is -1. Why? By Axiom 1, the determinant of the identity matrix is 1. By Theorem 1, flipping two columns will make the determinant negative. Thus, the determinant of $\boldsymbol{A}$ is simply -1. 

Below is an illustration of what happens to a set of vectors that form the outline of a hand when transformed by the matrix $\boldsymbol{A}$. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/negative_determinant_inversion_2D.png" alt="drawing" width="700"/></center>

Here we see that this matrix simply flipped the orientation of vectors across the thick dotted line (you can see this by tracing the location of the thumb outlined by the thin dotted lines). 

This same phenomenon occurs in higher dimensions too. Here is an example in three dimensions where a 3D hand is transformed by a matrix $\boldsymbol{A}$ that again represents the identity matrix, but with the first and third columns flipped. Notice how the hand went from being a right hand to a left hand by the transformation:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/determinant_inversion_hand.png" alt="drawing" width="700"/></center>

Intuiting determinants as "signed volume"
-----------------------------------------

In [some explanations](https://en.wikipedia.org/wiki/Determinant), the determinant is explained as describing a "signed volume". What is meant by signed volume? For me, it helps to think about determinants in a similar way that we think about integrals. Integrals express the "signed" area under a curve where the sign tells you whether there is more area above versus below zero. Consider a sequence of univariate functions where each function's curve approaches zero until it cross zero and becomes more negative:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/integral_analogy_determinant.png" alt="drawing" width="700"/></center> 

We see that the integral starts out as positive, shrinks to zero, and then becomes more negative.

Analagously, we can see that as two vectors are rotated towards one another, the determinant is positive but decreases until the vectors are aligned. Once they cross one another, the determinant becomes negative:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/negative_determinant_rotate_vecs.png" alt="drawing" width="800"/></center>

Thus, the "sign" of an integral is sort of like the "sign" of an integral. Where a negative integral tells you that the function has more area below zero than above zero, a negative determinant tells you that two columns vectors, in a sense, "crossed" with one another thus inverting space across those two column vectors.


Appendix
--------

<span style="color:#0060C6">**Theorem 1:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if we exchange any two column-vectors of $\boldsymbol{A}$ to form a new matrix $\boldsymbol{A}'$, then $\text{Det}(\boldsymbol{A}') = -\text{Det}(\boldsymbol{A})$</span>

**Proof:**

Let columns $i$ and $j$ be the columns that we exchange within $\boldsymbol{A}$. For ease of notation, let us define 

$$\text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j}) := \text{Det}_{i,j}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m})$$

to be the determinant of $\boldsymbol{A}$ as a function of only the $i$th and $j$th column-vectors of $\boldsymbol{A}$ where the other column-vectors are held fixed. Then, we see that

$$\begin{align*} \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j}) &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j})  + \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i}) && \text{Axiom 2} \\ &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) - \text{Det}_{i,j}(\boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 2} \\ &= \text{Det}_{i,j}(-\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= -\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= -(\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i}) - \text{Det}_{i,j}(\boldsymbol{a}_{*,j},\boldsymbol{a}_{*,j})) && \text{Axiom 3} \\ &=  -\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i}) && \text{Axiom 2}\end{align*}$$

$\square$



<span style="color:#0060C6">**Theorem 2:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if it's column-vectors are [linearly dependent](https://mbernste.github.io/posts/linear_independence/), then its determinant is zero.</span>

**Proof:**

Given a matrix $\boldsymbol{A}$ with columns,

$$\boldsymbol{A} := \begin{bmatrix}\boldsymbol{a}_{*,1}, \boldsymbol{a}_{*,2}, \dots, \boldsymbol{a}_{*,m}\end{bmatrix}$$

if the column-vectors of $\boldsymbol{A}$ are [linearly dependent](https://mbernste.github.io/posts/linear_independence/), then there exists a vector $\boldsymbol{a}_{*,j}$ that can be expressed as a linear combination of the remaining vectors:

$$\boldsymbol{a}_{*,j} = \sum_{i \neq j} c_i\boldsymbol{a}_{*,i}$$

for some set of constants. Thus we can write the determinant as:

$$\begin{align*}\text{Det}(\boldsymbol{A}) &= \text{Det}(\boldsymbol{a}_{*,1}, \boldsymbol{a}_{*,2}, \dots, \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m} \\ &= \text{Det}\left(\boldsymbol{a}_{*,1}, \boldsymbol{a}_{*,2}, \dots, \sum_{i \neq j} c_i\boldsymbol{a}_{*,i}, \dots, \boldsymbol{a}_{*,m}\right)  \\ &= \sum_{i \neq j} \text{Det}\left(\boldsymbol{a}_{*,1}, \boldsymbol{a}_{*,2}, \dots,  c_i\boldsymbol{a}_{*,i}, \dots, \boldsymbol{a}_{*,m}\right) && \text{Axiom 3} \\ &= \sum_{i \neq j} c_i \text{Det}\left(\boldsymbol{a}_{*,1}, \boldsymbol{a}_{*,2}, \dots,  \boldsymbol{a}_{*,i}, \dots, \boldsymbol{a}_{*,m}\right) && \text{Axiom 3} \\ &= 0 && \text{Axiom 2}  \end{align*}$$ 

In the last line, we see that all of the determinants in the summation are zero because each term is the determinant of a matrix that has a duplicate column vector.

$\square$



<span style="color:#0060C6">**Theorem 3:** Given a triangular matrix, $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, its determinant can be computed by multiplying its diagonal entries.</span>

**Proof:**

We will start with an upper triangular $3 \times 3$ matrix:

$$\boldsymbol{A} := \begin{bmatrix} a_{1,1} & a_{1,2} & a_{1,3} \\ 0 & a_{2,2} & a_{2,3} \\ 0 & 0 & a_{3,3}\end{bmatrix}$$

Now, we will take the second column-vector and decompose it into the sum of two vectors. Because the determinant is linear by Axiom 3, we can rewrite the determinant as follows:

$$\text{Det}(\boldsymbol{A}) = \text{Det}\left(\begin{bmatrix} a_{1,1} & a_{1,2} & a_{1,3} \\ 0 & 0 & a_{2,3} \\ 0 & 0 & a_{3,3}\end{bmatrix} \right) + \text{Det}\left(\begin{bmatrix} a_{1,1} & 0 & a_{1,3} \\ 0 & a_{2,2} & a_{2,3} \\ 0 & 0 & a_{3,3}\end{bmatrix}\right)$$

Note that in the first term of this sum, the column vectors are _linearly dependent_ because the second column-vector can be re-written as a multiple of the first. Thus, according to Theorem 2, its determinant is zero. Hence, the entire first term is zero. Thus, we have:

$$\text{Det}(\boldsymbol{A}) = \text{Det}\left(\begin{bmatrix} a_{1,1} & 0 & a_{1,3} \\ 0 & a_{2,2} & a_{2,3} \\ 0 & 0 & a_{3,3}\end{bmatrix}\right)$$

We can repeat this process with the third column vector by decomposing it into the sum of two vectors and then utilizing the fact that the determinant is linear:

$$\text{Det}(\boldsymbol{A}) = \text{Det}\left(\begin{bmatrix} a_{1,1} & 0 & a_{1,3} \\ 0 & a_{2,2} & 0 \\ 0 & 0 & 0\end{bmatrix}\right) + \text{Det}\left(\begin{bmatrix} a_{1,1} & 0 & 0 \\ 0 & a_{2,2} & a_{2,3} \\ 0 & 0 & 0\end{bmatrix}\right) + \text{Det}\left(\begin{bmatrix} a_{1,1} & 0 & 0 \\ 0 & a_{2,2} & 0 \\ 0 & 0 & a_{3,3}\end{bmatrix}\right)$$

Again, the first and second terms are zero because the columns of each matrix are linearly dependent. This leaves only the third term, which is the determinant of a diagonal matrix. Finally, we see that

$$\begin{align*}\text{Det}(\boldsymbol{A}) &= \text{Det}\left(\begin{bmatrix} a_{1,1} & 0 & 0 \\ 0 & a_{2,2} & 0 \\ 0 & 0 & a_{3,3}\end{bmatrix}\right) \\ &= a_{1,1}a_{2,2}a_{3,3}\text{Det}\left(\begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1\end{bmatrix}\right) && \text{Axiom 3} \\ &= a_{1,1}a_{2,2}a_{3,3} && \text{Axiom 1}\end{align*}$$

Thus, we see that the determinant of the diagonal matrix can be computed by multiplying the entries along the diagonal.

$\square$




<span style="color:#0060C6">**Theorem 4:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, adding a multiple of one column-vector of $\boldsymbol{A}$ to another column-vector does not change the determinant of $\boldsymbol{A}$.</span>

**Proof:**

Say we add $k$ times column $j$ to column $i$. First, 

$$\begin{align*}\text{Det}(\boldsymbol{a}_{*,1} \dots, k\boldsymbol{a}_{*,j} + \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m}) &=  \text{Det}(\boldsymbol{a}_{*,1} \dots, k\boldsymbol{a}_{*,j}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m}) + \text{Det}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m})  && \text{Axiom 3} \\ &= k\text{Det}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,j}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m}) + \text{Det}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m}) && \text{Axiom 3} \\ &= \text{Det}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m}) && \text{Axiom 2}\end{align*}$$

The last line follows from the fact that the first term is computing the determinant of a matrix that has duplicate column-vectors. By Axiom 2, its determinant is zero.

$\square$



<span style="color:#0060C6">**Theorem 5:** Given an elementary matrix that represents row-scaling, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$, where $\boldsymbol{E}$ scales the $j$th row of a system of linear equations by $k$, its determinant is simply $k$.</span>

**Proof:**

Such a matrix would be a diagonal matrix with all ones along the diagonal except for the $j$th entry, which would be $k$. For example, a $4 \times 4$ row-scaling matrix that scales the second row by $4$ would look as follows:

$$\boldsymbol{A} := \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & k & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1\end{bmatrix}$$

Note that this is a triangular matrix and thus, its determinant is given by the product along its diagonals, which is simply $k$. 

$\square$




<span style="color:#0060C6">**Theorem 6:** Given an elementary matrix that represents row-swapping, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that swaps the $i$th and $j$th rows of a system of linear equations, its determinant is simply -1.</span>

**Proof:**

A row-swapping matrix that swaps the $i$th and $j$th rows of a system of linear equations can be formed by simply swapping the $i$th and $j$th column vectors of the identity matrix.  For example, a $4 \times 4$ row-scaling matrix that swaps the second and third rows would look as follows:

$$\boldsymbol{A} := \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1\end{bmatrix}$$

Axiom 1 for the definition of the determinant states that the determinant of the identity matrix is 1. According to Theorem 1, if we swap two column-vectors of a matrix, its determinant is multiplied by -1. Here we are swapping two column-vectors of the identity matrix yielding a determinant of -1.

$\square$




<span style="color:#0060C6">**Theorem 7:** Given an elementary matrix that represents a row-sum, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$, that adds row $j$ multiplied by $k$ to row $i$, its determinant is simply 1.</span>

**Proof:**

An elementary matrix representing a row-sum, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that adds row $j$ multiplied by $k$ to row $i$, is simply the identity matrix, but with element $(i, j)$ equal to $k$. For example, a $4 \times 4$ row-scaling matrix that adds three times the first row to the third would be given by:

$$\boldsymbol{A} := \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 3 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1\end{bmatrix}$$

This matrix is a lower-triangular matrix. By Theorem 3, the determinant of a triangular matrix is the product of the diagonal entries. In this case, all of the diagonal entries are 1. Thus, the determinant is 1. 

$\square$



<span style="color:#0060C6">**Theorem 8:** Given matrices $\boldsymbol{A}, \boldsymbol{B} \in \mathbb{R}^{m \times m}$, it holds that $\text{Det}(AB) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{B})$</span>

**Proof:**

First, if $\boldsymbol{A}$ is singular, then $\text{Det}(AB)$ is also singular. By Theorem 2, we know that the determinant of a singular matrix is zero and thus it trivially holds that $\text{Det}(AB) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{B})$ since both $\text{Det}(AB) = 0$ and also $\text{Det}(A)\text{Det}(B) = 0$ (since $\text{Det}(A)=0$). The same is true if $\boldsymbol{B}$ is singular. Thus, our proof will focus only on the case in which $\boldsymbol{A}$ and $\boldsymbol{B}$ are both invertible.

We first begin by proving that given an elementary matrix $\boldsymbol{E}$, it holds that

$$\text{Det}(AE) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E})$$

To show this, let us consider each of the three types of elementary matrices individually. First, if $\boldsymbol{E}$ is a scaling matrix where the $i$th diagonal entry is a scalar $k$, then $\boldsymbol{AE}$ will scale the $i$th column of $\boldsymbol{A}$ by $k$. By Axiom 3 of the determinant, scaling a single column will scale the full deterimant. Moreover, by Theorem 5, the determinant of $\boldsymbol{E}$ is $k$. Thus,

$$\begin{align*}\text{Det}(\boldsymbol{AE}) &= \text{Det}(\boldsymbol{A})k && \text{Axiom 3} \\ &= \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E}) && \text{Theorem 5}\end{align*}$$

Now let's consider the case where $\boldsymbol{E}$ is a row-swapping matrix that swaps rows $i$ and $j$. Here, $\boldsymbol{AE}$ will swap the $i$th and $j$th columns of $\boldsymbol{A}$. By Theorem 1, swapping any two columns of a matrix flips the sign of the determinant. Moreover, by Theorem 6, the determinant of $\boldsymbol{E}$ is $-1$. Thus,

$$\begin{align*}\text{Det}(\boldsymbol{AE}) &= -\text{Det}(\boldsymbol{A}) && \text{Theorem 1} \\ &= \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E}) && \text{Theorem 6}\end{align*}$$

Finally let's consider the case where  $\boldsymbol{E}$ is an elementary matrix that adds a multiple of one row to another. Here, $\boldsymbol{AE}$ will add a multiple of one column of $\boldsymbol{A}$ to another column. By Theorem 4, this does not change the determinant. Moreover, by Theorem 7, the determinant of $\boldsymbol{E}$ determinant is simply 1. Thus,

$$\begin{align*}\text{Det}(\boldsymbol{AE}) &= -\text{Det}(\boldsymbol{A}) && \text{Theorem 4} \\ &= \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E}) && \text{Theorem 7}\end{align*}$$

Now we have proven that for an invertible matrix $\boldsymbol{A}$ and elementary matrix $\boldsymbol{E}$ it holds that $\text{Det}(\boldsymbol{AE}) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E})$. Let's now turn to the general case where we are multiplying two invertible matrices $\boldsymbol{A}$ and $\boldsymbol{B}$.

As [we have shown](https://mbernste.github.io/posts/row_reduction/), any invertible matrix can be decomposed as the product of some sequence of elementary matrices. Thus, we can write,

$$\boldsymbol{AB} = \boldsymbol{A}\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_m$$

Then we apply our newly proven fact that for an elementary matrix $\boldsymbol{E}$ it holds that $\text{Det}(\boldsymbol{AE}) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E})$. We apply this fact in an iterative way from right to left as shown below:

$$\begin{align*}\text{Det}(\boldsymbol{AB}) &= \text{Det}(\boldsymbol{A}\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_{m-1}\boldsymbol{E}_m) \\ &= \text{Det}(\boldsymbol{A}\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_{m-1})\text{Det}(\boldsymbol{E}_m) \\ &= \text{Det}(\boldsymbol{A}\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_{m-2})\text{Det}(\boldsymbol{E}_{m-1})\text{Det}(\boldsymbol{E}_m) \\ &= \text{Det}(\boldsymbol{A})\prod_{i=1}^m \text{Det}(\boldsymbol{E}_i)  \end{align*}$$

Now we reverse the rule that $\text{Det}(\boldsymbol{AE}) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{E})$ again moving going from right to left:

  $$\begin{align*}\text{Det}(\boldsymbol{AB}) &= \text{Det}(\boldsymbol{A})\prod_{i=1}^m \text{Det}(\boldsymbol{E}_i) \\ &= \text{Det}(\boldsymbol{A})\left( \prod_{i=1}^{m-2}\text{Det}(\boldsymbol{E}_i)\right) \text{Det}(\boldsymbol{E}_{m-1}\boldsymbol{E}_{m}) \\ &= \text{Det}(\boldsymbol{A})\left( \prod_{i=1}^{m-3}\text{Det}(\boldsymbol{E}_i)\right) \text{Det}(\boldsymbol{E}_{m-2} \boldsymbol{E}_{m-1}\boldsymbol{E}_{m}) \\ &= \text{Det}(\boldsymbol{A}) \text{Det}(\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_{m-1}\boldsymbol{E}_m) \\ &=  \text{Det}(\boldsymbol{AB})\end{align*}$$

$\square$


<span style="color:#0060C6">**Theorem 9:** Given a square matrix $\boldsymbol{A}$, it holds that $\text{Det}(\boldsymbol{A}) = \text{Det}(\boldsymbol{A}^T)$.</span>

**Proof:**

First, if $\boldsymbol{A}$ is singular, then $\boldsymbol{A}^T$ [is also singular](https://en.wikipedia.org/wiki/Transpose#:~:text=The%20transpose%20of%20an%20invertible,either%20of%20these%20equivalent%20expressions.). By Theorem 2, the determinant of a singular matrix is zero and thus, $\text{Det}(\boldsymbol{A}) = \text{Det}(\boldsymbol{A}^T) = 0$. 

If $\boldsymbol{A}$ is invertible, then we can express $\boldsymbol{A}$ as the product of some sequence of elementary matrices:

$$\boldsymbol{A} = \boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_m$$

Then, 

$$\boldsymbol{A}^T = \boldsymbol{E}_m^T \boldsymbol{E}_{m-1}^T \dots \boldsymbol{E}_1^T$$

We note that the determinant of every elementary matrix is equal to its transpose. Both scaling elementary matrices and row-swapping matrices are symmetric and thus, their transposes are equal to themselves. Thus the determinant of their transpose is equal to themselves. For a row-sum elementary matrix, the transpose is still a diagonal matrix and thus, its determinant also equals the determinant of its transpose (since by Theorem 3, the determinant of a triangular matrix can be computed by summing the diagonal entries).

Then, we apply Theorem 8 and see that

$$\begin{align*}\text{Det}(\boldsymbol{A}) &= \text{Det}(\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_m\boldsymbol{E}_m) \\ &= \text{Det}(\boldsymbol{E}_1) \text{Det}(\boldsymbol{E}_2) \dots \text{Det}(\boldsymbol{E}_m) \\ &= \text{Det}(\boldsymbol{E}_1^T) \text{Det}(\boldsymbol{E}_2^T) \dots \text{Det}(\boldsymbol{E}_m^T) \\ &= \text{Det}(\boldsymbol{E}_{m}^T) \text{Det}(\boldsymbol{E}_{m-1}^T) \dots \text{Det}(\boldsymbol{E}_1^T) \\ &= \text{Det}(\boldsymbol{E}_m^T \boldsymbol{E}_{m-1}^T \dots \boldsymbol{E}_1^T) \\ &= \text{Det}(\boldsymbol{A}^T)\end{align*}$$

$\square$



<span style="color:#0060C6">**Theorem 10:** Tbe determinant of matrix is linear with respect to the row vectors of the matrix</span>

**Proof:**

This proof follows from Theorem 9 and Axiom 3 of the determinant. Specifically, given a square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$. Let $\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,n}$ be the column vectors of $\boldsymbol{A}^T$. By Axiom 3, it holds that 

$$Det(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j} + \boldsymbol{v}, \dots, \boldsymbol{a}_{*,n}) = Det(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,n}) + Det(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{v}, \dots, \boldsymbol{a}_{*,n})$$

where $\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,n}$ are the column vectors of some matrix $\boldsymbol{A}$.

By Theorem 9, 

$$Det(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j} + \boldsymbol{v}, \dots, \boldsymbol{a}_{*,n}) = Det(\boldsymbol{a}_{1,*}, \dots, \boldsymbol{a}_{j,*}, \dots, \boldsymbol{a}_{n,*}) + Det(\boldsymbol{a}_{1,*}, \dots, \boldsymbol{v}, \dots, \boldsymbol{a}_{n,*})$$

 Next, By Axiom 3, it holds that 

 $$Det(\boldsymbol{a}_{*,1}, \dots, c\boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,n}) = cDet(\boldsymbol{a}_{*,1}, \dots, \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,n})$$


$/square$



<span style="color:#0060C6">**Theorem 11:** Let $\text{Det} : \mathbb{R}^{n \times n} \rightarrow \mathbb{R}$ be a function that satisfies the following three properties:</span>

<span style="color:#0060C6">1. $\text{Det}(\boldsymbol{I}) = 1$</span>

<span style="color:#0060C6">2. Given $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, if any two columns of $\boldsymbol{A}$ are equal, then $\text{Det}(\boldsymbol{A}) = 0$</span>

<span style="color:#0060C6">3. $\text{Det}$ is linear with respect to the column-vectors of its input.</span>

<span style="color:#0060C6">Then $\text{Det}$ is given by</span>

<span style="color:#0060C6">$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$</span>

**Proof:**

Given a matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, let $\boldsymbol{A}_{i,j}$ be the sub-matrix of $\boldsymbol{A}$ where the $i$th and $j$th rows are deleted. For example, for a $3 \times 3$ matrix 

$$\boldsymbol{A} := \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i \end{bmatrix}$$

$\boldsymbol{A}_{1,1}$ would be 

$$\boldsymbol{A}_{1,1} = \begin{bmatrix} e & f \\ h & i \end{bmatrix}$$








