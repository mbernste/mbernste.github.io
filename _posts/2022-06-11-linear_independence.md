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

In the figure below, we show two vectors, $\boldsymbol{x}_1$ and $\boldsymbol{x}_2$ (left), and two examples of vectors in their span: 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/span_of_vectors.png" alt="drawing" width="300"/></center>

Note, we can see that in the example above we could construct _ANY_ two dimensional vector from $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$. Thus, the span of these two vectors is all of $\mathbb{R}^2$!

In the figure below, we show another example:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/span_of_vectors_2.png" alt="drawing" width="450"/></center>

This time, $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$ don't span all of $\mathbb{R}^2, but rather, only the line on which $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$ lie.

Linear independence
-------------------

Given a [vector space](https://mbernste.github.io/posts/vector_spaces/), $(\mathcal{V}, \mathcal{F})$, and a set of vectors $S := \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \in \mathcal{V}$, the vectors are said to be **linearly independent** if each vector lies outside the span of the remaining vectors.

Said differently, a set of vectors are linearly independent if you cannot form any of the vectors in the set using a linear combination of any of the other vectors.

Below we demonstrate a set of linearly independent vectors (left) and a set of linearly dependent vectors (right):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_independence.png" alt="drawing" width="450"/></center>

Why is the set on the right linearly dependent? As you can see below, we can use any of the two vectors to construct the third:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_independence_symmetry.png" alt="drawing" width="450"/></center>

This example illustrates an important point about linear dependence: it is a quality that pertains to a _set of vectors_ rather than any particular vector within the set. That is, if a set of vectors are linearly dependent, then ANY of the vectors can be constructed using the remaining vectors. 

Intuition
---------

At an intuitive level, if a set of vectors is linearly dependent, then in a sense there is no "reduntancy" in the set of vectors. What do we mean by redundancy? By removing a vector from a linearly dependent set of vectors, the span of the set of vectors will remain the same! On the other hand, for a linearly dependent set of vectors, each vector is vital for defining the span of the set's vectors. If you remove even one vector, the span of the vectors will change -- in fact, it will get smaller!
