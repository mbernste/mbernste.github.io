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

$$X_1, X_2, X_3, \dots, X_m \overset{\text{i.i.d.}}{\sim} \text{Cat}(\boldsymbol{p})$$
and
$$\forall i \ X_i \in \mathcal{X}$$
where $$\mathcal{X}$$ is a finite set called the **source alphabet** and $$\boldsymbol{p}$$ is a vector describing the probabilities that a given $$X_i$$ will take on a given value in $$\mathcal{X}$$.   

Person A will then *encode* each $$X_i$$ using a particular sequence of symbols from a **code alphabet**, denoted $$\mathcal{A}$$.  The coding alphabet is used by Person A to encode each source symbol $$X_i$$.  

Before communicating each source symbol $X_i$ to Person B, Person A will first *encode* each symbol using a **code function** $$C$$.  The code function $$C$$ takes as input a source symbol and outputs a sequence of code symbols from the code alphabet. Specifically, if we denote $$\mathcal{A}*$$ to be the set of sequences of source symbols 

$$\mathcal{A}* := \{a_1a_2\dots a_k \mid k \geq 0, \forall i a_i \in \mathcal{A}\}$$

then $$C$$ is a function

$$C: \mathcal{X} \rightarrow \mathcal{A}*$$

Example: Morse Code
------------

For example, in the die toss example where $$\mathcal{X} := \{1, 2, 3, 4, 5, 6\}$$, we may have be dealing with a biased die where $$X_i \sim \text{Cat}(0.1, 0.2, 0.1, 0.4, 0.1, 0.1)$$.

For example, in [Morse Code](https://en.wikipedia.org/wiki/Morse_code) the code alphabet consists of just two symbols: a dot and a dash.  That is, $$\mathcal{A} := \{\cdot, -\}.$$

For example, in messages in [Morse Code](https://en.wikipedia.org/wiki/Morse_code) are encoded using dots and dashes -- that is, in Morse Code $$\mathcal{A} := \{-, the letter "b" is encoded using \cdot \}$$.  The code function in Morse Code is simply the mapping from each English letter to a particular sequence of dots and dashes (e.g., 

For example, the letter "b" in Morse Code is encoded using the sequence "$$-\cdot\cdot\cdot$$".  
