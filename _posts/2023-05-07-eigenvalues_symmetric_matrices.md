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

We may ask, which unit vector solves the following optimization function:

$$\text{arg max}_\boldsymbol{u} \boldsymbol{u^T}\boldsymbol{Su}$$

such that 

$$\boldsymbol{u}^T\boldsymbol{u} = 1$$

We can re-write this optimization problem as 

The Spectral Theorem tells us that because $\boldsymbol{S}$ is symmetric it is _orthogonally diagonalizable_, meaning that we can decompose $\boldsymbol{S}$ as:

$$\boldsymbol{S} = \boldsymbol{PSP^{-1}}$$

Moreover, because $P$ is orthogonal, it holds that $\boldsymbol{P}^{-1} = \boldsymbol{P}^T$. Thus we can write 

$$\text{arg max}_\boldsymbol{u} \boldsymbol{u}^T\boldsymbol{PS}\boldsymbol{P}^T\boldsymbol{u}$$



Note that because $\boldsymbol{P}$ is an orthonormal matrix, we can interpret it as a change-of-basis matrix. Moreover, we see that $\boldsymbol{u}^T\boldsymbol{P} = \boldsymbol{P}^T\boldsymbol{u}$ and that this vector is simply $\boldsymbol{u}$ but expressed using a different basis. Thus, we can simply let 

$$\boldsymbol{z} := \boldsymbol{u}^T\boldsymbol{P} = \boldsymbol{P}^T\boldsymbol{u}$$

and can re-write our optimization problem as 

$$\text{arg max}_\boldsymbol{z}\boldsymbol{zDz}$$

$$\boldsymbol{z}^T\boldsymbol{z} = 1$$

We can write out our objective function more explicitly

$$\boldsymbol{zDz} := \sum_{j=1}^D z_j^2 d_{j,j}$$

This is just a weighted sum of the diagonal entries of $\boldsymbol{D}$ (i.e., eigenvalues of $\boldsymbol{S}$) with weights $z_1^2, \dots, z_d^2$. Moreover, we see that that these weights sum to 1:

$$\sum_{j=1}^D z_j^2 = 1$$

Why is this true? We are enforcing that $\boldsymbol{z}$ is a unit vector and thus:

$$\begin{align*} ||\boldsymbol{z}|| &= 1 \\ \implies \sqrt{\sum_{j=1}^D z_j^2} &= 1 \\ \implies \sum_{j=1}^D z_j^2} &= 1\end{align*}$$ 

Thus, we can re-write our objective function as 

$$\text{arg max}_{z_1, \dots, z_D} \sum_{j=1}^D z_j^2 d_{j,j}$$

such that

$$\sum_{j=1}^D z_j^2 = 1$$

Now, let's reason about the solution to this problem. We see that to maximize the objective, we simply want to assign all of our available weight to the term in the summation with the largest value. That term is the term with the largest eigenvalue: the first term associated with $d_{1,1}$! Thus, our solution is simply the first basis vector:

$$\boldsymbol{z} := \begin{bmatrix}1 & 0 & \dots, 0 \end{bmatrix}$$


