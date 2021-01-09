---
title: 'A primer on RNA-seq and what it provides'
date: 2021-01-07
permalink: /posts/rnaseq_tpm_vs_median_ratio/
tags:
  - tutorial
  - bioinformatics
  - RNA-seq
  - gene expression
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
---------

At a high level RNA sequencing (RNA-seq) measures the transcription of each gene in a biological sample (i.e. a group of cells or a single single).  The type of data that RNA-seq provides is relatively complex and because of this complexity, there is a good amount of confusion regarding the units of gene expression derived from RNA-seq data and the various methods used for normalizing these expression measurements across samples. In this post, I will discuss how the various normalization methods that are used in RNA-seq analysis result from the following problem: RNA-seq provides a measurement of *relative* gene expression between genes rather than *absolute* gene expression.  I believe that this discrepancy is the cause for much confusion regarding the various units of gene expression derived from RNA-seq as well as the methods for normalizing those measurements between samples.

A high-level primer on RNA-seq
-----------

Let's start with the input to an RNA-seq experiment. The input to an RNA-seq experiment is a random subset of RNA molecules (i.e., transcripts) in a biological sample. Below, we depict a set of transcripts where each transcript is colored according to the gene from which it was derived (Blue, Green, Yellow):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_input.png" alt="drawing" width="500"/></center>

In an ideal world, we would have a procedure to tell us exactly how many transcripts in our sample origiante from each gene.  That is, our procedure would tell us that we have 7 transcripts from the Blue gene, 4 transcripts from the Green gene, and 2 transcripts from the Yellow gene. These values are the **absolute expression** of each gene. Unfortunately, RNA-seq does provide such measurements.  (Note that these numbers are just a toy example. In reality, a single cell contains [hundreds of thousands](https://www.qiagen.com/us/resources/faq?id=06a192c2-e72d-42e8-9b40-3171e1eb4cb8&lang=en) of transcripts.) 

So what does RNA-seq provide? To understand what RNA-seq provides, we need to understand what RNA-seq does.  Essentially, RNA-seq repeatedly samples *locations* along any of the transcripts in the sample (these are the sequencing reads). If you sum up all of the sampled locations, then you get a **count** for each gene gene. This can be visualized as follows:

These counts are the raw numerical measurements that an RNA-seq experiment provides.  

What RNA-seq gives you versus what you want
-------------

These sampled locations do not tell us the absolute expression of each gene.











