---
title: 'Hypothesis testing versus supervised machine learning: A unified framework'
date: 2021-06-14
permalink: /posts/hypothesis_vs_ml/
tags:
  - machine learning
  - statistics
  - tutorial
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
-----------

Statistical hypothesis testing and supervised machine learning are two very different frameworks for making binary decisions with data. A [recent article](https://doi.org/10.1016/j.patter.2020.100115) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given binary decision problem at hand. Indeed, the two strategies are very different given that they were born from two different scientific fields (statistics and computer science) and are generally best-suited for different kinds of problems. For some problems, the choice is obvious. For example, when attempting to decide whether the means between two groups differ based on a finite sample, then the obvious method to use is hypothesis testing. Alternatively, when attempting to classify images as being of either say, a dog or a cat, machine learning is often the much better choice. 

Nonetheless, there are problems for which the best method is not so obvious. Such problems are pervasive in computational biology. For example, inferring gene regulatory networks is a problem that has been addressed using [both hypothesis testing and supervised machine learning](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2217-z). Of course, understanding the differences between the two frameworks and their respective strengths and weaknesses, is vital for choosing the appropriate strategy for one's problem. However, I also think that understanding their similarities is important and I have not seen a comprehensive discussion that places these two strategies into a common conceptual framework. 

On the surface, the biggest difference between hypothesis testing and supervised machine learning is that one approach requires training data while the other does not.  That is, machine learning requires training data, but (seemingly) few assumptions about the data whereas hypothesis testing requires (seemingly) no training data, but requires strong assumptions about the data in the form of the null distribution. This seems to be a huge difference! In the remainder of this blog post, I will argue that this difference is not as vast as it seems.  When dealing with complex data, such as for applications in computational biology, the development of a novel hypothesis test requires looking at a lot of data!  In some sense, one can view this as "learning" or "training", even though it isn't being performed by a machine.  Conversely, all machine learning algorithms make assumptions about the data; they just do so a bit more implicitly than hypothesis testing.  These implicit assumptions, collectively called the **inductive bias** of a learning algorithm, are crucial to undersand when applying machine learning to a problem.

Before digging into these commonalities, I will provide a very brief (and not comprehensive) review of the binary classification task, hypothesis testing, and supervised machine learning.  The language and mathematical notation I use will be a sort of hybrid between the language and notation traditionally used in statistics and machine learning. My goal is to highlight the similarities between the two approaches. 

Making binary decisions with data
----------

The problem we're interested in addressing is the following: we're given data, $X$, describing some object or sample and we want to use $X$ in order to make some kind of binary decision between two choices $C_0$ or $C_1$. We'll use the variable $Y$ to denote the correct choice and thus, we are attempting to determine whether $Y = C_0$ or $Y = C_1$.  

There are many scenarios that fit this description. For example, $X$ might be an image of either a cat or a dog and we are interested in classifying which it is. In this case, $Y$ is the decision regarding whether the image is of a cat or dog. A very different example would be that $X$ is a sample of datapoints (e.g., test scores) from two populations (e.g., students from two different schools) and we are interested in deciding whether the true (unobserved) means of the two groups are equal based upon our observed, but limited sample $X$.  Here, $C_0$ might be the conclusion/decision that indeed the two groups of students have the same underlying test scores whereas $C_1$ is the conclusion that the two groups' mean scores differ.

Traditionally, machine learning is used for examples like the former (classifying images as either cats or dogs) and hypothesis testing is used for the latter (deciding whether the mean scores between two populations of students are equal). While indeed machine learning is usually a better fit for problems similar to the former and statistical testing for the latter (see the [article](https://doi.org/10.1016/j.patter.2020.100115) by Li and Tong), this does not necessarily have to be the case. Both of these problems can be cast as the problem of making a binary decision between two choices, which can be addressed by either hypothesis testing or machine learning.

A brief review of hypothesis testing  
-----------

In hypothesis testing, we summarize our data $X$ using a summarization function $T$ called a **statistic**. For example, if $X$ consists of test scores for a sample of students, then $T$ might be a function that simply computes the mean test score.  When performing hypothesis testing, one makes the very strong assumption that if one of the two choices, say $C_0$, is correct, then $T(X)$ will follow a specified distribution.  In hypothesis testing parlance, this distribution is called the [null distribution](https://en.wikipedia.org/wiki/Null_distribution#:~:text=Null%20distribution%20is%20a%20tool,is%20said%20to%20be%20true) which we'll denote as $P_{\text{null}}$.  In hypothesis testing, one computes the probability of drawing a sample from the null distribution that is "at least as extreme" as $T(X)$.  This probability is called a [p-value](https://en.wikipedia.org/wiki/P-value): 

$$\text{p-value} := \int P_{\text{null}}(x) \ \mathbb{I}(x \ \text{is more extreme than} \ T(X)) \ dx$$

where $\mathbb{I}$ is the indicator function.

A low p-value means that the null distribution is a poor explanation for our observed $T(X)$ and that we should look elsewhere for an explanation of $X$.  That is, a low p-value supports the choosing the alternate category, $C_1$, for $X$ rather than $C_0$ (making this choice is called "rejecting the null hypothesis"; the null hypothesis is the hypothesis that the null distribution produced $T(X)$). Traditionally, one pre-specifies a threshold, $\alpha$, such that if the p-value is below $\alpha$, one chooses $C_1$ rather than $C_0$.

In mathematical notation, this decision function is:

$$f(T(X)) := \begin{cases}C_1  \ \text{if} \ \mathbb{I}\left(\text{p-value} < \alpha \right) = 1 \\  C_0  \ \text{otherwise} \end{cases}$$

where $\mathbb{I}$ is the indicator function.

A brief review of supervised machine learning
-----------------

In supervised machine learning for binary classification, our data $X$ is summarized using a summarization function $T$ in a similar manner to hypothesis testing.  In machine learning, $T(X)$ are called [features](https://en.wikipedia.org/wiki/Feature_selection) of $X$ and are usually a numerical vector rather than a single number as is usually the case in hypothesis testing.  Furthermore, to use machine learning, one is required to have on hand a set of *training examples* consisting of items and their associated correct decisions. We denote these item-decision pairs as 

$$\mathcal{D} := (X_1, Y_1), (X_2, Y_2), \dots, (X_n, Y_n)$$ 

Then, given these training examples, we employ a **learning algorithm** that looks at these data and finds a decision function, $f$, that will make perform the binary decision when given $T(X)$.  

If one views the learning algorithm itself as a function, $\mathcal{A}$, that takes as input a training set $\mathcal{D}$ and outputs a decision function $f$, then we can formulate the complete machine learning-based decision making algorithm as:

$$f(T(X)) := \mathcal{A}(\mathcal{D})(T(X))$$

where $\mathcal{A}(\mathcal{D})$ is the decision function output by the learning algorithm $\mathcal{A}$ when trained on dataset $\mathcal{D}$.

Both approaches may require training data
-----------------

The use of training data in machine learning is obvious; training models using data is the whole point! On the other hand, the use of training data in hypothesis testing is much less obvious, but I would argue is still present, at least in the development of hypothesis tests for complex problems.  Here, I use "training data" in a very loose sense to mean all data that was used by either person or machine to formulate the decision function $f$.  Im machine learning, $f$ is output by the learning algorithm $\mathcal{A}$.  In hypothesis testing, $f$ is usually more handcrafted. Nonetheless, this handcrafting of $f$ almost always requires data. 

As an illustrative example, let's look at the problem of [identifying differentially expressed genes]() in [RNA-seq](https://mbernste.github.io/posts/rna_seq_basics/) data.  In this problem, one is given two conditions on which we measure the expression of a set of genes. We are interested in identifying the subset of genes whose mean expression differs between the two conditions.  This fundamental problem has been addressed by a multitude of approaches in bioinformatics.

Both approaches require assumptions about the data
-----------------

It is obvious that hypothesis testing requires one to make strong assumptions about the data. These assumptions take the form of the null distribution -- that is, we assume a probability distribution over $T(X)$ conditioned on $Y = C_0$.  If data as extreme as $T(X)$ looks unlikely under the null distribution, we choose $C_1$.

In supervised machine learning, the assumptions made about the data are less obvious, but they are always present. In fact, their presence is a mathematical certainty! The [No Free Lunch Theorem]() in statistical learning theory states that no machine learning algorithm will work for every possible distribution of data. That is, ANY algorithm will work well on some distributions and poorly on others. One can view the distributions on which the model works well as the assumptions that the model is making about the data. These assumptions are often called the **inductive bias** of the algorithm.  

Here are a few examples of some inductive biases of well-known algorithms:
* [Logistic regression]() assumes that the $Y$ is a linear function of $T(X)$. If this does not hold, then logistic regression may not work well!
* [Bayesian networks]() make explicit the expected distribution of the data and highlight the conditional dependencies between elements of $T(X)$. 
* [Convolutional neural networks]() assume that useful groups of elements within $T(X)$ are invariant to spatial shifts and rotations. If this is not the case, then convolutional neural networks might not be the best choice.

A note on "inference" versus "prediction"
-----------------

