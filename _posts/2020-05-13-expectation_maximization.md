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

$\begin{align*}Q_t(\theta) &:= E_{Z\mid x, \theta_t}\left[ \log p(x, z ; \theta) \right] \\ &= \int p(z \mid x ; \theta_t) \log p(x,z ; \theta) dz\end{align*}$

