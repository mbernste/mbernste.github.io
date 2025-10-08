---
title: "Self-Attention"
date: 2025-10-07
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

Transformers are a neural network architecture that have powered the development of [large language models](https://en.wikipedia.org/wiki/Large_language_model) and enabled their meteoric rise. The key conceptual advance behind the transformer architecture is a specific neural network mechanism (or "layer") called **self-attention**, which was introduced by Vaswani *et al.* (2017) in their landmark paper, *[Attention Is All You Need](https://papers.nips.cc/paper_files/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf)*. At its core, self-attention is a neural network mechanism that enables a model to decide dynamically how different components of its input relate to one another. For example, if the input to the model is natural language text -- i.e., a sequence of words -- then, self-attention is a mechanism that enables the neural network to decide how different words relate to one another. 

For example, take the sentence, "I like sushi because it makes me happy." The self-attention mechanism enables a model to learn relationships between these words. For example, the word "it" in this sentence is referring to "sushi". The words "me" and "I" are both referring to the speaker. The word "happy" is describing the speaker -- that is, the same entity being referred to by "I" and "me". The self-attention layer of a neural network seeks to tease out these relationships as it is trained to perform its task, whether that task be autoregressive langauge generation (which is how LLMs generate responses), machine translation, and even [computer vision tasks](https://en.wikipedia.org/wiki/Computer_vision). 

In this blog post, we will step through the self-attention mechanism and describe how it works both mathematically and intuitively. Much of my understanding of this material came from the excellent blog post, *[The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)* by Jay Allamar, which goes beyond self-attention to cover the full transformer. In this post, we will stick to only covering attention. We will start with the predecessor of self-attention, which was introduced by [Bahdanau, Cho, and Bengio (2015)](https://arxiv.org/pdf/1409.0473.pdf) in the context of machine translation. We will link the ideas from their work to the modern self-attention mechanism that powers transformers today. We will describe how Vaswani _et al_. took this concept and used it to construct an entire neural network layer, the "self-attention" layer. 


A Bit of history: Attention in machine translation
--------------------------------------------------

It was not that long ago that the task of translating between languages was a challenging open problem in computer science and machine learning (though it feels like a very long time ago!). 

From my understanding, the predecessor of self-attention was introduced by [Bahdanau, Cho, and Bengio (2015)](https://arxiv.org/pdf/1409.0473.pdf) as a mechanism that was sort of "appended" onto a traditional [recurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network) to boost their performance in machine translation.

Inputs and outputs of the self-attention layer
----------------------------------------------

At their core, a self-attention layer is a layer of a neural network that performs a mapping between sets of vectors. That is, the transformer accepts a set and then outputs a vector embedding of that set.  For example, the input set may be a sequence of words, like a sentence, or a DNA sequence. Each element, or **token**, of the input set (e.g., a word in the case of a sentence) is represented as a vector. If we are considering the first layer, then these input vectors are **feature vectors** associated with each word. Interestingly, the length of the input set does not need to be fixed, but can be variable! This is a powerful feature as it enables a transformer layer to operate on arbitrary-lengthed sequences (this is similar to how a [graph convolutional neural network](https://mbernste.github.io/posts/gcn/) can operate on arbitrary-sized graphs). This process is depicted below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_input_output.png" alt="drawing" width="350"/></center>

<br>

TODO More specifically, we can break the transformer layer down into two main sublayers: an attention sublayer followed by a fully connected sublayer:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_attention_and_fully_connected.png" alt="drawing" width="350"/></center>

<br>

The idea behind self-attention is that when we consider the output vector associated with a given token, we intuitively want the model to pay greater "attention" to some input tokens and less attention to others ("attention" used here in the colloquial sense). 

For example, let's say we are generating output vectors for input vectors associated with the sentence, "I like sushi because it makes me happy." Let us consider the case in which we are generating the output token for "delicious". Intuitively, we know that "delicious" is referring to "sushi". It makes sense that when the model is generating the output token for "delicous" it should consider the word "sushi" more heavily, than say, "because". The word "delicious" is referring directly to "sushi" whereas "because" is a conjunction playing a more complicated role in the sentence joining multiple ideas together. This is depicted in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_sushi_example1.png" alt="drawing" width="600"/></center>

<br>

In contrast when generating the output vector for "happy", intuitively, we might want to place more weight on the word, "I", because "happy" is referring directly to the subject, "I". This is depicted in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformer_attention_sushi_example2.png" alt="drawing" width="600"/></center>

<br>

In summary, when generating each output vector, the self-attention mechanism considers _all_ of the input vectors and weights them according to how much "attention" to pay them when computing the output vector. We depict this process in the smaller example sentence, "I am hungry", below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/transformers_input_output_attention.png" alt="drawing" width="800"/></center>

The nuts and bolts of the attention layer
-----------------------------------------

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


