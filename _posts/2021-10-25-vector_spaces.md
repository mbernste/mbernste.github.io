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

_The concept of a vector space is a foundational concept in mathematics, physics, and the data sciences. In this post, we first present and explain the definition of a vector space and then go on to describe properties of vector spaces. Lastly, we present a few examples of vector spaces that go beyond the usual Euclidean vectors that are often taught in introductory math and science courses._

Introduction
------------

The concept of a vector space is a foundational concept in mathematics, physics, and the data sciences. In most introductory courses, only vectors in a Euclidean space are discussed. That is, vectors are presented as arrays of numbers:

$$\boldsymbol{x} = \begin{bmatrix}1 \\ 2\end{bmatrix}$$

If the array of numbers is of length two or three, than one can visualize the vector as an arrow:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/EuclideanVector.png" alt="drawing" width="300"/></center>

While this definition is adequate for most applications of vector spaces, there exists a more abstract, and therefore more sophisticated definition of vector spaces that is required to have a deeper understanding of topics in math, statistics, and machine learning. In this post, we will dig into the abstract definition for vector spaces and discuss a few of their properties. Moreover, we will look at a few examples of vector spaces outside of the usual Euclidean vectors and see how the formal definition generalizes to other mathematical constructs such as [matrices](https://mbernste.github.io/posts/matrices/) and functions.

Formal definition
-----------------

As we mentioned before, vectors are usually introduced as arrays of numbers, and consequently, as arrows. These arrows can be added together and scaled as depicted below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/AddScaleVectors.png" alt="drawing" width="420"/></center>

A **vector space** generalizes this notion of adding and scaling things that behave like Euclidean vectors.   

At a more rigorous mathematical level, a vector space consists of both a set of vectors $\mathcal{V}$ and a [field](https://en.wikipedia.org/wiki/Field_(mathematics)) of scalars $\mathcal{F}$ for which one can add together vectors in $\mathcal{V}$ as well as scale these vectors by elements in the field $\mathcal{F}$ according to a specific list of rules (in most cases, the field of scalars are the real numbers, $\mathbb{R}$). These rules are spelled out in the definition for a vector space:

<span style="color:#0060C6">**Definition 1 (vector space):** Given a set of objects $\mathcal{V}$ called vectors and a field $\mathcal{F} := (C, +, \cdot, -, ^{-1}, 0, 1)$ where $C$ is the set of elements in the field, called scalars, the tuple $(\mathcal{V}, \mathcal{F})$ is a **vector space** if for all $\boldsymbol{v}, \boldsymbol{u}, \boldsymbol{w} \in \mathcal{V}$ and $c, d \in C$, the following ten axioms hold:</span>  

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

Properties
----------

The ten axioms outlined in the definition for a vector space may seem somewhat arbitrary (at least, they did for me); however, as we will show, these axioms are sufficient for ensuring that vector spaces have all of the properties that we intuitively associate with Euclidean vectors. Specifically, from these axioms, we can derive the following properties:

1. **The zero vector is unique** (Theorem 1 in the Appendix). There is only one distinct zero vector in a vector space. Notice in a Euclidean vector space, there is only one point at the origin, which represents the zero vector in Euclidean spaces. 
2. **Any vector multiplied by the zero scalar is the zero vector** (Theorem 2 in the Appendix).The zero scalar converts any vector into the zero vector.  That is, given a vector $\boldsymbol{v}$, it holds that $0\boldsymbol{v} = \boldsymbol{0}$. This generalizes the notion of how multiplying a vector in a Euclidean space by zero should shrink the vector to the origin.
3. **The negative of a vector is unique** (Theorem 3 in the Appendix).  Given a vector $\boldsymbol{v}$, we denote its negative vector as $-\boldsymbol{v}$.  This is analogous to each real number $x \in \mathbb{R}$ having a matching negative number $-x$ that lies $\|x\|$ distance from 0 on the opposite side of 0.
4. **Multiplying a negative vector by the scalar -1 produces its negative vector** (Theorem 4 in the Appendix).  That is, given a vector $\boldsymbol{v}$, it holds that $-1\boldsymbol{v} = -\boldsymbol{v}$. This is analogous to the fact that if you multiply any number $x$ by $-1$ you get the number $-x$ that lies $\|x\|$ distance from 0 on the opposite side of 0.
5. **The zero vector multiplied by any scalar is the zero vector** (Theorem 5 in the Appendix).  The zero vector remains the zero vector despite being multiplied by any scalar. That is, $c\boldsymbol{0} = \boldsymbol{0}$ for any $c \in \mathcal{F}$. This is analogous to the fact that zero multiplied by any number remains zero.
6. **The only vector whose negative is not distinct from itself is the zero vector** (Theorem 6 in the Appendix). For every vector other than the zero vector, its negative vector is a distinct vector in the vector space.  For the zero vector, its negative is itself.  This is analogous to the fact that for any number $x \neq 0$, the number $-x$ is a distinct number from $x$ that lies on the opposite side of 0. However, for $x = 0$, $-x = x$.

Examples of vector spaces
-------------------------

**The real numbers**

It turns out that the real numbers themselves (when equipped with standard addition and multiplication) are themselves a vector space in which the real numbers are both vectors and scalars! This example may be a bit trivial and silly; however, I like it because it highlights the generality of the definition of a vector space. In the vector space consisting of real numbers, the number zero acts as the zero vector. 

**Matrices**

Although generally not thought of as vectors, the space of real-valued [matrices](https://mbernste.github.io/posts/matrices/) of a fixed size $$\mathbb{R}^{m \times n}$$ form a vector space in which the matrices are vectors. Intuitively, you can add matrices together:

$$\begin{bmatrix}1 & 2 \\ 3 & 4\end{bmatrix} + \begin{bmatrix}3 & 2 \\ 2 & 5\end{bmatrix} = \begin{bmatrix}4 & 4 \\ 5 & 9\end{bmatrix}$$

You can also scale them:

$$2\begin{bmatrix}1 & 2 \\ 3 & 4\end{bmatrix} = \begin{bmatrix}2 & 4 \\ 6 & 8\end{bmatrix}$$

The zero matrix acts as the zero vector:

$$\begin{bmatrix}0 & 0 \\ 0 & 0\end{bmatrix}$$

This may seem a bit confusing because as we discuss in [another blog post](https://mbernste.github.io/posts/matrices_as_functions/), matrices act as functions between Euclidean vector spaces. Nonetheless, matrices can form vector spaces all on their own distinct from the vector spaces that they act upon!

**Functions**

Appendix: Proofs of properties of vector spaces
-----------------------------------------------

<span style="color:#0060C6">**Theorem 1 (Uniqueness of zero vector):** Given vector space $(\mathcal{V}, \mathcal{F})$, the zero vector is unique.</span>

**Proof:**

Assume for the sake of contradiction that there exists a vector $\boldsymbol{a}$ such that $\boldsymbol{a} \neq \boldsymbol{0}$ and that $\forall \boldsymbol{v} \in \mathcal{V}$

$$\boldsymbol{a} + \boldsymbol{v} = \boldsymbol{v}$$

Then, this implies that 

$$\boldsymbol{a} + \boldsymbol{0} = \boldsymbol{0}$$

However, Axiom 4 of the definition for a vector space states that if a vector is the zero-vector, it must be that $\boldsymbol{a} + \boldsymbol{0} = \boldsymbol{a}$.

Since $\boldsymbol{a} \neq \boldsymbol{0}$ , we reach a contradiction.  Therefore, there does not exist a vector $\boldsymbol{a} \neq \boldsymbol{0}$ for which  $\forall \boldsymbol{v} \in \mathcal{V} \ \ \ \boldsymbol{a} + \boldsymbol{v} = \boldsymbol{v}$.  Thus, the zero-vector is unique.

$\square$

<span style="color:#0060C6">**Theorem 2 (The product of the zero scalar and any vector is the zero vector):** Given a vector space $(\mathcal{V}, \mathcal{F})$, it holds that $\forall \boldsymbol{v} \in \mathcal{V}, 0\boldsymbol{v} = \boldsymbol{0}$.</span>

**Proof:**
  
Assume for the sake of contradiction that there exists a vector $\boldsymbol{a} \neq \boldsymbol{0}$ such that

$$0\boldsymbol{v} = \boldsymbol{a}$$

Now, for any scalar $c \neq 0$, we have

$$\begin{align*}c\boldsymbol{v} &= (c + 0)\boldsymbol{v} \\ &= c\boldsymbol{v} + 0\boldsymbol{v} && \text{by Axiom 8} \\ &=  c\boldsymbol{v} + \boldsymbol{a}\end{align*}$$

Our assumption assumed that $\boldsymbol{a} \neq \boldsymbol{0}$ must be false because by Theorem 1 the only vector $\boldsymbol{a}$ for which $c\boldsymbol{v} + \boldsymbol{a} = c\boldsymbol{v}$ would be true is the zero-vector. 

$\square$


<span style="color:#0060C6">**Theorem 3 (Each vector has a unique negative vector):** Given a vector space $(\mathcal{V}, \mathcal{F})$ and vector $\boldsymbol{v} \in \mathcal{V}$, its negative, $-\boldsymbol{v}$, is unique.  That is, $\boldsymbol{v} + \boldsymbol{a} = \boldsymbol{0} \iff \boldsymbol{a} = -\boldsymbol{v}$.</span>

**Proof:**

We need only prove $\boldsymbol{v} + \boldsymbol{a} = \boldsymbol{0} \implies \boldsymbol{a} = -\boldsymbol{v}$.  The other direction is stated in the axioms for the definition of a vector space.

$$\begin{align*}\boldsymbol{v} + \boldsymbol{a} &= \boldsymbol{0} \\ \implies -\boldsymbol{v} + \boldsymbol{v} + \boldsymbol{a} &= -\boldsymbol{v} + \boldsymbol{0} \\ \implies [-\boldsymbol{v} + \boldsymbol{v}] + \boldsymbol{a} &= -\boldsymbol{v} \\ \implies \boldsymbol{0} + \boldsymbol{a} &= -\boldsymbol{v} &&\text{by Axiom 5} \\ \implies \boldsymbol{a} &= -\boldsymbol{v} && \text{by Axiom 4}\end{align*}$$

$\square$

<span style="color:#0060C6">**Theorem 4 (Derivation of a vector's negative):** Given a vector $\boldsymbol{v} \in \mathcal{V}$, it's negative is $(-1)\boldsymbol{v}$.  That is, $-\boldsymbol{v} = (-1)\boldsymbol{v}$.</span>

**Proof:**

$$\begin{align*}\boldsymbol{v} + (-1)\boldsymbol{v} &= (1)\boldsymbol{v} + (-1)\boldsymbol{v} && \text{by Axiom 10} \\ &= (1-1)\boldsymbol{v} && \text{by Axiom 8} \\ &= 0\boldsymbol{v} \\ &= \boldsymbol{0} && \text{by Theorem 2}\end{align*}$$

Then, by Axiom 5, it must be that $(-1)\boldsymbol{v} = -\boldsymbol{v}$.

$\square$

<span style="color:#0060C6">**Theorem 5 (The zero vector multiplied by any scalar is the zero vector):** Given a vector space $(\mathcal{V}, \mathcal{F})$, it holds that $c\boldsymbol{0} = \boldsymbol{0} \iff \boldsymbol{a} = \boldsymbol{0}$.</span>

**Proof:**
$$\begin{align*}\boldsymbol{0}  + \boldsymbol{0} &= \boldsymbol{0}  && \text{by Axiom 4} \\ c(\boldsymbol{0}  + \boldsymbol{0}) &= c\boldsymbol{0} \\ c\boldsymbol{0}  + c\boldsymbol{0} &= c\boldsymbol{0} && \text{by Axiom 8}\end{align*}$$

By Theorem 1, the only vector $\boldsymbol{a}$ in $\mathcal{V}$ for which $\boldsymbol{a} + \boldsymbol{v} = \boldsymbol{v}$ for all vectors $\boldsymbol{v} \in \mathcal{V}$ is the zero vector $\boldsymbol{0}$.  Thus, $c\boldsymbol{0} = \boldsymbol{0}$. 

$\square$

<span style="color:#0060C6">**Theorem 6 (The zero vector is its own negative):** Given a vector space $(\mathcal{V}, \mathcal{F})$, it holds that $-\boldsymbol{0} = \boldsymbol{0}$</span>

**Proof:**

$$\begin{align*}\boldsymbol{a} + -\boldsymbol{a} &= \boldsymbol{0} && \text{by Axiom 5} \\ \boldsymbol{a} + \boldsymbol{a} &= \boldsymbol{0} && \text{assume $\boldsymbol{a} = -\boldsymbol{a}$} \\ \implies 2\boldsymbol{a} &= \boldsymbol{0} \\ \implies \boldsymbol{a} &= \boldsymbol{0} && \text{by Theorem 5}\end{align*}$$

Thus, if we assume $\boldsymbol{a} = -\boldsymbol{a}$, then $\boldsymbol{a}$ must be the zero vector.

$\square$
