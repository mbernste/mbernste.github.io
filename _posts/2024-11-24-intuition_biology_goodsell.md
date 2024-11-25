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

A second thing that struck me was the fascinating interplay between order and chaos that exists within cells. As an example, see this illustration by Goodsell depicting the coronovirus lifecycle:

<center><img src="https://cdn.rcsb.org/pdb101/goodsell/png-800/coronavirus-life-cycle.png" alt="drawing" width="400"/></center>
Acknowledgement: David S. Goodsell, RCSB Protein Data Bank; doi: 10.2210/rcsb_pdb/goodsell-gallery-023. Integrative illustration for coronavirus outreach (2020) PLoS Biol 18: e3000815 doi: 10.1371/journal.pbio.3000815

Notice that despite the messy distribution of proteins and other biomolecules, clear structures form (membranes, gradients, etc.). In the above picture we see, emerging from the chaos, the insidious formation of new viruses! 

How order emerges from the chaos: connections to network biology
----------------------------------------------------------------

If you work in computational biology, there is little doubt that you have been exposed to concepts found in [network biology](https://en.wikipedia.org/wiki/Biological_network). A common way to describe the biochemical processes that occur in cells is to depict and model these processes mathematically as networks or graphs. For example, protein-protein interaction networks are networks in which proteins form the nodes of the graph and an edge between two proteins indicates that those two proteins interact or bind with one another. Such protein interaction networks form [signaling pathways](https://en.wikipedia.org/wiki/List_of_signalling_pathways) in which the information flow through a cell is mediated by cascading interactions between proteins and other molecules. For example, below is a depiction of the [TNF-alpha signalling pathway](https://www.wikipathways.org/pathways/WP231.html), which is a signalling pathway used to modulate immune cell function:

<center><img src="https://www.wikipathways.org/wikipathways-assets/pathways/WP231/WP231.png" alt="drawing" width="1500"/></center>
Acknowledgement: Agrawal A, et al. (2024) WikiPathways 2024: next generation pathway database. NAR.

Now, if cells are so crowded, how exactly does the orderly structure of a signalling pathways and networks emerge at all from the chaotic environment of the cell? If all these molecules are constantly bumping into eachother, won't we get spurious interactions between molecules? Moreover, how do two interacting proteins/molecules "find" one another at a high enough frequency? In short, how can we model cells using networks at all?

To answer these questions, it helped me to learn four fundamental properties about the biophysics and chemistry that occurs within cells:

1. Chemical interactions between biomolecules are hyper specific
2. Many chemical reactions require enzymatic catalysis
3. Cells are highly compartmentalized
4. Despite being so packed molecules move extremely fast inside cells

Now, let's address the first question: if proteins and other biomolecules are so packed within the cell and constantly bumping into one another, wouldn't we expect many abberant interactions between molecules? This was my intuition at least. However, it's important to realize that proteins are hyper-specific in regards to what they will interact with.  Because of this, the vast, vast majority of physical interactions between proteins don't result in any chemical reaction at all. Moreover, most chemical reactions in a cell require enzymatic catalysis to occur. That is, even if two molecules bump into one another that _could_ react, they often won't. 

To provide some intuition, let's look at the numbers. Proteins diffuse through water at a speed of XXXXX. That is pretty fast! Now, because cells are so crowded, proteins move a lot more slowly, but they are still moving around quite a lot. It takes about 10 seconds for a protein to move the distance of a [HeLa cell's]() length (note, the motion of proteins in the cell is random and follows [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion)). Because _all_ proteins are moving at this speed, we can deduce that every 10 seconds each protein will be in a completely new location within the cell and thus the cell will be highly rearranged (subject to the tight compartmentalization imposed by organelles and other structures). This offers a lot of opportunity for interacting proteins to "find" one another in the chaos.

Putting this all together a picture begins to emerge: 

* The cell is tightly packed with proteins and other biomolecules
* These molecules are rapidly moving and bumping into one another; however, the vast majority of these collisions don't result in any chemical reaction due to their hyperspecificy, compartmentalization, and requirements for catalysis
* However, because of how fast the molecules are moving these hyper specific interactions occur on a regular basis and carry out the biomolecular functions required to sustain life   

In essence, we find the cell to be a tightly regulated "machine" and networks are a natural mathematical structure to model this machine and make its complexity ammenable to the human mind.





