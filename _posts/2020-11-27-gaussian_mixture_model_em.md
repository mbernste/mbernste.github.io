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

$$\phi(\boldsymbol{x}; \boldsymbol{\mu}, \boldsymbol{\Sigma}) := \frac{1}{ (2\pi)^{\frac{n}{2}} \vert \boldsymbol{\Sigma} \vert^{\frac{1}{2}} } \exp \left[ -\frac{1}{2} (\boldsymbol{x} - \boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x} - \boldsymbol{\mu})  \right] $$

Here's an example density function for a two-dimensional GMM with three Gaussians (i.e. $$K = 3$$):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GMM_example_density.png" alt="drawing" width="600"/></center>

Notice that the distribution has three modes corresponding to the means of the three Gaussians.  Furthermore, the height of the $$k$$th mode is a function of both $$\alpha_k$$ as well as how "spread" out the Guassian is, which is determined by the the covariance matrix $$\boldsymbol{\Sigma}_k$$.

GMM's generate datapoints that form clusters.  That is, if we are given a GMM and we generate a set of i.i.d. samples, $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n$$ from the GMM, these datapoints will cluster around the $$K$$ means of the $$K$$ Guassian distributions. Moreover, the number of points we sample from each Gaussian will be proportional to the $$\alpha_1, \dots, \alpha_k$$ probabilities. 

A model for data clustering
--------------

Let's say we are presented with some dataset $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \in \mathbb{R}^n$$ and our goal is find [clusters](https://en.wikipedia.org/wiki/Cluster_analysis) such that points within a cluster are more similar to eachother than points in other clusters.  GMM's provide one framework for clustering data.

To cluster the data, we make a very strong assumption: that our datapoints were samples from a GMM with $$K$$ Gaussians ($$K$$ is the number of clusters we assume describe the data). Unfortunately, we don't know the GMM's parameters (i.e., each Gaussian's mean and covariance) nor do we know which Guassian generated each data point (i.e. the $$Z_1, \dots, Z_n$$ random variables). 

This situation is depicted in the figure below. On the left-hand side, we have a hypothetical situation in which we have a known GMM and samples  $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$ from that model. Note, that we also know which Guassian generated each data point -- that is, we know the values $$z_1, \dots, z_n$$ (these are the colors of each datapoint).  In the right-hand figure, we are only given $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$.  We do not the model's parameters $$\Theta$$ nor do we know $$z_1, \dots, z_n$$.  Said differently, $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$ constitutes the *observed data* and $$z_1, \dots, z_n$$ constitutes the *latent data*.  

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/gmm_example_data.png" alt="drawing" width="700"/></center>

In order to perform clustering on $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$, we can perform the following steps. First, we need to estimate the values for $$\Theta$$. This estimation task will be the subject of much of this blog post, but for now, let's say we have an estimate which we will denote as 

$$\hat{\Theta} := \{ \hat{\boldsymbol{\mu}_1}, \hat{\boldsymbol{\Sigma}_1}, \dots, \hat{\boldsymbol{\mu}_K}, \hat{\boldsymbol{\Sigma}_K}, \hat{\alpha_1}, \dots, \hat{\alpha_K} \}$$

Given this estimate, we can assign $$\boldsymbol{x}_i$$ to the Gaussain (i.e., cluster) that was most likely to generate $$\boldsymbol{x}_i$$:

$$\text{arg max}_{k \in \{1, \dots, K \}} P(Z_i = k \mid \boldsymbol{x}_i ; \hat{\Theta})$$

Using Bayes' rule, we have 

$$\begin{align*} P(Z_i = k \mid \boldsymbol{x}_i ; \hat{\Theta}) &= \frac{p(\boldsymbol{x}_i \mid Z_i = k ; \Theta)P(Z_i = k)}{\sum_{h=1}^K p(\boldsymbol{x}_i \mid Z_i = h ; \Theta)P(Z_i = h)} \\ &= \frac{\phi(\boldsymbol{x}_i \mid \hat{\boldsymbol{\mu}_k}, \hat{\boldsymbol{\Sigma}_k}) \alpha_k}{\sum_{h=1}^K \phi(\boldsymbol{x}_i \mid \hat{\boldsymbol{\mu}_h}, \hat{\boldsymbol{\Sigma}_h}) \alpha_h} \end{align*}$$

This is depicted in the figure below. In the left-hand figure, we depict our estimate for $$\Theta$$. In the right-hand figure, we assign each point to the Gaussian that was most likely to generate that point.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/gmm_example_clustering.png" alt="drawing" width="700"/></center>

Note that we have recovered three clusters in the data that correspond to the three Gaussians. 

Now, let's come back to the task of estimating values for $$\Theta$$.  We can approach this via the principle of maximum-likelihood:

$$\hat{\Theta} := \text{arg max}_{\Theta} \prod_{i=1}^n p(\boldsymbol{x}_i ; \Theta)$$

How do we solve this optimization problem? It turns out that the EM algorithm provides a very straightforward approach!

Maximum-likelihood estimation for GMM's via expectation-maximization
--------------

The EM algorithm is a natural choice for performing maximum likelihood estimation for a GMM's parameters because the algorithm is quite simple to implement.  First, let's state the algorithm and then we will derive it.

**E-Step**

On the E-step, we must formulate the Q-function. Let $$t$$ be a given iteration of the algorithm. The $$t$$th Q-function is 

$$Q_t(\Theta) := \sum_{i=1}^n \sum_{k=1}^K \gamma_{t,i,k} \log \left[ \alpha_k \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k) \right]$$

where 

$$\gamma_{t,i,k} := \frac{\alpha_{t,k} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,k}, \boldsymbol{\Sigma}_{t,k})}{\sum_{h=1}^K \alpha_{t,h} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,h}, \boldsymbol{\Sigma}_{t,h})}$$

and $$\alpha_{t,k}$$, $$\boldsymbol{\mu}_{t,k}$$, and $$\boldsymbol{\Sigma}_{t,k}$$ are the $$t$$th estimates of $$\alpha_k$$, $$\boldsymbol{\mu}_{k}$$, and $$\boldsymbol{\Sigma}_{k}$$ respectively.

We note that the computation that must be done on this step is computing the $$\gamma_{t,i,l}$$ variables. As will be showin in the derivation, these variables represent the probability that each data point were sample from each Gaussian as estimated using the set of parameters $$\Theta_t$$. That is, $$\gamma_{t,i,l}$$ represents the probability that data point $$i$$ was generated by the $$k$$th Gaussian as estimated at the $$t$$th step of the algorithm.

**M-Step**

On the M-step, we find $$\Theta$$ that maximizes $$Q_t(\Theta)$$. That is, we must compute the following:

$$\Theta_{t+1} := \text{arg max}_{\Theta} \ Q_t(\Theta)$$

The solution to this optimization problem is given by 

$$\begina{align*}\forall k, \alpha_{t+1, k} &:= \\  \forall k, \alpha_{t+1, k, i} &:= \\ \forall k, \Sigma_{t+1, i, k} &:=\end{align*}$$

**Derivation of the E-step**

**Derivation of the M-step**
