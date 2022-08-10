---
title: 'Elementary row operations, elementary matrices, and the general linear group'
date: 2022-08-09
permalink: /posts/elementary_matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

In a [previous blog post](https://mbernste.github.io/posts/systems_linear_equations/), we showed how systems of linear equations can be represented as a matrix equation. For example, the system of linear equations,

$$\begin{align*}a_{1,1}x_1 + a_{1,2}x_2 + a_{1,3}x_3 &= b_1 \\ a_{2,1}x_1 + a_{2,2}x_2 + a_{2,3}x_3 &= b_2 \\ a_{3,1}x_1 + a_{3,2}x_2 + a_{3,3}x_3 &= b_3 \end{align*}$$

can be represented succinctly as

$$\boldsymbol{Ax} = \boldsymbol{b}$$

where $\boldsymbol{A}$ is the matrix of coefficients $a_{1,1}, a_{1,2}, \dots, a_{3,3}$ and $\boldsymbol{b}$ is the matrix of coefficients of $b_1, b_2,$ and $b_3$.  Furthermore, we noted that this system will have exactly one solution if $\boldsymbol{A}$ is an [invertible matrix](https://mbernste.github.io/posts/inverse_matrices/). 

In this post, we will discuss how one can solve for this exact solution using a series of operations of the system that involve a particular class of invertible matrices called the **elementary matrices**. We will show that any invertible matrix can be converted to another invertible matrix by performing some sequence of matrix multiplications with elementary matrices. 

Elementary row operations
--------------------------

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

First, let's _row swap_ the first and third equations:

$$\begin{align*}2 x_1 + 4 x_2 &= 10  \\ 3 x_2  &= 3 \\ -x_1 - 2 x_2 + x_3 &= -3\end{align*}$$

Next, let's perform _scalar multiplication_ and multiply the first equation by 1/2:

$$\begin{align*}x_1 + 2 x_2 &= 5  \\ 3 x_2 &= 3 \\ -x_1 - 2 x_2 + x_3 &= -3\end{align*}$$

Next, let's perform a _row sum_ and add the first row to the third:

$$\begin{align*}x_1 + 2 x_2 &= 5  \\  3 x_2  &= 3 \\ x_3 &= 2\end{align*}$$

Next, let's perform _scalar multiplication_ and multiply the second equation by 1/3:

$$\begin{align*}x_1 + 2 x_2 &= 5  \\ x_2 &= 1 \\  x_3 &= 2\end{align*}$$

Finally, let's perform a _row sum_ and add -2 multiplied by the second row to the first:

$$\begin{align*}x_1 &= 3  \\ x_2 &= 1 \\ x_3 &= 2\end{align*}$$

And there we go, we've solved the system using these three kinds of operations.

Elementary row operations in matrix notation
--------------------------------------------

Recall, we can represent a system of linear equations as a [matrix equation](https://mbernste.github.io/posts/systems_linear_equations/), we showed how systems of linear equations can be represented as a matrix equation.

The linear system that we just solved can be written as:


When solving the system using the elementary row operations, we needn't write out all of the equations. Really, all we need to do is keep track of how $$\boldsymbol{A}$$ and $$\boldsymbol{b}$$ are being transformed upon each iteration. For ease of notation, we can join $$\boldsymbol{A}$$ and $$\boldsymbol{b}$$ into a single matrix, called an **augmented matrix**. In our example, this augmented matrix would look like:


