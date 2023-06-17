---
title: 'Span and linear independence'
date: 2022-06-11
permalink: /posts/linear_independence/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

_A very important concept linear algebra is that of linear independence. In this blog post we present the definition for the span of a set of vectors. Then, we use this definition to discuss the definition for linear independence. Finally, we discuss some intuition into this fundamental idea._

Introduction
------------

A very important concept in the study of vector spaces is that of _linear independence_. At a high level, a set of vectors are said to be **linearly independent** if you cannot form any vector in the set using any combination of the other vectors in the set. If a set of vectors does not have this quality -- that is, a vector in the set can be formed from some combination of others -- then the set is said to be **linearly dependent**.

In this post, we will first present a more fundamental concept, the _span_ of a set of vectors, and then move on to the definition for linear independence. Finally, we will discuss high-level intuition for why the concept of linearly independence is so important.

Span
----

Given a set of vectors, the **span** of these vectors is the set of the vectors that can be "generated" by taking linear combinations of these vectors. More rigorously,

<span style="color:#0060C6">**Definition 1 (span):** Given a [vector space](https://mbernste.github.io/posts/vector_spaces/), $(\mathcal{V}, \mathcal{F})$ and a set of vectors $S := \\{ \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \\} \in \mathcal{V}$, the **span** of $S$, denoted $\text{Span}(S)$ is the set of all vectors that can be formed by taking a linear combination of vectors in $S$. That is,</span>

<center><span style="color:#0060C6">$$\text{Span}(S) := \left\{ \sum_{i=1}^n c_i\boldsymbol{x}_i \mid c_1, \dots, c_n \in \mathcal{F} \right\}$$ </span></center>

Intuitively, you can think of $S$ as a set of "building blocks" and the $\text{Span}(S)$ as the set of all vectors that can be "constructed" from these building blocks. To illustrate this point, we illustrate two vectors, $\boldsymbol{x}_1$ and $\boldsymbol{x}_2$ (left), and two examples of vectors in their span (right): 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/span_of_vectors.png" alt="drawing" width="600"/></center>

In this example we see that we can construct _ANY_ two dimensional vector from $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$. Thus, the span of these two vectors is all of $\mathbb{R}^2$! This is not always the case. In the figure below, we show an example of two vectors in $\mathbb{R}^2$ with a different span:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/span_of_vectors_2.png" alt="drawing" width="600"/></center>

Here, $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$ don't span all of $\mathbb{R}^2$, but rather, only the line on which $\boldsymbol{x}_1$ and $\boldsymbol{x_2}$ lie.

Linear independence
-------------------

Given a [vector space](https://mbernste.github.io/posts/vector_spaces/), $(\mathcal{V}, \mathcal{F})$, and a set of vectors $S := \\{ \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \\} \in \mathcal{V}$, the vectors are said to be **linearly independent** if each vector lies outside the span of the remaining vectors. More rigorously,

<span style="color:#0060C6">**Definition 2 (linear independence):** Given a [vector space](https://mbernste.github.io/posts/vector_spaces/), $(\mathcal{V}, \mathcal{F})$ and a set of vectors $S := \\{ \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \\} \in \mathcal{V}$, $S$ is called **linearly independent** if for each vector $\boldsymbol{x_i} \in S$, it holds that $\boldsymbol{x}_i \notin \text{Span}(S \setminus \\{ \boldsymbol{x}_i \\})$.</span>

Said differently, a set of vectors are linearly independent if you cannot form any of the vectors in the set using a linear combination of any of the other vectors. Below we demonstrate a set of linearly independent vectors (left) and a set of linearly dependent vectors (right):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_independence.png" alt="drawing" width="600"/></center>

Why is the set on the right linearly dependent? As you can see below, we can use any of the two vectors to construct the third:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_independence_symmetry.png" alt="drawing" width="600"/></center>

Linear independence among a set of vectors implies another key fact about these vectors: the only way to construct the zero vector from these vectors is by using coefficients that are only zeros. That is, if $S := \\{ \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \\}$ are linearly independent, then in order for the following to hold

$$\boldsymbol{\sum_{i=1}^n c_i \boldsymbol{x}_i} = \boldsymbol{0}$$

it must be the case that all of the coefficients are zero. That is, $c_1 = c_2 = \dots, c_n = 0$. In contrast, for a dependent set of vectors, we can construct the zero vector by canceling one vector out using a combination of the other vectors as shown below.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/linear_dependence_zero_vector.png" alt="drawing" width="300"/></center>

This is proven formally in Theorem 1 in the Appendix to this blog post.


Intuition for linear independence
---------------------------------

There are two ways I think about linear independence: in terms of information content and in terms of [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/). Let me explain.

First, if a set of vectors is linearly dependent, then in a sense there is "reduntant information" within these vectors. What do I mean by "redundant information"? In a linear dependent set, there exists a vector in that set for which if we removed that vector, the span of the set would remain the same! On the other hand, for a linearly independent set of vectors, each vector is vital for defining the span of the set's vectors. If you remove even one vector, the span of the vectors will change (it will become smaller)!

One can also think about the concept of linear dependence/indepence in terms of [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/) . That is, a set of $n$ linearly independent vectors $S := \\{ \boldsymbol{x}_1, \dots, \boldsymbol{x}_n \\}$ spans a space with an [intrinsic dimensionality](https://mbernste.github.io/posts/intrinsic_dimensionality/) of $n$ because in order to specify any vector $\boldsymbol{v}$ in the span of these vectors, one must specify the coefficients $c_1, \dots, c_n$ to construct $\boldsymbol{v}$ from the vectors in $S$. That is,  

$$\boldsymbol{v} = c_1\boldsymbol{x}_1 + \dots + c_n\boldsymbol{x}_n$$ 

However, if $S$ is linearly dependent, then we can throw away "redundant" vectors in $S$.  In fact, we see that the intrinsic dimensionality of a linearly dependent set $S$ is the maximum sized subset of $S$ that is linearly independent!

Appendix
--------


