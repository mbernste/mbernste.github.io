---
title: 'Demystifying measure-theoretic probability theory (part 2: random variables)'
date: 2020-01-04
permalink: /posts/measure_theory_2/
tags:
  - mathematics
  - measure theory
  - probability
  - statistics
  - tutorial
---

*In this series of posts, I present my understanding of some basic concepts in measure theory — the mathematical study of objects with “size”— that have enabled me to gain a deeper understanding into the foundations of probability theory.*

*In [part 1](https://mbernste.github.io/posts/measure_theory_1/) of this series, I presented the measure-theoretic definition for probability. In part 2, I will present the measure-theoretic definition for a random variable.*

Introduction
-----

In part 1 of this series, I introduced the measure-theoretic definition of a probability space:

<span style="color:#0060C6">**Definition 1:** A **probability space** is a measure space ($\Omega$, $E$, $P$) where $P(\Omega) = 1$ where </span>
1. <span style="color:#0060C6">The set $\Omega$, is called the **sample space**.</span>
2. <span style="color:#0060C6">The $\sigma$-algebra over $\Omega$, denoted $E$, called the set of **events**.</span>
3. <span style="color:#0060C6">The measure $P$ for the measureable space $(\Omega, E)$ is the **probability measure**.</span>

This definition says that a probability space is simply a measure space where the measure P assigns the entire set $\Omega$ (i.e. the "object")  a value of 1.  In a probability space, the set Ω is called the sample space, and a subset of the sample-space e ∈ E is called an event. 

I interpret this definition as follows: The sample space represents all conceivable futures and and an event represents some subset of conceivable futures. The probability measure assigns each event e a value between 0 and 1, which represents our degree of certainty that our future will be contained in the event.  Specifically, 1 represents full certainty that our future will be contained in the event and 0 represents full certainty that our future will not be contained in the event.   

Recall, our goal for this series, as outlined in [part 1](https://mbernste.github.io/posts/measure_theory_1/), is to unify the definitions of discrete and continuous random variables. How does this measure theoretic definition for probability achieve this goal? 

Random variables
-----

A **random variable** is usually first introduced as a variable (like those used in basic algebra: $y = 2x$) whose value is random. For example, the outcome of a die-roll can be modeled as a random variable $X$ whose value is randomly either 1,2,3,4,5, or 6. We then go on to discuss probabilities regarding which value $X$ will be. For example, for a fair six-sided die, $P(X=1) = 1/6$.

This definition, though not all that rigorous, tends to work fine for basic applications. Now let's look at its measure-theoretic definition:

**Definition 6:** A **random variable** $X$ is a measurable function from a probability space $(\Omega, E, P)$ to a meausrable space $(H, \mathcal{H})$ where $H$ is a set, $\mathcal{H}$ is a $\sigma$-algebra over $H$, and $X$ maps elements from $\Omega$ to $H$.

Wait what? A random variable is really a function?  And what on earth is a measurable function? 

Let's dig into this definition. As we will soon see, not only will both discrete and continuous random variables fit under this definition, but this definition will enable us to talk about other kinds of random variables including random variables that are not even numeric! 

Measurable functions
-----

A measurable function is defined as follows:

**Definition 7:** Given measure spaces $(F, \mathcal{F})$ and $(H, \mathcal{H})$, a function
$$f : F \rightarrow H$$
is a **measurable function** if for all $A \in \mathcal{H}$, $f^{-1}(A) \in \mathcal{F}$.

Now let's parse this definition. 

First off, a measurable function, like any function, maps elements in one set to elements in another set. Given two sets $F$ and $H$, a function $f$ is a mapping from elements in $F$ (called the [domain](https://en.wikipedia.org/wiki/Domain_of_a_function) of $f$) to elements in $H$ (called the [codomain](https://en.wikipedia.org/wiki/Codomain) of $f$). 

A measurable function has a few more layers to it than a plain old function. First, the domain and codomain of $f$ are both measurable spaces equipped with $\sigma$-algebras $\mathcal{F}$ and $\mathcal{H}$ respectively. Lastly, and most importantly, **a measurable function has the ability to "transport" a measure defined for the domain's measurable space $(F, \mathcal{F})$ over to the codomain's measurable space $(H, \mathcal{H})$.** 

What do I mean by this? Say we have a measure μ defined over $(F, \mathcal{F})$ -- that is, $(F, \mathcal{F}, \mu)$ forms a complete measure space. Then we can use f to construct a measure for $(H, \mathcal{H})$ as follows: For any set $A \in \mathcal{H}$, we give it the measure $\mu(f^{-1}(A))$. By the definition of a measurable function, $A$ is guaranteed to be in the $\sigma$-algebra $\mathcal{F}$ and thus, it can be assigned a measure by $\mu$!

An illustration of a measurable function is depicted in part B of the figure below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/measurable_function.png" alt="drawing" width="500"/></center>
