---
title: 'Row reduction, elementary matrices, and the general linear group'
date: 2022-10-02
permalink: /posts/row_reduction/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

In this post we discuss the row reduction algorithm for solving a system of linear equations that have exactly one solution. We will then show how the row reduction algorithm can be represented as a process involving a sequence of matrix multiplications involving a special class of matrices called elementary matrices. That is, each elementary matrix represents a single elementary row operation in the row reduction algorithm. By viewing row reduction through the lense of matrix multiplication, we can reveal an interesting relationship between invertible matrices: that is, invertible matrices form a mathematical group called the "general linear group".

Introduction
------------

In a [previous blog post](https://mbernste.github.io/posts/systems_linear_equations/), we showed how systems of linear equations can be represented as a matrix equation. For example, the system of linear equations,

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

can be represented succinctly as

$$\boldsymbol{Ax} = \boldsymbol{b}$$

where $\boldsymbol{A}$ is the matrix of coefficients $a_{1,1}, a_{1,2}, \dots, a_{3,3}$ and $\boldsymbol{b}$ is the matrix of coefficients of $b_1, b_2,$ and $b_3$.  Furthermore, we noted that this system will have exactly one solution if $\boldsymbol{A}$ is an [invertible matrix](https://mbernste.github.io/posts/inverse_matrices/). 

In this post, we will discuss how one can solve for this exact solution using a process called called **row reduction** which entails performing a series of algebraic operations on the system. We will then show how the row reduction algorithm can be represented as a process that entails [multiplying](https://mbernste.github.io/posts/matrix_multiplication/) $\boldsymbol{A}$ by a series of matrices called **elementary matrices** in order to convert $\boldsymbol{A}$ to the identity matrix. Each elementary matrix represents a single step of the row reduction algorithm.  

Finally, we will discuss how viewing row reduction this way, we can reveal an elegant mathematical structure regarding invertible matrices: they form a [mathematical group](https://en.wikipedia.org/wiki/Group_(mathematics)). That is, you can always convert one invertible matrix to another by multiplying it by some third invertible matrix! The group formed by invertible matrices is called the **general linear group**.

Row reduction
--------------

Before digging into matrices, let's first discuss how one can go about solving a system of linear equations. Say we have a system with three equations and three variables:

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

To solve such a system, our goal is perform simple algebraic operations on these equations until we convert the system to one with the following form:

$$\begin{align*}x_1 &= c_1 \\ x_2 &= c_2 \\ x_3 &= c_3 \end{align*}$$

where $c_1, c_2$, and $c_3$ are the solutions to the system -- that is, they are the values we can assign to $x_1, x_2$, and $x_3$ so that all of the equations in the system are valid.  

Now, what kinds of algebraic operations can we perform on the equations of the system to solve it? There are three main categories, called **elementary row operations** (we'll see soon, why they have this name):

1. **Scalar multiplication**: Simply multiply both sides of one of the equations by a scalar. For example, 
2. **Row swap**: You can move one equation above or below another. Note, the order the equations are written is irrevalent to the solution, so swapping rows is really just changing how we organize the formulas. Nonetheless, this organization will be important as we demonstrate how elementary matrices can be used to solve the system.
3. **Row sum**: Add a multiple of one equation to another. Note, this is a perfectly valid operation because, if the equality truly holds, then this equations to simply adding the same quantity to both sides of a given equation.

Let's use these operations to solve the following system:

$$\begin{align*}-x_1 - 2 x_2 + x_3 &= -3 \\  3 x_2 &= 3 \\ 2 x_1 + 4 x_2  &= 10\end{align*}$$

1\. First, we _row swap_ the first and third equations:

$$\begin{align*}2 x_1 + 4 x_2 &= 10  \\ 3 x_2  &= 3 \\ -x_1 - 2 x_2 + x_3 &= -3\end{align*}$$

2\. Next, let's perform _scalar multiplication_ and multiply the first equation by 1/2:

$$\begin{align*}x_1 + 2 x_2 &= 5  \\ 3 x_2 &= 3 \\ -x_1 - 2 x_2 + x_3 &= -3\end{align*}$$

3\. Next, let's perform a _row sum_ and add the first row to the third:

$$\begin{align*}x_1 + 2 x_2 &= 5  \\  3 x_2  &= 3 \\ x_3 &= 2\end{align*}$$

4\. Next, let's perform _scalar multiplication_ and multiply the second equation by 1/3:

$$\begin{align*}x_1 + 2 x_2 &= 5  \\ x_2 &= 1 \\  x_3 &= 2\end{align*}$$

5\. Finally, let's perform a _row sum_ and add -2 multiplied by the second row to the first:

$$\begin{align*}x_1 &= 3  \\ x_2 &= 1 \\ x_3 &= 2\end{align*}$$

And there we go, we've solved the system using these elementary row operations. This process of using elementary row operations to solve a system of linear equations is called **row reduction**.

Elementary row operations in matrix notation
--------------------------------------------

Recall, we can represent a system of linear equations as a [matrix equation](https://mbernste.github.io/posts/systems_linear_equations/), we showed how systems of linear equations can be represented as a matrix equation.

The linear system that we just solved can be written as:

$$\begin{bmatrix}-1 & -2 & 1 \\ 0 & 3 & 0 \\ 2 & 4 & 0 \end{bmatrix}\begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}-3 \\ 3 \\ 10\end{bmatrix}$$

When solving the system using the elementary row operations, we needn't write out all of the equations. Really, all we need to do is keep track of how $\boldsymbol{A}$ and $$\boldsymbol{b}$$ are being transformed upon each iteration. For ease of notation, we can join $\boldsymbol{A}$ and $\boldsymbol{b}$ into a single matrix, called an **augmented matrix**. In our example, this augmented matrix would look like:

$$\begin{bmatrix}-1 & -2 & 1 & -3 \\ 0 & 3 & 0 & 3 \\ 2 & 4 & 0 & 10 \end{bmatrix}$$

In the augmented matrix, the final column stores $\boldsymbol{b}$ and all of the previous columns store the columns of $\boldsymbol{A}$. Our execution of the row operations can now operate only on this augmented matrix as follows:

1/. _Row swap_: swap the first and third equations:

$$\begin{bmatrix}2 & 4 & 0 & 10 \\ 0 & 3 & 0 & 3 \\ -1 & -2 & 1 & -3  \end{bmatrix}$$

2/. _Scalar multiplication_: Multiply the first equation by 1/2:

$$\begin{bmatrix}1 & 2 & 0 & 5 \\ 0 & 3 & 0 & 3 \\ -1 & -2 & 1 & -3  \end{bmatrix}$$

3/. _Row sum_: add the first row to the third:

$$\begin{bmatrix}1 & 2 & 0 & 5 \\ 0 & 3 & 0 & 3 \\ 0 & 0 & 1 & 2  \end{bmatrix}$$

4/. _Scalar multiplication_: Multiply the second equation by 1/3:

$$\begin{bmatrix}1 & 2 & 0 & 5 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 2  \end{bmatrix}$$

5/. _Row sum_ and add -2 multiplied by the second row to the first:

$$\begin{bmatrix}1 & 0 & 0 & 3 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 2  \end{bmatrix}$$

Now, let's re-write the augmented matrix as a matrix equation:

$$\begin{bmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}\begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}3 \\ 1 \\ 2\end{bmatrix}$$

Note that $$\boldsymbol{A}$$ has been _transformed_ to the identity matrix $$\boldsymbol{I}$$. This will be a key observation as we move into the next section.

Elementary matrices
-------------------

Notice on each elementary row operation, we transformed the matrix $\boldsymbol{A}$ using a series of steps until it became the identity matrix $\boldsymbol{I}$. In fact, each of these elementary row operations can be represented as a matrix that is operating on $\boldsymbol{I}$. Such a matrix that represents an elementary row operation is called an **elementary matrix**. 

To demonstrate, that our elementary row operations can be performed using matrix multiplication, let's look back at our example. We start with the matrix 

$$\boldsymbol{A} := \begin{bmatrix}-1 & -2 & 1 \\ 0 & 3 & 0 \\ 2 & 4 & 0 \end{bmatrix}$$

Then, first we _row swap_ the first and third equations:

$$\underbrace{\begin{bmatrix}0 & 0 & 1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \end{bmatrix}}_{\boldsymbol{E}_1} \underbrace{\begin{bmatrix}-1 & -2 & 1 \\ 0 & 3 & 0 \\ 2 & 4 & 0 \end{bmatrix}}_{\boldsymbol{A}} = \begin{bmatrix}2 & 4 & 0  \\ 0 & 3 & 0  \\ -1 & -2 & 1  \end{bmatrix}$$

Then perform _scalar multiplication_ and multiply the first equation by 1/2:


$$\underbrace{\begin{bmatrix}1/2 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}}_{\boldsymbol{E_2}} \underbrace{\begin{bmatrix}2 & 4 & 0 \\ 0 & 3 & 0 \\ -1 & -2 & 1  \end{bmatrix}}_{\boldsymbol{E}_1\boldsymbol{A}}  = \begin{bmatrix}1 & 2 & 0 \\ 0 & 3 & 0 \\ -1 & -2 & 1  \end{bmatrix}$$

Then perform a _row sum_ and add the first row to the third:

$$\underbrace{\begin{bmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 0 & 1 \end{bmatrix}}_{\boldsymbol{E}_3} \underbrace{\begin{bmatrix}1 & 2 & 0 \\ 0 & 3 & 0 \\ -1 & -2 & 1  \end{bmatrix}}_{\boldsymbol{E}_2\boldsymbol{E}_1\boldsymbol{A}} = \begin{bmatrix}1 & 2 & 0 \\ 0 & 3 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

Then perform _scalar multiplication_ and multiply the second equation by 1/3:

$$\underbrace{\begin{bmatrix}1 & 0 & 0 \\ 0 & 1/3 & 0 \\ 0 & 0 & 1 \end{bmatrix}}_{\boldsymbol{E}_4} \underbrace{\begin{bmatrix}1 & 2 & 0 \\ 0 & 3 & 0 \\ 0 & 0 & 1 \end{bmatrix}}_{\boldsymbol{E}_3\boldsymbol{E}_2\boldsymbol{E}_1\boldsymbol{A}} = \begin{bmatrix}1 & 2 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1  \end{bmatrix}$$

Then perform a _row sum_ and add -2 multiplied by the second row to the first:

$$\underbrace{\begin{bmatrix}1 & -2 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}}_{\boldsymbol{E}_5} \underbrace{\begin{bmatrix}1 & 2 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1  \end{bmatrix}}_{\boldsymbol{E}_4\boldsymbol{E}_3\boldsymbol{E}_2\boldsymbol{E}_1\boldsymbol{A}} = \begin{bmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1  \end{bmatrix}$$

Notice, we've derived a series of matrices that when multiplied by $\boldsymbol{A}$ produces the identity matrix:

$$\boldsymbol{E}_5\boldsymbol{E}_4\boldsymbol{E}_3\boldsymbol{E}_2\boldsymbol{E}_1\boldsymbol{A} = \boldsymbol{I}$$

By the [definition of an inverse matrix](https://mbernste.github.io/posts/inverse_matrices/), we see that the matrix formed by $\boldsymbol{E}_5\boldsymbol{E}_4\boldsymbol{E}_3\boldsymbol{E}_2\boldsymbol{E}_1$ is the inverse of $\boldsymbol{A}$! That is,

$$\boldsymbol{A}^{-1} = \boldsymbol{E}_5\boldsymbol{E}_4\boldsymbol{E}_3\boldsymbol{E}_2\boldsymbol{E}_1$$

Thus, we have found a way to decompose the inverse of $\boldsymbol{A}$ into a set of matrices that when multiplied together yield its inverse. Each of these matrices represents a transformation on $\boldsymbol{A}$ equivalent to an elementary row operation that one would use to solve an equation of the form $\boldsymbol{Ax} = \boldsymbol{b}$!

Transforming one invertible matrix to another via a third invertible matrix
---------------------------------------------------------------------------

Viewing the row reduction algorithm through the lense of matrix multiplication provides insight into invertible matrices in general. Specifically, we can show that any invertible matrix $\boldsymbol{A}$ can be converted to another invertible matrix $\boldsymbol{B}$ by multiplying $\boldsymbol{A}$ by a third invertible matrix $\boldsymbol{C}$. 

First, notice that each elementary matrix is invertible. The inverse of an elementary matrix that row-scales by a constant $c$ is simply the elementary matrix that scales the row by $\frac{1}{c}$. The inverse of an elementary matrix that row swaps is simply the elementary matrix that swaps the rows back to their original configuration. The inverse of an elementary matrix that performs a row sum is simply the elementary matrix that performs the subtraction. Thus we see that not only are elementary matrices invertible, but their inverses are also elementary matrices!

Because these elementary row matrices are invertible, instead of starting with some invertible matrix $\boldsymbol{A}$ and producing the identity matrix $\boldsymbol{I}$ via some sequence of multiplications, 

$$\boldsymbol{I} = \boldsymbol{E}_n \dots, \boldsymbol{E}_1\boldsymbol{A}$$

we can instead start with the identity matrix and produce $\boldsymbol{A}$:

$$\boldsymbol{A} = \boldsymbol{E}^{-1}_1 \dots \boldsymbol{E}^{-1}_n\boldsymbol{I} $$

From this fact, we can see that we can go from any invertible matrix to another by multiplying the matrix with some series of elementary matrices. For example, say we have two different invertible matrices $\boldsymbol{A}$ and $\boldsymbol{B}$. Then we can transform $\boldsymbol{A}$ into the identity matrix via some some sequence of multiplications by elementary matrices:

$$\boldsymbol{I} = \boldsymbol{E}_n \dots, \boldsymbol{E}_1\boldsymbol{A}$$

We can also transform $\boldsymbol{B}$ into the identity matrix via some some sequence of multiplications by elementary matrices:

$$\boldsymbol{I} = \boldsymbol{E}_{n+m} \dots, \boldsymbol{E}_{n+1}\boldsymbol{B}$$

We can convert $\boldsymbol{A}$ to $\boldsymbol{B}$ by converting $\boldsymbol{A}$ to $\boldsymbol{I}$ and then convert $\boldsymbol{I}$ to $\boldsymbol{B}$ via the inverses of the elementary matrices used to convert $\boldsymbol{B}$ to $\boldsymbol{I}$:

$$\boldsymbol{B} = \boldsymbol{E}^{-1}_{n+1} \dots \boldsymbol{E}^{-1}_{n+m}\boldsymbol{E}_n \dots, \boldsymbol{E}_1\boldsymbol{A}

Let's let the matrix $\boldsymbol{C}$ be defined as:

$$\boldsymbol{C} := \boldsymbol{E}^{-1}_{n+1} \dots \boldsymbol{E}^{-1}_{n+m}\boldsymbol{E}_n \dots, \boldsymbol{E}_1$$

Then, we see that 

$$\boldsymbol{B} = \boldsymbol{CA}$$

Notably, $\boldsymbol{C}$ is also an invertible matrix because all of the elementary matrices we multiplied together to produce $\boldsymbol{C}$ are all invertible! 

The general linear group
------------------------

Now we can see that the set of all invertible matrices of shape $n \times n$, together with the matrix multiplication operation, form a [group](https://en.wikipedia.org/wiki/Group_(mathematics)).



