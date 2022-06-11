
---
title: 'Span and linear independence'
date: 2022-06-11
permalink: /posts/linear_independence/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

Introduction
------------

An extremely important concept in the study of vector spaces is that of _linear independence_. At a high level, a set of vectors are said to be **linearly independent** if you cannot form any vector in the set using any combination of the other vectors in the set. If a set of vectors does not have this quality -- that is, a vector in the set can be formed from some combination of others -- then the set is said to be **linearly dependent**.

In this post, we will present a more foundatioanl concept, the _span_ of a set of vectors, and then move on to the definition for linear independence. Finally, we will discuss a high-level intuition for why the concept of linearly independence is so important.

Span
----

Specifically, given a [vector space](https://mbernste.github.io/posts/vector_spaces/), $(\mathcal{V}, \mathcal{F})$
and a set of vectors $S := \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \in \mathcal{V}$ the set of all vectors that can be formed via a weighted sum of the vectors is called the **span** of these vectors. 

That is, the span of a set of vectors $S$ is the set 

$$\text{Span}(S) := \left\{ \sum_{i=1}^n c_i\boldsymbol{x}_i \mid c_1, \dots, c_n \in \mathcal{F} \right\}$$

Intuitively, you can think of $\text{Span}(S)$ as the set of all vectors that can be "constructed" by the vectors in $S$. 

In the figure below, we show two vectors, $\boldsymbol{x}_1 and $\boldsymbol{x}_2$ (left), and two examples of vectors in the span of $\boldsymbol{x}_1 and $\boldsymbol{x}_2$: 

Note, we can see that in the example above we could construct _ANY_ two dimensional vector from $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$. Thus, the span of these two vectors is all of $\mathbb{R}^2$!




Linear independence
-------------------

A set of vectors $\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_n \in \mathcal{V}$ are said to be **linearly independent** if you cannot form any of the vectors in the set using a weighted combination, or **linear combination**, of any of the other vectors.

For example, say we have a set of three vectors, $$\boldsymbol{x}_1, \boldsymbol{x}_2, \boldsymbol{x}_3\ \in \mathbb{R}^3$$ where:

$$\boldsymbol{x}_1 := \begin{bmatrix}1 \\ 2 \\ 3\end{bmatrix}$$

$$\boldsymbol{x}_2 := \begin{bmatrix}2 \\ 1 \\ 3\end{bmatrix}$$

$$\boldsymbol{x}_3 := \begin{bmatrix}5 \\ 4 \\ 9\end{bmatrix}$$

These vectors are NOT linearly independent becase we can see that $\boldsymbol{x}_3$ is simply a weighted sum of $\boldsymbol{x}_1$ and $\boldsymbol{x}_2$:

$$\begin{align*}\boldsymbol{x}_3 &= \boldsymbol{x}_1 + 2\boldsymbol{x}_3 \\ \begin{bmatrix}5 \\ 4 \\ 9\end{bmatrix} &= \begin{bmatrix}1 \\ 2 \\ 3\end{bmatrix} + 2 \begin{bmatrix}2 \\ 1 \\ 3\end{bmatrix}\end{align*}$$

Geometrically, we see that these vectors span a plan in three dimensional space.

In contrast


Intuition
---------

At an intuitive level, if a set of vectors is linearly independent, then in a sense there is no "redundancy" in the set of vectors. Each vector contributes something unique to the set of vectors. On the other hand, a linearly dependent set of vectors has some amount of redundancy: if you can form one of the vectors using the other vectors, then why not just remove that vector? We could recover it from the reduced set of vectors any!
