---
title: 'Blackbox variational inference via the reparameterization gradient'
date: 2022-10-30
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

In a [previous blog post](https://mbernste.github.io/posts/variational_inference/), we presented the variational inference (VI) paradigm for estimating posterior distributions when computing them intractable. To review, VI is used in situations in which we have a model that involves hidden random variables $Z$, observed data $X$, and some posited probabilistic model over the hidden and observed random variables $$P(Z, X)$$. Our goal is to compute the posterior distribution $P(Z \mid X)$. Under an ideal situation, we would do so by using Bayes theorem:

$$p(z \mid x) = \frac{p(x \mid z)p(z)}{p(x)}$$

where $$z$$ and $$x$$ are realizations of $$Z$$ and $$X$$ respectively and $$p(.)$$ are probability mass/density functions for the distributions implied by their arguments.  In practice, it is often difficult to compute $p(z \mid x)$ via Bayes theorem because the denominator $p(x)$ does not have a closed form. 

Instead of computing $$p(z \mid x)$$ exactly via Bayes theorem, VI attempts to find another distribution $q(z)$ from some set of distributions $\mathcal{Q}$, called the **variational family** that minimizes the KL-divergence to $$p(z \mid x)$$. This minimization occurs implicitly by maximizing a surrogate quantity called the [evidence lower bound (ELBO)](https://mbernste.github.io/posts/elbo/):

$$\text{ELBO}(q) :=  E_{Z \sim q}\left[\log p(x, Z) - \log q(Z) \right]$$

Thus, our goal is to solve the following maximization problem:

$$\hat{q} := \text{arg max}_{q \in \mathcal{Q}} \text{ELBO}(q)$$

When each member of $\mathcal{Q}$ is characterized by a set of parameters $\phi$, the ELBO can be written as a function of $\phi$

$$\text{ELBO}(\phi) :=  E_{Z \sim q_\phi}\left[\log p(x, Z) - \log q_\phi(Z) \right]$$

Then, the optimziation problem reduces to optimizing over $\phi$:

$$\hat{\phi} := \text{arg max}_{\phi} \text{ELBO}(\phi)$$

In this post, we will present a flexible method, called **blackbox variational inference via the reparameterization gradient**, co-invented by [Kingma and Welling (2014)](https://arxiv.org/abs/1312.6114) and [Rezende, Mohamed, and Wierstra (2014)](https://arxiv.org/abs/1401.4082), for solving this optimization problem under the following conditions:
1. $q$ is paramterized by some set of variational parameters $\phi$ and is continuous with respect to these paramters
2. Sampling from $q_\phi$ can be performed via the **reparameterization trick** (to be discussed)

The method is often called "blackbox" VI because it works for a large set of models $p$ and $q$ and it acts as a "blackbox" for which $p$ and $q$ can simply be plugged into the algorithm thereby avoiding the tedious model-specific, mathematical derivations that developing a variational inference algorithm often requires (See the [Appendix](https://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf) to the original paper presenting [Latent Dirichlet Allocation](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation) for an example of such a model-specific VI derivation).

The reparameterization gradient
-------------------------------

[Gradient ascent](https://en.wikipedia.org/wiki/Gradient_descent) is a straightforward method for solving optimization problems for continuous functions and is a very heavily studied method in machine learning. Thus, it is natural to attempt to optimize the ELBO via gradient ascent. Applying gradient ascent to the ELBO would entail iteratively computing the [gradient](https://en.wikipedia.org/wiki/Gradient) of the ELBO with respect to $\phi$ and then  updating our estimate of $\phi$ via this gradient. That is, at each iteration $t$, we have some estimate of $\phi$, denoted $\phi_t$ that we will update as follows:

$$\phi_{t+1} := \phi_t + \alpha \nabla_\phi \left. \text{ELBO}(\phi) \rvert_{\phi_t}$$

where $\alpha$ is the learning rate. This step is repeated until we converge on a local optimum of the ELBO. Now, the question becomes how do we compute the gradient of the ELBO? The key challenge here is dealing with the expectation (i.e., the integral) in the ELBO. 

One idea to get around is to approximate the ELBO using Monte Carlo estimates of the expectation by sampling $L$ values from $q_\phi$ as follows

$z'_1, \dots, z'_L \overset{\text{i.i.d.}}{\sim}q_\phi$

and then estimate the expectation via:

$$\begin{align*}\text{ELBO}(\phi) := E_{Z \sim q_phi}\left[\log p(x, Z) - \log q_\phi(Z) \right] \\ \approx \frac{1}{L} \sum_{l=1}^L \left[\log p(x, z'_l) - \log q_\phi(z'_l) \right] \end{align*}$$

We'll use $\text{ELBO}'$ to denote the Monte Carlo estimate of the ELBO. Now, it may be tempting to simply compute the gradient of $\text{ELBO}'$ with respect to $\phi$ and use this in our gradient ascent algorithm. Unfortunately, this would not be correct due to the fact that 




Example: Bayesian linear regression
-----------------------------------
