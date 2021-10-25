---
title: 'Vector spaces and additional structures: inner products, norms, and Hilbert spaces'
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

$$\boldsymbol{x} = \begin{bmatrix}1 \\ 3\end{bmatrix}$$

If the array of numbers is of length two or three, than one can visualize the vector as an arrow:



While this definition is adequate for most applications of vector spaces, there exists a more abstract, and therefore more sophisticated definition of vector spaces that is required to have a deeper understanding of topics in math, statistics, and machine learning. Moreover, it is upon this more foundationational definition upon which one can construct more complex spaces with additional structure. Moreover, because these definitions are abstract, they are more powerful; that is, they can be used to model more than just Euclidean vectors. For example, they can  model the structure among sets of [functions, matrices, or polynomials](https://en.wikipedia.org/wiki/Examples_of_vector_spaces)!

In this post, we will dig into vector spaces and then will proceed to define and discuss the following mathematical structures that build upon vector spaces:

1. Vector spaces
2. Inner product spaces
3. Normed vector spaces
4. Banach spaces
5. Hilbert spaces

This final structure, the Hilbert space, is a generalization of Euclidean space and thus, provides a powerful, abstract model to define all spaces that behave like Euclidean spaces. 

Vector spaces
-------------

A **vector space** consists of an abstract set of elements, called **vectors** that can be added together and scaled.  The notion of "scaling" is modeled by a [field](https://en.wikipedia.org/wiki/Field_(mathematics)).  That is, a vector space involves a set of vectors $\mathcal{V}$ and a field of scalars $\mathcal{F}$ for which one can add together vectors in $\mathcal{V}$ as well as scale these vectors by elements in the field $\mathcal{F}$ according to the set of rules outlined in the following definition:

<span style="color:#0060C6">**Definition 1 (vector space):** Given a set of objects $\mathcal{V}$ called vectors and a field $\mathcal{F} := (C, +, \cdot, -, ^{-1}, 0, 1)$ where $C$ is the set of elements in the field, called scalars, the tuple $(\mathcal{V}, \mathcal{F})$ is a \textbf{vector space} if for all $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $c, d \in C$, it obeys the following ten axioms:</span>  

<span style="color:#0060C6">1. $\boldsymbol{u} + \boldsymbol{v} \in \mathcal{V}$</span>
<span style="color:#0060C6">2. $\boldsymbol{u} + \boldsymbol{v} = \boldsymbol{v} + \boldsymbol{u}$</span>
3. $(\boldsymbol{u} + \boldsymbol{v}) + \boldsymbol{w} = \boldsymbol{u} + (\boldsymbol{v} + \boldsymbol{w})$ 
4. There exists a zero vector $\boldsymbol{0} \in \mathcal{V}$ such that $\boldsymbol{u} + \boldsymbol{0} = \boldsymbol{u}$
5. For each $\boldsymbol{u \in \mathcal{V}}$ there exists a $\boldsymbol{u'} \in \mathcal{V}$ such that $\boldsymbol{u} + \boldsymbol{u'} = \boldsymbol{0}$.  We call $\boldsymbol{u}'$ the negative of $\boldsymbol{u}$ and denote it as $-\boldsymbol{u}$
6. The scalar multiple of $\boldsymbol{u}$ by $c$, denoted by $c\boldsymbol{u}$ is in $\mathcal{V}$
7. $c(\boldsymbol{u} + \boldsymbol{v}) = c\boldsymbol{u} + c\boldsymbol{v}$
8. $(c + d)\boldsymbol{u} = c\boldsymbol{u} + d\boldsymbol{u}$
9. $c(d\boldsymbol{u}) = (cd)\boldsymbol{u}$
10. $1\boldsymbol{u} = \boldsymbol{u}$

Axioms 1-5 of the definition describe how vectors can be added together. Axioms 6-10 describe how these vectors can be scaled using the field of scalars.

The Euclidean spaces defined by $\mathbb{R}^n$ are the most common examples of vector spaces.  The vector spaces $\mathbb{R}^2$ and $\mathbb{R}^3$ are easily visualized as arrows starting from the origin and provide intuition into most concepts involving vectors. 

