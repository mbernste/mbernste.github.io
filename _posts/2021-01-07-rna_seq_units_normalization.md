---
title: 'A primer on RNA-seq'
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

Inputs and outputs
---------

RNA-seq is a procedure for estimating the relative abundances of transcripts from each gene in a sample.  The input to an RNA-seq experiment is a subset of RNA molecules (i.e., transcripts) from a biological sample. Below, we depict a set of transcripts where each transcript is colored according to the gene from which it was derived (Blue, Green, Yellow):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_input.png" alt="drawing" width="700"/></center>

In this toy example, we have 13 total transcripts: 7 transcripts from the Blue gene, 4 transcripts from the Green gene, and 2 transcripts from the Yellow gene. In reality, a single cell contains [hundreds of thousands](https://www.qiagen.com/us/resources/faq?id=06a192c2-e72d-42e8-9b40-3171e1eb4cb8&lang=en) of transcripts. 

RNA-seq estimates the *fraction* of transcripts from each gene.  That is, rather than the estimate the **absolute abundance** -- in our toy example, the values 7, 4, and 2 -- RNA-seq estimates the **relative abundance** of transcripts from each gene: 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_transcript_abundance.png" alt="drawing" width="400"/></center>

The steps of an RNA-seq experiment
-----------

Now that we have looked at the inputs and outputs to an RNA-seq experiment, let's dig into its steps:

1. **RNA isolation:** Isolate RNA molecules from a cell or population of cells. 
2. **Fragmentation:** Break RNA molecules into fragments.
3. **Reverse transcription:** Reverse transcribe the RNA into DNA.
4. **Amplification:** Amplify the DNA molecules using [polymerase chain reaction](https://en.wikipedia.org/wiki/Polymerase_chain_reaction).
5. **Sequencing:** Feed the amplified DNA fragments to a sequencer.  The sequencer randomly samples fragments and records a short subsequence from the end (or both ends) of the fragment (on the order of a few hundred bases). These measured subsequences are called **sequencing reads**.  A sequencing experiment generates millions of reads that are stored on a digital file.
7. **Alignment:** Align the reads to the genome. That is, we wish to find a character-to-character match between each read and a location within the genome.  This is a challenging computational task given that genomes consist of billions of bases and we are dealing with millions of reads. (Caveat: New algorithms, such as [kallisto](https://www.nature.com/articles/nbt.3519) and [Salmon](https://www.nature.com/articles/nmeth.4197), circumvent the computationally expensive task of performing character-to-character alignment.)
8. **Quantification:** For each gene, count the number of reads that align to the gene. (Caveat: because of errors, noise, and the presence of reads that align to multiple genes, one performs [statistical inference](https://academic.oup.com/bioinformatics/article/26/4/493/243395) to infer the gene of origin for each read. Counting alignments to each gene is a crude inference procedure.)

By design, each step of the RNA-seq protocol preserves, in expectation, the relative abundance of each transcript so that at the end, one is able to estimate the relative abundances of each transcript.  Here's a figure illustrating all of these steps:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_schematic.png" alt="drawing" width="700"/></center>

Distilling RNA-seq down to its essence
-----------

All of the aforementioned steps may seem little complex, so let me try to distill the RNA-seq process down to its essence. At the end of the day, one may view an RNA-seq experiment as a *sampling process*, where we randomly sample *locations* along the transcripts in the sample. That is, each read is viewed as a *sampled location*.  

Let's take the toy example from above that consisted of 13 transcripts from three genes: 7 from the Blue gene, 4 from the Green gene, and 2 from the Yellow gene.  If our RNA-seq experiment generated 10 reads, then we can view these 10 reads as randomly sampled locations from anywhere along the 13 transcripts:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_read_locations.png" alt="drawing" width="700"/></center>

Because we are sampling *locations* along all of the transcripts in the sample, we will tend to get more reads from longer genes and fewer reads from short genes. Thus, these counts will not, by themselves be an accurate estimation of the fraction of transcripts from each gene.

Let's say in our toy example the Blue gene is 4 bases long, the Green gene is 7 bases long, and the yellow gene is 2 bases long.  Then, the expected fraction of locations/reads sampled from each transcript will be the following:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_reads_vs_transcript_abundance.png" alt="drawing" width="500"/></center>

Notice how these fractions differ from the fraction of transcripts that originate from each gene. Notably, the fraction of the reads from the Green gene is higher than the fraction of transcripts from the Green gene. This is because the Green gene is long and thus, when we sample locations along the transcript, we are more likely to select locations along a Green gene. 

Normalizing read counts to account for gene length
----------------


A note on RPKM and FPKM
----------------


Estimating absolute abundance via median-ratio normalization
----------------









