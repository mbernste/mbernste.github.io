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

At the heart of the field of [spectral graph theory](https://en.wikipedia.org/wiki/Spectral_graph_theory) as well as a number of important machine learning algorithms, such as [spectral clustering](https://en.wikipedia.org/wiki/Spectral_clustering), lies a matrix called the **graph Laplacian**.  (In fact, the first step in spectral clustering is to compute the Laplacian matrix of the data's k-nearest neighbors graph... perhaps to be discussed in some future blog post.)  

The Laplacian matrix is defined as follows: Given a graph $$G := (V, E)$$ where $$V$$ is the set of nodes/vertices and $$E$$ is the set of edges, with an adjacency matrix $$A \in \{0,1\}^{\vert V \vert}$$, where 

$$A_{i,j} := \begin{cases} 1,& \text{if there is an edge between} \ i \ \text{and} \ j \\ 0, & \text{otherwise}\end{cases}$$

and degree matrix $$D \in \mathbb{Z}^{\vert V \vert}$$, where

$$D_{i,j} :=  \begin{cases} \text{degree}(i),& \text{if} \ i = j \\ 0, & \text{otherwise}\end{cases} $$ 

the Laplacian matrix is defined as 

$$L := D - A$$

This definition is super simple, but it describes something quite deep: it's the discrete analogue to the Laplacian operator on multivariate continuous functions.  How does such a simple definition capture such a complex idea?  We will demonstrate this in the remainder of this post.

Review of the Laplacian for continuous, multivariate functions
--------------

First, let's review the basics behind the Laplacian for continuous, multivariate functions. Given a multivariate function 

$$f: \mathbb{R}^n \rightarrow \mathbb{R}$$

the Laplacian of $$f$$ is defined as

$$\Delta f(\boldsymbol{x}) := \text{\nabla} \cdot \nabla f(\boldsymbol{x})$$

That is, the Laplacian of $$f$$ is the [divergence](https://en.wikipedia.org/wiki/Divergence) of $$f$$'s [gradient](https://en.wikipedia.org/wiki/Gradient).  

Okay, let's break this down. First, let's discuss the gradient. The gradient of a multivariate function $$\nabla f$$ returns a vector field where each vector at each point $$\bold{x}$$, denoted $$\nabla f(\bold{x})$$, points in the direction of $$f$$'s steepest ascent. Moreover, the magnitude of the gradient vector at point $$x$$ describes how steeply the function changes at $$x$$.  That is, the steeper the function, the larger the gradient vector. This is depicted in the figure below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GradientOperator.png" alt="drawing" width="500"/></center>


One important point to keep in mind is that the gradient is an operator that takes as input a multivariate function and produces a vector field. 

Now let's discuss divergence.  In contrast to the gradient, the divergence operator takes as input a vector field and produces a multivariate function.  More specifically, the divergence at some point $$x$$ within a vector field intuitively describes how much "flow" is coming into and out of $$x$$ where the flow is described by the vectors in the vector field surrounding $$x$$.

For example, in the following figure we three scenarios of a point $$x$$ within a vector field.  In the left-hand figure, intuitively you can see that there is more "flow" coming out of the point than into the point. The divergence at this point $$x$$ is positive because flow is "diverging" away from $$x$$.  In the center figure, there is more "flow" into $$x$$ than going away from $$x$$ and thus, the divergence at this point is negative.  Finally, in the right-hand figure, there is an equal amount of flow going into and out of $$x$$ and thus, the divergence at this point is zero. 

In the figure below, we have a 2-variate function $$f$$ (top), with its gradient vector field depicted in the bottom left.  As you can see, the vectors point in the direction where $$f$$ is increasingly most steeply at any given point.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/LaplacianExample.png" alt="drawing" width="500"/></center>


