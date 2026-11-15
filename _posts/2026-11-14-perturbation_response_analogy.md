---
title: "An analogy between cell perturbation response prediction and computer vision"
date: 2026-11-14
permalink: /posts/perturbation_response_image_analysis/
tags:
  - ai
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

## Introduction

The dream of creating an _in silico_ model capable of predicting how a biological cell will respond to a provided stimulus is not new. The idea to predict cell behavior with mathematics and computation goes back [at least to the 1950's](https://pmc.ncbi.nlm.nih.gov/articles/PMC1392413/) and has continued to exist as a grand ambition in the field of computational biology. As our understanding of molecular biology grew through the decades, and as we learned more about the many thousands of species of molecules that play a role in the molecular biology of the cell, many dreamed of and devised early computational models that sought to simulate the cell at the level of individual molecules (e.g., [E-Cell](https://doi.org/10.1093/bioinformatics/15.1.72) and XXXXXXXX). However, despite our ability to measure cells with ever-increasing resolution, and despite the _drastic_ increases in the amount of data we could generate (and have generated!), this ability to generate data has so far exceeded our ability to _model_ it. 

However, within the last several years, the field of machine learning matured and brought with it powerful artificial intelligence. Indeed the promise of this technology has grown too large to contain and we cannot help but to dream that perhaps _it_ holds the key to true predictive biology. Perhaps, instead of simulating each molecule within the cell, we instead teach a powerful machine learning algorithm how cells respond to stimuli by simply showing it enough examples. Indeed, this vision is gaining considerable momentum, with substantial investment from both industry and philanthropy. A number of companies been formed with this vision, including my own, [Cellular Intelligence](https://www.cellularintelligence.com). Recently, Department of Energy, Google, and Meta have also [promised $1.8 billion](https://biohub.org/news/virtual-biology-initiative-expansion/) towards [BioHub](https://biohub.org)'s effort to use AI to train a virtual cell!

For those working in this space, such as myself, I feel a tension between great optimism but with a healthy dose of scientific humility. On the one hand, many of the pieces seem to be in place: we have powerful learning algorithms, access to enormous computational resources, and the ability to generate high-throughput molecular measurements of perturbed cells. On the other hand, biology is dizzyingly complex, and there is still much we don't understand about what it will take to build truly predictive models of cellular behavior.

Adding to the challenge of this endeavor, the bimolecular measurements on which these models are being trained, predominantly gene expression data are inherently difficult to visualize, intuit, and reason over. In a transcriptomics assay, such as RNA-seq, one obtains a measure of how much each gene, across the genome is expressed. The human genome comprises ~20k protein-coding genes, and thus, these measurement vectors are on the order of 20k dimensions long.


Please note, the opinions expressed in this article are my own and not reflective of those held by my employer.


