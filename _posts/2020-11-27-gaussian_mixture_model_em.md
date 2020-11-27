---
title: 'Gaussian mixture models'
date: 2020-11-24
permalink: /posts/gmm_em/
tags:
  - tutorial
  - machine learning
  - statistics
  - probability
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

*Gaussian mixture model's are a very popular method for data clustering. In this post, I will define the Gaussian mixture model and also derive the EM algorithm for performing maximum likelihood estimation of its paramters.*

Introduction
--------------

Gaussian mixture model's are a very popular method for data clustering. In this post, I will define the Gaussian mixture model and also derive the EM algorithm for performing maximum likelihood estimation of its paramters. Aside from being useful models in and of themselves, they also provide a great demonstration of when the expectation-maximization (EM) algorithm is a suitable strategy for performing maximum likelihood.  Thus, this blog post is a good a followup to my [previous post](https://mbernste.github.io/posts/em/) where I discussed the theory and intuition behind the EM algorithm. 

Definition
--------------

The Gaussian mixture model (GMM) is a family of distributions over real-valued vectors in $$\mathbb{R}^n$$. The GMM is defined as follows: First, a we assume that there exist $$K$$ Gaussian distributions.  Then, in order to generate a sample $$\boldsymbol{x} \in \mathbb{R}^n$$, we first select one of these $$K$$ Guassians according to a Categorical distribution:

$$Z \sim \text{Cat}(\alpha_1, \dots, \alpha_K)$$

where $$Z \in \{1, 2, \dots, K\}$$ tells us which Gaussian to pick (i.e., if $$Z = 2$$, then we choose the 2nd Gaussian) and $$\alpha_k$$ is the probability of choosing the $$k$$th Gaussian. Then, we sample $$\boldsymbol{X}$$ from that $$z$$th Gaussian.  That is,

$$\boldsymbol{X} \sim N(\boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k)$$

where $$\boldsymbol{\mu}_k$$ is the $$k$$th Gaussian's mean, and $$\boldsymbol{\Sigma}_k$$ is its covariance matrix.

This model is depicted by the following graphical model:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GMM_graphical_model.png" alt="drawing" width="200"/></center>

Note, that each of the $$K$$ Gaussian distributions has a separate set of parameters (i.e., a mean vector and a covariance matrix).  Furthermore, the probabilities of picking the Guassians $$\alpha_1, \dots, \alpha_k$$ are also parameters to the model.  We will denote this full set of model parameters as

$$\Theta = \{ \boldsymbol{\mu}_1, \boldsymbol{\Sigma}_1, \dots, \boldsymbol{\mu}_K, \boldsymbol{\Sigma}_K, \alpha_1, \dots, \alpha_K \}$$

As we will see in the next section of this blog post, $$\boldsymbol{X}$$ is usually the primary random variable of interest rather than $$Z$$. Thus, we will be interested in the marginal distribution of $$\boldsymbol{X}$$ whose density function is given by

$$\begin{align*}p(\boldsymbol{x}; \Theta) &:= \sum_{k=1}^K P(Z=k ; \Theta)p(\boldsymbol{x} \mid Z=k; \Theta) \\ &= \sum_{k=1}^K \alpha_k \phi(\boldsymbol{x}; \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k)\end{align*}$$

where $$\phi$$ is the probability density function of the [multivariate Guassian distribution](https://en.wikipedia.org/wiki/Multivariate_normal_distribution):

$$\phi(\boldsymbol{x}; \boldsymbol{\mu}, \boldsymbol{\Sigma}) := \frac{1}{ (2\pi)^{\frac{n}{2}} \vert \boldsymbol{\Sigma} \vert^{\frac{1}{2}} }$$

$$\left[ \exp -\frac{1}{2}(\boldsymbol{x} - \boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x} - \boldsymbol{\mu})} \right] $$

Here's an example density function for a two-dimensional GMM with three Gaussians (i.e. $$K = 3$$):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GMM_example_density.png" alt="drawing" width="600"/></center>

Notice that the distribution has three modes corresponding to the means of the three Gaussians.  Furthermore, the height of the $$k$$th mode is a function of both $$\alpha_k$$ as well as how "spread" out the Guassian is, which is determined by the the covariance matrix $$\boldsymbol{\Sigma}_k$$.

A model for data clustering
--------------

GMM's generate datapoints that form clusters.  That is, if we are given a GMM and we generate a set of i.i.d. samples, $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n$$ from the GMM, these datapoints will cluster around the $$K$$ means of the $$K$$ Guassian distributions. Moreover, the number of points we sample from each Gaussian will be proportional to the $$\alpha_1, \dots, \alpha_k$$ probabilities. 

Now let's flip this situation around. Instead of generating points from a known GMM, let's say we are presented with some dataset $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \in \mathbb{R}^n$$ and we assume that a GMM generated these points, but we don't know the GMM's parameters. Our clustering task then is to infer the unknown parameters of the GMM in order to figure out which Guassian generated which datapoint.

This situation is depicted in the figure below. On the left-hand side, we have a hypothetical situation in which we have a known GMM and samples  $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$ from that model. Note, that we also know which Guassian generated each data point -- that is, we know the values $$z_1, \dots, z_n$$ (these are the colors of each datapoint).  In the right-hand figure, we are only given $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$.  We do not the model's parameters $$\Theta$$ nor do we know $$z_1, \dots, z_n$$.  Said differently, $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$ constitutes the *observed data* and $$z_1, \dots, z_n$$ constitutes the *latent data*.  

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GMM_example_data.png" alt="drawing" width="700"/></center>

In order to perform clustering on $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$, we can perform the following steps. First, we need to estimate the values for $$\Theta$$. Once we have our estimate, 

$$\hat{\Theta} := \{ \hat{\boldsymbol{\mu}_1}, \hat{\boldsymbol{\Sigma}_1}, \dots, \hat{\boldsymbol{\mu}_K}, \hat{\boldsymbol{\Sigma}_K}, \hat{\alpha_1}, \dots, \hat{\alpha_K} \}$$

then we can assign $$\boldsymbol{x}_i$$ to the Gaussain (i.e., cluster) that was most likely to generate $$\boldsymbol{x}_i$$:

$$\text{arg max}_{k \in \{1, \dots, K \}} P(Z_i = k \mid \boldsymbol{x}_i ; \hat{\Theta})$$

where

$$\begin{align*} P(Z_i = k \mid \boldsymbol{x}_i ; \hat{\Theta}) &= p(boldsymbol{x}_i \mid Z_i = k ; \Theta)P(Z_i = k) \\ &= \phi(\boldsymbol{x}_i \mid \hat{\boldsymbol{\mu}_k}, \hat{\boldsymbol{\Sigma}_k}) \alpha_k\end{align*}$$

This is depicted in the figure below. In the left-hand figure, we depict our estimate for $$\Theta$$. In the right-hand figure, we assign each point to the Gaussian that was most likely to generate that point.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GMM_example_clustering.png" alt="drawing" width="700"/></center>

So our task is to infer the values for $$\Theta$$.  We can approach this via the principle of maximum-likelihood:

$$\hat{\Theta} := \text{arg max}_{\Theta} \prod_{i=1}^n p(\boldsymbol{x}_i ; \Theta)$$

And how do we optimize this function? We can do it easily with the EM algorithm!

Maximum-likelihood estimation for GMM's via expectation-maximization
--------------

