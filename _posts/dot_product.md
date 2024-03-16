---
title: 'Dot product'
date: 2021-10-27
permalink: /posts/dot_product/
tags:
  - tutorial
  - mathematics
  - linear algebra
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

_The dot product is a fundamental operation on two Euclidean vectors that captures a notion of similarity between the vectors. In this post, we'll define the dot product and offer a number of angles for which to intuit the idea captured by this fundamental operation._

Introduction
------------

The **dot product** is a fundamental operation on two Euclidean vectors that captures a notion of similarity between the vectors. It is defined as follows:

<span style="color:#0060C6">**Definition 1 (dot product):** Given vectors $\boldsymbol{v}, \boldsymbol{u} \in \mathbb{R}^n, the **dot product** between these vectors is defined as, $\boldsymbol{v} \cdot \boldsymbol{u} := \sum_{i=1}^n v_i u_i$</span>

There are three perspectives I find useful for thinking about the dot products. Ordered from the least abstract to the most abstract, these perspectives are:
1. The dot product succinctly describes a weighted sum
2. The dot product describes a geometric relationship between two Euclidean vectors
3. The dot product is an analogy to the product between scalars (i.e., normal multiplication between numbers)
4. The dot describes a notion of similarity between two Euclidean vectors

These perspectives are described in the remaining sections of this post.

The dot product as a weighted sum
---------------------------------

The least abstract way of viewing a dot product is as a weighted sum of variables. Lets say we have a vector of variables storing some kind of data $\boldsymbol{x}$.  Let's say we have a vector of weights $\boldsymbol{w}$ and we want to sum the variables in $\boldsymbol{x}$ where each element $x_i$ in $\boldsymbol{x}$ is multiplied by its weight $w_i$ in $\boldsymbol{w}$.  This operation is stated succinctly as $\boldsymbol{w} \cdot \boldsymbol{x}$.

Whenever you find a dot product, it often helps to think about the operation as a sum of variables where each variable is multiplied by a weight.

The dot product describes a geometric relationship
--------------------------------------------------

The dot product uses the relationship between the directions in which the two vectors point.  More specifically, if the two vectors point in a similar direction, the magnitude of the dot product increases.  If they point in drastically different directions, the dot product decreases.  Now, the question becomes: what do we mean by "point in a similar direction?" More specifically, what do we mean by "similar"? The dot product asserts that the angle between the two vectors measures how similarly they point.   The smaller the angle, the larger will be the dot product.  

To show how this works, we note that the dot product between two vectors $\boldsymbol{a}$ and $\boldsymbol{b}$, can be computed using the angle between them as follows (see Theorem 1 in the Appendix to this post):

$$\boldsymbol{a} \cdot \boldsymbol{b} = \vert\vert \boldsymbol{a} \vert\vert \vert\vert \boldsymbol{b} \cos \theta$$

If $\theta := 0$, then the two vectors point in the same direction.  In this case, $\cos \theta = 1$ and the dot product reduces to simply computing the product of the two vectors' magnitudes. If $\theta = \pi / 2$, then the two vectors point in perpendicular directions (i.e. maximally different directions).  We see that $\cos \pi/2 = 0$ and the dot product between the two vectors is zero.

Another way to understand how this works is to look at the projection of one vector onto the other.  That is, given two vectors $\boldsymbol{a}$, $\boldsymbol{b}$, the dot product between these vectors computes the product of the magnitudes of $\boldsymbol{a}$ and $\boldsymbol{b}$ along the direction that the two vectors share (Figure~\ref{fig:projection_2}). Said differently, the dot product $\boldsymbol{a} \cdot \boldsymbol{b}$ can be viewed as the magnitude of the projection of one of the vectors onto the other vector multiplied by the magnitude of the vector being projected upon.  That is,

$$\begin{align*}\boldsymbol{a} \cdot \boldsymbol{b} &= \vert\vert \text{proj}(\boldsymbol{a}, \boldsymbol{b}) \vert\vert  \vert\vert\boldsymbol{b} \vert\vert \\
&= \norm{\text{proj}(\boldsymbol{b}, \boldsymbol{a})} \norm{\boldsymbol{a}}  \end{align*}$$

If the two vectors are orthogonal, then the projection of either vector onto the other will be zero and thus the dot product will be zero.  In contrast, if two vectors point in the same direction, then the projection of the smaller vector onto the larger vector is simply the smaller vector so we multiply the magnitude of the smaller vector by the magnitude of the larger vector (i.e. simply multiply their norms).

Given this geometric interpretation of the dot product, we can see that taking the dot product of some vector $\bold{a}$ and a \textit{unit vector} $\bold{b}$, finds the length of the projection of $\bold{a}$ along the axis defined by $\boldsymbol{b}$:

$$\begin{align*} \boldsymbol{a} \cdot \boldsymbol{b} &= \vert\vert \boldsymbol{a} \vert\vert \text{proj}(\bold{b}, \bold{a}) \vert\vert \\ &= \vert\vert \text{proj}(\boldsymbol{b}, \boldsymbol{a}) \vert \vert && \text{because $\norm{\bold{a}} = 1$} \end{align*}$$

Thus, whenever one of the vectors in a dot product is a unit vector, the operation can always be viewed as the length of the projection along the axis defined by the unit vector.
