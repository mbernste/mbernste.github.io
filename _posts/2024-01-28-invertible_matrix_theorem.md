---
title: 'The invertible matrix theorem'
date: 2024-01-28
permalink: /posts/invertible_matrix_theorem/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

Throughout many of my prior linear algebra posts, we have seen theorems of the form "A matrix has property X if and only if it is an invertible matrix". In this post, we will bring these theorems into one place and form a set of equivalent statements that all can be used to define an invertible matrix. These statements form what is called the **invertible matrix theorem**. 

Importantly, any single one of the statements listed in the invertible matrix theorem imply all of the rest of the statements and really, any single statement can be used as the fundamental definition of an invertible matrix. Thus, this theorem not only provides a [multi-angled perspective](https://mbernste.github.io/posts/understanding_3d/) into the nature of invertible matrices, it is also practically useful because if one has some matrix, $\boldsymbol{A}$, then one needs only to prove a single one of the statements in the invertible matrix theorem in order to learn that _all of the remaining statements_ of the invertible matrix theorem are also true of the matrix. 

The invertible matrix therorem
------------------------------

The invertible matrix theorem is stated as follows:

<span style="color:#0060C6">**Theorem 1**: For a given square matrix $\boldsymbol{A} \in \mathbb{R}^n$, if any of the following statements are true of that matrix, then all the remaining statements are also true.</span>

<span style="color:#0060C6">1. There exists a square matrix $\boldsymbol{C} \in \mathbb{R}^{n \times n}$ such that $\boldsymbol{AC} = \boldsymbol{CA} = \boldsymbol{I}$</span>

<span style="color:#0060C6">2. The columns of $\boldsymbol{A}$ are linearly independent</span>

<span style="color:#0060C6">3. The rows of $\boldsymbol{A}$ are linearly independent</span>

<span style="color:#0060C6">4. The columns of $\boldsymbol{A}$ span all of $\mathbb{R}^n$</span>

<span style="color:#0060C6">5. The rows of $\boldsymbol{A}$ span all of $\mathbb{R}^n$</span>

<span style="color:#0060C6">6. The rank of $\boldsymbol{A}$ is $n$</span>

<span style="color:#0060C6">7. The nullity of $\boldsymbol{A}$ is $0$</span>

<span style="color:#0060C6">8. The linear transformation $T(\boldsymbol{x}) := \boldsymbol{Ax}$ is one-to-one and onto.</span>

<span style="color:#0060C6">9. The equation $\boldsymbol{Ax} = \boldsymbol{0}$ has only the trivial solution $\boldsymbol{x} = \boldsymbol{0}$</span>

<span style="color:#0060C6">10. It is possible to use the row reduction algorithm to transform $\boldsymbol{A}$ into $\boldsymbol{I}$</span>

<span style="color:#0060C6">11. There exists a sequence of elementary matrices $\boldsymbol{E}_1, \boldsymbol{E}_2, \dots, \boldsymbol{E}_m$ such that $\boldsymbol{E}_1\boldsymbol{E}_2 \dots \boldsymbol{E}_m\boldsymbol{A} = \boldsymbol{I}$</span>

<span style="color:#0060C6">12. $\text{Det}(\boldsymbol{A}) > 0$</span>

In different texts, the invertible matrix theorem can be written somewhat differently with some texts including some statements that others don't. The _essence_ of the invertible matrix theorem is that there are many seemingly different statements that all define an invertible matrix. Any of these statements imply all of the rest.

To prove the invertible matrix theorem, we will prove the following implications between these statements. Notice that there is a path from every statement to every other statement through these implications. Given two statements $X$ and $Y$ from from the invertible matrix theorem it holds that "$X$ if and only if $Y$". 

The proofs of each of these implications are described below:

**1 $\implies$ 2**: This was proven by [Theorem 4 from my post on invertible matrices](https://mbernste.github.io/posts/inverse_matrices/).

**1 $\implies$ 8**: This was proven by [Theorems 2 and 3 from my post on invertible matrices](https://mbernste.github.io/posts/inverse_matrices/)

**2 $\implies$ 8**: By Theorem XXXX in the Appendix to this post.

**2 $\iff$ 7**: By [Definition 3 from my post on spaces induced by matrices](https://mbernste.github.io/posts/matrixspaces/), the column rank of a matrix is defined to be the maximum number of linearly independent vectors that span the column space of the matrix. By [Theorem 2 from this same post](https://mbernste.github.io/posts/matrixspaces/) the rank of a matrix equals the column rank (since the column rank and row rank are equal, we refer to either as simply the "rank").

**2 $\iff$ 4**: Theorem XXXX in the Appendix to this post.

**3 $\iff$ 7**: By [Definition 3 from my post on spaces induced by matrices](https://mbernste.github.io/posts/matrixspaces/), the row rank of a matrix is defined to be the maximum number of linearly independent vectors that span the row space of the matrix. By [Theorem 2 from this same post](https://mbernste.github.io/posts/matrixspaces/) the rank of a matrix equals the row rank (since the column rank and row rank are equal, we refer to either as simply the "rank").

**3 $\iff$ 5**: Theorem XXXX in the Appendix to this post.

**6 $\iff$ 7**: By [Theorem 3 (Rank-Nullity Theorem) from my post on spaces induced by matrices](https://mbernste.github.io/posts/matrixspaces/).

**7 $\iff$ 9**: By [Definition 5 (nullity) from my post on spaces induced by matrices](https://mbernste.github.io/posts/matrixspaces/).

**8 $\iff$ 10**: By [the discussion presented in my post on row reduction](https://mbernste.github.io/posts/row_reduction/).

**10 $\iff$ 11**: By [the discussion presented in my post on row reduction](https://mbernste.github.io/posts/row_reduction/).

**11 $\implies$ 1**: By Theorem XXXX in the Appendix to this post.

**12 $\iff$ 1**: By Theorem XXXX in the Appendix to this post.


Reconsidering the definition of an invertible matrix
----------------------------------------------------

Recall in our [first post on invertible matrices](https://mbernste.github.io/posts/inverse_matrices/), we defined an invertible matrix as follows:

<span style="color:#0060C6">**Definition 1 (Inverse matrix):** Given a square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, it's **inverse matrix** is the matrix $\boldsymbol{C}$ that when either left or right multiplied by $\boldsymbol{A}$, yields the identity matrix. That is, if for a matrix $\boldsymbol{C}$ it holds that $$\boldsymbol{AC} = \boldsymbol{CA} = \boldsymbol{I}$$, then $\boldsymbol{C}$ is the inverse of $\boldsymbol{A}$. This inverse matrix, $\boldsymbol{C}$ is commonly denoted as $\boldsymbol{A}^{-1}$.</span>

This follows Statement 1 of the invertible matrix theorem. However, in light of the invertible matrix theorem, _any of the statements_ about invertible matrices could have been chosen as the definition of an invertible matrix. While we chose Statement 1, other texts may choose other statements. The rest of the statements would then be proven from that definition. 

Appendix
--------

<span style="color:#0060C6">**Theorem XXXX**:</span>

**Proof:**

Though not proven formally, it is evident that elementary row matrices are invertible.  That is, you can always "undo" the transformation imposed by an elementary row matrix (e.g. for an elementary row matrix that swaps rows, you can always swap them back). Furthermore, since the product of invertible matrices is also invertible, $(\boldsymbol{E}_1\dots\boldsymbol{E}_k)$ is invertible. Thus,

$$\begin{align*} & (\boldsymbol{E}_1\dots\boldsymbol{E}_k)\boldsymbol{A} = \boldsymbol{I} \\ \implies & (\boldsymbol{E}_1\dots\boldsymbol{E}_k)^{-1} (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)\boldsymbol{A} = (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1}\boldsymbol{I} \\ \implies & \boldsymbol{A} = (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1} \boldsymbol{I} \\ \implies & \boldsymbol{A} = \boldsymbol{I}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1} \\ \implies & \boldsymbol{A}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k) = \boldsymbol{I}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k)^{-1}(\boldsymbol{E}_1 \dots \boldsymbol{E}_k) \end{align*}$$ 

Hence, $\boldsymbol{C} := (\boldsymbol{E}_1 \dots \boldsymbol{E}_k)$ is the matrix for which $\boldsymbol{AC} = \boldsymbol{CA} = \boldsymbol{I}$ and is thus $\boldsymbol{A}$'s inverse.

$\square$

<span style="color:#0060C6">**Theorem XXXX**: Given a square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$, $\vert \text{Det}(\boldsymbol)\vert > 0 \iff $ there exists a matrix $\boldsymbol{A}^{-1}$, such that $\boldsymbol{A}\boldsymbol{A}^{-1} = \boldsymbol{A}^{-1}\boldsymbol{A} = \boldsymbol{I}$</span>

**Proof:**





