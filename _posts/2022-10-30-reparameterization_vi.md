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

$$\phi_{t+1} := \phi_t + \alpha \nabla_\phi \left. \text{ELBO}(\phi) \right|_{\phi_t}$$

where $\alpha$ is the learning rate. This step is repeated until we converge on a local optimum of the ELBO. 

Now, the question becomes how do we compute the gradient of the ELBO? A key challenge here is dealing with the expectation (i.e., the integral) in the ELBO. One approach called the **reparameterization gradient** method, co-proposed by [Kingma and Welling (2014)](https://arxiv.org/abs/1312.6114) and [Rezende, Mohamed, and Wierstra (2014)](https://arxiv.org/abs/1401.4082), entails performing [stochastic gradient ascent](https://en.wikipedia.org/wiki/Stochastic_gradient_descent) using computationally tractable random gradients instead of using the computationally _intractable_ exact gradient.

Stochastic gradient ascent works as follows: Instead of computing the exact gradient of the ELBO with respect to $\phi$, we formulate a random variable $G(\phi)$, whose expectation is the gradient of the ELBO at $\phi$ -- that is, for which $E[G(\phi)] = \nabla_\phi ELBO(\phi)$. Then, we sample approximate gradients from this distribution and take small steps in the direction of these approximations:

$$\begin{align*} \boldsymbol{g} &\sim G(\phi_t) \\ \phi_{t+1} &:= \phi_t + \alpha \boldsymbol{g} \end{align*}$$

The reparameterization gradient samples stochastic gradients by employing the **reparameterization trick**. The reparameterization trick works as follows: we re-formulate the distribution $q_\phi(z)$ in terms of a surrogate random variable $\epsilon$, and a determinstic function $g$ as follows:

$$\begin{align*}\epsilon &\sim \mathcal{D} \\ z &:= g_\phi(\epsilon)\end{align*}$$

Then, we can write the ELBO as

$$\text{ELBO}(\phi) := E_{\epsilon \sim \mathcal{D}} \left[ \log p(x, g_\phi(\epsilon)) - \log q_\phi(g_\phi(\epsilon)) \right]$$

What does this reformulation get us exactly? By performing this reparameterization we can sample stochastic gradients! That is, we sample a stochastic gradient via the following generative process:

$$\begin{align*}\epsilon_1, \dots, \epsilon_L &\sim \mathcal{D} \\ \tilde{ELBO}(\phi) &:= \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right] \\ \nabla_\phi \tilde{ELBO}(\phi) &:= \nabla_\phi \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right] \end{align*}$$ 

Notice here that $\nabla_\phi \tilde{ELBO}(\phi)$ is a random vector where the randomness comes from sampling of $\epsilon_1, \dots, \epsilon_L$.  Moreover, the expectation of $\nabla_\phi \tilde{\text{ELBO}}(\phi)$ is equal to $\nabla_\phi \text{ELBO}(\phi)$



and then estimate the expectation via:


We'll use $\text{ELBO}'$ to denote the Monte Carlo estimate of the ELBO. Now, it may be tempting to simply compute the gradient of $\text{ELBO}'$ -- that is, compute $\nabla_\phi \text{ELBO}'(\phi)$ with respect to $\phi$ and use this in our gradient ascent algorithm. Unfortunately, this would not be correct due to the fact that we _sampled_ from $q_\phi$ which itself includes the parameters $\phi$. That i 




Example: Bayesian linear regression
-----------------------------------
