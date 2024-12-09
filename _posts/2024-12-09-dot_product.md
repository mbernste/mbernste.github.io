---
title: 'Dot product'
date: 2024-12-09
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

<span style="color:#0060C6">**Definition 1 (dot product):** Given vectors $\boldsymbol{v}, \boldsymbol{u} \in \mathbb{R}^n$, the **dot product** between these vectors is defined as, $\boldsymbol{v} \cdot \boldsymbol{u} := \sum_{i=1}^n v_i u_i$</span>

Despite the simplicity of its definition, the dot product can be understood from a number of [different perspectives](https://mbernste.github.io/posts/understanding_3d/).  Here are four perspectives I find useful for thinking about the dot products. Ordered from the least abstract to the most abstract, these perspectives are:

1. The dot product succinctly describes a weighted sum
2. The dot product describes a a geometric relationship between two Euclidean vectors
3. The dot product is an analogy to multiplication between scalars (i.e., plain old multiplication between numbers)
4. The dot describes a notion of similarity between two Euclidean vectors

These perspectives are described in the remaining sections of this post.

The dot product as a weighted sum
---------------------------------

The least abstract way of viewing a dot product is as a weighted sum of variables. Lets say we have a vector of variables storing some kind of data $\boldsymbol{x}$.  Let's say we have a vector of weights $\boldsymbol{w}$ and we want to sum the variables in $\boldsymbol{x}$ where each element $x_i$ in $\boldsymbol{x}$ is multiplied by its weight $w_i$ in $\boldsymbol{w}$.  This operation is stated succinctly as $\boldsymbol{w} \cdot \boldsymbol{x}$.

Whenever you find a dot product, it often helps to think about the operation as a sum of variables where each variable is first multiplied by a weight before summed. Which vector describes the "weights" and which the "variables" depends on the context. This perspective is often helpful in machine learning contexts where "weights" are often mutable model parameters and "variables" are fixed pieces of data.

The dot product describes a geometric relationship between Euclidean vectors
----------------------------------------------------------------------------

The dot product uses the relationship between the directions in which the two vectors point.  More specifically, if the two vectors point in a similar direction, the magnitude of the dot product increases.  If they point in drastically different directions, the dot product decreases.  Now, the question becomes: what do we mean by "point in a similar direction?" More specifically, what do we mean by "similar"? The dot product asserts that the angle between the two vectors measures how similarly they point.   The smaller the angle, the larger will be the dot product.  

To show how this works, we note that the dot product between two vectors $\boldsymbol{a}$ and $\boldsymbol{b}$, can be computed using the angle between them as follows (see Theorem 1 in the Appendix to this post):

$$\boldsymbol{a} \cdot \boldsymbol{b} = \vert\vert \boldsymbol{a} \vert\vert \vert\vert \boldsymbol{b} \vert\vert \cos \theta$$

If $\theta := 0$, then the two vectors point in the same direction.  In this case, $\cos \theta = 1$ and the dot product reduces to simply computing the product of the two vectors' magnitudes. If $\theta = \pi / 2$, then the two vectors point in perpendicular directions (i.e. maximally different directions).  We see that $\cos \pi/2 = 0$ and the dot product between the two vectors is zero.

Another way to understand how this works is to look at the projection of one vector onto the other.  That is, given two vectors $\boldsymbol{a}$, $\boldsymbol{b}$, the dot product between these vectors computes the product of the magnitudes of $\boldsymbol{a}$ and $\boldsymbol{b}$ along the direction that the two vectors share. Said differently, the dot product $\boldsymbol{a} \cdot \boldsymbol{b}$ can be viewed as the magnitude of the projection of one of the vectors onto the other vector multiplied by the magnitude of the vector being projected upon.  That is,

$$\begin{align*}\boldsymbol{a} \cdot \boldsymbol{b} &= \vert\vert \text{proj}(\boldsymbol{a}, \boldsymbol{b}) \vert\vert  \vert\vert\boldsymbol{b} \vert\vert \\
&= \vert\vert \text{proj}(\boldsymbol{b}, \boldsymbol{a}) \vert\vert \vert\vert \boldsymbol{a} \vert\vert  \end{align*}$$

If the two vectors are orthogonal, then the projection of either vector onto the other will be zero and thus the dot product will be zero.  In contrast, if two vectors point in the same direction, then the projection of the smaller vector onto the larger vector is simply the smaller vector so we multiply the magnitude of the smaller vector by the magnitude of the larger vector (i.e. simply multiply their norms).

Given this geometric interpretation of the dot product, we can see that taking the dot product of some vector $\boldsymbol{a}$ and a [unit vector](https://mbernste.github.io/posts/normed_vector_space/) $\boldsymbol{b}$, finds the length of the projection of $\boldsymbol{a}$ along the axis defined by $\boldsymbol{b}$:

$$\begin{align*} \boldsymbol{a} \cdot \boldsymbol{b} &= \vert\vert \boldsymbol{a} \vert\vert \text{proj}(\boldsymbol{b}, \boldsymbol{a}) \vert\vert \\ &= \vert\vert \text{proj}(\boldsymbol{b}, \boldsymbol{a}) \vert \vert && \text{because $\vert \vert \boldsymbol{a} \vert\vert = 1$} \end{align*}$$

Thus, whenever one of the vectors in a dot product is a unit vector, the operation can always be viewed as the length of the projection along the axis defined by the unit vector.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/dot_product_projection.png" alt="drawing" width="300"/></center>

The dot product is analogous to the product on scalars
------------------------------------------------------

One way to understand the dot product is as an operation on vectors that is analogous to multiplication between scalars.  Given two scalars, $x, y \in \mathbb{R}$, it is obvious that the more we increase the magnitude (i.e. absolute value) of either $x$ or $y$, the more that the magnitude of their product will grow.  The dot product on vectors behaves similarly.  Given two vectors, $\boldsymbol{a}$ and $\boldsymbol{b}$, if we increase the norm of either of the vectors, the magnitude of the dot product increases.  We see this clearly expressed in the $\vert\vert \boldsymbol{a} \vert\vert \vert\vert \boldsymbol{b} \vert\vert $ term of the geometric definition of the dot product:

$$\boldsymbol{a} \cdot \boldsymbol{b} =\vert\vert \boldsymbol{a}\vert\vert \vert\vert  \boldsymbol{b}\vert\vert   \cos \theta$$

However, unlike multiplication between scalars, the dot product between vectors also takes into account the direction in which the two vectors point. The dot product asserts that if the two vectors point in a similar direction, the magnitude of the dot product increases.  If they point in drastically different directions, the dot product decreases.  

One feature of multiplication between scalars is that if $x$ and $y$ have opposite signs then $xy < 0$ (for example, $-2 \times 3 = -6$).  Is this feature shared with the dot product? In a way, yes! But we first need to express the concept of ``opposite signs" between two vectors. To do that, note that if the angle between the vectors $\boldsymbol{a}$ and $\boldsymbol{b}$ is obtuse, then their dot product will be negative:

$$\begin{align*} -\frac{\pi}{2} > \theta_{\boldsymbol{a}, \boldsymbol{b}} >- \frac{3\pi}{2} \implies & \cos  \theta_{\boldsymbol{a}, \boldsymbol{b}}  < 0 \\ \implies  & \vert\vert \boldsymbol{a}\vert\vert \vert\vert\boldsymbol{b} \vert\vert \cos  \theta_{\boldsymbol{a}, \boldsymbol{b}} < 0 \\ \implies & \boldsymbol{a} \cdot \boldsymbol{b} < 0 \end{align*}$$

This is visualized below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/dot_product_acute_obtuse.png" alt="drawing" width="700"/></center>

Thus, two vectors ``have opposite signs", in context of thinking about the dot product, if the angle between them is greater than $\pi / 2$ and less than $3\pi/4$. 

Please note, this is just an _analogy_ -- that is, a way to think about the dot product as sharing certain familiar characteristics with multiplication between numbers.

The dot product as a notion of similarity
-----------------------------------------

Lastly, the dot product between two vectors can be thought about as a notion of similarity between two vectors. Recall that the dot product between two vectors can be written in terms of the projection of one vector onto another:

$$\begin{align*}\boldsymbol{a} \cdot \boldsymbol{b} &= \vert\vert \text{proj}(\boldsymbol{a}, \boldsymbol{b}) \vert\vert  \vert\vert\boldsymbol{b} \vert\vert \\
&= \vert\vert \text{proj}(\boldsymbol{b}, \boldsymbol{a}) \vert\vert \vert\vert \boldsymbol{a} \vert\vert  \end{align*}$$

If we think of the magnitude of the projection of one vector onto another as the amount of "directionality" that the two vectors share, then the dot product can be understood as performing the following sequence of calculations:

1. **Alignment:** Calculate the amount of "directionality" shared between them -- that is, the length of the projection of one vector onto the other.
2. **Multiplication:** Multiply this shared directionality

That is, the dot product is the magnitude of one vector multiplied by its shared directionality with the other. (Note, it doesn't matter which vector we project onto the other, the final result will be the same either way.) If the vectors are perpendicular to one another, then they share no directionality and thus, the dot product is zero. In essence, these vectors share nothing in common -- they are pointing in completely different directions! No matter how large either vector is, because they don't share any directionality, their dot product is zero. In this context, what is the interpretation of a negative dot product? I like to think about it as follows: a negative dot product indicates that the two vectors _do_ share some directionality, just with opposite trends. That is, they share a projection along the same line, but they point in opposite directions along that line. 

Appendix
--------

<span style="color:#0060C6">**Theorem 1:** Given $\theta$ is the angle between the two vectors, $\boldsymbol{v}$ and $\boldsymbol{w}$, the following definition for the dot product between $\boldsymbol{v}$ and $\boldsymbol{w}$ is equivalent to Definition 1: $\boldsymbol{v} \cdot \boldsymbol{w} = \vert\vert \boldsymbol{v} \vert\vert \vert\vert \boldsymbol{w} \vert\vert \cos \theta$.</span>

**Proof:**


$\square$
