---
title: 'Perplexity: a human-interpretable measure of entropy'
date: 2021-10-08
permalink: /posts/perplexity/
tags:
  - information theory
  - probability
  - statistics
  - tutorial
---

*Perplexity is an information theoretic quantity that, like entropy, provides a measure for the uncertainty of a random variable. In fact, perplexity is simply a monotonic function of entropy and thus, in some sense, they can be used interchangeabley. In this post, we discuss the relationship between perplexity and entropy as well as how to interpret perplexity.*  

Introduction
------------

Perplexity is an information theoretic quantity that crops up in a number of contexts such as [natural language processing](https://en.wikipedia.org/wiki/Perplexity) and is a parameter for the popular [t-SNE](https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding) algorithm used for dimensionality reduction.

Like [entropy](https://mbernste.github.io/posts/entropy/), perplexity provides a measure of the amount of uncertainty of a random variable. In fact, perplexity is simply a monotonic function of entropy. Given a discrete random variable, $X$, perplexity is defined as:

$\text{Perplexity}(X) := 2^{H(X)}$

where $H(X)$ is the entropy of $X$.

When I first saw this definition, I asked myself: what is the point of it? That is, if perplexity is simply exponentiated entropy, which is a monotonic function of entropy, why do we need it? After all, we have a good intuition for entropy already: it describes [the number of bits](https://mbernste.github.io/posts/sourcecoding/) needed to encode random samples from $X$'s probability distribution. So why perplexity?

A "human-interpretable" measure of uncertainty
----------------------------------------------

Perplexity is often used instead of entropy due to the fact that it is arguably more interpretable than entropy.  Of course, as we've discussed in a [previous blog post](https://mbernste.github.io/posts/sourcecoding/), entropy describes the number of bits needed to encode random samples from a distribution, which one may argue is already interpretable; however, I would argue that it is hard to intuit at a gut level.  If I tell you that a given random variable has an entropy of 7, how should you _feel_ about that?

Arguably, perplexity provides a more human-interpretable way of thinking about the random variable's uncertainty and that interpretation arises from the fact that the perplexity of a uniform, discrete random variable with K outcomes is K (see the Appendix to this post)! For example, the perplexity of a fair coin is two and the perplexity of a fair six-sided die is six. This provides a frame of reference for interpreting a perplexity value. That is, if the perplexity of some random variable X is 20, our uncertainty towards the outcome of X is equal to the uncertainty we would have towards a 20-sided die. This helps _intuit_ the uncertainty level at a more gut level!

Appendix
--------

<span style="color:#0060C6">**Theorem:** Given a discrete uniform random variable $X \sim \text{Cat}(p_1, p_2, \dots, p_K)$ where $\forall i,j \in [K], p_i = p_k it holds that the perplexity of $X$ is $K$.</span>

**Proof:**

$$\begin{align*}
\text{Perplexity}(X) &:= 2^{H(X)} \\
&= 2^{\frac{1}{K} \sum_{i=1}^K \log_2 \frac{1}{K}} \\
&= 2^{-\log_2 \frac{1}{K}} \\
&= K
\end{align*}$$

$\square$



