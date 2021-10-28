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

In the barebones definition of a [vector space](), there is no notion of how similar two vectors are.  Rather, a vector space only describes how vectors are added together and scaled.  The notion of how similar two vectors are is captured by an additional mathematical structure that one can define on a vector space called an **inner product**.   

The properties of abstract vector spaces do not capture all of the behavior that we inuitively associate with the more familiar Euclidean vector spaces.  For example, in a Euclidean vector space, we can come up with a function that describes how "similar" two vectors are.  One such function, called the **dot product**, is taught in introductory linear algebra classes.  That is, given two vectors $$\boldsymbol{u}, \boldsymbol{v} \in \mathbb{R}^n$$, the product is defined as:

$$\boldsymbol{u} \dot \boldsymbol{v} := \sum_{i=1}^n u_iv_i$$

That is, the dot product is the summation of the products of the corresponding elements of each vector. 

<span style="color:#0060C6">**Definition 2 (inner product):** Given a vector space $(\mathcal{V}, \mathcal{F})$, a function
$$\langle ., .\rangle : \mathcal{V} \times \mathcal{V} \rightarrow \mathbb{R}$$
is an **inner product** on the vector space if every $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $\alpha \in \mathcal{F}$ satisfy the following:</span>

1. $\langle \boldsymbol{v} + \boldsymbol{u}, \boldsymbol{w} \rangle = \langle \boldsymbol{v}, \boldsymbol{w} \rangle + \langle \boldsymbol{u}, \boldsymbol{w} \rangle$ 
2. $\langle \alpha \boldsymbol{v}, \boldsymbol{w} \rangle = \alpha \langle \boldsymbol{v}, \boldsymbol{u} \rangle$ 
3. $\langle \boldsymbol{v}, \boldsymbol{w} \rangle =  \langle \boldsymbol{w}, \boldsymbol{v} \rangle$ 
4. $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle \geq 0$ and $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle= 0 \iff \boldsymbol{v} = \boldsymbol{0}$


Properties
----------

1. **Linearity:**






