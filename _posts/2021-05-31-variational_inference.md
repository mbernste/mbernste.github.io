---
title: 'A high-level overview of variational inference'
date: 2021-05-31
permalink: /posts/em/
tags:
  - machine learning
  - probability
  - statistics
  - tutorial
---

Variational inference is a high-level paradigm for estimating a posterior distribution when computing it explicitly is intractable.  In this post, we will 

Introduction
------------

Variational inference is a high-level paradigm for estimating a posterior distribution when computing it explicitly is intractable.  More specifically, variational inference is used in situations in which we have a model that involves hidden random variables $Z$, observed data $X$, and some posited probabilistic model over the hidden and observed random variables $$P(Z, X)$$. Our goal is to perform inference on the hidden data via the posterior distribution over $Z$ as given by Bayes theorem:

$$p(z \mid x) := \frac{p(x \mid z)p(z)}{p(x)}$$

where $$z$$ and $$x$$ are realizations $$Z$$ and $$X$$ respectively and $$p(.)$$ are probability mass/density functions for the distributions implied by their arguments.

Instead of computing $$p(z \mid x)$$ exactly, variational inference attempts to find another distribution $q(z)$ that is ``close" to $$p(z \mid x)$$.  Ideally, $q(z)$ is easier to evaluate than $$p(z \mid x)$$, and, if $$p(z \mid x)$$ and $$q(z)$$ are similar, then we can use $$q(z)$$ as a replacement for $p(z \mid x)$ for any relevant downstream tasks.  

We restrict our search for $$q(z)$$ to a family of surrogate distributions over $$Z$$, called the *variational distribution family*, denoted by the set of distributions $\mathcal{Q}$.  Our goal then is to find the distribution $q \in \mathcal{Q}$ that makes $q(z)$ as ``close" to $p(z \mid x)$ as possible.    When, each member of $\mathcal{Q}$ is characterized by the values of a set of parameters $\phi$, we call $\phi$ the *variational parameters*.  Our goal is then to find the value for $\hat{\phi}$ that makes $q(z \mid \phi)$ as close to $p(z \mid x)$ as possible
and return $$q(z \mid \hat{\phi})$$ as our approximation of the true posterior.


Details
------------

Variational inference uses the KL-divergence from $p(z \mid x)$ to $q(z)$ as a measure of ``closeness":

$$KL(q(z) \ || \ p(z \mid \phi)) := E_{Z \sim q}\left[\log\frac{q(Z)}{p(Z \mid x)} \right]$$

Thus, variational inference attempts to find 

$$\hat{q} := \text{argmin}_q \ KL(q(z) \ || \ p(z \mid x))$$

and then returns $\hat{q}(z)$ as the approximation to the posterior.

Variational inference minimizes the KL-divergence in Equation~\ref{eq:kl_variational} by maximizing a surrogate quantity called the \textbf{evidence lower bound} (ELBO) which is a lower bound on the log-marginal likelihood, $\log p(x)$ -- also called the \textbf{evidence}.  That is, the KL-divergence can be formulated as the evidence minus the ELBO:
