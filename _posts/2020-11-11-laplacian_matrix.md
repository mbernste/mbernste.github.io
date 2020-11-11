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

At the heart of of a number of important machine learning algorithms, such as [spectral clustering](https://en.wikipedia.org/wiki/Spectral_clustering), lies a matrix called the graph Laplacian.  In fact, the first step in spectral clustering is to compute the Laplacian matrix of the data's k-nearest neighbors graph (to be discussed in some future blog post).  The Laplacian matrix is defined as follows: Given a graph's adjacency matrix $$A$$, where 

$$A_{i,j} := \begin{cases} 1,& \text{if there is an edge between} \ i \ \text{and} \ j \\ 0, & \text{otherwise}\end{cases}$$


and degree matrix $$D$$, where

$$D_{i,j} :=  \begin{cases} \text{degree}(i),& \text{if} \ i = j \\ 0, & \text{otherwise}\end{cases} $$ 

the Laplacian matrix is defined as 

$$L := D - A$$

This definition is super simple, but it describes something quite deep: it's the discrete analogue to the Laplacian operator on multivariate continuous functions.  In the remainder of this post we will demonstrate why this is.

Review of the Laplacian for continuous multivariate functions
--------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/LaplacianExample.png" alt="drawing" width="500"/></center>

