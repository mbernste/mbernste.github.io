---
title: "An analogy between cell perturbation response prediction and computer vision"
date: 2026-11-14
permalink: /posts/perturbation_response_image_analysis/
tags:
  - ai
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

## Introduction

The dream of creating an _in silico_ model capable of predicting how a biological cell will respond to a provided stimulus is not new. The idea to predict cell behavior with mathematics and computation goes back [at least to the 1950's](https://pmc.ncbi.nlm.nih.gov/articles/PMC1392413/) and has continued to exist as a grand ambition in the field of computational biology. As our understanding of molecular biology grew through the decades, and as we learned more about the many thousands of species of molecules that play a role in the molecular biology of the cell, many dreamed of and devised early computational models that sought to simulate the cell at the level of individual molecules (e.g., [E-Cell](https://doi.org/10.1093/bioinformatics/15.1.72) and XXXXXXXX). However, despite our ability to measure cells with ever-increasing resolution, and despite the _drastic_ increases in the amount of data we could generate (and have generated), our ability to generate data has so far exceeded our ability to _model_ it. 

However, within the last several years, the field of machine learning matured and the promise of this technology has grown so large that we cannot help but to pursue the possibility that perhaps _it_ holds the key to true predictive biology. Perhaps, instead of simulating each molecule within the cell, we instead teach a powerful machine learning algorithm how cells respond to stimuli by simply showing it enough training examples. Indeed, this vision is gaining considerable momentum with substantial investment from both industry and philanthropy. A number of companies been formed with this vision, including my own, [Cellular Intelligence](https://www.cellularintelligence.com), and recently, the Department of Energy, Google, and Meta have [invested $1.8 billion](https://biohub.org/news/virtual-biology-initiative-expansion/) towards the goal of training virtual cell models with AI.

A common, general formulation the virtual cell modeling task is that, given a high-dimensional bimolecular measurement, most commonly a gene expression vector, $x$, and a perturbation, $p$, we seek to predict how that measurement will change in response to the perturbation. That is, to predict $x'$, the resultant gene expression profile after $p$ is applied:




For those working in this space, such as myself, I feel great optimism towards this goal, but it is coupled with a healthy dose of scientific humility. On the one hand, many of the pieces seem to be in place: we have powerful learning algorithms, access to enormous computational resources, and the ability to generate high-throughput molecular measurements of perturbed cells. On the other hand, biology is dizzyingly complex, and there is debate in the field around exactly how much data will be required, what modalities will be required, and what variables must be accounted for in order to train accurate, and useful predictive models of how cells respond to perturbations. 

In this blog post, I will present an analogy of the perturbation modeling task that I feel captures, to some loose degree, the challenge that we face with this task and that I think may even hold some clue on to how to approach it (at least, at a high, strategic level). **This analogy frames the cell perturbation modeling task not as predicting the transcriptome of a cell that has been perturbed, but instead, as the task of predicting how the image of a backyard (yes, a backyard behind a house!) would change if you "perturbed" the scene with some kind of action (like throwing a frisbee into the yard).** I will drawn an analogy not only between this task and the cell perturbation modeling task, but also an analogy between various aspects of this task including the challenges of batch effects between samples, the context-specificity of cellular response to perturbation, and the challenges in reproducing perturbations between experiments. Through this analogy, I will seek to argue for a high-level mindset shift in the field towards our approach to this task.

Please note, the opinions expressed in this article are my own and not reflective of those held by my employer.


