---
title: 'Demystifying determinants'
date: 2023-05-29
permalink: /posts/determinants/
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

In the previous section, we outlined three axioms that define fundamental ways in which the volume of a parallelogram is related to the vectors that form its sides. We will show that there is only one analytica formula for the determinant that satisfies these axioms. That formula is:

$$\text{Det}(\boldsymbol{A}) := \begin{cases} a_{1,1}a_{2,2} - a_{1,2}a_{2,1} & \text{if $m = 2$} \\ \sum_{i=1}^m (-1)^{i+1} a_{i,1} \text{Det}(\boldsymbol{A}_{-1,-i}) & \text{if $m > 2$}\end{cases}$$

For now, we will assume that there exists a function $\text{Det}: \mathbb{R}^{m \times m} \rightarrow \mathbb{R}$ that satisfies our three axioms and will subsequently prove a series of theorems and lemmas that will build up to this final formula. Many of these theorems/lemmas will make heavy use of the fact that [invertible matrices can be decomposed into the product of elementary matrices](https://mbernste.github.io/posts/row_reduction/).

<span style="color:#0060C6">**Theorem 1:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if we exchange any two column-vectors of $\boldsymbol{A}$ to form a new matrix $\boldsymbol{A}'$, then $\text{Det}(\boldsymbol{A}') = -\text{Det}(\boldsymbol{A})$</span>

<span style="color:#0060C6">**Theorem 2:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if if it's column-vectors are [linearly dependent](https://mbernste.github.io/posts/linear_independence/), then its determinant is zero.</span>

<span style="color:#0060C6">**Theorem 3:** Given a triangular matrix, $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, its determinant can be computed by multiplying its diagonal entries.</span>

<span style="color:#0060C6">**Theorem 4:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, adding a multiple of one column-vector of $\boldsymbol{A}$ to another column-vector does not change the determinant of $\boldsymbol{A}$.</span>

<span style="color:#0060C6">**Theorem 5:** Given an [elementary matrix](https://mbernste.github.io/posts/row_reduction/) that represents row-scaling, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$, where $\boldsymbol{E}$ scales the $j$th row of a system of linear equations by $k$, its determinant is simply $k$.</span>

<span style="color:#0060C6">**Theorem 6:** Given an [elementary matrix](https://mbernste.github.io/posts/row_reduction/) that represents row-swapping, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that swaps the $i$th and $j$th rows of a system of linear equations, its determinant is simply -1.</span>

<span style="color:#0060C6">**Theorem 7:** Given an [elementary matrix](https://mbernste.github.io/posts/row_reduction/) that represents a row-sum, $\boldsymbol{E} \in \mathbb{R}^{m \times m}$ that multiplies row $j$ by $k$ times row $i$, its determinant is simply 1.</span>

<span style="color:#0060C6">**Theorem 8:** Given a square matrix $\boldsymbol{A}$, it holds that $\text{Det}(\boldsymbol{A}) = \text{Det}(\boldsymbol{A}^T)$.</span>

<span style="color:#0060C6">**Theorem 9:** Given matrices $\boldsymbol{A}, \boldsymbol{B} \in \mathbb{R}^{m \times m}$, it holds that $\text{Det}(AB) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{B})$</span>


If determinants capture the notion of volume, then why can it be negative?
--------------------------------------------------------------------------

The relationship between determinants and the invertability of a matrix
-----------------------------------------------------------------------

The determinant of a matrix product
-----------------------------------

Appendix
--------

<span style="color:#0060C6">**Theorem 1:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if we exchange any two column-vectors of $\boldsymbol{A}$ to form a new matrix $\boldsymbol{A}'$, then $\text{Det}(\boldsymbol{A}') = -\text{Det}(\boldsymbol{A})$</span>

**Proof:**

Let columns $i$ and $j$ be the columns that we exchange within $\boldsymbol{A}$. For ease of notation, let us define 

$$\text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j}) := \text{Det}_{i,j}(\boldsymbol{a}_{*,1} \dots, \boldsymbol{a}_{*,i}, \dots,  \boldsymbol{a}_{*,j}, \dots, \boldsymbol{a}_{*,m})$$

to be the determinant of $\boldsymbol{A}$ as a function of only the $i$th and $j$th column-vectors of $\boldsymbol{A}$ where the other column-vectors are held fixed. Then, we see that

$$\begin{align*} \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j}) &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,j})  + \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i}) && \text{Axiom 2} \\ &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= \text{Det}_{i,j}(\boldsymbol{a}_{*,i}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) - \text{Det}_{i,j}(\boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 2} \\ &= \text{Det}_{i,j}(-\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= -\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i} + \boldsymbol{a}_{*,j}) && \text{Axiom 3} \\ &= -(\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i}) - \text{Det}_{i,j}(\boldsymbol{a}_{*,j},\boldsymbol{a}_{*,j})) && \text{Axiom 3} \\ &=  -\text{Det}_{i,j}(\boldsymbol{a}_{*,j}, \boldsymbol{a}_{*,i}) && \text{Axiom 2}\end{align*}$$

$\square$



<span style="color:#0060C6">**Theorem 2:** Given a matrix $\boldsymbol{A} \in \mathbb{R}^{m \times m}$, if if it's column-vectors are [linearly dependent](https://mbernste.github.io/posts/linear_independence/), then its determinant is zero.</span>

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



<span style="color:#0060C6">**Theorem 8:** Given a square matrix $\boldsymbol{A}$, it holds that $\text{Det}(\boldsymbol{A}) = \text{Det}(\boldsymbol{A}^T)$.</span>

**Proof:**

First, let's assume that $\boldsymbol{A}$ is singular. This means that the column-vectors of $\boldsymbol{A}$ are linearly dependent and thus, by Theorem 2, $\text{Det}(\boldsymbol{A}) = 0$. While not proven here, it holds that the [rank](https://en.wikipedia.org/wiki/Rank_(linear_algebra)) of the column space of a matrix equals the rank of the row space. We know that a matrix is singular if and only if it's column-rank is less than than the number of columns. Thus, 

$\square$





