---
title: 'Gaussian Mixture Models'
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

Gaussian mixture model's are a very popular method for data clustering. Furthermore, they also provide an example of where the expectation-maximization algorithm provides an excellent strategy for performing maximum likelihood.  In this post, I will define the GMM and also derive the EM algorithm for performing maximum likelihood estimation of its paramters. This blog post is designed to be a followup to my [previous post](), where I discussed the theory and intuition behind the EM algorithm. 

Gaussian Mixture Models
--------------

The Gaussian mixture model (GMM) is a family of distributions over real-valued vectors in $$\mathbb{R}^n$$. The GMM is defined as follows: First, a we assume that there exist $$K$$ Gaussian distributions, which we will denote as $$\phi_1, \dots, \phi_K$$.  Then, in order to generate a sample $$\bold{x} \in \mathbb{R}^n$$, we first select one of these $$K$$ Guassians according to a Categorical distribution:

$$z \sim \text{Cat}(\alpha_1, \dots, \alpha_K)$$

where $$z \in \{1, 2, \dots, K}$$ tells us which Gaussian to pick (i.e., if $$z = 2$$, then we choose the 2nd Gaussian) and $$\alpha_k$$ is the probability of choosing the $$k$$th Gaussian. Then, we sample $$\boldsymbol{x}$$ from that $$z$$th Gaussian.  That is,

$$\boldsymbol{x} \sim \phi_z$$

This model is depicted by the following graphical model:

Note, that each of the $$K$$ Gaussian distributions, $$\phi_k$$, has it's own set of parameters: $$\boldsymbol{\mu}_k$$, its mean, and $$\boldsymbol{\Epsilon}_k$$, its covariance matrix.  Furthermore, the probabilities of picking the Guassians $$alpha_1, \dots, alpha_k$$ are also parameters to the model.  Thus, the full set of parameters of the GMM are each Guassian's mean, each Guassian's covariance matrix, and the probabilities of picking each Gaussian. We will denote this set of parameters as

$$\Theta = \{\boldsymbol{\mu}_1, \boldsymbol{\Epsilon}_1, \dots, \boldsymbol{\mu}_K, \boldsymbol{\Epsilon}_K, \alpha_1, \dots, \alpha_K \}$$



A model for data clustering
--------------

GMM's are most often used for data clustering.  The premise is as follows: 

