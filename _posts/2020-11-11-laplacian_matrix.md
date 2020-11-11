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

$$\Delta f(\boldsymbol{x}) := \nabla \cdot \nabla f(\boldsymbol{x})$$

That is, the Laplacian of $$f$$ is the [divergence](https://en.wikipedia.org/wiki/Divergence) of $$f$$'s [gradient](https://en.wikipedia.org/wiki/Gradient).  

Okay, let's break this down. First, let's discuss the gradient. The gradient of a multivariate function $$\nabla f$$ returns a vector field where each vector at each point $$\boldsymbol{x}$$, denoted $$\nabla f(\boldsymbol{x})$$, points in the direction of $$f$$'s steepest ascent. Moreover, the magnitude of the gradient vector at point $$x$$ describes how steeply the function changes at $$\boldsymbol{x}$$.  That is, the steeper the function, the larger the gradient vector. This is depicted in the figure below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/GradientOperator.png" alt="drawing" width="500"/></center>


One important point to keep in mind is that the gradient is an operator that takes as input a multivariate function and produces a vector field. 

Now let's discuss divergence.  In contrast to the gradient, the divergence operator takes as input a vector field and produces a multivariate function.  That is, given a vector field $$\boldsymbol{v}(\boldsymbol{x})$$, the divergence $$\nabla \cdot \boldsymbol{v}(\boldsymbol{x})$$ produces a scalar field.  More specifically, the divergence at some point $$x$$ within a vector field intuitively describes how much "flow" is coming into and out of $$x$$ where the flow is described by the vectors in the vector field surrounding $$x$$.

For example, in the following figure we depict three scenarios of a point $$\boldsymbol{x}$$ within a vector field.  In the left-hand figure, there is more "flow" coming out of the point than into the point. The divergence at this point $$\boldsymbol{x}$$ is positive because flow is "diverging" away from $$\boldsymbol{x}$$.  In the center figure, there is more "flow" into $$\boldsymbol{x}$$ than going away from $$\boldsymbol{x}$$ and thus, the divergence at this point is negative.  Finally, in the right-hand figure, there is an equal amount of flow going into and out of $$\boldsymbol{x}$$ and thus, the divergence at this point is zero. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/DivergenceAtPoint.png" alt="drawing" width="500"/></center>

Finally, we come back to the Laplacian.  Given a continuous, multivariate function $$f$$, the Laplacian is now simply the divergence of $$f$$'s gradient.  This is depicted in the figure below:

In the figure below, we have a 2-variate function $$f$$ (top), with its gradient vector field depicted in the bottom left.  As you can see, the vectors point in the direction where $$f$$ is increasingly most steeply at any given point.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/LaplacianExample.png" alt="drawing" width="500"/></center>

Intuitively, what does the Laplacian describe?  Well, following our understanding that $$f$$'s gradient provides vectors that point in $$f$$'s direction of steepest ascent with magnitude proportional to its steepness, we see that the "flow" at any point in this vector field will correspond to how much the gradient vectors of $$f$$ are changing. If the steepness at some point is not changing -- that is, we're at a steady incline or a steady decline -- then the divergence of the vectors in that regime will be zero.  That is, the Laplacian will be zero.  On the other hand, if at some point the gradients are shrinking or growing -- that is, because we're close to a local maximum/minimum -- then the divergence (i.e. Laplacian) will be either large or small (large if we're approaching a minimum and small if we're approaching a maximum).

Said differently, the Laplacian tells us, in some sense, how close we are to a local maximum/minimum. It's the analogue to the second derivative for a continuous, single-variate function!

We will save a rigorous definition for the gradient, divergence, and laplacian for another blog post. In the meantime, this high-level intuition will hopefully be sufficient for understanding the core ideas behind the graph Laplacian.

Constructing a Laplacian for graphs
--------------
