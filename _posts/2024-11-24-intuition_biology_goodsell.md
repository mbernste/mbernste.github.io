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

As a computer scientist working in biomedical research, I have had to develop my biology knowledge on the fly. Over the course of this effort, there have been certain concepts, articles, figures, and other bodies of work that provided notable step-functions in my ability to "intuit" biological systems. (my use of the word "intuit" is quite strained here, but I digress). In this series of blog posts, I will collect some of these works and provide a little bit of commentary describing why I found these works so helpful. I hope the centralization of these resources serves others who are on a similar journey as I am!

In the first post of this series, I will attempt to tie two seemingly contradictory ideas together through the work of [David S. Goodsell](https://en.wikipedia.org/wiki/David_Goodsell):

1. Cells are densely packed, chaotic places
2. We can describe cellular processes with [graphs/networks](https://en.wikipedia.org/wiki/Biological_network)

I will begin by discussing the visual depictions of cells by [David S. Goodsell](https://en.wikipedia.org/wiki/David_Goodsell). Dr. Goodsell is a structural biologist at the Scripps Research Institute and Rutgers University and is well known for his scientifically accurate depictions of cells and the molecules that they are comprised of. [His work](https://ccsb.scripps.edu/goodsell/) is both educational and beautiful and helped expand my understanding of biology.

As I will discuss, Dr. Goodsell's work highlights how densely packed, and seemingly chaotic the environments within cells are. The packed, chaotic nature of these environments seems to contradict the fact that biologists routinely describe cells using the clean, mathematical language of networks and graphs. In this post, I will attempt to renconcile these two ideas. 

Cells are absolutely packed
---------------------------

What struck me most from Dr. Goodsell's work is how densely packed cells really are. Below is an example illustration that depicts the density of the cell:

<center><img src="https://cdn.rcsb.org/pdb101/goodsell/tif/model-of-a-mycoplasma-cell.tif" alt="drawing" width="400"/></center>
Acknowledgement: Martina Maritan, Ludovic Autin, David S. Goodsell, Scripps Research and RCSB Protein Data Bank. doi: 10.2210/rcsb_pdb/goodsell-gallery-040

This is a far cry from the image I had previously held of cells as a little, uncrowded "bags of water". I believe this incorrect mental model was fomented in my mind by images like the following that are meant to teach the organelles found in the cell:

<center><img src="https://upload.wikimedia.org/wikipedia/commons/4/4b/Cell-organelles-labeled.png" alt="drawing" width="400"/></center>
Acknowledgement: Bingbongboing as found on [Wikipedia](https://en.wikipedia.org/wiki/Cellular_compartment#/media/File:Cell-organelles-labeled.png)

Though images like this are effective for teaching the different organelles found in cells, they imply that cells are empty (at least that was my impression). This was a misconception that I had held for a good portion of my computational biology journey.

A second thing that struck me was the interplay between order and chaos that exists within cells. As an example, see this illustration by Goodsell depicting the coronovirus lifecycle:

<center><img src="https://cdn.rcsb.org/pdb101/goodsell/png-800/coronavirus-life-cycle.png" alt="drawing" width="400"/></center>
Acknowledgement: David S. Goodsell, RCSB Protein Data Bank; doi: 10.2210/rcsb_pdb/goodsell-gallery-023. Integrative illustration for coronavirus outreach (2020) PLoS Biol 18: e3000815 doi: 10.1371/journal.pbio.3000815

Notice that despite the messy distribution of proteins and other biomolecules, clear structures form (membranes, gradients, etc.). In the above picture we see, emerging from the chaos, the insidious formation of new viruses! 

How order emerges from the chaos: connections to network biology
----------------------------------------------------------------

If you work in computational biology, there is little doubt that you have been exposed to concepts found in [network biology](https://en.wikipedia.org/wiki/Biological_network). A common way to describe the biochemical processes that occur in cells is to depict and model these processes mathematically as networks or graphs. For example, protein-protein interaction networks are networks in which proteins form the nodes of the graph and an edge between two proteins indicates that those two proteins interact or bind with one another. Such protein interaction networks form [signaling pathways](https://en.wikipedia.org/wiki/List_of_signalling_pathways) in which the information flow through a cell is mediated by cascading interactions between proteins and other molecules. For example, below is a depiction of the [TNF-alpha signalling pathway](https://www.wikipathways.org/pathways/WP231.html), which is a signalling pathway used to modulate immune cell function:

<center><img src="https://www.wikipathways.org/wikipathways-assets/pathways/WP231/WP231.png" alt="drawing" width="1500"/></center>
Acknowledgement: Agrawal A, et al. (2024) WikiPathways 2024: next generation pathway database. NAR.

Now, if cells are so crowded, how exactly does the orderly structure of a signalling pathways and networks emerge at all from the chaotic environment of the cell? Learning the following four facts helped explain, to some extent, how the network model can be used to describe cellular processes:

1. Molecules move extremely fast inside cells
2. Proteins are hyper-specific in regards to what they will bind to
3. Many chemical reactions require enzymatic catalysis to occur
4. Cells are highly compartmentalized

Now, let's address the first question: if proteins and other biomolecules are so packed within the cell and constantly bumping into one another, wouldn't we expect many abberant interactions between molecules? This was my intuition at least; however, that intuition is wrong. 

First, proteins are hyper-specific in regards to what they will interact with. Most proteins have a very "tight" binding pocket that will only bind to a very specific target. For example, XXXXXXXX:


Because of this, the vast, vast majority of physical interactions between proteins don't result in any binding and/or chemical reaction at all. 

Second, most chemical reactions in a cell have a very high activation energy and thus, will rarely occur on their own without something to catalyze their reaction. That is, even if two molecules bump into one another that _could_, in theory, react together, they often won't unless a third molecule is there to catalyze that reaction. From this, we realize that the vast majority of objects colliding into one another won't actually result in a chemical reaction. I imagine a bunch of billiard balls bouncing harmlessly off one another.


To provide some intuition, let's look at the numbers. Proteins diffuse through water at a speed of XXXXX. That is pretty fast! Now, because cells are so crowded, proteins move a lot more slowly, but they are still moving around quite a lot. It takes about 10 seconds for a protein to move the distance of a [HeLa cell's]() length (note, the motion of proteins in the cell is random and follows [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion)). Because _all_ proteins are moving at this speed, we can deduce that every 10 seconds each protein will be in a completely new location within the cell and thus the cell will be highly rearranged (subject to the tight compartmentalization imposed by organelles and other structures). This offers a lot of opportunity for interacting proteins to "find" one another in the chaos.

Putting this all together a picture begins to emerge: 

* The cell is tightly packed with proteins and other biomolecules
* These molecules are rapidly moving and bumping into one another; however, the vast majority of these collisions don't result in any binding and/or chemical reaction due to their hyperspecificy, compartmentalization, and requirements for catalysis
* However, because of how fast the molecules are moving these hyper specific interactions occur on a regular basis and carry out the biomolecular functions required to sustain life   

In essence, we find the cell to be a tightly regulated "machine" and networks are a natural mathematical structure to model this machine.

Related Reading
---------------
* [David S. Goodsell's homepage](https://ccsb.scripps.edu/goodsell/)
* [This blog post by Ken Shirriff](http://www.righto.com/2011/07/cells-are-very-fast-and-crowded-places.html)



