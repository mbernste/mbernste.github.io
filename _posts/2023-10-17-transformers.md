---
title: "Transformers re-illustrated"
date: 2023-10-17
permalink: /posts/transformers/
tags:
  - tutorial
  - machine learning
  - deep learning
  - transformers
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_


Introduction
------------

Transformers are a neural network architecture that have transformed the machine learning landscape (pun intended) as they are the key technology behind a number of breakthrough machine learning models such as [OpenAI](https://openai.com/)'s [ChatGPT](https://chat.openai.com/) and [Google Translate](https://translate.google.com/). Transformers were first introduced in the seminal paper, "[Attention Is All You Need](https://arxiv.org/abs/1706.03762)" by Vaswani et al. (2017). As the name of this paper suggests, transformers are built upon a mechanism called **attention**. Attention was originally introduced by [Bahdanau, Cho, and Bengio (2015)](https://arxiv.org/pdf/1409.0473.pdf) as a mechanism that was sort of "appended" onto a traditional recurrent neural network to boost their performance. Vaswani _et al_. took this concept and used it to construct a novel neural network architecture built only out of attention mechanisms.

A recent blog post, [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer), by Jay Alammar, provides an amazing explanation of transformers and attention. It was from this blog that I came to my understanding of these models. In this blog post, I will expound upon this foundation and provide an alternative explanation of transformers using slightly different diagrams that articulate my own mental model of the transformer. Lastly, we will implement a small transformer in [PyTorch](https://pytorch.org/) to classify [T cell receptors (TCR)](https://en.wikipedia.org/wiki/T-cell_receptor) sequences as either originating from a tumor or healthy tissue. This example will provide a basic demonstration of an application of transformers in computational biology.

Inputs and outputs of a transformer
-----------------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_input_output.png" alt="drawing" width="350"/></center>


Attention
---------


The transformer architecture
----------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors.png" alt="drawing" width="500"/></center>


<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_mechanism.png" alt="drawing" width="850"/></center>
