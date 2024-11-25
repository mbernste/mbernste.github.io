---
title: 'Intuiting biology (Part 1: Order and chaos in the crowded cell)'
date: 2024-11-24
permalink: /posts/intuit_biology_goodsell/
tags:
  - biology
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

As a computer scientist working in biomedical research, I have had to develop my biology knowledge on the fly. Over the course of this effort, there have been certain concepts, articles, figures, and other bodies of work that provided notable step-functions in my ability to "intuit" biological systems. (I place "intuit" in quotes because my use of this word is quite stretched -- biology is staggeringly complex and whatever understanding of biology I may have, it falls far short of intuition, but I digress). In this series of blog posts, I will collect some of these works and provide a little bit of commentary describing why I found these works so helpful. I hope the centralization of these resources serves others who are on a similar journey as I am!

In the first post of this series, I will discuss some insights I gained through the work of [David S. Goodsell](https://en.wikipedia.org/wiki/David_Goodsell). Dr. Goodsell is a structural biologist at the Scripps Research Institute and Rutgers University and is well known for his scientifically accurate depictions of cells and the molecules that they are comprised of. His work is both educational and beautiful and helped expand my understanding of biology.

More specifically, in this post, I will discuss two ideas communicated in his work:

1. Cells are absolutely packed with biomolecules
2. There is a fascinating interplay of order and chaos in the cell

Finally, I will attempt to connect these ideas to concepts found in [network biology](https://en.wikipedia.org/wiki/Biological_network), by attempting to answer the following question: If cells are so packed and chaotic, how is it that we can model them mathematically with networks?


Cells are absolutely packed
---------------------------

What struck me most from Dr. Goodsell's work is how densely packed cells really are. Below is an example illustration that depicts the density of the cell:

<center><img src="https://cdn.rcsb.org/pdb101/goodsell/tif/model-of-a-mycoplasma-cell.tif" alt="drawing" width="400"/></center>
Acknowledgement: Martina Maritan, Ludovic Autin, David S. Goodsell, Scripps Research and RCSB Protein Data Bank. doi: 10.2210/rcsb_pdb/goodsell-gallery-040

This is a far cry from the image I had previously held of cells as a little, uncrowded "bags of water". I believe this incorrect mental model was fomented in my mind by images like the following that are meant to teach the organelles found in the cell:

<center><img src="https://upload.wikimedia.org/wikipedia/commons/4/4b/Cell-organelles-labeled.png" alt="drawing" width="400"/></center>
Acknowledgement: Bingbongboing as found on [Wikipedia](https://en.wikipedia.org/wiki/Cellular_compartment#/media/File:Cell-organelles-labeled.png)

Though images like this are effective for teaching the different organelles found in cells, they imply that cells are empty (at least that was my impression). This was a misconception that I had held for a good portion of my computational biology journey.

The interplay of order and chaos
--------------------------------

A second thing that struck me was the fascinating interplay between order and chaos that exists within cells. As an example, see this illustration by Goodsell depicting the coronovirus lifecycle:

<center><img src="https://cdn.rcsb.org/pdb101/goodsell/png-800/coronavirus-life-cycle.png" alt="drawing" width="400"/></center>
Acknowledgement: David S. Goodsell, RCSB Protein Data Bank; doi: 10.2210/rcsb_pdb/goodsell-gallery-023. Integrative illustration for coronavirus outreach (2020) PLoS Biol 18: e3000815 doi: 10.1371/journal.pbio.3000815

Notice that despite the messy distribution of proteins and other biomolecules, clear structures form (membranes, gradients, etc.). In the above picture we see, emerging from the chaos, the insidious formation of new viruses! 

Connections to network biology
------------------------------

If you work in computational biology, there is little doubt that you have been exposed to concepts found in [network biology](https://en.wikipedia.org/wiki/Biological_network). A common way to describe the biochemical processes that occur in cells is to depict and model these processes mathematically as networks or graphs. For example, protein-protein interaction networks are networks in which proteins form the nodes of the graph and an edge between two proteins indicates that those two proteins interact or bind with one another. Such protein interaction networks form [signaling pathways](https://en.wikipedia.org/wiki/List_of_signalling_pathways) in which the information flow through a cell is mediated by cascading interactions between proteins (and other molecules). For example, the [KEGG Database]() is a well known database of curated cellular pathways that is routinely used in computational biology work. For example, below is a depiction of the [NF-kB signalling pathway](), which is a key signalling pathway used to modulate immune cell function:

Now, if cells are so crowded, how exactly does the orderly structure of a signalling pathways and networks emerge at all from the chaotic environment of the cell? How do two interacting proteins/molecules "find" one another at a high enough frequency? If all these molecules are constantly bumping into eachother, won't we get spurious interactions between molecules? In short, how can we model cells with networks at all?

To answer these questions, it helped me to realize two fundamental properties about the biophysics and chemistry that occurs within cells:

1. Despite being so packed molecules move extremely fast inside cells
2. Chemical interactions between biomolecules are hyper specific

To provide some intuition, let's look at the numbers. Proteins diffuse through water at a speed of XXXXX. That is pretty fast! Now, because cells are so crowded, proteins move a lot more slowly, but they are still moving around quite a lot. It takes about 10 seconds for a protein to move the distance of a [HeLa cell's]() length. Because _all_ proteins are moving at this speed, we can deduce that every 10 seconds the spatial arangement of proteins in a cell are highly rearranged (subject to the tight compartmentalization imposed by organelles and other structures). This offers a lot of opportunity for proteins to randomly bump into their binding partners.






