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

At its core the reparameterization gradient method is a method for performing stochastic gradient ascent on the ELBO. It does so by employing a reformulation of the ELBO using the reparameterization trick. In this post, we will review stochastic gradient descent, present the reparameterization gradient method, and finally, dig into an example of implementing this method in [PyTorch](https://pytorch.org/) for performing Bayesian linear regression.

Stochastic gradient ascent of the ELBO
--------------------------------------

[Gradient ascent](https://en.wikipedia.org/wiki/Gradient_descent) is a straightforward method for solving optimization problems for continuous functions and is a very heavily studied method in machine learning. Thus, it is natural to attempt to optimize the ELBO via gradient ascent. Applying gradient ascent to the ELBO would entail iteratively computing the [gradient](https://en.wikipedia.org/wiki/Gradient) of the ELBO with respect to $\phi$ and then  updating our estimate of $\phi$ via this gradient. That is, at each iteration $t$, we have some estimate of $\phi$, denoted $\phi_t$ that we will update as follows:

$$\phi_{t+1} := \phi_t + \alpha \nabla_\phi \left. \text{ELBO}(\phi) \right|_{\phi_t}$$

where $\alpha$ is the learning rate. This step is repeated until we converge on a local optimum of the ELBO. 

Now, the question becomes how do we compute the gradient of the ELBO? A key challenge here is dealing with the expectation (i.e., the integral) in the ELBO. At its core, the reparameterization gradient method entails performing [stochastic gradient ascent](https://en.wikipedia.org/wiki/Stochastic_gradient_descent) using computationally tractable random gradients instead of using the computationally _intractable_ exact gradient.

Stochastic gradient ascent works as follows: Instead of computing the exact gradient of the ELBO with respect to $\phi$, we formulate a random variable $V(\phi)$, whose expectation is the gradient of the ELBO at $\phi$ -- that is, for which $E[V(\phi)] = \nabla_\phi ELBO(\phi)$. Then, at iteration $t$, we sample approximate gradients from $V(\phi_t)$ and take a small step in the direction of this random gradients:

$$\begin{align*} v &\sim V(\phi_t) \\ \phi_{t+1} &:= \phi_t + \alpha v \end{align*}$$

The question now becomes, how do formulate a distribution $V(\phi)$ whose expectation is the gradient of the ELBO, $\nabla_\phi \text{ELBO}(\phi)$? As discussed in the next section, the reparameterization trick will enable one approach towards formulating such a distribution.

The reparameterization trick
----------------------------

Before discussing how we formulate our distribution of stochastic gradients $V(\phi)$, let us first present the reparameterization trick, which was co-invented by co-invented by [Kingma and Welling (2014)](https://arxiv.org/abs/1312.6114) and [Rezende, Mohamed, and Wierstra (2014)](https://arxiv.org/abs/1401.4082).  It works as follows: we "reparameterize" the distribution $q_\phi(z)$ in terms of a surrogate random variable $\epsilon$ distributed according to some "simple" distribution $\mathcal{D}$ that we can easily sample from (e.g., a standard normal distribution), and a determinstic function $g$ in such a way that sampling $z$ from $q_\phi(z)$ is performed as follows:

$$\begin{align*}\epsilon &\sim \mathcal{D} \\ z &:= g_\phi(\epsilon)\end{align*}$$

One way to think about this is that instead of sampling $z$ directly from our variational posterior $q_\phi(z)$, we "re-design" the generative process of $z$ such that we first sample a surrogate random variable $\epsilon$ and then transform $\epsilon$ into $z$ all while ensuring that in the end, the distribution of $z$ still follows $q_\phi$. This process can be depicted below:

&nbsp;

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/reparameterization_example_ring.png" alt="drawing" width="700"/></center>

&nbsp;

Reparmaterizing $q_\phi(z)$ can be tricky; however, for many common choices of variational families, it can made to be easy. For example, if $q_\phi(z)$ is a [location-scale family](https://en.wikipedia.org/wiki/Location%E2%80%93scale_family) distribution then reparameterization becomes quite simple. For example, if $q_\phi(z)$ is a Gaussian distribution 

$$q_\phi := N(\mu, \sigma^2)$$

where the variational parameters are simply $\phi := \left\\{\mu, \sigma^2\right\\}$ (i.e., the  mean $\mu$ and variance $\sigma^2$), we can reparameterize $q_\phi(z)$ such that sampling $z$ is done as follows:

$$\begin{align*}\epsilon \sim N(0, 1) \\ z = \mu + \sigma \epsilon\end{align*}$$

Here, the surrogate random variable is a simple standard normal distribution. The deterministic function $g$ is the function that simply shifts $\epsilon$ by $\mu$ and scales it by $\sigma$. Note that $z \sim N(\mu, \sigma^2) = q_\phi(z)$ and thus, this is a valid reparameterization.

Now, what does this reparameterization trick get us? How does it enable us to compute random gradients of the ELBO? First, we note that following the reparameterization trick, we can re-write the ELBO as follows:

$$\text{ELBO}(\phi) := E_{\epsilon \sim \mathcal{D}} \left[ \log p(x, g_\phi(\epsilon)) - \log q_\phi(g_\phi(\epsilon)) \right]$$

This formulation enables us to now approxiamte the ELBO via Monte Carlo Sampling. That is, we can first sample random variables from our surrogate distribution $\mathcal{D}$:

$$\epsilon_1, \dots, \epsilon_L \sim \mathcal{D}$$

Then we can compute a Monte Carlo approximation to the ELBO:

$$\tilde{ELBO}(\phi) := \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right]$$ 

So long as $g_\phi$ is continuous with respect to $\phi$ (i.e., $q_\phi$ is continuous with respect to $\phi$) and $p$ is continuous with respect to $z$, we can take gradient of this approximation:

$$\nabla_\phi \tilde{ELBO}(\phi) := \nabla_\phi \frac{1}{L} \sum_{l=1}^L \left[  \log p(x, g_\phi(\epsilon'_l)) - \log q_\phi(g_\phi(\epsilon'_l)) \right]$$

Notice that $\nabla_\phi \tilde{ELBO}(\phi)$ is a random vector (previously denoted by $\boldsymbol{g}$ in the general case) where the randomness comes from sampling of $\epsilon_1, \dots, \epsilon_L$ from $\mathcal{D}$.  Moreover, it can be proven that 

$$E[\nabla_\phi \tilde{\text{ELBO}}(\phi)] = \nabla_\phi \text{ELBO}(\phi)$$

Thus, the process of sampling $\epsilon_1, \dots, \epsilon_L$ from $\mathcal{D}$, computing the approximate ELBO, and then calculating the gradient to this approximation is equivalent to sampling from a distribution of random gradients $V(\phi)$ whose expectation is the gradient of the ELBO!


Example: Bayesian linear regression
-----------------------------------

The reparameterized gradient method can be applied to a wide variety of models. Here, we'll apply it to Bayesian linear regression. Let's first describe the probabilistic model behind linear regression. Our data consists of covariates $\boldsymbol{x}_1, \dots, \boldsymbol{x}_n \in \mathbb{R}^J$ paired with response variables $y_1, \dots, y_n \in \mathbb{R}^n$. Our data model is then defined as

$$p(y_1, \dots, y_n \mid \boldsymbol{x}_1, \dots, \boldsymbol{x}_n) := \prod_{i=1}^n N(y_i; \boldsymbol{\beta}^T\boldsymbol{x}_i, \sigma^2)$$

where $N(.; a, b)$ is the probability density function parameterized by mean $a$ and variance $b$. We will assume that the first covariate for each $\boldsymbol{x}_i$ is defined to be 1 and thus, the first coefficient of $\boldsymbol{\beta}$ is the intercept term.

That is, we assume that each $y_i$ is "generated" from its $\boldsymbol{x}_i$ via the following process:

$$\begin{align*}\mu_i & := \boldsymbol{\beta}^T\boldsymbol{x}_i \\ y_i &\sim N(\mu_i, \sigma^2)\end{align*}$$

Notice that the variance $\sigma^2$ is constant across all data points and thus, our model assumes [homoscedasticity](https://en.wikipedia.org/wiki/Homoscedasticity_and_heteroscedasticity). Furthmore, our data only consists of the pairs $(\boldsymbol{x}_1, y_1), \dots, (\boldsymbol{x}_n, y_n)$, but we don't know $\boldsymbol{\beta}$ or $\sigma^2$. We can infer the value of these variables using Bayesian inference! Specifically, we will define a prior distribution over $\boldsymbol{\beta}$, denoted $p(\boldsymbol{\beta})$. For simplicity, let us assume that all parameters are independently and normally distributed with each parameter's prior mean being zero with a large variance of 10 (because we are unsure apriori, what the parameters are). That is, let

$$p(\boldsymbol{\beta}) := \prod_{j=1}^J N(\beta_j; 0, 10)$$

Then, our complete data likelihood is given by

$$p(y_1, \dots, y_n, \boldsymbol{\beta} \mid \boldsymbol{x}_1, \dots, \boldsymbol{x}_n) := \prod_{j=1}^J N(\beta_j; 0, 10) \prod_{i=1}^n N(y_i; \boldsymbol{\beta}^T\boldsymbol{x}_i, \sigma^2)$$

We will treat $\sigma^2$ as a parameter to the model rather than a random variable. Our goal is to compute the posterior distribution of $\boldsymbol{\beta}$:

$$p(\boldsymbol{\beta} \mid y_1, \dots, y_n, \boldsymbol{x}_1, \dots, \boldsymbol{x}_n)$$

We can approximate this posterior using blackbox VI via the reparameterization gradient! To do so, we must first specify our approximate posterior distribution. For simplicity, we will assume that $q_\phi(\boldsymbol{\beta})$ factors into independent normal distributions (like the prior):

$$q_\phi(\boldsymbol{\beta}) := \prod_{j=1}^J N(\beta_j; \mu_j, \sigma^2_j)$$

Note the full set of variational parameters $\phi$ are the collection of mean and variance parameters for all of the normal distributions. Let us represent these means and variances as vectors:

$$\begin{align*}\boldsymbol{\mu} &:= [\mu_0, \mu_1, \dots, \mu_J] \\ \boldsymbol{\sigma}^2 &:= [\sigma^2_0, \sigma^2_1, \dots, \sigma^2_J] \end{align*}$$ 

Then the variational parameters are:

$$\phi := \{\boldsymbol{\mu}, \boldsymbol{\sigma}^2 \}$$

Now, we must derive a reparameterization of $q_\phi$. This can be done quite easily as follows:

$$\begin{align*}\boldsymbol{\epsilon} &\sim N(\boldsymbol{0}, \boldsymbol{I}) \\ \boldsymbol{\beta} &= \boldsymbol{\mu} + \boldsymbol{\epsilon} \odot \boldsymbol{\sigma} \end{align*}$$

where $\odot$ represent element-wise multiplication between two vectors.  Finally, the reparameterized ELBO for this model and variational posterior is:

$$ELBO(\boldsymbol{\beta}) := E_{\boldsymbol{\epsilon} \sim N(\boldsymbol{0}, \boldsymbol{I})}\left[\sum_{j=0}^J \log N(\mu_j + \epsilon_j \sigma_j; 0, 10) + \sum_{i=1}^n \log N(y_i; (\boldsymbol{\mu} + \boldsymbol{\epsilon} \odot \boldsymbol{\sigma})^T\boldsymbol{x}_i, \sigma^2) - \sum_{j=0}^J \log N(\mu_j + \epsilon_j \sigma_j; \mu_j, \sigma^2_j)\right]$$

Now, we can use this reparameterized ELBO to perform stochastic gradient descent! This may appear daunting, but can be done automatically with the help of automatic differentiation algorithms! 

Here is an implementation of this algorithm for univariate linear regression in Python using [PyTorch](https://pytorch.org/). For ease of understanidng, the ELBO is broken up into small chunks:

```
N_ITERS = 500
N_MONTE_CARLO = 5000
PRIOR_BETA_MEAN = [0,0]
PRIOR_STD = 100.
STD_OF_Y = 10.

q_mean = torch.tensor([0., 0.], requires_grad=True)
q_logstd = torch.ones_like(X[0], requires_grad=True)

losses = []
q_means = []
q_logstds = []
optimizer = optim.Adam([q_mean, q_logstd], lr=0.25)
for iter in range(N_ITERS):
  # Generate L monte carlo samples
  eps = torch.randn(size=(N_MONTE_CARLO, n_dims))
  
  # Construct random betas from these samples
  beta = q_mean + torch.exp(q_logstd) * eps

  # An LxN matrix storing each the mean
  # of each dot(beta_l, x_i) 
  y_means = torch.matmul(beta, X.T)

  # The distribution N(dot(beta_l, x_i), 1)
  # This is the error of the residuals
  y_dist =  torch.distributions.normal.Normal(
      y_means,
      torch.ones_like(y_means)*STD_OF_Y
  )

  # An LxN matrix of the probabilities 
  # p(y_i \mid x_i, beta_l)
  y_probs = y_dist.log_prob(
      Y.repeat(y_means.shape[0],1)
  )

  # An L-length array storing the probabilities
  # \sum_{i=1}^N p(y_i \mid x_i, beta_l)
  # for all L Monte Carlo samples
  y_prob_per_l = torch.sum(y_probs, axis=1)

  # The prior distribution of each parameter p(\beta)
  # given by N(PRIOR_BETA_MEAN, PRIOR_STD)
  prior_beta_mean = torch.zeros_like(beta[0]).repeat(y_prob_per_l.shape[0], 1) + torch.tensor(PRIOR_BETA_MEAN)
  prior_beta_std = (torch.ones_like(beta[1]) * PRIOR_STD).repeat(y_prob_per_l.shape[0],1)
  prior_beta_dist = torch.distributions.normal.Normal(
    prior_beta_mean,
    prior_beta_std
  )

  # An LxD length matrix of \log p(\beta_{l,d}), which is
  # the prior log probabilities of each parameter" 
  prior_beta_probs = prior_beta_dist.log_prob(beta)

  # An L-length array of probabilities
  # \log p(\beta_l) = \sum_{d=1}^D \log p(\beta_{l,d})
  prior_beta_per_l = X.shape[0] * torch.sum(prior_beta_probs, axis=1)

  # An L-length array of probabilities
  # \log p(\beta_l) + \sum_{i=1}^N \log p(y_i \mid \beta_l, x_i)
  y_beta_prob_per_l = y_prob_per_l + prior_beta_per_l 

  # The variational distribution over beta approximating the posterior
  # N(q_mean, q_std)
  beta_dist = torch.distributions.normal.Normal(
    q_mean, 
    torch.exp(q_logstd)
  )

  # An LxD-length matrix of the variational log probabilities of each parameter
  # \log q(beta_{l,d})
  q_beta_probs = beta_dist.log_prob(beta)

  # An L-length array of \log q(beta_l)
  q_beta_prob_per_l = torch.sum(q_beta_probs, axis=1)

  # An L-length array of the ELBO value for each Monte Carlo sample
  elbo_per_l = y_beta_prob_per_l - q_beta_prob_per_l

  # The final loss value! 
  loss = -1 * torch.mean(elbo_per_l)

  optimizer.zero_grad()
  loss.backward()
  optimizer.step()
```

There are a few points to note regarding the above implementation. First, instead of taking the gradient with respect to $\boldsymbol{\sigma}^2$, we will take it with respect to $\log \boldsymbol{\sigma}^2$ in order to ensure that $\sigma$ is always positive throughout the procedure. Second, we use the [Adam](https://arxiv.org/abs/1412.6980) optimizer to choose the step size rather than use a fixed step size as would be done in standard gradient ascent.
