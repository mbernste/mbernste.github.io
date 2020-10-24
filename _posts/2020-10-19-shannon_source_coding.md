---
title: "Foundations of information theory: Shannon's Source Coding Theorem (part 3)"
date: 2020-10-19
permalink: /posts/sourcecoding/
tags:
  - information theory
  - tutorial
---
THIS POST IS CURRENTLY UNDER CONSTRUCTION

*The mathematical field of information theory attempts to mathematically describe the concept of “information”. In the first two posts, we discussed the concepts of self-information and information entropy.  In this post, we step through Shannon's Source Coding Theorem to see how information entropy of a probability distribution describes the best-achievable efficiency required to communicate samples from the distribution.  My understanding of this material came, in part, from watching this excellent series of videos by [mathematicalmonk on YouTube](https://www.youtube.com/watch?v=UrefKMSEuAI&t=8s)*

Introduction
-----------

On our quest to understand what "information" really means in the context of the mathematical Information Theory, we discussed how intuitvely "information" is regarded as the amount of surprise experienced when we learn the outcome of a random event.  Moreover, we measure this "surprise" by the number of symbols that are required to communicate the outcome of this random event to another person or agent. This connection, from "surprise" to "symbols", is made concrete by [Shannon's Source Coding Theorem](https://en.wikipedia.org/wiki/Shannon%27s_source_coding_theorem), which proves that the information entropy, described in the [previous post](https://mbernste.github.io/posts/entropy/), defines the minimal number of symbols we would need to communicate the outcome of a random event to another person or agent. 

Let us more rigorously dig into Shannon's theorem.

Encoding and communicating samples from a distribution
-----------

Recall from the [previous post](https://mbernste.github.io/posts/entropy/), we discussed how the information entropy of a random variable tells you, on average, the minimum number of symbols that you will need to use to communicate the outcome of a random variable. That is, let us say we have two people, Person A and Person B, who are trying to communicate with one another. Specifically, Person A is observing samples, drawn one at a time, from some distribution X. Person A then wishes to communicate each sample to Person B. For example, $$X$$ might be a coin and Person A wishes to communicate to Person B the outcomes of repeated coin flips.  Let us first rigorously describe the mathematical framework in which Person A is communicating messages to Person B.  To do so, we will introduce a bunch of fundamental concepts from [Coding Theory](https://en.wikipedia.org/wiki/Coding_theory). 

First, instead of calling each draw from $$X$$ a "sample", we will instead call each draw a **symbol**.  The idea here is that Person A is going to come up with some random sequence of symbols, each drawn from a distribution $$X$$, and attempt to communicate this random message, composed of the random sequence of symbols, to Person B.  We'll call this random message the **sequence of source symbols**: 

$$X_1, X_2, X_3, \dots, X_m \overset{\text{i.i.d.}}{\sim} X$$

The idea of each $$X_i$$ being a "symbol", intuitively implies that the number of outcomes that each $$X_i$$ can take on is finite. To make this concrete, we will assert that $$X$$ is a categorical distribution.  That is,

$$X_1, X_2, X_3, \dots, X_m \overset{\text{i.i.d.}}{\sim} \text{Cat}(\boldsymbol{\theta})$$

such that

$$\forall i \ X_i \in \mathcal{X}$$

where $$\mathcal{X}$$ is a finite set of symbols called the **source alphabet** and $$\boldsymbol{\theta}$$ is a vector describing the probabilities that a given $$X_i$$ will take on a given symbol in $$\mathcal{X}$$.   

Before communicating each source symbol $X_i$ to Person B, Person A will first *encode* each symbol using a **code function** $$C$$.  The code function $$C$$ takes as input a source symbol and outputs a sequence of symbols from a new set of symbols called the **code alphabet**, denoted $$\mathcal{A}$$. The code is called a **$$b$$-ary code** if the size of the code alphabet is $$b$$.  That is, if $$\vert\mathcal{A}\vert = b$$.  For example, if $$\mathcal{A}$$ consists of two symbols, we call the code 2-ary (a.k.a. binary).

To make this concrete, let's look at a simplified, 2-ary version of [Morse Code](https://en.wikipedia.org/wiki/Morse_code) for encoding the English alphanumeric symbols into two symbols: "dots" and "dashes".  In Morse Code, the source alphabet, $$\mathcal{X}$$ consists of the alphanumeric symbols, the code alphabet $$\mathcal{A}$$ consists of only a dot and dash, and the code function $$C$$ maps each alphanumeric symbol to a sequence of dots and dashes. More specifically:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/MorseCode.png" alt="drawing" width="400"/></center>

For example, the name "Morse" would be encoded as follows:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/morse_code_example.png" alt="drawing" width="400"/></center>

Stated more rigorously, if we denote $$\mathcal{A}^*$$ to be the *set of sequences* of code symbols 

$$\mathcal{A}^* := \{a_1, a_2, \dots, a_k \mid k \geq 0, \forall i \ a_i \in \mathcal{A}\}$$

then $$C$$ is a function

$$C: \mathcal{X} \rightarrow \mathcal{A}^*$$  

We refer call each element $$\alpha \in C(\mathcal{X}$$ a **code word** where $$C(\mathcal(X))$$ is the [image](https://en.wikipedia.org/wiki/Image_(mathematics)) of $$C$$. We denote the length of a code word $$\alpha \in C(\mathcal{X})$$ as $$\vert\alpha\vert$$. In the above example, the length of code word "$$\cdot$$ - $$\cdot$$" (i.e. $$C(X_3)$$) is simply 3.

We also note that the code word length $$\vertC(X)\vert$$ is a random variable whose expectation is

$$E\left[\vertC(X)\vert\right] := \sum_{x \in \mathcal{X}} \vert C(x) \vert P(X = x)$$

For the purposes of our discussion, we will focus only on **uniquely decodable** code functions. A code function is uniquely decodable if it is an invertible function. Stated plainly, if a code $$C$$ is uniquely decodable, then we can always decode the code words unambiguously into the original sequence of source symbols using the inverse of $$C$$.  Most codes used in practice are uniquely decodable. A non-uniquely decodable code would not be very useful since Person B who receives the encoded message from Person A would be unable to unambiguously decode Person A's message.


Shannon's Source Code Theorem
--------

The Shannon Source Code Theorem is a statement about the smallest achievable expected code word length, $$E\left[\vert C(X)\vert\right]$$,  for some categorical distribution $$X$$ no matter what uniquely decodable $$C$$ you choose. Specifically, Shannon's Source Code Thoerem says that no matter what uniquely decodable $$C$$ you choose, the expected code word length will never be smaller than the the entropy of $$X$$, denote $$H(X)$$.  That is,

$$E\left[\vertC(X)\vert\right\] \geq H(X)$$

More rigorously, Shannon's Source Coding Thoerem goes as follows:

<span style="color:#0060C6">**Theorem 1 (Shannon's Source Coding Thoerem):** Given a categorical random variable $$X$$ over a finite source alphabet $$\mathcal{X}$$ and a code alphabet $$\mathcal{A}$$, then for all uniquely decodable $$C : \mathcal{X} \rightarrow \mathcal{A}^*$$, it holds that $$E\left[\vertC(X)\vert\right\ \geq H(X)$$.</span>

We will attempt to this theorem by forming an optimization problem: 

$$\text{min}_{C | C : \mathcal{X} \rightarrow \mathcal{A}^*} \vertC(X)\vert P(X = x)$$

This optimization problem is pretty unwieldy because it requires that we find a code function $$C$$ over *all possible* code functions in order to minimize the expected code word length.  Where do we go from here?   

To proceed, we will utilize another result: the converse of the [Kraft-McMillan Inequalities](https://en.wikipedia.org/wiki/Kraft–McMillan_inequality). This theorem goes as follows:

<span style="color:#0060C6">**Theorem 2:**Given a finite source alphabet $$\mathcal{X} := \{x_1, x_2, \dots, x_m\}$$, an integer $$B$$, and a set of integers $$\mathcal{L} := \ell_1, \ell_2, \dots, \ell_m$$ where>

<span style="color:#0060C6">$$\sum_{i = 1}^{m} \frac{1}{B^{\ell_i}} \leq 1$$
  
<span style="color:#0060C6">then there exists a $$B$$-ary uniquely decodable code $$C$$, a one-to-one, onto function<\span> 
  
<span style="color:#0060C6">$$\ell: \mathcal{X} \rightarrow \mathcal{L}$$ 

<span style="color:#0060C6">such that $$\vert C(x) \vert = \ell(x)$$.
 
Basically, this says that if you give me some set of lengths of code words $$\mathcal{L}$$ that satisfiy a certain inequality, then there exists a uniquely decodable $$C$$ that will map each source symbol $$x \in \mathcal{X}$$ to a code word with length $$\vert C(x) \vert \in \mathcal{L}$$. 

This thoerem will enable us to reformulate the aforementioned optimziation problem in a way that will be more straightforward. That is, our reformulation will enable us to avoid talking about specific code functions $$C$$, and will instead enable us to talk about code word lengths, given by $$\ell$$.  That is, we will no longer be burdened with reasoning about specific codes, but can simply talk about code word lengths given by some hypothetical code. Specifically, we will attempt to optimize the following:

$$\text{min}_{\ell_1, \ell_2, \dots, \ell_m} \sum_{i = 1}^m \ell_i \vert P(X = x_i)$$







