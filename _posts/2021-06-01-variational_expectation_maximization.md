---
title: 'Variational expectation-maximization'
date: 2021-06-01
permalink: /posts/vem/
tags:
  - machine learning
  - probability
  - statistics
  - tutorial
---

*Expectation-maximization (EM) is a popular algorithm for performing maximum-likelihood estimation of the parameters in a latent variable model. In this post, I discuss an adapation of the EM algorithm, called variational EM, that performs approximate maximum-likelihood estimation when the posterior distribution required in the E-step is untractable. While often used succesfully in practice, it does not have the same theoretical gaurantees as standard EM.*

Introduction
------------

In a [previous post](https://mbernste.github.io/posts/em/), I discussed the theory and intuition behind the expectation-maximization (EM) algorithm. To review, the EM algorithm is used for performing maximum-likelihood estimation of the parameters in a latent variable. In this problem setting, we have two sets of random variables: observed random variables $X$, for which we have observed its value, and latent random variables $Z$, whose realizations we have not observed.  Furthermore, we have a joint probabilistic model, $P(X,Z;\theta)$, over all random variables where $\theta$ are a set of parameters that parameterize this joint distribution.

