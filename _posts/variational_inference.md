---
title: 'A high-level overview of variational inference'
date: 2020-05-13
permalink: /posts/em/
tags:
  - machine learning
  - probability
  - statistics
  - tutorial
---

THIS POST IS UNDER CONSTRUCTION

Variational inference is a high-level paradigm for estimating a posterior distribution when computing it explicitly is intractable.  Unlike expectation maximization, variational inference estimates a closed form density function for the posterior rather than a point estimate for the latent variables.  Thus, variational inference is also different from MCMC methods in that it involves approximating the posterior with an analytical approximation rather than via sampling. 

More specifically, variational inference is used in situations in which we have a model that involves hidden random variables $Z$, observed data $X$, and joint model over the hidden and observed data $p(z, x)$. Our goal is to perform inference on the hidden data via the posterior distribution over $Z$ as given by Bayes theorem:

$$p(z \mid x) := \frac{p(x \mid z)p(z)}{p(x)}$$

Variational inference casts the problem of computing the posterior as that of finding another distribution $q(z)$ that is ``close" to $$p(z \mid x)$$.  Ideally, $q(z)$ is easier to evaluate than $p(z \mid x)$, and, if $p(z \mid x)$ and $q(z)$ are similar, then we can use $q(z)$ as a replacement for $p(z \mid x)$ in our inference tasks.  

We restrict our search for $$q(z)$$ to a family of surrogate distributions over $Z$, called the \textbf{variational distribution family}, denoted by the set of distributions $\mathcal{Q}$.  Our goal then is to find the distribution $q \in \mathcal{Q}$ that makes $q(z)$ as ``close" to $p(z \mid x)$ as possible.    When, each member of $\mathcal{Q}$ is characterized by the values of a set of parameters $\phi$, we call $\phi$ the \textbf{variational parameters}.  Our goal is then to find the value for $\hat{\phi}$ that makes $q(z \mid \phi)$ as close to $p(z \mid x)$ as possible
and then returns $$q(z \mid \hat{\phi})$$ as the approximation to the posterior.

In general, there are many algorithms for performing variational inference, each with strengths and weaknesses depending on $$p(z, x)$$ and the variational family.  Variational inference is a high-level strategy rather an explicit algorithm.
