---
title: 'The basics of RNA-seq'
date: 2021-01-07
permalink: /posts/rna_seq_basics/
tags:
  - tutorial
  - bioinformatics
  - RNA-seq
  - gene expression
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
---------

At a high level RNA sequencing (RNA-seq) measures the transcription of each gene in a biological sample (i.e. a group of cells or a single single). In this post, I will review the RNA-seq protocol and explain how to interpret the most commonly used units of gene expression derived from an RNA-seq experiment: transcripts per million.  This post will assume a basic understanding of the [Central Dogma](https://en.wikipedia.org/wiki/Central_dogma_of_molecular_biology) of molecular biology.

Before getting started, let's review the inputs and outputs of an RNA-seq protocol. We're given a biological sample consisting of a cell or a population of cells, and our goal is to estimate the **transcript abundances** from each gene in the sample -- that is, the *fraction* of transcripts in the sample that originate from each gene. A toy example is depicted below where the genome consists only of three genes: a Blue gene, a Green gene, and a Yellow gene.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_input_output.png" alt="drawing" width="700"/></center>

The transcript abundances can be encoded as a vector of numbers where each element $i$ of the vector stores the fraction of transcripts in the sample originating from gene $i$.  This vector is often called a **gene expression profile**.

Overview of RNA-seq
--------

Here's a an overview of the genral steps that comprise the RNA-seq protocol:

1. **Isolation:** Isolate RNA molecules from a cell or population of cells. 
2. **Fragmentation:** Break RNA molecules into fragments.
3. **Reverse transcription:** Reverse transcribe the RNA into DNA.
4. **Amplification:** Amplify the DNA molecules using [polymerase chain reaction](https://en.wikipedia.org/wiki/Polymerase_chain_reaction).
5. **Sequencing:** Feed the amplified DNA fragments to a sequencer.  The sequencer randomly samples fragments and records a short subsequence from the end (or both ends) of the fragment (on the order of a few hundred bases). These measured subsequences are called **sequencing reads**.  A sequencing experiment generates millions of reads that are stored on a digital file.
7. **Alignment:** Computationally align the reads to the genome. That is, we wish to find a character-to-character match between each read and a location within the genome.  This is a challenging computational task given that genomes consist of billions of bases and we are dealing with millions of reads. (Caveat: New algorithms, such as [kallisto](https://www.nature.com/articles/nbt.3519) and [Salmon](https://www.nature.com/articles/nmeth.4197), circumvent the computationally expensive task of performing character-to-character alignment via approximate alignments called "pseudoalignment" and "quasi-aligmnent" respectively. These ideas are [very similar](https://liorpachter.wordpress.com/2015/11/01/what-is-a-read-mapping/).)
8. **Quantification:** For each gene, count the number of reads that align to the gene. (Caveat: because of sequencing errors and the presence of reads that align to multiple genes, one performs [statistical inference](https://academic.oup.com/bioinformatics/article/26/4/493/243395) to infer the gene of origin for each read.  That is the read "counts" for each gene are inferred quantities.   Explicit counting of reads aligning to each gene can be viewed as a crude inference procedure.)

By design, each step of the RNA-seq protocol preserves, in expectation, the relative abundance of each transcript so that at the end, one is able to estimate the relative abundances of each transcript.  Here's a figure illustrating all of these steps (Taken from [Bernstein, 2019](https://search.proquest.com/openview/af4f51ec373a0b13438c59e7731adeed/1?pq-origsite=gscholar&cbl=18750&diss=y)). This figure depicts a toy example where the genome consists of only five genes specified by the colors red, blue, purple, green, and orange:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_schematic.png" alt="drawing" width="800"/></center>

An abstracted overview of RNA-seq
-----------

The RNA-seq protocol may appear somewhat complex so let's look at an abstracted view of the RNA-seq procedure.  In this abstracted view, we will simplify RNA-seq down to two steps. First, we extract all of the transcripts from the cells in the sample. Then, we randomly sample *locations* along all of the transcripts in the sample. That is, each read is viewed as a *sampled location* from some transcript in the sample.  Of course, this is not physically what RNA-seq is doing, rather it is a mathematically equivalent process.

In the figure below, we depict a toy example where we have a total of three genes in the genome, each with only one isoform: a Blue gene, a Green gene, and a Yellow gene. We then extract 13 total transcripts from the sample: 7 transcripts from the Blue gene, 4 transcripts from the Green gene, and 2 transcripts from the Yellow gene. In reality, a single cell contains [hundreds of thousands](https://www.qiagen.com/us/resources/faq?id=06a192c2-e72d-42e8-9b40-3171e1eb4cb8&lang=en) of transcripts. We can then think of the reads that we generate from the RNA-seq experiment as random locations along these 10 transcripts. Here we depict 10 reads.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_abstracted.png" alt="drawing" width="800"/></center>

Because we are sampling *locations* along all of the transcripts in the sample, we will tend to get more reads from longer genes and fewer reads from shorter genes. Thus, these counts will not, by themselves be an accurate estimation of the fraction of transcripts from each gene.

Let's say in our toy example the Blue gene is 4 bases long, the Green gene is 7 bases long, and the yellow gene is 2 bases long.  Then, the expected fraction of locations/reads sampled from each transcript will be the following:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_reads_vs_transcript_abundance.png" alt="drawing" width="700"/></center>

Notice how these fractions differ from the fraction of transcripts that originate from each gene. Notably, the fraction of the reads from the Green gene is higher than the fraction of transcripts from the Green gene. This is because the Green gene is long and thus, when we sample locations along the transcript, we are more likely to select locations along a Green gene.  In the next section, we will discuss how to counteract this effect in order to recover the fraction of transcripts from each gene.

Estimating the fraction of transcripts from each gene
----------

Before we get started, let's define some quick mathematical notation:

1. Let $G$ be the number of genes. 
2. Let $N$ be the number of reads. 
3. Let $c_i$ be the number of reads aligning to gene $i$.
4. Let $t_i$ be the number of transcripts from gene $i$ in the sample. 
5. Let $l_i$ be the length of gene $i$.

Now let's look at the quantity that we are after, the fraction of transcripts from each gene, which we will denote as $\theta_i$:

$$\theta_i := \frac{t_i}{\sum_{j=1}^G t_j}$$

How do we estimate this from our read counts?  First, we realize that the total number of bases belonging to gene $i$ in the sample can be computed by multiplying the length of gene $i$ by the number of transcripts from gene $i$: 

$$n_i := l_it_i$$

This is the total number of RNA bases within all of the RNA transcripts floating around in the cells in the sample that originated from gene $i$.  Furthermore, recall that each read can be thought of as a random sample from the set of all possible locations along the transcripts in the sample. In this light, $n_i$ represents the total number of possible start sites for a given read from gene $i$.  Therefore, the fraction of reads we would expect to see from gene $i$ is 

$$p_i := \frac{n_i}{\sum_{j=1}^G n_j}$$

This is the probability that if we select a read, that read will have originated from gene $i$.  This is simply the probability parameter for a [Bernoulli random variable](https://en.wikipedia.org/wiki/Bernoulli_distribution), and thus, its maximum likelihood estimate is simply:

$$\hat{p}_i := \frac{c_i}{N}$$

With our estimated $\hat{p}_i$, we can then estimate $\hat{\theta}_i$ as follows:

$$\hat{\theta}_i := \frac{p_i}{l_i} \left(\sum_{j=1}^G \frac{p_j}{l_j} \right)^{-1}$$

Let's derive it:

$$\begin{align*} \theta_i &= \frac{t_i}{\sum_{j=1}^G t_j} \\ &= \frac{ \frac{n_i}{l_i} }{ \sum_{j=1}^G \frac{n_j}{l_j}} && \text{because} \ n_i = l_it_i \implies t_i = \frac{n_i}{l_i} \\ &= \frac{ \frac{p_i \sum_{j=1}^G n_j}{l_i}  }{\sum_{j=1}^G p_j \frac{\sum_{k=1}^G n_k}{l_j}} && \text{because} \ p_i = \frac{n_i}{\sum_{j=1}^G n_j} \implies n_i = p_i \sum_{j=1}^G n_j \\ &=  \frac{ \frac{p_i}{l_i}} {\sum_{j=1}^G \frac{p_j}{l_j}} \end{align*}$$

Then, to estimate $\theta_i$, we simply plug in our estimate $\hat{p}_i$ for each gene to arrive at our estimate $\hat{\theta}_i$.

Note that these $\hat{\theta}_i$ values will be very small because there are so many genes. Therefore, it is common to multiply each ${p}_i$ by one million. The resulting values, called **transcripts per million (TPM)** tells you the number of transcripts in the cell from each gene if you select one million transcripts at random:

$$\text{TPM}_i := 10^6 \times \frac{p_i}{l_i} \left(\sum_{j=1}^G \frac{p_j}{l_j} \right)^{-1}$$

Thus, if we substitute $\hat{p}_i$ into the above equation, we have an *estimate* of the transcripts per million in the sample for gene $i$.

Handling genes with multiple isoforms
----------

Most genes in the human genome are [alternatively spliced](https://en.wikipedia.org/wiki/Alternative_splicing), resulting in multiple isoforms of the gene.  In the example above, we assumed that each gene had only one isoform. How do we handle the case in which a gene has multiple isoforms?

In fact, this is quite trivial. We simply compute the fraction of transcripts *of each isoform* as described above, and then simply sum the fractions of all isoforms for each gene to arrive at the fraction of transcripts originating from the gene. This is depicted in the figure below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/RNA_seq_isoform_vs_gene_abundance.png" alt="drawing" width="350"/></center>

Thus, if we have isoform-level estimates of each gene's TPM, then we simply sum these estimates across isoforms for each gene to arrive at an estimate of the TPM of for the gene as a whole.

Handling noise and multi-mapped reads
----------

So far, we have assumed an idealized scenario in which we know with certainty which gene "produced" each read.  In reality, this is not the case.  Sometimes, a read may align to multiple isoforms within a single gene (extremely common), or it might align to multiple genes (common enough to affect results), or it might align imperfectly to a gene and we might wonder whether the read really was produced by the gene. That is, was the mismatch in alignment due to a sequencing error, or was the read *not* produced by that gene (for example, the read may have been produced by a contaminant DNA fragment)? 

So how do we estimate the relative gene abundances in the real world where we have these issues? Because we don't know which gene produced each read, we have to infer it.  State-of-the methods perform this inference under an assumed [probabilistic generative model](https://doi.org/10.1093/bioinformatics/btp692) of the reads-generating process (to be discussed in a future post).

RPKM versus TPM
-----------

In the [early days of RNA-seq](https://doi.org/10.1038/nmeth.1226), read counts were summarized in units of reads per killobase per million mapped reads (RPKM).  These units are often still used to this day despite the fact that they are known to suffer from a fundamental issue. 

Before digging into the problem with RPKM, let's first define it.  Recall, the issue that comes with the raw read counts is that we will tend to sample more reads from longer isoforms/genes and thus, the raw counts will not reflect the relative abundance of each isoform or gene.  To get around this, we might try the following normalization procedure: simply divide the fraction of reads from each gene/isoform by the length of each gene.  That is, 

$$\frac{c_i}{N l_i} = \frac{\hat{p}_i}{l_i}$$

Let's try to wrap our head around the units of this quantity. First, we see that $\frac{c_i}{l_i}$ is the *number* of reads *per base* of the gene/isoform.  That is, it is the average number of reads generated from each base along the gene/isoform.  Then, if we divide this quantity by the total number of reads, $N$, we arrive at the number of reads per base of the gene/isoform *per read*. 

This is a bit confusing. It almost seems circular that we're computing the number of reads per base per read.  Here's another way to think about it: we're computing the *fraction of all reads*, $\frac{c_i}{N}$, per base of the gene/isoform.  That is, on average, we're computing the fraction all of the reads were generated, on average, by each base of a gene.  This inherently normalizes for gene length because the units are a single base!

We note that $N$ is very large (on the order of millions) and so too is $l_i$ (on the order of thousands), so to avoid dealing with such small numbers, we multiply $\frac{c_i}{N l_i}$ by $10^9$.  The resulting units are reads per killobase per million reads of a given gene:

$$\text{RPKM}_i := 10^9 \times \frac{c_i}{N l_i}$$

Note that $10^9$ is the result of multiplying by one million reads and one thousand bases.

Now that we've defined RPKM, what is it's problem?  











