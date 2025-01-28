---
title: "Self-Attention"
date: 2023-10-17
permalink: /posts/selfattention/
tags:
  - tutorial
  - machine learning
  - deep learning
  - transformers
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_


Introduction
------------

Transformers are a neural network architecture that have transformed the machine learning field (pun intended) as they are the key technology behind the meteoric rise of large language models like [OpenAI](https://openai.com/)'s [ChatGPT](https://chat.openai.com/). 

A recent blog post, [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer), by Jay Alammar, provides an amazing explanation of transformers and self-attention. It was from this blog that I came to my understanding of these models. In this post, I will expound upon this foundation and provide an alternative explanation of transformers using different diagrams that articulate my own mental model of how they work. I will focus specifically on the self-attention layer of the transformer, as these are the crucial mechanism that gives transformers their power. Lastly, we will implement a small neural network in [PyTorch](https://pytorch.org/) that uses self-attention to classify [T cell receptors (TCR)](https://en.wikipedia.org/wiki/T-cell_receptor) sequences as either originating from a tumor or healthy tissue. 

A note on terminology: Transformers and self-attention
------------------------------------------------------

Inputs and outputs of the self-attention layer
----------------------------------------------

At their core, a self-attention layer is a layer of a neural network that performs a mapping between sets of vectors. That is, the transformer accepts a set and then outputs a vector embedding of that set.  For example, the input set may be a sequence of words, like a sentence, or a DNA sequence. Each element, or **token**, of the input set (e.g., a word in the case of a sentence) is represented as a vector. If we are considering the first layer, then these input vectors are **feature vectors** associated with each word. Interestingly, the length of the input set does not need to be fixed, but can be variable! This is a powerful feature as it enables a transformer layer to operate on arbitrary-lengthed sequences (this is similar to how a [graph convolutional neural network](https://mbernste.github.io/posts/gcn/) can operate on arbitrary-sized graphs). This process is depicted below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_input_output.png" alt="drawing" width="350"/></center>

<br>

In the next section, we will dig into the mechanics of the self-attention layer. 

Attention
---------

Transformers were first introduced in the seminal paper, "[Attention Is All You Need](https://arxiv.org/abs/1706.03762)" by Vaswani _et al_. (2017). As the name of this paper suggests, transformers are built upon a mechanism called **attention**. Attention was originally introduced by [Bahdanau, Cho, and Bengio (2015)](https://arxiv.org/pdf/1409.0473.pdf) as a mechanism that was sort of "appended" onto a traditional [recurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network) to boost their performance. Vaswani _et al_. took this concept and used it to construct a novel neural network architecture built only out of attention mechanisms. More specifically, we can break the transformer layer down into two main sublayers: an attention sublayer followed by a fully connected sublayer:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_attention_and_fully_connected.png" alt="drawing" width="350"/></center>

<br>

The idea behind attention is that when we consider the output vector associated with a given token, we intuitively want the model to pay greater "attention" to some input tokens and less attention to others ("attention" used here in the colloquial sense). Attention, in the technical sense, is a neural network architecture that pushes the model to explicitly pay attention to some input tokens and not others.

For example, let's say we are generating output vectors for input vectors associated with the following sentence: "I like sushi because it makes me happy." Let us consider the case in which we are generating the output token for "delicious". Intuitively, we know that "delicious" is referring to "sushi". It makes sense that when the model is generating the output token for "delicous" it should consider the word "sushi" more heavily, than say, "because". The word "delicious" is referring directly to "sushi" whereas "because" is a conjunction playing a more complicated role in the sentence joining multiple ideas together. This is depicted in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_sushi_example1.png" alt="drawing" width="600"/></center>

<br>

In contrast when generating the output vector for "happy", intuitively, we might want to place more weight on the word, "I", because "happy" is referring directly to the subject, "I". This is depicted in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_sushi_example2.png" alt="drawing" width="600"/></center>

<br>

In summary, when generating each output vector, the attention mechanism considers _all_ of the input vectors and weights them according to how much "attention" to pay them when computing the output vector. We depict this process in the smaller example sentence, "I am hungry", below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_input_output_attention.png" alt="drawing" width="800"/></center>

The attention layer
-------------------

We will now dig into the details of the attention mechanism by building our understanding step-by-step. We will use the sentence, "I am hungry", going forward. 

In the first step, the model generates a vector associated with each input vector called the **values** (or "value vectors") by multiplying each input vector by a weights matrix $\boldsymbol{W}\_V$. Let's let $\boldsymbol{x}\_\text{I}$, $\boldsymbol{x}\_\text{am}$, $\boldsymbol{x}\_\text{hungry}$ denote our input vectors and $\boldsymbol{v}\_\text{I}$, $\boldsymbol{v}\_\text{am}$, $\boldsymbol{v}\_\text{hungry}$ denote the value vectors. Then, the value vectors are generated via:

$$\begin{align*}\boldsymbol{v}_\text{I} &:= \boldsymbol{W}_V\boldsymbol{x}_\text{I}  \\ \boldsymbol{v}_\text{am} &:= \boldsymbol{W}_V\boldsymbol{x}_\text{am} \\ \boldsymbol{v}_\text{hungry} &:= \boldsymbol{W}_V\boldsymbol{x}_\text{hungry}\end{align*}$$

This is depicted schematically below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors_only_values.png" alt="drawing" width="500"/></center>

<br>

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

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors_only_queries_keys.png" alt="drawing" width="500"/></center>

<br>

The queries and keys are then used to construct the attention weights. Let us start by generating the single attention weight, $a_{\text{I}, \text{am}}$ that tells the model how much to weight "am" when generating the word "I". We start by taking the [dot product](https://en.wikipedia.org/wiki/Dot_product) between the query vector for $I$, $\boldsymbol{q}\_{\text{I}}$, and the key vector for "am", $\boldsymbol{k}\_{\text{am}}$:

$$s_{\text{I}, {am}} := \boldsymbol{q}\_{\text{I}} \boldsymbol{k}\_{\text{I}}^T$$

We'll call this value the "score" between word "I" and word "am" and it will be used to form the attention weight. This is depicted schematically below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_score_dot_product.png" alt="drawing" width="300"/></center>

<br>

Intuitively, if a given pair of words have a high score (i.e., high dot product between the first's query and the second's key) then this means that the given query and key are similar, and consequently we should pay attention to the second word (associated with the key) when forming the output vector associated with the first word (associated with query). 

With this reasoning, it seems that the score alone would serve as a good attention weight; however there is practical problem with using the score directly: there is no upper bound for the value of the dot product and thus, if we stack many transformer layers together (as we'll show later), we can encounter numerical instability as these values blow up. We thus need a way to normalize the score. To do so, we transform the score by first scaling by a constant value, usually $\sqrt{d}$ where $d$ is the dimensions of the queries and key vectors, and then computing the softmax using _all_ of the scores when examining the other words in the input sequence. This forms the final attention weight. For example, for words "I" and "am", the attention weight is given by:

$$\begin{align*}a_{\text{I}, \text{am}} &:= \text{softmax}\left( \frac{ s_{\text{I},\text{I}}}{\sqrt{d}}, \frac{s_{\text{I},\text{am}}}{\sqrt{d}}, \frac{s_{\text{I},\text{hungry}}}{\sqrt{d}} \right) \\ &= \frac{\exp{\frac{s_{\text{I},\text{am}}}{\sqrt{d}}}}{\exp{\frac{s_{\text{I},\text{am}}}{\sqrt{d}}} + \exp{\frac{s_{\text{I},\text{am}}}{\sqrt{d}}} + \exp{\frac{s_{\text{I},\text{am}}}{\sqrt{d}}}}\end{align*}$$

This is depicted in the schematic below for all of the attention weights when generating the output vector for "I":

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_generate_attention_weights.png" alt="drawing" width="300"/></center>

The intuition behind this normalization procedure is that the first scaling operation that scales each score by $\sqrt{d}$ normalizes for the number of terms in the summation used to compute the dot product. The softmax then performs a final normalization that forces the sum of the attention weights to equal one!  

The fully connected layer
-------------------------

The attention layer is followed by a fully connected layer. This layer is quite simple: we simply take the vectors that were produced by the attention layer and pass them through a fully connected neural network! Thus, we perform a non-linear transformation of these attention-derived vectors. This steps injects more non-linearity into the model so that, when we stack transformer layers together, we can complex functions for computing attention.

In the next section, we will put all of these steps together and show how they can be performed in parallel using [matrix multiplication](https://mbernste.github.io/posts/matrix_multiplication/).

Putting it all together: The transformer layer
----------------------------------------------

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_intermediate_vectors.png" alt="drawing" width="500"/></center>

<br>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_mechanism.png" alt="drawing" width="850"/></center>


Multi-headed attention
----------------------

Positional encodings
--------------------

Case study: classifying T cell receptor sequences
-------------------------------------------------


