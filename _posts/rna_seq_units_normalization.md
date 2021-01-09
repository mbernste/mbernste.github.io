---
title: 'What you want from RNA-seq versus what you get'
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

At a high level RNA-seq measures the transcription of each gene in a biological sample (i.e. a group of cells or a single single).  The type of data that RNA-seq provides is relatively complex and because of this complexity, there is a good amount of confusion regarding the units of gene expression derived from RNA-seq data and the various methods used for normalizing these units across samples.

In this post, I am going to describe what RNA-seq is capable of providing -- relative gene expression -- versus what many biologists *want* RNA-seq to provide -- absolute expression -- and why this discrepancy can result in confusion. One common "unit" for measuring gene expression derived from RNA-seq is **transcripts per million**. This unit describes relative gene expression rather than absolute gene expression. If one has multiple RNA-seq samples, one may attempt to measure absolute gene expression via the method of **median ratio normalization**; however, this method will only work if you assume that there exists a good number of genes that are not differentially expressed between your various samples.






