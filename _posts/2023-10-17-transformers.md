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

Transformers are a neural network architecture that have transformed the machine learning field (pun intended) as they are the key technology behind a number of breakthrough machine learning models such as [OpenAI](https://openai.com/)'s [ChatGPT](https://chat.openai.com/) and [Google Translate](https://translate.google.com/). Transformers were first introduced in the seminal paper, "[Attention Is All You Need](https://arxiv.org/abs/1706.03762)" by Vaswani _et al_. (2017). As the name of this paper suggests, transformers are built upon a mechanism called **attention**. Attention was originally introduced by [Bahdanau, Cho, and Bengio (2015)](https://arxiv.org/pdf/1409.0473.pdf) as a mechanism that was sort of "appended" onto a traditional [recurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network) to boost their performance. Vaswani _et al_. took this concept and used it to construct a novel neural network architecture built only out of attention mechanisms.

A recent blog post, [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer), by Jay Alammar, provides an amazing explanation of transformers and attention. It was from this blog that I came to my understanding of these models. In this blog post, I will expound upon this foundation and provide an alternative explanation of transformers using slightly different diagrams that articulate my own mental model of how they work. Lastly, we will implement a small transformer in [PyTorch](https://pytorch.org/) to classify [T cell receptors (TCR)](https://en.wikipedia.org/wiki/T-cell_receptor) sequences as either originating from a tumor or healthy tissue. This example will provide a basic demonstration of an application of transformers in computational biology.

Inputs and outputs of a transformer layer
-----------------------------------------

At their core, a transformer is a layer of a neural network that performs a mapping between sequences of vectors. That is, the transformer accepts a sequence and then outputs a vector embedding of that sequence.  For example, the input sequence may be a sequence of words, like a sentence, or a DNA sequence. Each element, or **token**, of the input sequence (e.g., a word in the case of a sentence) is represented as a vector. If we are considering the first layer, then these input vectors are **feature vectors** associated with each word. Interestingly, the length of the input sequence to the transformer layer does not need to be fixed, but can be variable! This is a powerful feature as it enables a transformer layer to operate on arbitrary-lengthed sequences (this is similar to how a [graph convolutional neural network](https://mbernste.github.io/posts/gcn/) can operate on arbitrary-sized graphs). This process is depicted below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_input_output.png" alt="drawing" width="350"/></center>

In the next section, we will dig into the mechanics of the transformer layer and discuss how the transformer layer implements a process called **attention** when performing this sequence to sequence mapping. 

Attention
---------


The transformer architecture
----------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors.png" alt="drawing" width="500"/></center>


<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_mechanism.png" alt="drawing" width="850"/></center>
