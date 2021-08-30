

Introduction
------------

What is "structure"? What is the task that we are trying to solve?

In this post, I am going to take a stab at more rigorously defining what one means by the phrase "preserve structure" in the data.

Let's say we have some high-dimensional data points, $$\boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_n$$. We then define some positive similarity function $$K_{\text{ambient}}$$ that operates on these points. Let us then define another function $$K_{\text{embed}}$$ that operates on points in the embedding space.

We then attempt to find an embedding that yields an isomorphism between $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$$ and $$\boldsymbol{y}_1, \dots, \boldsymbol{y}_n$$ where the pairwise similarities between points in the ambient space are defined by $$K_{\text{ambient}}$$ and the pairwise similarities between points in the embedding space are defined by $$K_{\text{embed}}$$.

This is all very abstract, so let me try to define all of these concepts. 

Isomorphisms
------------

Examples using common dimensionality reduction methods
----------------

