---
title: 'Median ratio normalization for bulk RNA-seq data'
date: 2023-09-05
permalink: /posts/median_ratio_norm/
tags:
  - tutorial
  - bioinformatics
  - RNA-seq
  - gene expression
---

*THIS POST IS CURRENTLY UNDER CONSTRUCTION* 

Introduction
------------

In my [previous post](https://mbernste.github.io/posts/rna_seq_basics/), we discussed the basics of RNA-sequencing and how to intuit the units of gene expression that this technology generates. To do so, we described a mathematical/statistical abstraction of the protocol that involved sampling mRNA transcriptics from the pool of transcripts in the sample and then sampling locations along those selected transcripts. Through this process, we obtain a set of _reads_, which are short sequences from these sampled locations. To obtain a measure of gene expression, we count the number of reads that align to each gene/isoform in the genome.

As we discussed, RNA-seq provides _relative_ expression values between genes. This is because we lose the information on how much total RNA was in each sample. The size of the pool of reads that we sequence is a technical parameter that we can adjust in our protocol, and thus, the more reads we sequence, the more counts we will obtain, on average, for each gene. Therefore, after accounting for the length of each gene/isoform, one can obtain an estimate for the relative amounts of each gene within a sample. This is what the units _transcripts per million_ (TPM) describes. If you sample a million transcripts from the sample, the TPM value for a given gene will tell you how many transcripts on average will have originated from the given gene of interest.

Of course, this begs the question: how can we compare the expression of a given gene values _between_ samples? One approach is to simply compare the TPMs between samples with the understanding that one is not really comparing the absolute amount of expression, but rather is comparing two relative amounts of expression. That is, if you see that your gene's TPM is higher in one condition compared to another, it might not be the case that there is actually more mRNA in the first condition; it might just be that the amount of mRNA from the _other_ genes in the sample is lower.  

Is it possible to compare the absolute expression of a given between two samples? In this post, we will describe one normalization strategy that seeks to enable such analyses: median ratio normalization. This approach was first introduced by [XXXXXX et al.] () and is the approach that is used by the popular [DESeq2]() method for normalizing bulk RNA-seq data prior to estimating differential expression. If you have ever used DESeq2, median ratio normalization is the approach that the tool uses by default to calculate the "size factors" of each sample.  

In this post, we will discuss the intuition behind median ratio normalization and the key assumptions that this method makes about the data. We will also discuss why this method only applies to bulk RNA-seq data, but cannot work for most single-cell RNA-seq datasets.

Intuition behind median ratio normalization
-------------------------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/median_ratio_assumption.png" alt="drawing" width="400"/></center>





Exploring median ratio normalization in real data
-------------------------------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/rna_seq_ranked_ratios_real_example.png" alt="drawing" width="700"/></center>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/count_distribution_pre_vs_post_median_ratio.png" alt="drawing" width="700"/></center>

