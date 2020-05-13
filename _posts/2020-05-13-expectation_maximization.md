---
title: 'Expectation Maximization: Theory and Intuition'
date: 2020-05-11
permalink: /posts/em/
tags:
  - machine learning
  - probability
  - statistics
  - tutorial
---

**THIS POST IS CURRENTLY UNDER CONSTRUCTION**

Expectation Maximization (EM) is a popular algorithm for performing maximum-likelihood estimation for the parameters in a latent variable model. Introductory machine learning and bioinformatics courses often teach the Expectation Maximization algorithms for estimating parameters in important models such as [Guassian Mixture Models](https://en.wikipedia.org/wiki/Mixture_model#Gaussian_mixture_model) and [Hidden Markov Models](https://en.wikipedia.org/wiki/Baum–Welch_algorithm).

After learning about this algorithm in introductory graduate school courses, the intuition was clear, but I still had several remaining questions.  When is EM preferred over some other method for estimating parameters?  What is EM really doing? Why is EM guaranteed to converge?

In this blog post, I'll describe my current understanding of the theory behind the EM algorithm, which helped me to answer the aformentioned questions. I'll also offer a few perspectives for intuiting this algorithm.

The Setting
---------

As mentioned previously, EM is used for performing maximum likelihood estimation on the parameters of a latent variable model. To review this task, let's say we have two sets of random variables $X$ and $Z$ and some parameterized joint distribution over these random variables:

$$p(x, z; \theta)$$

where $p$ is the probability mass/density function, $x$ and $z$ are values for $X$ and $Z$, and $\theta$ parameterizes the distribution.

Further, we assume that we have observed $x$, the value of $X$, but have not observed $z$, the value of $Z$. Despite not observing $z$, we wish to find the value for $\theta$ that makes $x$ most likely under our model. Since we have not observed z, our likelihood function must marginalize over z:

$$l(\theta) := \log p(x ; \theta) = \log \int_z p(x, z ; \theta)$$

In practice, maximizing this function over θ may be difficult to do analytically due to this integral. For such situations, the EM algorithm may provide a method for computing a local maximum of this function with respect to θ.

Description of EM
---------

The EM algorithm alternates between two steps: an expectation-step (E-step) and a maximization-step (M-step). Throughout execution, the algorithm maintains an estimate of the parameters $\theta$ that is updated on each iteration. As the algorithm progresses, this estimate of $\theta$ converges to a local maximum of $l(\theta)$. Let $t$ denote a given step of the algorithm. On the $t$th step, we’ll denote $\theta_t$ as the $t$th estimate of $\theta$.

Each step works as follows: On the $t$th E-step, the algorithm formulates a function of $\theta$ called the Q-function, denoted $Q_t(\theta)$. Then, on the next M-step, the algorithm assigns $\theta_{t+1}$ to be the value that maximizes $Q_t(\theta)$. 

This alternation between formulating a Q-function and maximizing that Q-function are repeated until the estimate of $\theta$ converges. As we will prove later, not only is this process guaranteed to converge, but it will converge to a local maximum of $l(\theta)$.

Moe specifically, the E-Step and M-Step work as follows:

**E-Step**

Compute the conditional probability $p(z \mid x ; \theta_t)$. From this calculation, formulate the Q-function:

$$Q_t(\theta) := E_{Z\mid x, \theta_t}\left[ \log p(x, z ; \theta) \right]$$ 

$$\ \ \ \ \ \ \ \ = \int p(z \mid x ; \theta_t) \log p(x,z ; \theta) \ dz$$

The "core" of formulating an EM algorithm for a particular model is calculating $p(z \mid x ; \theta_t)$. If the model admits an easy calculation of this function, then the EM algorithm may be a good a choice!

**M-Step**

Assign $\theta_{t+1}$ to be the value that maximizes the Q-function that was formulated on the previous E-step:

$$\theta_{t+1} := \text{arg max}_\theta Q_t(\theta)$$

We repeat the E-Step and M-Step until the difference between $\theta_t$ and $\theta_{t+1}$ is small, indicating convergence. We also note that $\theta_0$ can be set to an arbitrary value -- usually set randomly.  Since EM finds a *local* maximum of $l(\theta)$, it is often wise to try many different $\theta_{0}$'s! 

EM is coordinate ascent on the evidence lower bound
-----------

Now, let's dig into what the EM algorithm is really doing.  Specifically, we will show that EM is a [coordinate ascent](https://en.wikipedia.org/wiki/Coordinate_descent) algorithm on a quantity called the [evidence lower bound](https://en.wikipedia.org/wiki/Evidence_lower_bound) (ELBO).

Coordinate ascent? ELBO? Before talking about EM, let's first dig into the these concepts:

**The evidence lower bound**

To understand the evidence lower bound, we must first understand what we mean by "evidence".  The **evidence**, quite a simply, just a name given to the likelihood function evaluated at a fixed $\theta$:

$$\text{evidence} := \log p(x ; \theta)$$

Why is this quantity often called the "evidence"? Intuitively, if we have chosen the right model $p$ and $\theta$, then we would expect that the marginal probability of our observed data $x$, would be high. Thus, a higher value of $\log p(x ; \theta)$ indicates, in some sense, that we may be on the right track with the model $p$ and parameters $\theta$ that we have chosen.

If we happen to also know (or posit) that $Z$ follows some distribution given by $q$ (and that $p(x, z; \theta) := p(x \mid z ; \theta)q(z)$), then the evidence lower bound is, well, a lower bound on the evidence that makes use of $q$.  Specifically, 

$$\log p(x ; \theta) \geq E_{Z \sim q}\left[\log \frac{p(x,Z; \theta)}{q(Z)} \right]$$

where the ELBO is simply the right-hand side of the above equation:

$${ELBO} := E_{Z \sim q}\left[\log \frac{p(x,Z; \theta)}{q(Z)} \right]$$

**Coordinate ascent**

Coordinate ascent is a relatively simple and iterative strategy for maximizing a function. Given a function $f(a, b)$ that takes two arguments $a$ and $b$, the idea of coordinate ascent is that we will iteratively fix $a$ to some value $\hat{a}$ and then choose for $b$ the value $\hat{b}$ that maximizes $f(\hat{a}, b)$ . Given $\hat{b}$, we then re-assign to $a$ the value that maximizes $f(a, \hat{b})$. This procedure is repeated until convergence.

**Coordinate ascent on the evidence lower bound**

In our setting, we don't yet know which value to use for $\theta$, nor do we know the distribution $q$ for $Z$. Thus, the ELBO becomes a function of both $\theta$ and $q$:

$${ELBO}(\theta, q) := E_{Z \sim q}\left[\log p(x,Z; \theta)\right] - E_{Z\sim q}\left[\log q(Z)\right]$$

EM is just coordinate ascent on this function. In the E-Step, we fix $\theta$ and solve for $q$. In the M-Step, we fix $q$ and solve for $\theta$. 

First, let's fix $\theta$ to $\theta_t$ (our current value for $\theta$) and solve for $q$:

$$\text{arg max}_q \text{ELBO}(q, \theta_t) = \text{arg max}_q E_{z \sim q}\left[ \log \frac{p(Z, x ; \theta)}{q(Z)} \right]$$




