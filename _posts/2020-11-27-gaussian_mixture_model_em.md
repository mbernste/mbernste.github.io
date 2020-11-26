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

Introduction
--------------

Gaussian mixture model's are a very popular method for data clustering. They are also models where the expectation-maximization (EM) algorithm provides an excellent strategy for performing maximum likelihood.  In this post, I will define the Gaussian mixture model and also derive the EM algorithm for performing maximum likelihood estimation of its paramters. This blog post is designed to be a followup to my [previous post](https://mbernste.github.io/posts/em/), where I discussed the theory and intuition behind the EM algorithm. 

Gaussian Mixture Models
--------------

The Gaussian mixture model (GMM) is a family of distributions over real-valued vectors in $$\mathbb{R}^n$$. The GMM is defined as follows: First, a we assume that there exist $$K$$ Gaussian distributions.  Then, in order to generate a sample $$\boldsymbol{x} \in \mathbb{R}^n$$, we first select one of these $$K$$ Guassians according to a Categorical distribution:

$$z \sim \text{Cat}(\alpha_1, \dots, \alpha_K)$$

where $$z \in \{1, 2, \dots, K\}$$ tells us which Gaussian to pick (i.e., if $$z = 2$$, then we choose the 2nd Gaussian) and $$\alpha_k$$ is the probability of choosing the $$k$$th Gaussian. Then, we sample $$\boldsymbol{x}$$ from that $$z$$th Gaussian.  That is,

$$\boldsymbol{x} \sim $$\phi_k := N(\boldsymbol{\mu}_k, \boldsymbol{\Epsilon}_k)$$$$

where $$\boldsymbol{\mu}_k$$ is the $$k$$th Gaussian's mean, and $$\boldsymbol{\Epsilon}_k$$ is its covariance matrix.

This model is depicted by the following graphical model:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GMM_graphical_model.png" alt="drawing" width="200"/></center>

Note, that each of the $$K$$ Gaussian distributions has a separate set of parameters (i.e., a mean vector and a covariance matrix).  Furthermore, the probabilities of picking the Guassians $$alpha_1, \dots, alpha_k$$ are also parameters to the model.  We will denote this full set of model parameters as

$$\Theta = \{\boldsymbol{\mu}_1, \boldsymbol{\Epsilon}_1, \dots, \boldsymbol{\mu}_K, \boldsymbol{\Epsilon}_K, \alpha_1, \dots, \alpha_K \}$$


A model for data clustering
--------------

GMM's are most often used for data clustering.  The premise is as follows: 

