---
title: 'Vector spaces and their extensions: inner product spaces, normed vector spaces, Banach spaces, and Hilbert spaces'
date: 2021-10-25
permalink: /posts/vector_spaces/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

_The concept of a vector space is a foundational concept in mathematics, physics, and the data sciences. In this post, we first present and explain the definition of a vector space and then go on to describe additional mathematical structures that can be built atop vector spaces in order to create ever-more powerful concepts. From vector spaces, we will define inner product spaces, normed vector spaces, Banach spaces, and finally, Hilbert spaces, which are generalization of Euclidean spaces._

Introduction
------------

The concept of a vector space is a foundational concept in mathematics, physics, and the data sciences. In most introductory courses, only vectors in a Euclidean space are discussed. That is, vectors are presented as arrays of numbers:

$$\boldsymbol{x} = \begin{bmatrix}1 \\ 2\end{bmatrix}$$

If the array of numbers is of length two or three, than one can visualize the vector as an arrow:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/EuclideanVector.png" alt="drawing" width="300"/></center>

While this definition is adequate for most applications of vector spaces, there exists a more abstract, and therefore more sophisticated definition of vector spaces that is required to have a deeper understanding of topics in math, statistics, and machine learning. Moreover, it is upon this more foundationational definition more complex spaces with additional structure can be constructed. 

In this post, we will dig into vector spaces and then will proceed to define and discuss the following mathematical structures that build upon vector spaces:

1. Vector spaces
2. Inner product spaces
3. Normed vector spaces
4. Banach spaces
5. Hilbert spaces

Importantly, in this post we will highlight how each of these mathematical constructs generalizes a more elementary idea; however it is in this generalization that these ideas hold their power. By being general, they can be used to model a wide variety of concepts and phenomena! For example, as we will see, inner products generalize the idea of "multiplication". Norms generalize the idea of "distance".  Banach spaces generalize the idea of a space that doesn't have any "holes" (such as the 3-dimensional volumetric world we live in). Hilbert spaces 0Euclidean spaces. 

Let's get in to it.

Vector spaces
-------------

As we alluded to before, vectors are usually introducted as arrays of numbers, and consequently, as arrows. These arrows can be added together, subtracted from one another, and scaled. This is depicted below:

A **vector space** generalizes this notion of adding things together and scaling them. Any space that comprises such elements is a vector space and its constitent elements are called **vectors**.  

At a more rigorous mathematical level, the notion of "scaling" is modeled by a [field](https://en.wikipedia.org/wiki/Field_(mathematics)) of scalars.  That is, a vector space involves a set of vectors $\mathcal{V}$ and a field of scalars $\mathcal{F}$ for which one can add together vectors in $\mathcal{V}$ as well as scale these vectors by elements in the field $\mathcal{F}$ according to a specific list of rules. These rules are spelled out in the definition for a vector space:

<span style="color:#0060C6">**Definition 1 (vector space):** Given a set of objects $\mathcal{V}$ called vectors and a field $\mathcal{F} := (C, +, \cdot, -, ^{-1}, 0, 1)$ where $C$ is the set of elements in the field, called scalars, the tuple $(\mathcal{V}, \mathcal{F})$ is a **vector space** if for all $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $c, d \in C$, it obeys the following ten axioms:</span>  

1. <span style="color:#0060C6">$\boldsymbol{u} + \boldsymbol{v} \in \mathcal{V}$</span>
2. <span style="color:#0060C6">$\boldsymbol{u} + \boldsymbol{v} = \boldsymbol{v} + \boldsymbol{u}$</span>
3. <span style="color:#0060C6">$(\boldsymbol{u} + \boldsymbol{v}) + \boldsymbol{w} = \boldsymbol{u} + (\boldsymbol{v} + \boldsymbol{w})$</span> 
4. <span style="color:#0060C6">There exists a zero vector $\boldsymbol{0} \in \mathcal{V}$ such that $\boldsymbol{u} + \boldsymbol{0} = \boldsymbol{u}$</span>
5. <span style="color:#0060C6">For each $\boldsymbol{u \in \mathcal{V}}$ there exists a $\boldsymbol{u'} \in \mathcal{V}$ such that $\boldsymbol{u} + \boldsymbol{u'} = \boldsymbol{0}$.  We call $\boldsymbol{u}'$ the negative of $\boldsymbol{u}$ and denote it as $-\boldsymbol{u}$</span>
6. <span style="color:#0060C6">The scalar multiple of $\boldsymbol{u}$ by $c$, denoted by $c\boldsymbol{u}$ is in $\mathcal{V}$</span>
7. <span style="color:#0060C6">$c(\boldsymbol{u} + \boldsymbol{v}) = c\boldsymbol{u} + c\boldsymbol{v}$</span>
8. <span style="color:#0060C6">$(c + d)\boldsymbol{u} = c\boldsymbol{u} + d\boldsymbol{u}$</span>
9. <span style="color:#0060C6">$c(d\boldsymbol{u}) = (cd)\boldsymbol{u}$</span>
10. <span style="color:#0060C6">$1\boldsymbol{u} = \boldsymbol{u}$</span>

Axioms 1-5 of the definition describe how vectors can be added together. Axioms 6-10 describe how these vectors can be scaled using the field of scalars.

Inner product spaces
--------------------

An **inner product space** is a vector space with a function, called an **inner product** that associates each pair of vectors in the space with a scalar quantity.  The inner product is denoted as $\langle ., .\rangle$.  


<span style="color:#0060C6">**Definition 2 (inner product):** Given a vector space $(\mathcal{V}, \mathcal{F})$, a function
$$\langle ., .\rangle : \mathcal{V} \times \mathcal{V} \rightarrow \mathbb{R}$$
is an \textbf{inner product} on the vector space if every $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $\alpha \in \mathcal{F}$ satisfy the following:</span>

1. $\langle \boldsymbol{v} + \boldsymbol{u}, \bold{w} \rangle = \langle \boldsymbol{v}, \boldsymbol{w} \rangle + \langle \boldsymbol{u}, \boldsymbol{w} \rangle$ 
2. $\langle \alpha \boldsymbol{v}, \boldsymbol{w} \rangle = \alpha \langle \boldsymbol{v}, \boldsymbol{u} \rangle$ 
3. $\langle \boldsymbol{v}, \boldsymbol{w} \rangle =  \langle \boldsymbol{w}, \boldsymbol{v} \rangle$ 
4. $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle \geq 0$ and $\langle  \boldsymbol{v}, \boldsymbol{v} \rangle= 0 \iff \boldsymbol{v} = \boldsymbol{0}$

Normed vector spaces
--------------------

Banach spaces
-------------

A Banach space extends normed vector spaces in the following, relatively simple way: a Banach space is a normed vector space that is also **complete**. A vector space is **complete** if every **Cauchy sequence** of vectors converges on a vector that is also in the vector space. 

Let's unravel this a bit. First, what is a Cauchy sequence? Roughly speaking, a Cauchy sequence is a sequence of vectors such that the distance between each subsequent pair of vectors shrinks until the distances between each successive pair becomes infinitesimally small. Stated more mathematically:

<span style="color:#0060C6">**Definition XXXXXX (Cauchy sequence):** A **Cauchy sequence** is an infinite sequence of vectors $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots$$ such that for $\forall \epsilon \in \mathbb{R}, \exists N$ such that $$\forall m, n > N$$ it holds that $$||\boldsymbol{x}_m - \boldsymbol{x}_{m}|| < \epsilon$$./span>

We visualize this concept in the schematic below:
  
<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/CauchySequence.png" alt="drawing" width="350"/></center>

Here we show the first five elements of a Cauchy sequence in $$\mathbb{R}^2$$ that converge to a point representing the vector in grey. The vector space is complete if for every such sequence, the vector that the sequence is converging on is also in the vector space.
  
At a more intuitive level, the completeness of a vector space means that the vector space doesn't have any "holes" in it. That is, if you start approaching a point in the limit, you are gauranteed that the point you are approaching is also a valid point. It's not "missing" from the vector space.
  
Hilbert spaces
--------------
