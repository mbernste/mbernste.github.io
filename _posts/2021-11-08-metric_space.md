---
title: 'Metric spaces'
date: 2021-11-08
permalink: /posts/metric_space/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
------------

A **normed vector** space is a vector space in which each vector is associated with a scalar value called a **norm**.  A norm generalizes the idea of vector-lengths in standard Euclidean vector spaces to any vector space.  

<span style="color:#0060C6">**Definition 1 (normed vector space):** A **normed vector space** is vector space $(\mathcal{V}, \mathcal{F})$ associated with a function $\norm{.} : \mathcal{V} \rightarrow \mathbb{R}$ that obeys the following axioms:</span>
1.<span style="color:#0060C6">$\forall \boldsymbol{v} \in \mathcal{V} \ \ \norm{\<span style="color:#0060C6">{v}} \geq 0$</span>
2.<span style="color:#0060C6">$\norm{\alpha\<span style="color:#0060C6">{x}} = |\alpha| \norm{\<span style="color:#0060C6">{x}}$</span>
3.<span style="color:#0060C6">$\norm{\<span style="color:#0060C6">{x} + \<span style="color:#0060C6">{y}} \leq \norm{\<span style="color:#0060C6">{x}} + \norm{\<span style="color:#0060C6">{y}}$</span> 

Intuition
---------

The norm of a vector captures the a notion of "length" for a vector.  Below we outline the intuition behind each axiom in the definition above and describe how these axioms capture this idea:

* Axiom 1 says that all vectors should have a positive length.  This enforces our intuition that a "length'' is a positive quantity.
* Axiom 2 says that if we multiply a vector by a scalar, it's length should increase by the magnitude (i.e. the absolute) value of that scalar. This axiom ties together the notion of scaling vectors (Axiom 6 in the definition of a vector space) to the notion of "length" for a vector.  It essentially says that to scale a vector is to stretch the vector.
* Axiom 3 says that the length of the sum of two vectors should not exceed the sum of the lengths of each vector.  This enforces our intuition that if we add together two objects that each have a "length", the resultant object should not exceed the sum of the lengths of the original objects.

Following the axioms for a normed vector space, one can also show that only the zero vector has zero length (Theorem 1 in the Appendix to this post).
  
Unit vectors
------------

 In a normed vector space, a unit vector is a vector with norm equal to 1. Given a vector $\boldsymbol{v}$, a unit vector can be derived by simply dividing the vector by its norm (Theorem 2 in the Appendix).  This unit vector, called the **normalized vector** of $\boldsymbol{v}$ is denoted $\hat{\boldsymbol{v}}$.  In a Euclidean vector space, the normalized vector $\hat{\boldsymbol{v}}$ is the unit vector that points in the same direction as $\boldsymbol{v}$.  Unit vectors are often used to denote a direction in a vector space.  That is, since it's magnitude is 1, the relevant information encoded in the vector is the direction in which it points.  
 
