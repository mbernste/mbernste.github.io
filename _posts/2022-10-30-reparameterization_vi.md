---
title: 'Blackbox variation inference via the reparameterization gradient'
date: 2022-10-10
permalink: /posts/reparameterization_vi/
tags:
  - tutorial
  - variational inference
  - probabilistic modeling
  - machine learning
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

In a [previous blog post](), we presented the variational inference paradigm for estimating posterior distributions when computing is intractable. To review, variational inference is used in situations in which we have a model that involves hidden random variables $Z$, observed data $X$, and some posited probabilistic model over the hidden and observed random variables $$P(Z, X)$$. Our goal is to compute the posterior distribution $P(Z \mid X)$. Under an ideal situation, we would do so by using Bayes theorem:

$$p(z \mid x) = \frac{p(x \mid z)p(z)}{p(x)}$$

where $$z$$ and $$x$$ are realizations of $$Z$$ and $$X$$ respectively and $$p(.)$$ are probability mass/density functions for the distributions implied by their arguments.  In practice, it is often difficult to compute $p(z \mid x)$ via Bayes theorem because the denominator $p(x)$ does not have a closed form. 

Instead of computing $$p(z \mid x)$$ exactly via Bayes theorem, variational inference attempts to find another distribution $q(z)$ from some set of distributions $\mathcal{Q}$ that minimizes the KL-divergence to $$p(z \mid x)$$. This minimization occurs implicitly by maximizing a surrogate quantity called the [evidence lower bound (ELBO)](https://mbernste.github.io/posts/elbo/):

$$\text{ELBO}(q) :=  E_{Z \sim q}\left[\log p(x, Z) - \log q(Z) \right]$$

Thus, our goal is to solve the following maximization problem:

$$\hat{q} := \text{arg max}_{q \in \mathcal{Q}} \text{ELBO}(q)$$

In this post, we will present a flexible method, called **blackbox variational inference via the reparameterization gradient** (also called the "pathwise gradient") for solving this optimization problem under the following conditions:
1. $p(x, z)$ is parameterized by some set of parameters $\theta$ and is continuous with respect to these parameters. We'll denote this distribution as $p_\theta(x, z)$.
2. $q(z)$ is paramterized by some set of variational parameters $\phi$ and is continuous with respect to these paramters. We'll denote this distribution as $q_\phi(z)$
3. Sampling from $q(z)$ can be performed via the **reparameterization trick** (to be discussed)

As the name suggests, we will use gradient ascent to solve the maximization problem. Moreover, the method is often called "blackbox" variational inference it works for a large set of models $p$ and $q$. That is, the algorithm acts as a "blackbox" for which $p$ and $q$ can simply be plugged into the algorithm and avoids the tedious mathematical derivations and model-specific algorithm that variational inference algorithms sometimes requires.

The reparameterization gradient
-------------------------------


Example: Bayesian linear regression
-----------------------------------
