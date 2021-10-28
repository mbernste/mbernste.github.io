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

Intuitively, the **inner product** generalizes the act of multiplication from numbers to vectors. Because of this, it helps to first think about some fundamental properties of multiplication of numbers. First and foremost, multiplication is _function_ that acts on two numbers to produce a number. In the same way, an inner product is a function that acts on two vectors and produces a number as defined below:

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



A vector space is **complete** if every **Cauchy sequence** of vectors converges on a vector that is also in the vector space. 

Let's unravel this a bit. First, what is a Cauchy sequence? Roughly speaking, a Cauchy sequence is a sequence of vectors such that the distance between each subsequent pair of vectors shrinks until the distances between each successive pair becomes infinitesimally small. Stated more mathematically:

<span style="color:#0060C6">**Definition 4 (Cauchy sequence):** A **Cauchy sequence** is an infinite sequence of vectors $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots$$ such that for $\forall \epsilon \in \mathbb{R}, \exists N$ such that $$\forall m, n > N$$ it holds that $$d(\boldsymbol{x}_m, \boldsymbol{x}_{m}) < \epsilon$$.</span>

We visualize this concept in the schematic below:
  
<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/CauchySequence.png" alt="drawing" width="350"/></center>

Here we show the first five elements of a Cauchy sequence in $$\mathbb{R}^2$$ that converge to a point represented by the grey vector. The vector space is complete if for every such sequence, the vector that the sequence is converging to (in this example, the grey vector) is also in the vector space. Thus, we have the following definitions:

<span style="color:#0060C6">**Definition 5 (Complete vector space):** Given a vector space $(\mathcal{V}, \mathcal{F})$ and associated metric function $$d$$, the vector space is **complete** if for every Cauchy sequence, $\boldsymbol{x}_1, \boldsymbol{x}_2, \dots$, it holds that $\lim_{n \rightarrow \infty} \boldsymbol{x}_n \in \mathcal{V}$$.  
  
At a more intuitive level, the completeness of a vector space means that the vector space doesn't have any "holes" in it. That is, if you start approaching a point in the limit, you are gauranteed that the point you are approaching is also a valid point. It's not "missing" from the vector space.
  
Banach spaces
-------------
  
Inner product spaces
--------------------

Intuitively, an inner product is generalizes multiplication of numbers to vectors.  More abstractly, multiplication on the real numbers constitutes a ring.  Axioms 1 and 2 are called the \textbf{linearity} properties, which preserves the right-distributivity of multiplication that we see in a ring.  That is, $(a+b)c = ac + bc$.  An **inner product space** is a vector space with a function, called an **inner product** that associates each pair of vectors in the space with a scalar quantity.  The inner product is denoted as $\langle ., .\rangle$.  

<span style="color:#0060C6">**Definition 2 (inner product):** Given a vector space $(\mathcal{V}, \mathcal{F})$, a function
$$\langle ., .\rangle : \mathcal{V} \times \mathcal{V} \rightarrow \mathbb{R}$$
is an **inner product** on the vector space if every $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $\alpha \in \mathcal{F}$ satisfy the following:</span>

1. $\langle \boldsymbol{v} + \boldsymbol{u}, \boldsymbol{w} \rangle = \langle \boldsymbol{v}, \boldsymbol{w} \rangle + \langle \boldsymbol{u}, \boldsymbol{w} \rangle$ 
2. $\langle \alpha \boldsymbol{v}, \boldsymbol{w} \rangle = \alpha \langle \boldsymbol{v}, \boldsymbol{u} \rangle$ 
3. $\langle \boldsymbol{v}, \boldsymbol{w} \rangle =  \langle \boldsymbol{w}, \boldsymbol{v} \rangle$ 
4. $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle \geq 0$ and $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle= 0 \iff \boldsymbol{v} = \boldsymbol{0}$



Axiom 3 is called the \textbf{symmetric} property of the inner product.  Intuitively, a product should not depend on the order of the operands.  Note that for complex vector spaces, this axiom would be \textbf{conjugate symmetry}.  That is,
$$\langle \bold{v}, \bold{w} \rangle = \overline{ \langle \bold{w}, \bold{v} \rangle}$$
The conjugate is used for complex vector spaces.  In real valued vector spaces, the conjugate can be ignored.
\\\\
Axiom 4 is called the \textbf{positive definite} property.  Intuitively, the product of a vector with itself should be greater than zero.  Only the zero-vector multiplied by itself should result in the zero-vector.
  
Hilbert spaces
--------------
