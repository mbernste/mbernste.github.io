---
title: 'Hypothesis testing versus binary classification: A unified framework'
date: 2021-06-13
permalink: /posts/hypothesis_vs_ml/
tags:
  - machine learning
  - statistics
  - tutorial
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
-----------

Statistical hypothesis testing and machine learning-based binary classification are two very different frameworks for making binary decisions with data. A [recent article](https://doi.org/10.1016/j.patter.2020.100115) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given binary decision problem at hand. Indeed, the two strategies are very different given that they were born from two different scientific fields (statistics and computer science). Understanding these differences, as well as the strengths and weaknesses of each, is vital for choosing the appropriate strategy for one's problem. Nonetheless, I also think it is helpful to understand how these two strategies are similar. In this post, I will emphasize the similarities between the two approaches. To do so, I will create a unified continuum for thinking about decision-making algorithms at large and will place hypothesis testing and machine learning into this common conceptual framework.  This post will take a more machine learning-centric perspective.

Binary decision making with data
----------

The problem we're interested in addressing is the following: we're given data, $X$, describing some object or sample and we want to determine whether that sample belongs to one of two categories: $C_0$ or $C_1$. We'll use the variable $Y$ to denote the true category of $X$. Thus, we are attempting to determine whether $Y = C_0$ or $Y = C_1$.  

There are many scenarios that fit this description. For example, $X$ might be an image of either a cat or a dog and we are interested in classifying which it is. A very different example would be that $X$ is a sample of datapoints (e.g., test scores) from two populations (e.g., students from two different schools) and we are interested in deciding whether the true means of the two groups as a whole are equal based upon our observed, but limited sample $X$.  This is a binary classification problem in that we are interested in inferring whether the two means are or are not different. 

Traditionally, machine learning is used for examples like the former (classifying images as either cats or dogs) and hypothesis testing is used for the latter (deciding whether the mean score between two populations of students are equal). While indeed machine learning is usually a better fit for problems similar to the former and statistical testing for the latter, this does not necessarily have to be the case. Both of these problems can be cast as the problem of making a binary decision between two choices, which can be addressed by either machine learning or hypothesis testing.  The [article](https://doi.org/10.1016/j.patter.2020.100115) by Li and Tong discuss the strengths of both methods.

A quick overview of hypothesis testing and machine learning-based classification
-----------

Before we get started, I will provide a very brief (and not comprehensive) description of the two frameworks.  The language and mathematical notation I use will attempt to highlight the similarities between the two approaches. 

In hypothesis testing, we summarize our data $X$ using a summarization function $T$, thereby computing $T(X)$.  In hypothesis testing, $T(X)$ is called the **test statistic**.  When performing hypothesis testing, one makes the very strong assumption that if $X$ belongs to one of the two categories, which we'll denote $C_0$, then $T(X)$ will follow a specified distribution.  In hypothesis testing parlance, this distribution is called the [null distribution](https://en.wikipedia.org/wiki/Null_distribution#:~:text=Null%20distribution%20is%20a%20tool,is%20said%20to%20be%20true). We'll denote the null distribution as $P_{\text{null}}$.  In hypothesis testing, one computes the probability of drawing a sample from the null distribution that is "at least as extreme" as $T(X)$.  This probability is called a [p-value](https://en.wikipedia.org/wiki/P-value): 

$$\text{p-value} := \int P_{\text{null}}(x \mid x \ \text{is more extreme than} \ T(X)) \ dx$$

A low p-value means that the null distribution is a poor explanation for our observed $T(X)$ and that we should look elsewhere for an explanation of our data $X$.  That is, a low p-value supports the choosing the alternate category, $C_1$, for $X$ rather than $C_0$ (making this choice is called "rejecting the null hypothesis"; the null hypothesis is the hypothesis that the null distribution produced $T(X)$). Traditionally, one pre-specifies a threshold such that if the p-value is below the given threshold, one chooses $C_1$ rather than $C_0$.

In machine learning-based binary classification, our data $X$ is also summarized using some summarization function $T$.  In machine learning, $T(X)$ are called [features](https://en.wikipedia.org/wiki/Feature_selection) of $X$. (Note, in hypothesis testing $T(X)$ is usually a single number and in machine learning $T(X)$ is usually a numeric vector).  In machine learning-based binary classification, one is required to have on hand a set of *training examples* consisting of items and their associated correct decisions. We denote these item-decision pairs as $(X_1, Y_1), (X_2, Y_2), \dots, (X_n, Y_n)$. Then, given these samples, we employ an algorithm to estimate the probability distribution:

$$P(Y = C_0 \mid T(X))$$

and assume that 

$$P(Y = C_1 \mid T(X)) = 1 - P(Y = C_0 \mid T(X))$$

Note that the null distribution from hypothesis testing can be viewed as

$$P_{null} := P(T(X) \mid Y = C_0)$$.


Hypothesis testing and machine learning are more similar than they appear
-----------

On the surface, the biggest difference between hypothesis testing and machine learning-based classification is that one approach does not require training data and the other does.  That is, hypothesis testing does not require training data, rather, it requires an assumption of the null distribution.  Machine learning on the other hand, requires training data to estimate the distribution of the data from scratch.  This seems to be a huge difference! 

In the remainder of this blog post, I will argue that this difference is not as vast as it seems.  In practice, the development of a novel hypothesis test requires that the developer looks at a lot of data! In converse, all machine learning algorithms make assumptions about the data -- they just do so a bit more implicitly than hypothesis testing.  Thus, I argue that both hypothesis testing and machine learning algorithms lie at two ends of a continuum of decision-making algorithms that is defined by the strength of the [inductive bias](https://en.wikipedia.org/wiki/Inductive_bias) made by the method!



