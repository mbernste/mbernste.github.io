---
title: 'The Eigenvalues of Symmetric Matrices'
date: 2023-05-07
permalink: /posts/eigensym/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_My understanding of this material partly arouse from the [blog posts by Peter Bloem](https://peterbloem.nl/blog/pca-2) re-written here in my own words._

Problem
-------

We are interested in solving a sequence of optimization problems where each solution contrains the solutions to the following problems. Given a symmetrix matrix $\boldsymbol{S}$, the first problem asks, which unit vector solves the following optimization function:

$$\underset{\boldsymbol{u}_1 }{\text{argmax}} \ \boldsymbol{u}_1^T\boldsymbol{S}\boldsymbol{u}_1$$

such that 

$$\boldsymbol{u}_1^T\boldsymbol{u}_1 = 1$$

For the next optimization problem we want to solve:

$$\underset{\boldsymbol{u}_2 }{\text{argmax}} \ \boldsymbol{u}_2^T\boldsymbol{S}\boldsymbol{u}_2$$

such that 

$$\boldsymbol{u}_1^T\boldsymbol{u}_1 = 1$$

with the additional constraint that _the first solution is orthogonal to the second_:

$$\boldsymbol{u}_1^T\boldsymbol{u}_2 = 0$$

More generally, we want each successive solution to be orthogonal to all of the previous solutions. For the $J$th optimization problem we want to solve:

$$\underset{\boldsymbol{u}_J }{\text{argmax}} \ \boldsymbol{u}_J^T\boldsymbol{S}\boldsymbol{u}_J$$


such that

$$\boldsymbol{u}_J^T\boldsymbol{u}_J = 1$$

with the additional constraint that _the first solution is orthogonal to the second_:

$$\forall i \in {1 \dots, J-1}, \ \boldsymbol{u}_J^T\boldsymbol{u}_i = 0$$


Solution
--------

Let's start with the first optimization problem: 

$$\underset{\boldsymbol{u}_1 }{\text{argmax}} \ \boldsymbol{u}_1^T\boldsymbol{S}\boldsymbol{u}_1$$

such that 

$$\boldsymbol{u}_1^T\boldsymbol{u}_1 = 1$$

The [Spectral Theorem](https://inst.eecs.berkeley.edu/~ee127/sp21/livebook/l_sym_sed.html) tells us that because $\boldsymbol{S}$ is symmetric it is _orthogonally diagonalizable_, meaning that we can decompose $\boldsymbol{S}$ as:

$$\boldsymbol{S} = \boldsymbol{PDP^{-1}}$$

where $boldsymbol{D}$ is a diagonal matrix with eigenvectors along the diagonal (in order of size) and $\boldsymbol{P}$ is an orthonormal matrix. Because $P$ is orthonogonal, it holds that $\boldsymbol{P}^{-1} = \boldsymbol{P}^T$. Thus we can write 

$$\underset{\boldsymbol{u}}{\text{argmax}} \ \boldsymbol{u}^T\boldsymbol{PS}\boldsymbol{P}^T\boldsymbol{u}$$



Note that because $\boldsymbol{P}$ is an orthonormal matrix, we can interpret it as a change-of-basis matrix. Moreover, we see that $\boldsymbol{u}^T\boldsymbol{P} = \boldsymbol{P}^T\boldsymbol{u}$ and that this vector is simply $\boldsymbol{u}$ but expressed using a different basis. Thus, we can simply let 

$$\boldsymbol{z} := \boldsymbol{u}^T\boldsymbol{P} = \boldsymbol{P}^T\boldsymbol{u}$$

and can re-write our optimization problem as 

$$\underset{\boldsymbol{z}}{\text{argmax}} \ \boldsymbol{zDz}$$

$$\boldsymbol{z}^T\boldsymbol{z} = 1$$

We can write out our objective function more explicitly

$$\boldsymbol{zDz} := \sum_{j=1}^D z_j^2 d_{j,j}$$

This is just a weighted sum of the diagonal entries of $\boldsymbol{D}$ (i.e., eigenvalues of $\boldsymbol{S}$) with weights $z_1^2, \dots, z_d^2$. Moreover, we see that that these weights sum to 1:

$$\sum_{j=1}^D z_j^2 = 1$$

Why is this true? We are enforcing that $\boldsymbol{z}$ is a unit vector and thus:

$$\begin{align*} ||\boldsymbol{z}|| &= 1 \\ \implies \sqrt{ \sum_{j=1}^D z_j^2 }  &= 1 \\ \implies \sum_{j=1}^D z_j^2 &= 1\end{align*}$$ 

Thus, we can re-write our objective function as 

$$\text{arg max}_{z_1, \dots, z_D} \sum_{j=1}^D z_j^2 d_{j,j}$$

such that

$$\sum_{j=1}^D z_j^2 = 1$$

Now, let's reason about the solution to this problem. We see that to maximize the objective, we simply want to assign all of our available weight to the term in the summation with the largest value. That term is the term with the largest eigenvalue: the first term associated with $d_{1,1}$! Thus, our solution is simply the first basis vector:

$$\boldsymbol{z} := \begin{bmatrix}1 & 0 & \dots & 0 \end{bmatrix}$$

What does this solution mean? It is telling us that the vector $\boldsymbol{u}$ that optimizes our original objective simply the vector $\boldsymbol{u}$ such that $\boldsymbol{P}^T\boldsymbol{u}$ is the first basis vector. Recall $\boldsymbol{P}^T$ re-expresses vectors into a new basis defined by the eigenvectors of $\boldsymbol{S}$. Thus, the $\boldsymbol{u}$ that maximizes our objective is itself the first eigenvector of $\boldsymbol{S}$!

Now, what about the next solutions in our iterative optimization problem?
