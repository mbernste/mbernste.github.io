---
title: 'Median ratio normalization for bulk RNA-seq data'
date: 2023-09-01
permalink: /posts/median_ratio_norm/
tags:
  - tutorial
  - bioinformatics
  - RNA-seq
  - gene expression
---

*THIS POST IS CURRENTLY UNDER CONSTRUCTION* 

Introduction
---------

In my [previous post](https://mbernste.github.io/posts/rna_seq_basics/), we discussed the basics of RNA-sequencing and how to intuit the units of gene expression that this technology generates. To do so, we described a mathematical/statistical abstraction of the protocol that involved sampling mRNA transcriptics from the pool of transcripts in the sample and then sampling locations along those transcripts. Through this process, we obtain a set of _reads_, which are short sequences from these sampled locations. To obtain a measure of gene expression, we count the number of reads that align to each transcript.

As we discussed, RNA-seq provides _relative_ expression values between genes. This is because the size of the pool of reads that we sequence is a technical parameter. The more reads we sequence the more counts we will obtain, on average, for each gene. Thus, when looking at counts within a sample, after accounting for the length of each gene/isoform, one can obtain measure the approximate difference in the relative amounts of each gene. This is what the units _transcripts per million_ (TPM) describes. If you sample a million transcripts from the sample, the TPM value for a given gene will tell you how many transcripts on average will have originated from the given gene of interest.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/median_ratio_assumption.png" alt="drawing" width="400"/></center>


<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/rna_seq_ranked_ratios_real_example.png" alt="drawing" width="700"/></center>


<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/count_distribution_pre_vs_post_median_ratio.png" alt="drawing" width="700"/></center>

