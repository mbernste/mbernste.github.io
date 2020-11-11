---
title: 'The graph Laplacian'
date: 2020-11-11
permalink: /posts/laplacian_matrix/
tags:
  - tutorial
  - spectral graph theory
  - mathematics
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

*At the heart of of a number of important machine learning algorithms, such as spectral clustering, lies a matrix called the graph Laplacian.  In this post, I'll walk through the intuition behind the graph Laplacian and describe how it represents the discrete analogue to the Laplacian operator on continuous multivariate functions.*

Introduction
--------------

In my introductory machine learning course in graduate school, I was introduced to the popular clustering algorithm called [spectral clustering](https://en.wikipedia.org/wiki/Spectral_clustering).  Spectral clustering is a nice alternative to clustering algorithms like [K-means](https://en.wikipedia.org/wiki/K-means_clustering) or [Gaussian mixture models](https://en.wikipedia.org/wiki/Mixture_model#Gaussian_mixture_model) because it is able to cluster datapoints together that form contiguous patterns rather than round/oval blobs (perhaps I'll write a later post on this algorithm).

The first step of spectral is to compute the K-nearest neighbors graph of your data points and then compute the **graph Laplacian matrix**.  Given the graph's adjacency matrix $$A$$, where 

$$A_{i,j} := \begin{cases} 1,& \text{if there is an edge between $$i$$ and $$j$$} \\ 0, & \text{otherwise}\end{cases}$$

and degree matrix $$D$$, where

$$D_{i,j} := $$ 

the Laplacian matrix is defined as 

$$L := D - A$$

Review of the Laplacian for continuous multivariate functions
--------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/LaplacianExample.png" alt="drawing" width="500"/></center>

