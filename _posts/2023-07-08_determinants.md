---
title: 'What the determinant tells us about a matrix'
date: 2023-07-08
permalink: /posts/determinants/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_


Determinants describe volume
----------------------------

As with most topics, it helps to view determinants from [multiple perspectives](https://mbernste.github.io/posts/understanding_3d/). To understand determinants from multiple perspectives, we will also need to view matrices from multiple perspectives. Recall from a [previous post](https://mbernste.github.io/posts/matrices/) that there are three perpectives I find helpful for viewing matrices:

1. **Perspective 1:** As a table of values
2. **Perspective 2:** As a list of column vectors (or row vectors)
3. **Perspective 3:** As a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/) between vector spaces

Let's start with viewing matrices from Perspective 2. Viewing a matrix as a list of column vectors, the determinant of a matrix can be understood to be a function that captures the geometric volume of the parallelopiped formed by the column vectors of the matrix. In fact, it is from this 

Determinants describe how much matrices grow or shrink objects
--------------------------------------------------------------

Recall from a [previous discussion](https://mbernste.github.io/posts/matrices/), that there are three main perspectives for which one can view a matrix:

1. As a table of values
2. As a list of column vectors (or row vectors)
3. As a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/) between vector spaces

So far, we have discussed how the determinant captures the volume of the paralellopiped formed by the column-vectors of a matrix. This discussion has thus primarily viewed matrices from Perspective 2: viewing matrices as a list of column vectors. Now, we will discuss what the determinant captures when viewing matrices from Perspective 3: viewing matrices as linear transformations between vector spaces.

First, let's think about what a matrix, $\boldsymbol{A} \in \mathbb{R}^{2 \times 2}$ will do to the standard basis vectors in $\mathbb{R}^{2 \times 2}$. Specifically, we see that the first standard basis vector will be transformed to the first column-vector of $\boldsymbol{A}$:

$$\begin{bmatrix}a & b \\ c & d\end{bmatrix}\begin{bmatrix}1 \\ 0\end{bmatrix} = \begin{bmatrix}a \\ c\end{bmatrix}$$

Similarly, the second standard basis vector will be transformed to the second column of $\boldsymbol{A}$:

$$\begin{bmatrix}a & b \\ c & d\end{bmatrix}\begin{bmatrix}0 \\ 1\end{bmatrix} = \begin{bmatrix}b \\ d\end{bmatrix}$$

Thus, if we multiply $\boldsymbol{A}$ by the matrix we that is formed by using the two standard basis vectors as columns (which is just the identity matrix), we get back $\boldsymbol{A}$:

$$\boldsymbol{AI} = \boldsymbol{A}$$

Here, we are viewing the matrix $\boldsymbol{A}$ as a function and are viewing $\boldsymbol{I}$ as a list of vectors. We see that $\boldsymbol{A}$ transforms the $\boldsymbol{I}$ into $\boldsymbol{A}$. Moreover, we see that the column vectors of $\boldsymbol{I}$ form the unit cube and $\boldsymbol{A}$ transforms this unit cube into a parallelogram with an area equal to the determinant of $\boldsymbol{A}$. Thus, we see that the matrix $\boldsymbol{A}$ has, in a sense, blown up the area of the original cube to an object that has a size equal to  $\lvert \text{Det}(\boldsymbol{A}) \rvert$. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/determinant_grow_unit_cube.png" alt="drawing" width="500"/></center>

This pattern does not just hold for unit cubes nor does it hold for just $\mathbb{R}^2$. In fact, any polyhedron in any $n$ dimensional space that is transformed by some matrix $\boldsymbol{A}$ will become a new polyhedron with an area that is grown or shrunk by a factor equal $\lvert \text{Det}(\boldsymbol{A}) \rvert$. Thus, determinants describe a very fundamental quality of a matrix's linear transformation. It describes the magnitude by which the matrix grows or shrinks things under its transformation.

From this perspective, we can gain a much better intuition for Theorem 9 presented in the previous section. Specifically, we see why it makes sense that $\text{Det}(\boldsymbol{AB}) = \text{Det}(\boldsymbol{A})\text{Det}(\boldsymbol{B})$. First, recall that a matrix product $\boldsymbol{AB}$ can be interpreted as a [composition of linear transformations](https://mbernste.github.io/posts/matrix_multiplication/). That is, the transformation carried out by $\boldsymbol{AB}$ is equivalent to the transformation carried out by $\boldsymbol{B}$ followed consecutively by $\boldsymbol{A}$. Let's now think about how the area of an object will change as we first transform it by $\boldsymbol{B}$ followed by $\boldsymbol{A}$. First, transforming it by $\boldsymbol{B}$ will scale its area by a factor of $\lvert \text{Det}(\boldsymbol{B}) \rvert$. Then, transforming it by $\boldsymbol{A}$ will scale its area by a factor of $\lvert \text{Det}(\boldsymbol{A}) \rvert$. The total change of its area is thus $\lvert \text{Det}(\boldsymbol{B}) \rvert \lvert \text{Det}(\boldsymbol{A}) \rvert$. This can ve visualized below:

<br>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/determinant_matrix_product.png" alt="drawing" width="800"/></center>

<br>

Above we see a unit cube first transformed into a parallelogram by $\boldsymbol{B}$. It's area grows by a factor of $\lvert \text{Det}(\boldsymbol{B}) \rvert$. This parallelogram is then transformed into another paralellogram by $\boldsymbol{A}$. It's transformation grows by an additional factor of $\lvert \text{Det}(\boldsymbol{A}) \rvert$. Thus, the final scaling factor of the unit cube's area under $\boldsymbol{AB}$ is $\lvert \text{Det}(\boldsymbol{A}) \rvert \lvert \text{Det}(\boldsymbol{B})\rvert$. Equivalently, because the unit cube was transformed by $\boldsymbol{AB}$, its area grew by a factor of $\lvert \text{Det}(\boldsymbol{AB}) \rvert$.



Interpreting the sign of the determinant
----------------------------------------

So far, we have shown how the absolute value of the determinant describes the volume of a parallelopiped formed by a matrix's columns; however, the determinant can be either positive or negative, which begs the question: what is the interpetation of a negative determinant?

Unfortunately, the determinant's ability to capture volume is not the full story! The determinant also captures an additional characteristic of a matrix's linear transformation: **it's ability to preserve or invert the orientation of objects that it transforms**.
