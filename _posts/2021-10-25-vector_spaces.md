---
title: 'Vector spaces'
date: 2021-10-25
permalink: /posts/vector_spaces/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

_The concept of a vector space is a foundational concept in mathematics, physics, and the data sciences. In this post, we first present and explain the definition of a vector space and then go on to describe additional mathematical structures that can be built atop vector spaces in order to create ever-more powerful concepts. From vector spaces, we will define inner product spaces, normed vector spaces, Banach spaces, and finally, Hilbert spaces, which generalize Euclidean spaces._

Introduction
------------

The concept of a vector space is a foundational concept in mathematics, physics, and the data sciences. In most introductory courses, only vectors in a Euclidean space are discussed. That is, vectors are presented as arrays of numbers:

$$\boldsymbol{x} = \begin{bmatrix}1 \\ 2\end{bmatrix}$$

If the array of numbers is of length two or three, than one can visualize the vector as an arrow:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/EuclideanVector.png" alt="drawing" width="300"/></center>

While this definition is adequate for most applications of vector spaces, there exists a more abstract, and therefore more sophisticated definition of vector spaces that is required to have a deeper understanding of topics in math, statistics, and machine learning. In this post, we will dig into the abstract definition for vector spaces and discuss a few of their properties. Moreover, we will look at a few examples of vector spaces and see how the formal definition generalizes the idea of vectors to other mathematical constructs as well, such as matrices and functions.


Formal definition
-----------------

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

**Properties**

Here are several properties of vector spaces that both provide insight into how they capture the notions of adding and scaling:




