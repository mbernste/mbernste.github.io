---
title: 'Three strategies for cataloging cell types'
date: 2021-03-04
permalink: /posts/cell_types_cataloging/
tags:
  - bioinformatics
  - RNA-seq
  - single-cell
  - gene expression
  - cell type
  - knowledge representation
  - ontologies
---

In my [previous post](), I outlined a conceptual framework for defining and reasoning about "cell types". Specifically, I noted that the idea of a "cell type" can be viewed as a human-made partition on the universal cellular state space. That is, the set of all possible states a living cell can exist in and the transitions between them. This idea can be summarized in the following figure:


In this framework, the task of cataloging cell types involves identifying "useful" subsets of cell states and giving those subsets names. Then, one can create a hierarchy of cell types by simpling computing the subset relationships between those subsets of cell types.

While this framework is conceptually clean and simple, there are a number of problems with implementing it in the real world. These problems include:
1. We don't know the full cellular state space
2. We don't have a language for describing subsets of that state space
3. We don't have a way of agreeing on how to partition the state space

Problems 1 and 2 are hard, and I'll save a discussion on these problems for later. In this post I will only discuss Problem 3: how do we agree on partitions of the state space. Said much more simply: how do we agree on a definition for a cell type.

In my opinion there are three core strategies that have been proposed by the scientific community; however, these ideas have taken different forms. In this post, I will attempt to tease out and more rigorously describe each of these strategies. 

These strategies are:
1. **Each scientist on their own!** Come up with your own cell type definition based on your own needs. In fact, this idea is central to a number of single-cell RNA-seq cell type classifiers such as [Garnett](). Garnett features a "zoo" of cell type classifiers that one can create and then use to label a new dataset.
2. **Crowd-sourcing.** In this strategy, one may look at all of the published genomics data out there in public repositories and use these to describe a consensus of how the scientific community uses cell type terms. This is the core idea behind [CellO](), a cell type classification tool that I worked on that uses the collection of publicly available primary cell data to train cell type classifiers.
3. **A central authority.** This is the idea behind the Human Cell Atlas. The idea here is that a single group, or committee, will collect tons of data and attempt to define the various cell types. These cell types will then serve as a reference for all of science.

Let me dig a bit into each of these strategies.

Each scientist on their own
----------------------

This is more or less the current state of affairs. 
