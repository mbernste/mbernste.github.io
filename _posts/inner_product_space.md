---
title: 'Inner product spaces'
date: 2021-10-28
permalink: /posts/inner_product/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
------------

The basic definition of a [vector space](https://mbernste.github.io/posts/vector_spaces/) does not capture all of the behavior that we inuitively associate with the more familiar Euclidean vector spaces. For example, in this basic definition, there is no notion of how similar two vectors are. Rather, a vector space only describes how vectors are added together and scaled.  The notion of how similar two vectors are is captured by an additional mathematical structure that one can define on a vector space called an **inner product**.   

One common inner-product on coordiante vector spaces is the **dot product**, which is taught in introductory linear algebra classes.  Given two vectors $$\boldsymbol{u}, \boldsymbol{v} \in \mathbb{R}^n$$, the dot product is defined as:

$$\boldsymbol{u} \dot \boldsymbol{v} := \sum_{i=1}^n u_iv_i$$

That is, the dot product is the summation of the products of the corresponding elements of each vector. The familiar dot product is just one specific example of the more general concept of an inner product. More rigorously, an inner product is defined as follows:

<span style="color:#0060C6">**Definition 2 (inner product):** Given a vector space $(\mathcal{V}, \mathcal{F})$, a function
$$\langle ., .\rangle : \mathcal{V} \times \mathcal{V} \rightarrow \mathbb{R}$$
is an **inner product** on the vector space if every $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $\alpha \in \mathcal{F}$ satisfy the following:</span>

1. $\langle \boldsymbol{v} + \boldsymbol{u}, \boldsymbol{w} \rangle = \langle \boldsymbol{v}, \boldsymbol{w} \rangle + \langle \boldsymbol{u}, \boldsymbol{w} \rangle$ 
2. $\langle \alpha \boldsymbol{v}, \boldsymbol{w} \rangle = \alpha \langle \boldsymbol{v}, \boldsymbol{u} \rangle$ 
3. $\langle \boldsymbol{v}, \boldsymbol{w} \rangle =  \langle \boldsymbol{w}, \boldsymbol{v} \rangle$ 
4. $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle \geq 0$ and $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle= 0 \iff \boldsymbol{v} = \boldsymbol{0}$

In the remainder of this post, we discuss the key properties of inner products and some intuition for how to think about them.

Properties
----------

1. **Linearity:**






