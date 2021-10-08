---
title: 'Perplexity: a more intuitive measure of uncertainty than entropy'
date: 2021-10-08
permalink: /posts/perplexity/
tags:
  - information theory
  - probability
  - statistics
  - tutorial
---

*Like entropy, perplexity is an information theoretic quantity that describes the uncertainty of a random variable. In fact, perplexity is simply a monotonic function of entropy and thus, in some sense, they can be used interchangeabley. So why do we need it? In this post, I'll discuss why perplexity is a more intuitive measure of uncertainty than entropy.*  

Introduction
------------

Perplexity is an information theoretic quantity that crops up in a number of contexts such as [natural language processing](https://en.wikipedia.org/wiki/Perplexity) and is a parameter for the popular [t-SNE](https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding) algorithm used for dimensionality reduction.

Like [entropy](https://mbernste.github.io/posts/entropy/), perplexity provides a measure of the amount of uncertainty of a random variable. In fact, perplexity is simply a monotonic function of entropy. Given a discrete random variable, $X$, perplexity is defined as:

$$\text{Perplexity}(X) := 2^{H(X)}$$

where $H(X)$ is the entropy of $X$.

When I first saw this definition, I did not understand its purpose? That is, if perplexity is simply exponentiated entropy, which is a monotonic function of entropy, why do we need it? After all, we have a good intuition for entropy already: it describes [the number of bits](https://mbernste.github.io/posts/sourcecoding/) needed to encode random samples from $X$'s probability distribution. So why perplexity?

An intuitive measure of uncertainty
-----------------------------------

Perplexity is often used instead of entropy due to the fact that it is arguably more intuitive to our human minds than entropy.  Of course, as we've discussed in a [previous blog post](https://mbernste.github.io/posts/sourcecoding/), entropy describes the number of bits needed to encode random samples from a distribution, which one may argue is already intuitive; however, I would argue that contrary. If I tell you that a given random variable has an entropy of 7, how should you _feel_ about that at a gut level?

Arguably, perplexity provides a more human way of thinking about the random variable's uncertainty and that is because the perplexity of a uniform, discrete random variable with K outcomes is K (see the Appendix to this post)! For example, the perplexity of a fair coin is two and the perplexity of a fair six-sided die is six. This provides a frame of reference for interpreting a perplexity value. That is, if the perplexity of some random variable X is 20, our uncertainty towards the outcome of X is equal to the uncertainty we would feel towards a 20-sided die. This helps _intuit_ the uncertainty at a more gut level!

Appendix
--------

<span style="color:#0060C6">**Theorem:** Given a discrete uniform random variable $X \sim \text{Cat}(p_1, p_2, \dots, p_K)$ where $\forall i,j \in [K], p_i = p_k$ it holds that the perplexity of $X$ is $K$.</span>

**Proof:**

$$\begin{align*}
\text{Perplexity}(X) &:= 2^{H(X)} \\
&= 2^{\frac{1}{K} \sum_{i=1}^K \log_2 \frac{1}{K}} \\
&= 2^{-\log_2 \frac{1}{K}} \\
&= \frac{1}{2^{\log_2 \frac{1}{K}}} \\
&= K
\end{align*}$$

$\square$



