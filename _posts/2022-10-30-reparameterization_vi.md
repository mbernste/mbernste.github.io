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
1. $q$ is paramterized by some set of variational parameters $\phi$ and is continuous with respect to these parameters
2. Sampling from $q_\phi$ can be performed via the **reparameterization trick** (to be discussed)
3. $p$ is continuous with respect to $z$ 

The method is often called "blackbox" VI because it works for a large set of models $p$ and $q$ and it acts as a "blackbox" for which $p$ and $q$ can simply be plugged into the algorithm thereby avoiding the tedious model-specific, mathematical derivations that developing a variational inference algorithm often requires (See the [Appendix](https://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf) to the original paper presenting [Latent Dirichlet Allocation](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation) for an example of such a model-specific VI derivation).

The reparameterization gradient
-------------------------------

[Gradient ascent](https://en.wikipedia.org/wiki/Gradient_descent) is a straightforward method for solving optimization problems for continuous functions and is a very heavily studied method in machine learning. Thus, it is natural to attempt to optimize the ELBO via gradient ascent. Applying gradient ascent to the ELBO would entail iteratively computing the [gradient](https://en.wikipedia.org/wiki/Gradient) of the ELBO with respect to $\phi$ and then  updating our estimate of $\phi$ via this gradient. That is, at each iteration $t$, we have some estimate of $\phi$, denoted $\phi_t$ that we will update as follows:

$$\phi_{t+1} := \phi_t + \alpha \nabla_\phi \left. \text{ELBO}(\phi) \right|_{\phi_t}$$

where $\alpha$ is the learning rate. This step is repeated until we converge on a local optimum of the ELBO. 

Now, the question becomes how do we compute the gradient of the ELBO? A key challenge here is dealing with the expectation (i.e., the integral) in the ELBO. One approach called the **reparameterization gradient** method, co-proposed by [Kingma and Welling (2014)](https://arxiv.org/abs/1312.6114) and [Rezende, Mohamed, and Wierstra (2014)](https://arxiv.org/abs/1401.4082), entails performing [stochastic gradient ascent](https://en.wikipedia.org/wiki/Stochastic_gradient_descent) using computationally tractable random gradients instead of using the computationally _intractable_ exact gradient.

Stochastic gradient ascent works as follows: Instead of computing the exact gradient of the ELBO with respect to $\phi$, we formulate a random variable $G(\phi)$, whose expectation is the gradient of the ELBO at $\phi$ -- that is, for which $E[G(\phi)] = \nabla_\phi ELBO(\phi)$. Then, we sample approximate gradients from this distribution and take small steps in the direction of these random gradients:

$$\begin{align*} \boldsymbol{g} &\sim G(\phi_t) \\ \phi_{t+1} &:= \phi_t + \alpha \boldsymbol{g} \end{align*}$$

How does the reparameterization gradient method compute these random gradients? It does so by employing the **reparameterization trick**. The reparameterization trick works as follows: we re-formulate the distribution $q_\phi(z)$ in terms of a surrogate random variable $\epsilon$, and a determinstic function $g$ as follows:

$$\begin{align*}\epsilon &\sim \mathcal{D} \\ z &:= g_\phi(\epsilon)\end{align*}$$

Then, we can write the ELBO as

$$\text{ELBO}(\phi) := E_{\epsilon \sim \mathcal{D}} \left[ \log p(x, g_\phi(\epsilon)) - \log q_\phi(g_\phi(\epsilon)) \right]$$

It turns out that by performing this reparameterization we can sample stochastic gradients! Specifically, we sample a stochastic gradient via the following process:

1. Sample random variables from our surrogate distribution:

$$\epsilon_1, \dots, \epsilon_L \sim \mathcal{D}$$

2. Compute a Monte Carlo approximation to the ELBO:

$$\tilde{ELBO}(\phi) := \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right]$$ 

3. Compute the gradient to this Monte Carlo approximation:

$$\nabla_\phi \tilde{ELBO}(\phi) := \nabla_\phi \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right]$$ 

Notice here that $\nabla_\phi \tilde{ELBO}(\phi)$ is a random vector (previously denoted by $\boldsymbol{g}$ in the general case) where the randomness comes from sampling of $\epsilon_1, \dots, \epsilon_L$ from $\mathcal{D}$.  Moreover, it can be proven that 

$$E[\nabla_\phi \tilde{\text{ELBO}}(\phi)] = \nabla_\phi \text{ELBO}(\phi)$$

That is, the expectation of this random gradient is the exact gradient of the ELBO! 

So long as $g_\phi$ is continuous with respect to $\phi$ (i.e., $q_\phi$ is continuous with respect to $\phi$) and $p$ is continuous with respect to $z$,  the random gradient $\nabla_\phi \tilde{\text{ELBO}}(\phi)$ exists. 

Reparameterization gradients in practice
----------------------------------------

Implementing the reparameterization gradient for a given model $p(x, z)$ (that is continuous with respect to $z$) can be quite simple in practice. We really only need to specificy two things:

1. **Variational distribution $q_\phi(z)$**: The form of the variational posterior depends on the problem at hand, but in many cases, one can assume the exact posterior $p(z \mid x)$ is approximately normal, and thus let $q_\phi(z)$ be a normal distribution parameterized by a mean $\mu$ and variance $\sigma^2$. Note, we only require that $q_\phi(z)$ be continuous with respect to $\boldsymbol{z}$.
2. **Reparameterization of $q_\phi(z)$**: This _can_ be tricky depending on chosen $q_\phi(z)$; however, for many common choices of variational families, it can be quite easy. For example, if $q_\phi(z)$ is a [location-scale family](https://en.wikipedia.org/wiki/Location%E2%80%93scale_family) distribution then reparameterization becomes quite simple. For example, if $q_\phi(z)$ is a Gaussian distribution where the variational parameters are simply $\phi := \{\mu, \sigma^2\}$ (i.e., the  mean $\mu$ and variance $\sigma^2$), we can reparameterize $q_\phi(z)$ as:

$$\begin{align*}\epsilon \sim N(0, 1) \\ z = \mu + \sigma \epsilon\end{align*}$$

Here, the surrogate random variable is a simple standard normal distribution. The deterministic function $g$ is the function that simply shifts $\epsilon$ by $\mu$ and scales it by $\sigma$. Note that $z \sim N(\mu, \sigma^2) = q_\phi(z)$ and thus, this is a valid reparameterization.

Once the variational family and reparameterization are specified, we can formulate the approximate ELBO:

$$\tilde{ELBO}(\phi) := \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right]$$ 

Then, we can use [automatic differentiation](https://en.wikipedia.org/wiki/Automatic_differentiation) algorithms, such as those implemented in modern machine learning libraries like [pytorch](https://pytorch.org/) or [tensorflow](https://www.tensorflow.org/) to compute the gradient $\nabla_\phi \tilde{ELBO}(\phi)$. Moreover, we can perform steps along the gradient using gradient-based optimziation methods implemented in these libraries as well!. 

Example: Bayesian linear regression
-----------------------------------
