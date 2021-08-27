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

Now the question is, what do we use for our function $$F$$? 

Here, it helps to take a step back and ask the question: what task are we trying to solve? At a high-level, one might say, "well, we want to visualize the high dimensional data!" But, of course, the problem is that you cannot! When you take high-dimensional data and squeeze it down into two dimensions, you are forced to throw away a lot of information. The amount of information you throw out is related to the [intrinsic dimensionality of the data](https://mbernste.github.io/posts/intrinsic_dimensionality/). If the intrinsic dimensionality is high, one may end of up throwing away a lot of information.  Often, I've heard, "we want to isolate the structure in the data." But what does one mean by "structure"? 

Ultimately, we really need to quantify exactly what qualities of the high dimensional data that we want preserved in our final two dimensions?  This is a very task-dependent (or hypothesis-dependent) question!  Importantly, "general purpose" dimensionality-reduction methods, such as PCA, t-SNE, and UMAP, each make very specific choices about what information it decides to keep and that which it decides to throw away. These choices may not actually align with the qualities that one actually wants to preserve in order to answer a particular question. Thus, one can be mislead if one does not understand sacrifices and trade-offs, in the form of discarded information, the method at-hand is making.

Understanding a method's loss-function is critical
-------------------

Loss-functions quantify how much some quality of the original data is preserved in the embedding

A quick synopsis of the loss-functions used by common dimensionality-reduction methods
-------------------

**Feature-selection**: Feature-selection involves keeping some of the original dimensions and throwing away the rest. This is the most simple, straightforward dimensionality reduction method as it simply entails throwing some dimensions away! Defining a loss-function for feature-selection is basically trivial, but for the sake of placing feature-selection into the same conceptual framework as other methods, let's define it. Let's say we would like to embed our data into two dimensions, $$\mathbb{R}^2$$, and we 



