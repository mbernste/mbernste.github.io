---
title: 'Dimensionality reduction is a task-dependent activity'
date: 2021-08-27
permalink: /posts/variational_inference/
tags:
  - machine learning
  - insight
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION!

Introduction
-------------

Dimensionality reduction is a common technique for visualizing high-dimensional data.  In my field, computational biology, dimensionality reduction is an extremely common (almost ubiquotous) method for visualizing single-cell genomics data.  In a single-cell genomics dataset, one is presented with a set of cells (on the order of thousands to hundreds of thousands) where each cell is associated with a high-dimensional measurement.  For example, in single-cell RNA-sequencing (scRNA-seq), one measures the relative abundance of RNA transcripts produced by each genomic features of interest (e.g., protein-coding genes), of which there exist tens of thousands. Thus, one can represent each cell as a vector $$\boldsymbol{x}_i \in \mathbb{R}^G$$ where $$G$$ is the number of genome-wide measurements.

Because these measurements are many dimensional, it is impossible to visualize the cells using a scatterplot in which each dot is a cell and each axis represents a single genomic feature, such as a gene.  The idea behind dimensionality reduction is that we will use some function $$F: \mathbb{R}^G \rightarrow \mathbb{R}^2$$ to reduce the dimensionality of each cell from, say 20,000 dimensions (the approximate number of protein coding genes in the human genome), down to two dimensions. That is, we will apply $$F$$ to a each cell, $$\boldsymbol{x}$$, and then produce a two-dimensional point that we can plot on a scatterplot:

$$(y_1, y_2) := F(\boldsymbol{x})$$

Now the question is, how do we choose our function $$F$$? Here, it helps to take a step back and ask the question: what task are we trying to solve? At a high-level, one might say, "well, we want to visualize the high dimensional data!" But, of course, the problem is that you cannot! So you will be forced to make trade-offs along various lines regarding how you decide to embed your high-dimensional datapoints in just a few dimensions.

Specifically, in my mind, there are three categories of criteria that I have seen used for choosing an $$F$$:

1. **What information is preserved.** Perhaps most obviously, one must decide what aspects of the original, high-dimensional data one wants to preserve in the low-dimensional embedding versus which aspects will be discarded or distorted.
2. **Incorporate prior knowledge.** One might have some set of prior knowledge about the high-dimensional data that you would like incorporated into the scatterplot. 
3. **Aesthetic quality**. This might seem like an unscientific criteria, but in fact, it is a motivating criteria for the t-SNE method!

In this blog post, I will discuss how these various criteria are priortized by various dimensionality reduction methods and the various pitfalls that come from over-relying on any one method. It is my opinion that dimensionality reduction methods do have value, but it is essential that one understands the mathematics and motivations behind each method. Unfortunately, knowing the intricacies of any given dimensionality reduction method can be daunting! In this way, these visualization techniques are best interpreted by specialists and should be avoided for communicating to general audiences.

Deciding what information is kept versus thrown away
----------------

Most obviously, dimensionality reduction potentially requires that we throw away a lot of information owing to the simple fact that we are compressing a lot of data down to a small amount of data. Intuitively, the amount of information that one will throw away is related to the [intrinsic dimensionality of the data](https://mbernste.github.io/posts/intrinsic_dimensionality/). If the intrinsic dimensionality is high, one may end of up throwing away more information.

So, we are forced to decide what information we want to keep. Before going further, let's just clarify what we mean by "information". In the context of this discussion, information is a tricky concept to define rigorously. There is probably some way to mathematically describe it using the concepts of information theory, but I have neither seen it nor worked it out. Nonetheless, let's give it a shot. 



Let's start with a very simple example. Let's say we only care about two dimensions in the original data. In scRNA-seq data, for example, we only care about the expression of two specific genes. Then, we might decide that want to keep ONLY the expression data for these two genes and throw away the rest. This "algorithm" for dimensionality-reduction is called [feature selection]() in the field of machine learning.

The form of the "information" that we decide to keep may be more complex than just picking out individual dimensions from the original high-dimensional space. Rather, it might entail some combination of dimensions. As an example, let's look at [principal components analysis (PCA)]().  In PCA, one does not keep an original dimension _per se_, but rather keeps a linear projection of the data onto a basis that preserves the most amount of variance. The intuition behind PCA is that if the data is changing a lot (high variance) along some direction in the ambient space, then that might indicate interesting "structure" and we want to preserve it. Here's an example illustrating how the two directions of high variance seem a bit more interesting than the two directions with less variance:   

As a final and more complex example, one might care about preserving the [topology]() of the data in the ambient space, by which one roughly means, points that are close together in the ambient space are also placed close together in the low-dimensional space. Algorithms that attempt to preserve this aspect of the high-dimensional data include [Sammon Mapping](), [t-SNE](), and [UMAP]().

Importantly, when one decides to preserve one aspect of the data in the ambient space, another is usually distorted. For example, t-SNE and UMAP are known to [distort the density of datapoints]() such that points that might be very spread apart in the ambient space tend to look more tightly packed in the embedding space, whereas this is not as big of a distortion in PCA. Here's an example of 3-dimensional points XXXXXXX. t-SNE and UMAP also (greatly) distort distances between points, especially far-away points.  On the otherhand, if datapoints cluster together in clumps, or "clusters", in the high-dimensional space, PCA tends to mash these clusters up whereas t-SNE and UMAP tend to preserve them. Here's an example of XXXXXXX.

Incorporating prior knowledge
----------------


Enforcing aesthetic critera
----------------


How and when should one use dimensionality-reduction methods for visualizing data? 
----------------



What do I mean by "information" here? Let me try to define my meaning of this word a bit more rigorously.  To define it, I will evoke the idea of a [loss functions]().  A loss function is a function that maps the output of an algorithm to a quantified measure of its "wrongness". In the dimension-reduction example, we are given a set of high dimensional vectors $$\boldsymbol{x}_1, \dots, \boldsymbol{x}_n \in \mathbb{R}^G$$ and our dimensionality reduction method will output a set of two-dimensional vectors $$\boldsymbol{y}_1, \dots, \boldsymbol{y}_n$$.  Our loss function is then a function on these two sets of vectors that quantify how "good" our low-dimensional vectors are:

$$\ell(\boldsymbol{y}_1, \dots, \boldsymbol{y}_n)$$

We can define "wrongness" any way that we want! 

one must decide what aspects of the original, high-dimensional data one wants to preserve in the low-dimensional embedding versus which aspects will be discarded or distorted.



Understanding a method's loss-function is critical
-------------------

Loss-functions quantify how much some quality of the original data is preserved in the embedding

A quick synopsis of the loss-functions used by common dimensionality-reduction methods
-------------------

**Feature-selection**: Feature-selection involves keeping some of the original dimensions and throwing away the rest. This is the most simple, straightforward dimensionality reduction method as it simply entails throwing some dimensions away! Defining a loss-function for feature-selection is basically trivial, but for the sake of placing feature-selection into the same conceptual framework as other methods, let's define it. Let's say we would like to embed our data into two dimensions, $$\mathbb{R}^2$$, and we 


Ultimately, we really need to quantify exactly what qualities of the high dimensional data that we want preserved in our final two dimensions?  This is a very task-dependent (or hypothesis-dependent) question!  Importantly, "general purpose" dimensionality-reduction methods, such as PCA, t-SNE, and UMAP, each make very specific choices about what information it decides to keep and that which it decides to throw away. These choices may not actually align with the qualities that one actually wants to preserve in order to answer a particular question. Thus, one can be mislead if one does not understand sacrifices and trade-offs, in the form of discarded information, the method at-hand is making.



