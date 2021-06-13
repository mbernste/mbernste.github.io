---
title: 'Binary classification with hypothesis testing and machine learning: A unified framework'
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

Statistical hypothesis testing and machine learning-based binary classification are two very different frameworks for making binary decisions with data. A [recent article](https://doi.org/10.1016/j.patter.2020.100115) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given binary decision problem at hand. Indeed, the two strategies are very different given that they were born from two different scientific fields (statistics and computer science) and are generally best-suited for different kinds of problems. Understanding these differences, as well as the strengths and weaknesses of each, is vital for choosing the appropriate strategy for one's problem. Nonetheless, I also think it is helpful to understand how these two strategies are similar. In this post, I will emphasize the similarities between the two approaches and present a framework for thinking about these two approaches as belonging to two ends of a continuum defined by the well-known [bias-variance tradeoff](https://en.wikipedia.org/wiki/Bias%E2%80%93variance_tradeoff). 

Before discussing this continuum, I will provide a very brief (and not comprehensive) review of the binary classification task, hypothesis testing, and machine learning.  The language and mathematical notation I use will be a sort of hybrid between the language and notation traditionally used in statistics and machine learning. My goal is to highlight the similarities between the two approaches. 


Binary decision making with data
----------

The problem we're interested in addressing is the following: we're given data, $X$, describing some object or sample and we want to use $X$ in order to make some kind of binary decision between two choices $C_0$ or $C_1$. We'll use the variable $Y$ to denote the correct choice and thus, we are attempting to determine whether $Y = C_0$ or $Y = C_1$.  

There are many scenarios that fit this description. For example, $X$ might be an image of either a cat or a dog and we are interested in classifying which it is. In this case, $Y$ is the decision regarding whether the image is of a cat or dog. A very different example would be that $X$ is a sample of datapoints (e.g., test scores) from two populations (e.g., students from two different schools) and we are interested in deciding whether the true (unobserved) means of the two groups as a whole are equal based upon our observed, but limited sample $X$.  Here, $C_0$ might be the decision that indeed the two groups of students have the same underlying test scores whereas $C_1$ is that the two groups differ.

Traditionally, machine learning is used for examples like the former (classifying images as either cats or dogs) and hypothesis testing is used for the latter (deciding whether the mean score between two populations of students are equal). While indeed machine learning is usually a better fit for problems similar to the former and statistical testing for the latter (see the [article](https://doi.org/10.1016/j.patter.2020.100115) by Li and Tong), this does not necessarily have to be the case. Both of these problems can be cast as the problem of making a binary decision between two choices, which can be addressed by either hypothesis testing or machine learning.

A quick overview of hypothesis testing  
-----------

In hypothesis testing, we summarize our data $X$ using a summarization function $T$ called a **statistic**. For example, if $X$ consists of test scores for a sample of students, then $T$ might be a function that simply computes the mean test score.  When performing hypothesis testing, one makes the very strong assumption that if one of the two choices, say $C_0$, is correct, then $T(X)$ will follow a specified distribution.  In hypothesis testing parlance, this distribution is called the [null distribution](https://en.wikipedia.org/wiki/Null_distribution#:~:text=Null%20distribution%20is%20a%20tool,is%20said%20to%20be%20true) which we'll denote as $P_{\text{null}}$.  In hypothesis testing, one computes the probability of drawing a sample from the null distribution that is "at least as extreme" as $T(X)$.  This probability is called a [p-value](https://en.wikipedia.org/wiki/P-value): 

$$\text{p-value} := \int P_{\text{null}}(x \mid x \ \text{is more extreme than} \ T(X)) \ dx$$

A low p-value means that the null distribution is a poor explanation for our observed $T(X)$ and that we should look elsewhere for an explanation of our data $X$.  That is, a low p-value supports the choosing the alternate category, $C_1$, for $X$ rather than $C_0$ (making this choice is called "rejecting the null hypothesis"; the null hypothesis is the hypothesis that the null distribution produced $T(X)$). Traditionally, one pre-specifies a threshold, $\alpha$, such that if the p-value is below $\alpha$, one chooses $C_1$ rather than $C_0$.

In mathematical notation, this decision function is:

$$f(T(X)) := \begin{cases}C_1  \ \text{if} \ \mathbb{I}\left(\text{p-value} < \alpha \right) = 1 \\  C_0  \ \text{otherwise} \end{cases}$$

where $\mathbb{I}$ is the indicator function.

A quick overview of machine learning-based classification
-----------------

In machine learning-based binary classification, our data $X$ is also summarized using some summarization function $T$.  In machine learning, $T(X)$ are called [features](https://en.wikipedia.org/wiki/Feature_selection) of $X$. (Note, in hypothesis testing $T(X)$ is usually a single number and in machine learning $T(X)$ is usually a numeric vector).  Furthermore, to use machine learning, one is required to have on hand a set of *training examples* consisting of items and their associated correct decisions. We denote these item-decision pairs as 

$$\mathcal{D} := (X_1, Y_1), (X_2, Y_2), \dots, (X_n, Y_n)$$ 

Then, given these samples, we employ a **learning algorithm** that looks at the data and finds a decision function, $f$, that will map a given item's features, $T(X)$, to a category.  

If one views the learning algorithm itself as a function, $\mathcal{A}$, that takes as input a training set $\mathcal{D}$ and outputs a decision function $f$, then we can formulate the complete machine learning-based decision making algorithm as:

$$f(T(X)) := \mathcal{A}(\mathcal{D})(T(X))$$

where $\mathcal{A}(\mathcal{D})$ is the decision function output by the learning algorithm $\mathcal{A}$ when trained on dataset $\mathcal{D}$.

A continuum of decision-making algorithms
-----------

On the surface, the biggest difference between hypothesis testing and machine learning-based classification is that one approach requires training data the other does not.  That is, machine learning requires training data, but little assumptions about the data whereas hypothesis testing requires no training data, but does require assumptions about the data in the form of the null distribution. This seems to be a huge difference! 

In the remainder of this blog post, I will argue that this difference is not as vast as it seems.  When dealing with complex data, such as for applications in computational biology, the development of a novel hypothesis test requires that the developer looks at a lot of data! In converse, all machine learning algorithms make assumptions about the data; they just do so a bit more implicitly than hypothesis testing.  Thus, I argue that both hypothesis testing and machine learning algorithms lie at two ends of the [bias-variance tradeoff](https://en.wikipedia.org/wiki/Bias%E2%80%93variance_tradeoff)!

Inductive bias and the bias-variance tradeoff
-----------

A central idea in statistical learning theory is the inductive bias of a learning algorithm.  Roughly speaking, the inductive bias of an algorithm are of the assumptions that the algorithm will bring to the table when attempting to find a decision function that will accurately make decisions from data.  If an algorithm has very strong assumptions about what the data will look like, and the underlying process that generated them, then the algorithm will perform very poorly if the data does not meet the algorithm's assumptions.  This problem can be mitigated by 

