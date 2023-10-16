---
title: "The Binomial Theorem"
date: 2023-10-16
permalink: /posts/binomial_theorem/
tags:
  - tutorial
  - mathematics
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_The binomial theorem pops up in many proofs across mathematics and mathematical statistics. In this post, I will walk through a proof of this theorem._

Introduction
============

The **Binomial Theorem** is a basic theorem in mathematics that states that a binomial expression of the form $(x+y)^n$ can be represented as a summation involving the [binomial coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient):

$$(x+y)^n = \sum_{k=0}^n {n \choose k} x^ky^{n-k}$$

This statement always appeared mysterious to me. What is the intuition for the summation? Moreover, why does the [binomial coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient), "$n$ choose $k$", appear? This seems to hint that there is some combinatorial process going on when calculating $x+y$. In this post I will provide a proof that helped me better intuit thsi theorem. 

Proof
=====

Let's start with a polynomial of the form

$$(a + b)(c + d)(e + f)$$

We can apply the [distributive property](https://en.wikipedia.org/wiki/Distributive_property) as follows:

$$(a + b)(c + d)(e + f) = a(c+d)(e+f) + b(c+d)(e+f)$$

Notice that the first and second terms are two separate polynomials involving $a$ and $b$ where the first _only_ involves $a$, but not $b$, whereas the second polynomial _only_ involves $b$, but not $a$. In fact, for each binomial factor (i.e. for each of
$(a + b)$, $(c + d)$, and $(e + f)$), only one of the terms of the binomial will appear in a given term of the fully expanded polynomial. 

$$\begin{align*}(a + b)(c + d)(e + f) &= a(c+d)(e+f) + b(c+d)(e+f) \\ &= a(c(e+f) + d(e+f)) + b(c(e+f) + d(e+f)) \\ &= ace + acf + ade + adf + bce + bcf + bde + bdf\end{align*}$$

To form a term in the fully expanded polynomial, we iterate over each binomial factor and choose _one_ of the terms to include. For example, from $(a+b)$, we choose either $a$ or $b$ to include in the term, but never both. This is because of how the distributive property works: as we expanded the expression, we separated the two terms in each binomial factor so that they never could appear in the same term of the expansion.

