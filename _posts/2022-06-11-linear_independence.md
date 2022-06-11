
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

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/span_of_vectors.png" alt="drawing" width="300"/></center>

Note, we can see that in the example above we could construct _ANY_ two dimensional vector from $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$. Thus, the span of these two vectors is all of $\mathbb{R}^2$!

In the figure below, we show another example:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/span_of_vectors_2.png" alt="drawing" width="300"/></center>


This time, $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$ don't span all of $\mathbb{R}^2, but rather, only the line on which $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$ lie.

Linear independence
-------------------

Given a [vector space](https://mbernste.github.io/posts/vector_spaces/), $(\mathcal{V}, \mathcal{F})$, and a set of vectors $S := \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \in \mathcal{V}$, the vectors are said to be **linearly independent** if each vector lies outside the span of the remaining vectors.

Said differently, a set of vectors are linearly independent if you cannot form any of the vectors in the set using a linear combination of any of the other vectors.

Below we demonstrate a set of linearly independent vectors (left) and a set of linearly dependent vectors (right):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_independence.png" alt="drawing" width="300"/></center>



Intuition
---------

At an intuitive level, if a set of vectors is linearly independent, then in a sense there is no "redundancy" in the set of vectors. Each vector contributes something unique to the set of vectors. On the other hand, a linearly dependent set of vectors has some amount of redundancy: if you can form one of the vectors using the other vectors, then why not just remove that vector? We could recover it from the reduced set of vectors any!
