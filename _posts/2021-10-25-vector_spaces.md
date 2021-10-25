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

In this post, we will first present vector spaces and then will build upon this concept to evermore complex spaces. Specifically, we will define and discuss the following mathematical concepts:

1. Vector spaces
2. Inner product spaces
3. Normed vector spaces
4. Banach spaces
5. Hilbert spaces

Vector spaces
-------------
Given a set of objects $\mathcal{V}$ called vectors and a field $\mathcal{F} := (C, +, \cdot, -, ^{-1}, 0, 1)$ where $C$ is the set of elements in the field, called scalars, the tuple $(\mathcal{V}, \mathcal{F})$ is a \textbf{vector space} if for all $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $c, d \in C$, it obeys the following ten axioms:  


1. $\boldsymbol{u} + \boldsymbol{v} \in \mathcal{V}$
2. $\boldsymbol{u} + \boldsymbol{v} = \boldsymbol{v} + \boldsymbol{u}$
3. $(\boldsymbol{u} + \boldsymbol{v}) + \boldsymbol{w} = \boldsymbol{u} + (\boldsymbol{v} + \boldsymbol{w})$ 
4. There exists a zero vector $\boldsymbol{0} \in \mathcal{V}$ such that $\boldsymbol{u} + \boldsymbol{0} = \boldsymbol{u}$
5. For each $\boldsymbol{u \in \mathcal{V}}$ there exists a $\boldsymbol{u'} \in \mathcal{V}$ such that $\boldsymbol{u} + \boldsymbol{u'} = \boldsymbol{0}$.  We call $\boldsymbol{u}'$ the negative of $\boldsymbol{u}$ and denote it as $-\boldsymbol{u}$
6. The scalar multiple of $\boldsymbol{u}$ by $c$, denoted by $c\boldsymbol{u}$ is in $\mathcal{V}$
7. $c(\boldsymbol{u} + \boldsymbol{v}) = c\boldsymbol{u} + c\boldsymbol{v}$
8. $(c + d)\boldsymbol{u} = c\boldsymbol{u} + d\boldsymbol{u}$
9. $c(d\boldsymbol{u}) = (cd)\boldsymbol{u}$
10. $1\boldsymbol{u} = \boldsymbol{u}$
