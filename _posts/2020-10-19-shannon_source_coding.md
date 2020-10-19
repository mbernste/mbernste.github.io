---
title: 'Foundations of information theory: Shannon's Source Coding Theorem (part 3)'
date: 2020-10-19
permalink: /posts/source_coding/
tags:
  - information theory
  - tutorial
---
THIS POST IS CURRENTLY UNDER CONSTRUCTION

*The mathematical field of information theory attempts to mathematically describe the concept of “information”. In the first two posts, we discussed the concepts of self-information and information entropy.  In this post, we step through Shannon's Source Coding Theorem to see how information entropy of a probability distribution describes the best-achievable efficiency required to communicate samples from the distribution.  My understanding of this material came, in part, from watching this excellent series of videos by [mathematicalmong on YouTube](https://www.youtube.com/watch?v=UrefKMSEuAI&t=8s)*

Introduction
-----------

Recall from the previous post, we discussed how the information entropy of a random variable tells you, on average, the minimum number of symbols that you will need to use to communicate the outcome of a random variable. That is, let us say we have two people, Person A and Person B, who are trying to communicate with one another. Specifically, Person A is observing samples, drawn one at a time, from some distribution X. Person A then wishes to communicate each sample to Person B. For example, $$X$$ might be a coin and Person A wishes to communicate to Person B the outcomes of repeated coin flips.

The catch is that Person A must use a sequence of symbols from some alphabet to communicate these outcomes. For example, Person A may be restricted to communicate using only two symbols, say “1” and “0” (called bits). For example, messages in Morse Code are encoded using bits (i.e. dots and dashes) as are messages stored in modern computers. Using these symbols, Person A must construct a code made from these symbols to communicate these outcomes (we assume that Person B always knows the code). Interestingly, according to Shannon’s Source Coding Theorem, no matter how Person A construct’s their code, in expectation, Person A will need to use at least the entropy of $$X$$ number of symbols, denoted $$H(X)$$, to communicate each outcome. No matter how clever, Person A will never be able to construct a code such that their average message will be smaller than $$H(X)$$. Said differently, entropy provides a lower bound on the average size of each message that Person A transmits to Person B.

Let us more rigorously prove this idea.

Encoding and communicating samples from a distribution
-----------

As we previously described, Person A is tasked with communicating the outcomes from some distribution $$X$$ to Person B.  We will call these samples the **sequence of source symbols**: 

$$X_1, X_2, X_3, \dots \in \mathcal{X}$$

where $$\mathcal{X}$$ is a finite set called the **source alphabet**. For example, $$\mathcal{X}$$ might simply be the standard English alphabet, or it may be the results of a coin flip $$\{H, T\}$$ where $$H$$ indicates heads and $$T$$ indicates tails.

Each source symbol $$X_i$$ is distributed according to a categorical random variable:

$$X_i \sim \text{Cat}(p_1, \dots, p_m)$$

where $$p_i$$ denotes the probability that $$X_i$$ will take on the $$i$$th symbol in $$\mathcal{X}$$. For example, in the coin flip example where $$\mathcal{X} := \{H, T\}$$, we may have be dealing with a biased coin where $$X_i \sim \text{Cat}(0.7, 0.3)$$ such that there is a 0.7 probability that $$X_i$$ comes up heads and a 0.3 probability that $$X_i$$ comes up tails.

