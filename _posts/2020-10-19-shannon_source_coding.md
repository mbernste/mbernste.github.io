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

Recall from the previous post, we discussed how the information entropy of a random variable tells you, on average, the minimum number of symbols that you will need to use to communicate the outcome of a random variable. That is, let us say we have two people, Person A and Person B, who are trying to communicate with one another. Specifically, Person A is observing samples, drawn one at a time, from some distribution X. Person A then wishes to communicate each sample to Person B. For example, $$X$$ might be a coin and Person A wishes to communicate to Person B the outcomes of repeated coin flips.

The catch is that Person A must use a sequence of symbols from some alphabet to communicate these outcomes. For example, Person A may be restricted to communicate using only two symbols, say “1” and “0” (called bits). Using these symbols, Person A must construct a code made from these symbols to communicate these outcomes to Person B (we assume that Person B always understands how to decode the encoding). Interestingly, according to Shannon’s Source Coding Theorem, no matter how Person A construct’s their code, in expectation, Person A will need to use at least the entropy of $$X$$ number of symbols, denoted $$H(X)$$, to communicate each outcome. No matter how clever, Person A will never be able to construct a code such that their average message will be smaller than $$H(X)$$. Said differently, entropy provides a lower bound on the average size of each message that Person A transmits to Person B.

Let us more rigorously prove this idea.

Encoding and communicating samples from a distribution
-----------

As we previously described, Person A is tasked with communicating the outcomes from some [categorical distribution](https://en.wikipedia.org/wiki/Categorical_distribution) $$X$$ to Person B.  We will call these samples the **sequence of source symbols**: 

$$X_1, X_2, X_3, \dots, X_m \overset{\text{i.i.d.}}{\sim} \text{Cat}(\boldsymbol{\theta})$$

and

$$\forall i \ X_i \in \mathcal{X}$$

where $$\mathcal{X}$$ is a finite set called the **source alphabet** and $$\boldsymbol{\theta}$$ is a vector describing the probabilities that a given $$X_i$$ will take on a given value in $$\mathcal{X}$$.   

Before communicating each source symbol $X_i$ to Person B, Person A will first *encode* each symbol using a **code function** $$C$$.  The code function $$C$$ takes as input a source symbol and outputs a sequence of symbols from a new set of symbols called the **code alphabet**, denoted $$\mathcal{A}$$. Specifically, if we denote $$\mathcal{A}^*$$ to be the *set of sequences* of code symbols 

$$\mathcal{A}^* := \{a_1, a_2, \dots, a_k \mid k \geq 0, \forall i a_i \in \mathcal{A}\}$$

then $$C$$ is a function

$$C: \mathcal{X} \rightarrow \mathcal{A}^*$$

We can also describe another function, $$C^*$$ called the **extension** of $$C$$, which simply maps *sequences* of source symbols rather than individual source symbols.  That is, 

$$C^* : \mathcal{X}^* \rightarrow \mathcal{A}^*$$

defined as

$$C^*(X_1, X_2, \dots, X_m) := C(X_1), C(X_2), \dots, C(X_m)$$

We call each element $$\alpha$$ in the image of $$C$$ (i.e. $$C(\mathcal{X})$$) a **code word**. We denote the length of a code word $$\alpha \in C(\mathcal{X})$$ as $$\vert\alpha\vert$$. 

For the purposes of our discussion, we will focus only on **uniquely decodable** code functions. A code function is uniquely decodable if it is an invertible function. Stated plainly, if a code $$C$$ is uniquely decodable, then we can always decode the code words unambiguously into the original sequence of source symbols using the inverse of $$C$$.  Most codes used in practice are uniquely decodable. A non-uniquely decodable code would not be very useful since Person B who receives the encoded message from Person A would be unable to unambiguously decode Person A's message.

Example: Morse Code
------------

[Morse Code](https://en.wikipedia.org/wiki/Morse_code) is a code for encoding the English alphanumeric symbols into "dots" and "dashes" that has been used in a variety of contexts such as in the early days of telecommunication when messages were sent by telegraph. In Morse Code, the source alphabet, $$\mathcal{X}$$, code alphabet $$\mathcal{A}$$, and code function $$C$$ are as defined as follows:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/MorseCode.png" alt="drawing" width="400"/></center>

For example, the name "Morse" would be encoded as follows:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/morse_code_example.png" alt="drawing" width="400"/></center>

In the above example, the length of code word "$$\cdot$$ - $$\cdot$$" (i.e. $$C(X_3)$$) is simply 3.  

The Kraft-McMillan inequality
------------

The Kraft-McMillan inequality is a fundamental result on which Shannon's Source Coding Theorem is based.  Before stating this theorem, we will first introduce a few more concepts related to code functions.

First, we call a code function a **prefix codes**.

