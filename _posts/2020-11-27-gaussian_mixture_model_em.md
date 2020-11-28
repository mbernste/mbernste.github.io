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

Let's say we are presented with some dataset consisting of points $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n \in \mathbb{R}^n$$ and our goal is to find [clusters](https://en.wikipedia.org/wiki/Cluster_analysis) within these data points such that points within a cluster are more similar to eachother than they are to points outside their cluster.  GMM's provide a framework for finding said clusters.

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

The EM algorithm is a natural choice for performing maximum likelihood estimation for a GMM's parameters because the algorithm is quite simple to implement.  For a thorough discussion of the EM algorithm, see my [previous blog post](https://mbernste.github.io/posts/em/). 

First, we will state the algorithm and then we will derive it.

**E-Step**

On the E-step, we must formulate the Q-function. Let $$t$$ be a given iteration of the algorithm. The $$t$$th Q-function is 

$$Q_t(\Theta) := \sum_{i=1}^n \sum_{k=1}^K \gamma_{t,i,k} \log \left[ \alpha_k \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k) \right]$$

where 

$$\gamma_{t,i,k} := \frac{\alpha_{t,k} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,k}, \boldsymbol{\Sigma}_{t,k})}{\sum_{h=1}^K \alpha_{t,h} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,h}, \boldsymbol{\Sigma}_{t,h})}$$

and $$\alpha_{t,k}$$, $$\boldsymbol{\mu}_{t,k}$$, and $$\boldsymbol{\Sigma}_{t,k}$$ are the $$t$$th estimates of $$\alpha_k$$, $$\boldsymbol{\mu}_{k}$$, and $$\boldsymbol{\Sigma}_{k}$$ respectively.

We note that the computation that must be done on this step is computing the $$\gamma_{t,i,l}$$ variables. As will be showin in the derivation, these variables represent the probability that each data point was sample from each Gaussian as estimated using the set of parameters $$\Theta_t$$. That is, $$\gamma_{t,i,l}$$ represents the probability that data point $$i$$ was generated by the $$k$$th Gaussian as estimated at the $$t$$th step of the algorithm.

**M-Step**

On the M-step, we find $$\Theta$$ that maximizes $$Q_t(\Theta)$$. That is, we must compute the following:

$$\Theta_{t+1} := \text{arg max}_{\Theta} \ Q_t(\Theta)$$

The solution to this optimization problem is given by 

$$\begin{align*}\forall k, \alpha_{t+1, k} &:= \frac{1}{n} \sum_{i=1}^n \gamma_{t,i,k}\\  \forall k, \boldsymbol{\mu}_{t+1, k, i} &:= \frac{1}{\gamma_{t,i,k}} \sum_{i=1}^n \gamma_{t,i,k}\boldsymbol{x}_i \\ \forall k, \boldsymbol{\Sigma}_{t+1, i, k} &:= \frac{1}{\gamma_{t,i,k}} \sum_{i=1}^n \gamma_{t,i,k}(\boldsymbol{x}_i - \boldsymbol{\mu}_{t,i,k})(\boldsymbol{x}_i - \boldsymbol{\mu}_{t,i,k})^T \end{align*}$$

**Derivation of the E-step**

Here we derive the Q-function at the $$t$$th iteration. Let $$X := \{\boldsymbol{x}_1, \dots, \boldsymbol{x}_n\}$$ be the collection of observed data (i.e., the data points) and $$Z := \{z_1, \dots, z_n\}$$ be the collection of latent data (i.e., which Gaussian generated each data point). Recall, the Q-function is defined as

$$Q_t(\Theta) := E_{Z \mid X; \Theta_t}\left[ \log p(X, Z; \Theta) \right]$$

Deriving the Q-function entails calculating an analytical form of this expectation so that we can implement it in a computer program. For GMM's that derivation is:

$$\begin{align*} Q_t(\Theta) &:= E_{Z \mid X; \Theta_t}\left[ \log p(X, Z; \Theta) \right] \\ &= \sum_{i=1}^n E_{z_i \mid \boldsymbol{x}_i; \Theta_t} \left[ \log p(\boldsymbol{x}_i, z_i ; \Theta) \right] \\ &= \sum_{i=1}^n \sum_{k=1}^K P(z_i = k \mid \boldsymbol{x}_i ; \Theta_t) \log p(\boldsymbol{x}_i, z_i ; \Theta) \ \ \ \ \ \text{by the linearity of expectation} \\ &= \sum_{i=1}^n \sum_{k=1}^K \frac{P(\boldsymbol{x}_i \mid z_i = k ; \Theta_t)P(z_i = k ; \Theta_t)}{\sum_{h=1}^K P(\boldsymbol{x}_i \mid z_i = h ; \Theta_t)P(z_i = h ; \Theta_t)} \log p(\boldsymbol{x}_i, z_i ; \Theta) \\ &= \sum_{i=1}^n \sum_{k=1}^K \frac{\alpha_{t,k} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,k}, \boldsymbol{\Sigma}_{t,k})}{\sum_{h=1}^K \alpha_{t,h} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,h}, \boldsymbol{\Sigma}_{t,h})} \log \alpha_k \phi(\boldsymbol{x}_i ; \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k) \\ &= \sum_{i=1}^n \sum_{k=1}^K \gamma_{t, i, k} \log \alpha_k \phi(\boldsymbol{x}_i ; \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k) \end{align*}$$

where we let 

$$\gamma_{t,i,k} := \frac{\alpha_{t,k} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,k}, \boldsymbol{\Sigma}_{t,k})}{\sum_{h=1}^K \alpha_{t,h} \phi(\boldsymbol{x}_i; \boldsymbol{\mu}_{t,h}, \boldsymbol{\Sigma}_{t,h})}$$

**Derivation of the M-step**

The M-step entails finding $$\Theta_{t+1}$$ that maximizes the Q-function. Note, that the $$\alpha_1, \dots, \alpha_k$$ are the probabilities that a given point is sampled from each Guassian, thus these probabilities must sum to one. Thus, when we optimize the Q-function with respect to these parameters, we must do so under the constraint that they sum to one.  That is, we must solve

$$\Theta_{t+1} := \text{arg max}_\Theta \ Q_t(\Theta)$$

subject to 

$$\sum_{k=1}^K \alpha_k = 1$$

Because of the equality constraint, and because the objective and constraint are continuous, this optimization problem can be solved using Lagrange multipliers. First, we form the Lagrangian:

$$L(\Theta, \lambda) := \sum_{i=1}^n \sum_{k=1}^K \gamma_{t,i,k} \log \alpha_k \phi(\boldsymbol{x}_i ; \boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k) + \lambda \left( \sum_{k=1}^K \alpha_k - 1 \right)$$

We now solve for $$\Theta$$ that makes the derivative of the Lagrangian equal to zero.

Let's start with $$\alpha_1, \dots, \alpha_K$$. For some $$k$$, 

$$\frac{\partial L(\Theta, \lambda)}{\partial \alpha_k} = \frac{1}{\alpha_k} \sum_{i=1} \gamma_{t,i,k} + \lambda$$

Setting to zero and solving for $$\alpha_k$$ we have

$$\begin{align*} 0 &= \frac{1}{\alpha_k} \sum_{i=1} \gamma_{t,i,k} + \lambda \\ \implies \alpha_k &= -\frac{1}{\lambda} \sum_{i=1}^n \gamma_{t,i,k}\end{align*}$$

Plugging this into the constraint $$\sum_{k=1}^K \alpha_k = 1$$ , we can solve for $$\lambda$$,

$$\begin{align*} \sum_{k=1}^K -\frac{1}{\lambda} \sum_{i=1}^n \gamma_{t,i,k} &= 1 \\ \implies \lambda &= - \sum_{i=1}^n \sum_{k=1}^K \gamma_{t,i,k} \\ \implies \lambda &= -n \ \ \ \ \text{because } \ \sum_{k=1}^K \gamma_{t,i,k} = 1\end{align*} $$

Finally, plugging $$\lambda$$ back into the equation that sets the derivative of the Lagrangian to zero, we can solve for the final value of $$\alpha_k$$:

$$\begin{align*}0 &= \frac{1}{\alpha_k} \sum_{i=1} \gamma_{t,i,k} - n \\ \implies \alpha_k &= \frac{1}{n} \sum_{i=1} \gamma_{t,i,k} \end{align*}$$

Now, let's compute the derivative of the Lagrangian with respect to $$\boldsymbol{\mu}_k$$ for some $$k$$:

$$\begin{align*}\frac{\partial L(\Theta, \lambda)}{\partial \boldsymbol{\mu}_k} := \end{align*}$$
