---
title: 'The spaces defined by matrices: column spaces, rows spaces, and null spaces'
date: 2023-05-29
permalink: /posts/matrixspaces/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------


Matrices are one of the fundamental objects studied in linear algebra. While on their surface they appear like simple tables of numbers, [as we have previously described](https://mbernste.github.io/posts/matrices/), there are many ways to view matrices that reveal them to be quite deep: Matrices are at once tables of numbers, sets of vectors, and perhaps most importantly, [linear functions between vector spaces](https://mbernste.github.io/posts/matrices_linear_transformations/). 

In this post, we will further dive into the deeper structures within matrices by showing three vector spaces that are implicitly defined by every matrix:
1. A column space
2. A row space
3. A null space

These spaces are not difficult to define; however the relationships between them are not so obvious. In this post, we will then discuss the properties of these spaces, their relationships to one another, and how their properties determine whether or not a matrix is [invertible or singular](https://mbernste.github.io/posts/inverse_matrices/).

The column space and row space of a matrix
------------------------------------------

The **column space** of a matrix is simply the [vector space](https://mbernste.github.io/posts/vector_spaces/) [spanned](https://mbernste.github.io/posts/linear_independence/) by the column-vectors of a matrix. Likewise, the **row space** of a matrix is the vector space spanned by the row-vectors of a matrix.  


Rank: the intrinsic dimensionality of the column space and row space
--------------------------------------------------------------------

Nullity: the intrinsic dimensionality of the null space
-------------------------------------------------------

The null space is the orthogonal complement to the row space
------------------------------------------------------------

The spaces induced invertible matrices
--------------------------------------

