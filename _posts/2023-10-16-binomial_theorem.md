---
title: "The Binomial Theorem"
date: 2023-10-16
permalink: /posts/binomial_theorem/
tags:
  - tutorial
  - mathematics
---

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

To form a term in the fully expanded polynomial, we imagine the process of iterating over each binomial factor and choosing _one_ of the two terms to include. For example, from $(a+b)$, we choose either $a$ or $b$ to include in the term, but never both. This is because of how the distributive property works: as we expanded the expression, we separated the two terms in each binomial factor so that they never could appear in the same term of the expansion.

Moreover, we see that _every_ combination of terms from each binomial factor will be used to form a term in the expanded polynomial. Again, this occurs from the process of carrying out the distributive property iteratively in the expansion: everytime we carry out the distributive property, we create two batches of terms in the expansion that will include either the first or second term from that binomial factor.

With this insight,  let’s look at the following polynomial: 

$$\begin{align*}(x + y) &= (x + y)(x + y)(x + y) \\ &= xxx + xyx + yxx + yyx + xxy + xyy + yxy + yyy \\ &= x^3 + 3x^2y + 3y^2x + y^3\end{align*}$$

Let’s say we’re interested in all terms in the expanded polynomial that have $k$ of the $x$ values. By the previous observation, the term that has $k$ of the $x$ values must have $n − k$ of the $y$ values because we only pick a single value from each binomial factor.  How many of the terms in the expanded polynomial will have $k$ of the $x$ values? Every combination of ways of picking $k$ of the $x$ values from the binomial factors will result in a term of the form $x^ky^{n-k}$ in the expanded polynomial. Thus, there will be ${n \choose k}$ such terms.

Finally, there are terms in the polynomial with $k$ values of $x$ for every value of $k$ between $0$ and $n$. This is a result of the fact that every combination of terms where each term is picked from a single binomial factor is represented. This final
observation leads to the Binomial Theorem:

$$(x+y)^n = \sum_{k=0}^n {n \choose k} x^ky^{n-k}$$

$\square$

