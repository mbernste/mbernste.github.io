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

Transformers are a neural network architecture that have transformed the machine learning field (pun intended) as they are the key technology behind a number of breakthrough machine learning models such as [OpenAI](https://openai.com/)'s [ChatGPT](https://chat.openai.com/) and [Google Translate](https://translate.google.com/). 

A recent blog post, [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer), by Jay Alammar, provides an amazing explanation of transformers and attention. It was from this blog that I came to my understanding of these models. In this blog post, I will expound upon this foundation and provide an alternative explanation of transformers using slightly different diagrams that articulate my own mental model of how they work. Lastly, we will implement a small transformer in [PyTorch](https://pytorch.org/) to classify [T cell receptors (TCR)](https://en.wikipedia.org/wiki/T-cell_receptor) sequences as either originating from a tumor or healthy tissue. This example will provide a basic demonstration of an application of transformers in computational biology.

Inputs and outputs of a transformer layer
-----------------------------------------

At their core, a transformer is a layer of a neural network that performs a mapping between sequences of vectors. That is, the transformer accepts a sequence and then outputs a vector embedding of that sequence.  For example, the input sequence may be a sequence of words, like a sentence, or a DNA sequence. Each element, or **token**, of the input sequence (e.g., a word in the case of a sentence) is represented as a vector. If we are considering the first layer, then these input vectors are **feature vectors** associated with each word. Interestingly, the length of the input sequence to the transformer layer does not need to be fixed, but can be variable! This is a powerful feature as it enables a transformer layer to operate on arbitrary-lengthed sequences (this is similar to how a [graph convolutional neural network](https://mbernste.github.io/posts/gcn/) can operate on arbitrary-sized graphs). This process is depicted below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_input_output.png" alt="drawing" width="350"/></center>

<br>

In the next section, we will dig into the mechanics of the transformer layer and discuss how the transformer layer implements a process called **attention** when performing this sequence to sequence mapping. 

Attention
---------

Transformers were first introduced in the seminal paper, "[Attention Is All You Need](https://arxiv.org/abs/1706.03762)" by Vaswani _et al_. (2017). As the name of this paper suggests, transformers are built upon a mechanism called **attention**. Attention was originally introduced by [Bahdanau, Cho, and Bengio (2015)](https://arxiv.org/pdf/1409.0473.pdf) as a mechanism that was sort of "appended" onto a traditional [recurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network) to boost their performance. Vaswani _et al_. took this concept and used it to construct a novel neural network architecture built only out of attention mechanisms.

The idea of attention when performing sequence-to-sequence mapping is that when we consider the output vector associated with a given token, we intuitively want the model to pay greater "attention" to some input tokens and less attention to others ("attention" used here in the colloquial sense). 

For example, let's say we are generating output vectors for input vectors associated with the following sentence: "I like sushi because it makes me happy." Let us consider the case in which we are generating the output token for "delicious". Intuitively, we know that "delicious" is referring to "sushi". It makes sense that when the model is generating the output token for "delicous" it should consider the word "sushi" more heavily, than say, "because". The word "delicious" is referring directly to "sushi" whereas "because" is a conjunction playing a more complicated role in the sentence joining multiple ideas together. This is depicted in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_sushi_example1.png" alt="drawing" width="600"/></center>

<br>

In contrast when generating the output vector for "happy", intuitively, we might want to place more weight on the word, "I", because "happy" is referring directly to the subject, "I". This is depicted in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_sushi_example2.png" alt="drawing" width="600"/></center>

<br>

In summary, when generating each output vector, the attention mechanism considers _all_ of the input vectors and weights them according to how much "attention" to pay them when computing the output vector. We depict this process in the smaller example sentence, "I am hungry", below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_input_output_attention.png" alt="drawing" width="800"/></center>

The transformer layer: a step-by-step explanation
-------------------------------------------------

We will now dig into the details of the attention mechanism by building our understanding step-by-step. We will use the sentence, "I am hungry", going forward. 

In the first step, the model generates a vector associated with each input vector called the **values** (or "value vectors") by multiplying each input vector by a weights matrix $\boldsymbol{W}_V$. Let's let $\boldsymbol{x}_\text{I}$, $\boldsymbol{x}_\text{am}$, $\boldsymbol{x}_\text{hungry}$ denote our input vectors and $\boldsymbol{v}_\text{I}$, $\boldsymbol{v}_\text{am}$, $\boldsymbol{v}_\text{hungry}$ denote the value vectors. Then, the value vectors are generated via:

$$\begin{align*}\boldsymbol{v}_\text{I} &:= \boldsymbol{W}_V\boldsymbol{x}_\text{I}  \\ \boldsymbol{v}_\text{am} &:= \boldsymbol{W}_V\boldsymbol{x}_\text{am} \\ \boldsymbol{v}_\text{hungry} &:= \boldsymbol{W}_V\boldsymbol{x}_\text{hungry}\end{align*}$$

This is depicted schematically below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors_only_values.png" alt="drawing" width="500"/></center>

To spoil the punchline, the output vector associated with each input vector will be constructed as a weighted sum of these values vectors where the weights represent the amount of attention we pay to each input vector (for now take these weights as given, we will show how they are generated soon). For example, to generate the output vector for the word "I", which we will denote as $\boldsymbol{h}_\text{I}$, we will take a weighted sum of the value vectors associated with all the other words in the sentence:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_attention_weighted_sum_one_word.png" alt="drawing" width="400"/></center>

Here, the weights $a_{\text{I},\text{I}}$, $a_{\text{I},\text{am}}$, and $a_{\text{I},\text{hungry}}$ are the attention weights! They are used to weight the other words in the sentence according to how much we should use that words information (i.e., their value vectors) when constructing the output for "I".

We repeat this for every token in the input sequence where, for each token, the attention weights are different and thus, we compute a different weighted sum of the value vectors:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_attention_weighted_sum_all_words.png" alt="drawing" width="800"/></center>

<br>

Now, how are these attention weights calculated? This is really the meat of the transformer layer and can appear a bit complicated at first as it requires additional vectors to be generated for each input token. That is, not only will we generate value vectors associated with each token, as described previously, but we will also generate two additional vectors associated with each input token: **queries** and **keys**. Like the value vectors, these will be generated using two matrices, denoted $\boldsymbol{W}\_Q$ and $\boldsymbol{W}\_K$ respectively. Let $\boldsymbol{q}\_\text{I}$, $\boldsymbol{q}\_\text{am}$, $\boldsymbol{q}\_\text{hungry}$ denote the query vectors and $\boldsymbol{k}\_\text{I}$, $\boldsymbol{k}\_\text{am}$, $\boldsymbol{k}\_\text{hungry}$ denote the key vectors. They are then generated as follows:

$$\begin{align*}\boldsymbol{q}_\text{I} &:= \boldsymbol{W}_Q\boldsymbol{x}_\text{I}  \\ \boldsymbol{q}_\text{am} &:= \boldsymbol{W}_Q\boldsymbol{x}_\text{am} \\ \boldsymbol{q}_\text{hungry} &:= \boldsymbol{W}_Q\boldsymbol{x}_\text{hungry}\end{align*}$$

$$\begin{align*}\boldsymbol{k}_\text{I} &:= \boldsymbol{W}_K\boldsymbol{x}_\text{I}  \\ \boldsymbol{k}_\text{am} &:= \boldsymbol{W}_K\boldsymbol{x}_\text{am} \\ \boldsymbol{k}_\text{hungry} &:= \boldsymbol{W}_K\boldsymbol{x}_\text{hungry}\end{align*}$$

This process is depicted below:


The queries and keys are then used to construct the attention weights. Let us start by generating the single attention weight, $a_{\text{I}, \text{am}}$ that tells the model how much to weight "am" when generating the word "I". We start by taking the [dot product](https://en.wikipedia.org/wiki/Dot_product) between the query vector for $I$, $\boldsymbol{q}_{\text{I}}$, and the key vector for "am", $\boldsymbol{k}_{\text{am}}$:


$$\text{I}_{\text{output}} := a_1 \text{I}_{V} + a_2 \text{am}_{V} + a_3 \text{hungry}_{V}$$

where the weights 

The transformer layer: putting it all together
----------------------------------------------


<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors.png" alt="drawing" width="500"/></center>

<br>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_mechanism.png" alt="drawing" width="850"/></center>
