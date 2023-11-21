---
title: 'Median-ratio normalization for bulk RNA-seq data'
date: 2023-11-21
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

Is it possible to compare the absolute expression of a given between two samples? In this post, we will describe one normalization strategy that seeks to enable such analyses: median-ratio normalization. This approach was first introduced by [XXXXXX et al.] () and is the approach that is used by the popular [DESeq2](https://doi.org/10.1186/s13059-014-0550-8) method for normalizing bulk RNA-seq data prior to estimating differential expression. If you have ever used DESeq2, median-ratio normalization is the approach that the tool uses by default to calculate the "size factor" corresponding to each sample.  

In this post, we will discuss the intuition behind median-ratio normalization and the key assumptions that this method makes about the data. We will also discuss why this method only applies to bulk RNA-seq data, but cannot work for most single-cell RNA-seq datasets.

Intuition behind median ratio normalization
-------------------------------------------

Let us start by defining some notation. Let,

$$\begin{align*}n &:= \text{Total number of samples} \\ g &:= \text{Total number of genes} \\ c_{i,j} &:= \text{Count of reads from gene $j$ in sample $i$}\end{align*}$$

We start by computing a "baseline" expression value for each gene by computing the geometric mean of each genes counts across all samples. The geometric mean is used instead of the arithmetic mean because it is more robust to outlier values. For gene $j$, this is computed as:

$$m_j := \left(\prod_{i=1}^n c_{i,j} \right)^{\frac{1}{n}}$$

Then, for each sample $i$, for each gene $j$, we compute the ratio of the counts of gene $j$ in sample $i$ (i.e., $c_{i,j}$), to the baseline expression value for gene $j$:

$$r_{i,j} := \frac{c_{i,j}}{m_j}$$

Intuitively, $r_{i,j}$ describes the deviation (more specifically the fold-change) between $c_{i,j}$ and a baseline expression value computed over all samples.  

Now, median-ratio normalization makes a key assumption: _most genes in any given sample are expressed at a common baseline level_. That is, for any given sample, most of its genes should not be over or under expressed relative to the other samples in the dataset. This key assumption must be met for median-ratio normalization to work. 

Now, with this assumption in mind, median-ratio normalization will _rank_ all of the ratios for all the genes in a given sample, $r_{i,1}, r_{i,2}, \dots, r_{i,g}$. Intuitively, if most genes are not changing significantly from baseline, then the genes that fall in the middle of this ranking represent those genes that are unchanging. An idealized scenario is illustrated in the schematic below where only a few genes are higher than baseline (red), a few genes are lower than baseline (blue), but most are unchanged (grey):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/median_ratio_assumption.png" alt="drawing" width="500"/></center>

Any deviation we see from baseline within the middle of this ranking is assumed to be driven by the total number of read counts. Thus, we can treat the median ratio as the "size factor" that we can use to re-scale the counts in the sample so that the ratios in the middle of the list are closer to the baseline. That is, we define the size factor for sample $i$ as,

$$s_i := \text{median}\left(r_{i,1}, r_{i,2}, \dots, r_{i,g}\right)$$

and then we re-scale all of the counts in this sample by dividing by $s_i$. That is, the normalized count for gene $j$ in sample $i$ would be computed as,

$$\tilde{c}_{i,j} := \frac{c_{i,j}}{s_i}$$

This is procedure is illustrated in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/median_ratio_normalization_schematic_scaling.png" alt="drawing" width="800"/></center>

Note, in practice, when computing the median ratio, we compute the median ratio using only those genes whose expression is non-zero across all samples. This is because we want to only use genes whose expression is high enough across all samples to be reliably detected. Intuitively, if a gene was failed to be detected (had zero counts), then it cannot tell us about the effect of library size so it is excluded. Stated mathematically, $s_i$ is computed as

$$s_i := \text{median}\left(\left\{ r_{k,j} \mid \forall k \in [n], \ \ c_{k,j} > 0 \right\}\right)$$

where $[n]$ are the set of integers from 1 to $n$.

Exploring median ratio normalization in real data
-------------------------------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/rna_seq_ranked_ratios_real_example.png" alt="drawing" width="700"/></center>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/count_distribution_pre_vs_post_median_ratio.png" alt="drawing" width="700"/></center>


Why median-ratio normalization cannot be applied to single-cell RNA-seq data
----------------------------------------------------------------------------
