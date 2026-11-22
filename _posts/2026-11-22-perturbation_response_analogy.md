---
title: "Backyard perturbation prediction: An analogy for virtual cell modeling"
date: 2026-11-22
permalink: /posts/perturbation_response_image_analysis/
tags:
  - ai
---

_As machine learning and AI have come to prominence, and as new technologies have come online for perturbing and measuring cells at scale, a renewed effort has emerged to develop virtual cells: computational models capable of predicting how biological cells respond to perturbations. In this blog post, I will present an analogy of the perturbation modeling task that I feel captures, to some loose degree, the challenge that we face with this task and that I think may even hold some clue on to how to approach it. This analogy frames the cell perturbation modeling task not as predicting the transcriptome of a cell that has been perturbed, but instead, as the task of predicting how the image of a backyard (yes, a backyard behind a house!) would change if you "perturbed" the scene with some kind of action (like throwing a frisbee into the yard). Please note, the opinions expressed in this article are my own and not reflective of those held by my employer._

## Introduction

As machine learning and AI have come to prominence, and as new technologies have come online for perturbing and measuring cells at scale, a renewed effort has emerged to develop virtual cells: computational models capable of predicting how biological cells respond to perturbations. Indeed, this vision is gaining considerable momentum with substantial investment from both industry and philanthropy. A number of companies have been formed with this vision and are pursuing it with vigor, including my own, [Cellular Intelligence](https://www.cellularintelligence.com). Recently, the Department of Energy, Google, and Meta have [invested $1.8 billion](https://biohub.org/news/virtual-biology-initiative-expansion/) towards the goal of training virtual cell models with AI.

A common, general formulation the virtual cell modeling task is that, given a high-dimensional bimolecular measurement, most commonly a [transcriptome](https://en.wikipedia.org/wiki/Transcriptome) as represented by a gene expression vector, $x$, and a perturbation, $p$, we seek to predict how that measurement will change in response to the perturbation. That is, to predict $x'$, the resultant gene expression profile after $p$ is applied:

<br>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/perturbation_model.png" alt="drawing" width="800"/></center>

<br>

Here, $x$ is a vector representing gene expression across thousands of genes in the human genome (up to ~20k protein coding genes, though it is common practice to restrict to a smaller set of highly varying genes). $p$ is a vector representation for a perturbation such as a gene knockout or a chemical compound. 

For those working in this space, such as myself, I feel great optimism towards this goal, but it is coupled with a healthy dose of scientific humility. On the one hand, many of the pieces seem to be in place: we have powerful learning algorithms, access to enormous computational resources, and the ability to generate high-throughput molecular measurements of perturbed cells. On the other hand, biology is dizzyingly complex, and there is debate in the field around exactly how much data will be required, what modalities will be required, and what variables must be accounted for in order to train accurate and useful predictive models of how cells respond to perturbations. 

In this blog post, I will present an analogy of the perturbation modeling task that I feel captures, to some loose degree, the challenge that we face with this task and that I think may even hold some clue on to how to approach it (or at the very least, enable better intuition for what approaches the community is currently pursuing). **This analogy frames the cell perturbation modeling task not as predicting the transcriptome of a cell that has been perturbed, but instead, as the task of predicting how the image of a backyard (yes, a backyard behind a house!) would change if you "perturbed" the scene with some kind of action (like throwing a frisbee into the yard).** I will drawn an analogy not only between this task and the cell perturbation modeling task, but also an analogy between various aspects of this task including the challenges of batch effects between samples, the context-specificity of cellular response to perturbation, and the challenges in reproducing perturbations between experiments.

Please note, the opinions expressed in this article are my own and not reflective of those held by my employer.

## An analogy: Perturbing a backyard

Gene expression profiles are hard to intuit. They are high-dimensional vectors that, unlike images or text, are difficult for a human to make sense of without a fairly rigorous analysis that cross-references patterns of expression seen in the gene expression profile with known biology of cell phenotype and function. For this reason, I personally find it difficult to intuitively reason about the perturbation-response prediction task without diving into deep data-driven analyses that feel somewhat devoid of real intuition. 

In fact, I'd argue that this is a problem that so far is limiting progress. Take for example, the recent observation that simple baseline machine learning models may in fact [outperform large foundation models](https://doi.org/10.1038/s41592-025-02772-6) in modeling transcriptomics data. To drive the point further, even [this observation is contested](https://doi.org/10.1038/s41587-026-03307-w)! The fact that the community cannot even agree on whether one model outperforms another is, I think, less of a problem where machine learning is being applied to domains that lie closer to human intuition such as computer vision and language where a person can literally see or read the objects of analysis. 

With this in mind, I propose an analogy of the perturbation modeling task to a more intuitive task that lies in the macro-world in which we live in and see: **"backyard perturbation"**. 

The backyard perturbation task goes as follows:

* **Given:** The image of a scene of a backyard behind a house. 
* **Perturb the backyard:** Perform some action that "perturbs" the backyard. 
* **Task:** Predict the image of the backyard 1 minute after the perturbation.


Maybe the image of a backyard has a dog in it. Perhaps a child as well. The perturbation may entail something like throwing a frisbee into the yard. Perhaps an ice cream truck pulls up to the adjacent street. Etc. An example of a pre-perturbation and post-perturbation image (where the perturbation is a thrown frisbee) is depicted below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_perturbation_example.jpg" alt="drawing" width="800"/></center>

<br>

Notice how after the frisbee is thrown into the yard, the dog has captured the frisbee, the boy is running after the dog, and he has dropped the football he was playing with. All of these changes belong to the post-perturbation "state" of the backyard. Our task is to train a machine learning model that, given the image on the left, will produce as output the image on the right. Image plus perturbation as input, and an image as output.

Not all backyards look like this, however, and a boy and dog may not respond in quite this way each time. Below are two more examples, similar to this one.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_more_examples.jpg" alt="drawing" width="800"/></center>

<br>

Now I pose the question: How hard is this prediction task? I'd argue, it is pretty hard! If the task is to produce the output image pixel-for-pixel (e.g., evaluated via the [mean squared error](https://en.wikipedia.org/wiki/Mean_squared_error)), then this is quite daunting. I'd argue that the cell perturbation modeling task may be a good deal harder than this.

In the following sections, I will draw further analogies between the backyard perturbation modeling task and the cell perturbation modeling task to highlight some of the key challenges that face this field and why I think this analogy may actually be a decent fit. 

### Backyard perturbation response is context-dependent

The backyard perturbation modeling task is "context-dependent", meaning that the way in which the backyard responds is highly dependent on who is in that backyard and what they are doing! A boy and his dog will respond to the frisbee differently than a pair of grandparents sitting on the patio. Even the boy and dog will respond differently depending on what they were doing and where they started out at the time the frisbee was thrown.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_perturbaiton_context_dependent.jpeg" alt="drawing" width="800"/></center>

<br>

Cellular response to perturbations are, of course, also context-dependent. A [T cell](https://en.wikipedia.org/wiki/T_cell) will respond differently to [TGF-β](https://en.wikipedia.org/wiki/Transforming_growth_factor_beta) than a [fibroblast](https://en.wikipedia.org/wiki/Fibroblast) will. 

### It is difficult to reproduce the perturbation the same way each time

Let's just stick to the frisbee example where the backyards we are perturbing consist simply of a boy and a dog. Each time you "perturb" the yard with a frisbee, you may not quite throw it into the yard the same way each time. Sometimes, you will throw it in such a way that the behavior of the boy and dog is different from the time you threw it previously. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/reproducing_backyard_perturbations.jpeg" alt="drawing" width="1000"/></center>

<br>

Perturbing cells is the same way. The same "perturbagen" may have subtly different properties. It may come from a different manufacturer. Perhaps the concentrations of the perturbagen in its solvent/media is not _quite_ the same as it had been in a previous experiment. 

### There is latent information that may lead to impossible-to-predict aspects of response

The image of the backyard does not capture all of the information that would be necessary to predict, pixel-for-pixel, the post-perturbation image. For example, perhaps the boy's mother was just about to come out of the house and tell the boy to come in for lunch.  As the first image was taken, the mother was inside the house and just about ready to emerge. There is no information present in the pre-perturbation image that could _ever_ help a model predict this, and therefore, I surmise an algorithm would not predict any of the mother's pixels accurately. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_perturbation_hidden_state.jpeg" alt="drawing" width="800"/></center>

The same goes in molecular measurements of cells. No matter the data modality, whether that be transcriptomics, chromatin-accessibility, proteomics, etc., there is almost certainly going to be _some_ latent information about the state of the cell that determines the cell's response to perturbation that is invisible in the measurement. How much information is hidden, however, remains an open scientific question. 

### Different times of day or weather lead to "batch effects"

A pervasive issue in "omics" data are systemic [batch effects](https://pmc.ncbi.nlm.nih.gov/articles/PMC3880143/) that result from subtle differences in the conditions of the experiment from run-to-run. Batch effects can arise from subtle changes to the instruments used to make the measurements or slight discrepancies between how cells are handled from batch-to-batch. Most of the time, the source of the batch effect is not fully known. This results in gene expression profiles that tend to cluster in their ambient high-dimensional space according to their batch rather than according to the innate biology that the experiment is designed to probe.

In our backyard perturbation analogy, perturbations carried out at different times of day, or in different weather conditions, will induce image-wide system effects even if the effect of the perturbation is the same. Evening images will have have different shades of color. Cloudy and rainy images will tend to have muted lighting.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_perturbation_batch_weather.jpeg" alt="drawing" width="1000"/></center>

## How many training examples would be needed to train a model to perform well at backyard perturbation prediction?

Now, let's put it all together and visualize some backyard perturbation examples that combine many of the effects from above. Let's add to this too examples from different climates, locations, and cultures. Immediately you can see the vast space of training data one would likely need to train a model to accurately predict pixel-for-pixel response.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_perturbation_diversity.jpeg" alt="drawing" width="800"/></center>

<br>

How many training examples do you think we may need to perform this task accurately on diverse images? **Whatever number you think, I surmise, we'd need at least that many for accurate perturbation response modeling of biological cells.**

## Gene-for-gene accuracy may not be the right metric

I do not think this "backyard perturbation" modeling analogy is only useful for explaining the challenges of the cell perturbation modeling task, but also highlights something important about how we should _approach_ the task. Specifically, I conjecture that evaluating or possibly even training cellular perturbation models on their ability to reconstruct the post-perturbation cell state gene-for-gene (e.g., via [mean squared error](https://en.wikipedia.org/wiki/Mean_squared_error)) may not be the optimal approach.

The challenge of truly generalizing to out-of-distribution samples accurately gene-by-gene feels _at least_ as challenging as predicting the image of a perturbed backyard pixel-for-pixel. 

More importantly, minimizing error may not actually be the most useful objective either. While certainly a machine learning model that could accurately predict every pixel in the post-perturbation image could generalize to any downstream use of these predictions, I argue that there are clear low-dimensional "phenotypes" that may be worth predicting first that may be much easier. 

Take for example, the following two predictions. Which prediction is more "accurate"? I would argue that the prediction that shows the dog and boy playing very clearly is a better prediction than the one in which the boy and dog are very blurry even though the blurry prediction would likely score higher on per-pixel accuracy:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/backyard_perturbation_good_semantic_poor_error.jpeg" alt="drawing" width="800"/></center>

<br>

In the above example, the right-hand prediction is predicting the correct "semantic" response of the backyard: Throwing a frisbee into this yard would induce the boy and dog to play. 

Perhaps too with virtual cell perturbation models we should be thinking about what it means for a prediction to be good beyond simple reconstruction. What are the biological "semantics" that we want to be predicting? In what cases are these semantics not captured by gene-wise error? 

I point out too that although the task of predicting the post-perturbation pixel-by-pixel feels extremely difficult, there are indeed recurrent patterns in these backyard perturbation responses. I point out a few examples below:

1. When children and pets are in the backyard, it is likely throwing a frisbee into the backyard will induce them to play (a "playing" backyard phenotype)
2. When only older adults are in the backyard, throwing a frisbee may only induce confusion and interest, but not much response
3. When throwing a frisbee into a backyard at night, or in inclement weather, the backyard will respond very little

With enough training examples, and enough perturbations, one can imagine a model could capture very rich patterns of behavior that are universal even with the vast diversity of possible backyards and their per-pixel responses. 

One last point: This idea of training models to predict "lower-dimensional" phenotypes from high-dimensional genomics data is not new at all. For example, many machine learning methods have been developed to [predict cell type](https://pmc.ncbi.nlm.nih.gov/articles/PMC12065632) based on a cell or sample's gene expression profile. While one can imagine similarly low-dimensional perturbation response prediction tasks, such as [predicting whether or not a cell will die or grow](https://pubmed.ncbi.nlm.nih.gov/29505029/) in response to a perturbation, I wonder whether we should think about this problem as a continuum. 

On one extreme, we can imagine framing the perturbation response prediction task as simple classification for a specific phenotype. On the other extreme, we seek to predict the actual measured expression value post-perturbation for every gene. Perhaps there exist framings somewhere in the middle that predict aspects of cell response that sit somewhere between extremely coarse phenotypes and per-gene response; something like the task of predicting how gene "programs" change (e.g., signaling pathways, aspects of metabolism, etc.). 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/virtual_cell_dimensionality_of_prediction.png" alt="drawing" width="800"/></center>

Perhaps too, we should focus first on the lower-dimensional, easier tasks before the harder, high-dimensional tasks. I point out that even automating the relatively simple task of cell type classification has arguably not been solved. Despite [dozens and dozens](https://docs.google.com/spreadsheets/d/1DK4ACsXCBlq_EiA_3QOJPELd_HiautGsbTPztAUKp6w/edit?usp=sharing) of machine learning methods for automating cell type classification (including [a method I worked on during my Ph.D.!](https://pmc.ncbi.nlm.nih.gov/articles/PMC7753962/)), the field has yet to firmly adopt these tools due to their inability to fully generalize outside their training sets!

## Where this analogy breaks down

Now, there's a clear aspect in which this analogy of predicting the image of a backyard diverges significantly from predicting a gene expression profile: Each individual pixel does not itself encode any meaning, but rather, meaning only forms from the relative pixel values across the image. An image taken of a dog from two angles will result in radically different per-pixel values across the image, but will still be a very clear image of a dog. 

This stands in contrast to a gene expression profile where each element ("pixel") records the expression level of a specific gene. That gene is meaningful on its own irrespective of the other gene expression measurements. Moreover, one can argue that this fact makes the task of predicting how a cell responds to perturbation _easier_ than predicting an image in the backyard perturbation analogy. This might be true! We don't fully know yet how difficult the perturbation task is; however, I will point out that there may be more similarity between a gene expression profile and an image than meets the eye.

Many genes, like transcription factors, arguably don't have "firm" meaning without further information about the cell since how they influence cell state downstream is highly dependent on such factors as the epigenetic state of the genome. For example, PAX6 plays a  role in regulating the organogenesis of such diverse organs as [the brain and the lens in the eye](https://pubmed.ncbi.nlm.nih.gov/26138486/). Understanding the role of PAX6 in development requires understanding expression of other genes. 

At a very high-level, an image is a planar projection of a complex 3D scene in an analogous way that a gene expression profile is a projection of a complex cell state onto a crude, low-dimensional measurement (low-dimensional when considered in the context of the complexity of the underlying cell state!).  

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/cell_perturbation_complex_projection.jpeg" alt="drawing" width="800"/></center>

<br>

All of these points can be debated, and there are likely many, many ways in which the backyard perturbation analogy is not a perfect fit. Nonetheless, despite this, I do wonder whether this framing can help us think more clearly about the cell perturbation modeling task and the challenges that lie before us.
