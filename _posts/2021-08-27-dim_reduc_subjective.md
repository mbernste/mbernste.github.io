---
title: 'Dimensionality reduction is a task-dependent activity'
date: 2021-08-27
permalink: /posts/variational_inference/
tags:
  - machine learning
  - insight
---

Introduction
-------------

Dimensionality reduction is a common technique for visualizing high-dimensional data.  In my field, computational biology, dimensionality reduction is an extremely common (almost ubiquotous) method for visualizing single-cell genomics data. As a quick review, in a single-cell genomics dataset, one is presented with a set of cells (on the order of thousands to hundreds of thousands) where each cell is associated with a high-dimensional measurement.  For example, in single-cell RNA-sequencing (scRNA-seq), one measures the relative abundance of RNA transcripts produced by each genomic features of interest (e.g., protein-coding genes), of which there exist tens of thousands. Thus, one can represent each cell as a vector $$\boldsymbol{x}_i \in \mathbb{R}^G$$ where $$G$$ is the number of genome-wide measurements.

Because these measurements are so high-dimensional it is impossible to visualize the cells using a scatterplot in which each dot is a cell and each axis represents a single genomic feature, such as a gene.  The idea behind dimensionality reduction is to use some function $$F: \mathbb{R}^G \rightarrow \mathbb{R}^2$$ to reduce the dimensionality of each cell into two dimensions. That is, apply $$F$$ to a given cell $$\boldsymbol{x}$$, one produces a two-dimensional point

$$(y_1, y_2) := F(\boldsymbol{x})$$

that one can then plot on a scatterplot.

The big problem is, how does one choose a function $$F$$? What does one even look for in such a function? 

Here, it helps to take a step back and ask the question: what task are we trying to solve? At a high-level, one might say, "well, we want to visualize the high dimensional data!" But, of course, the problem is that you cannot! When you take high-dimensional data and squeeze it down into two dimensions, you are forced to throw away a lot of information. The amount of information you throw out is related to the [intrinsic dimensionality of the data](https://mbernste.github.io/posts/intrinsic_dimensionality/). If there intrinsic dimensionality is high, one may end of up throwing away a lot of information in the data.

So we must therefore ask ourselves, what qualities of the high dimensional data do we want preserved in our final two dimensions?  This is a very task-dependent (or hypothesis-dependent) question! It depends on what question we have that we think a visual instrument will help us answer.  Importantly, "general purpose" dimensionality-reduction methods, such as PCA, t-SNE, and UMAP, each make very specific choices about what information it decides to keep and that which it decides to throw away. These choices may not actually align with the qualities that one actually wants to preserve in order to answer a particular question about the data. Thus, one can be mislead if one does not understand sacrifices and trade-offs, in the form of discarded information, the method at-hand is making.

Loss-functions encode how much a given characteristic in the original data is preserved
-------------------





