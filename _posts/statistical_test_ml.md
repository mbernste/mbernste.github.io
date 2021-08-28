---
title: 'Hypothesis testing versus machine learning: A unified perspective'
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

Statistical hypothesis testing and supervised machine learning are two different frameworks that can be used for making decisions with data. A [recent article by Bzdok et al.](https://www.nature.com/articles/nmeth.4642) differentiates statistical testing from supervised machine learning by arguing that the two approaches address different tasks: namely, _inference_ and _prediction_ respectively. [Another article](https://doi.org/10.1016/j.patter.2020.100115) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given problem. Indeed, the two strategies are very different; they were born from two different scientific fields -- statistics and computer science -- and are generally best-suited for different kinds of problems. However, in this post, I will attempt to argue that these two frameworks are not as different as they seem.

Specifically, I will argue that statistical testinng and supervised machine learning are similar in the following ways: First, I argue that at a high level, they address the same task: making claims about an unknown variable using data.  I argue that "prediction" and "inference" can be viewed as the same thing -- namely, they are the act of claiming something about an unknown variable. Second, both statistical testing and supervised machine learning often require some form of training data. In hypothesis testing, this prior information takes the form of a null distribution. In supervised learning, this prior information is the training set. Third, and finally, both methods require assumptions about the data.

Before digging into these commonalities, I will provide a very brief (and not comprehensive) review of the binary classification task, hypothesis testing, and supervised machine learning.  The language and mathematical notation I use will be a sort of hybrid between the language and notation traditionally used in statistics and machine learning. My goal is to highlight the similarities between the two approaches. 

Prediction versus inference
----------

A [recent article by Bzdok et al.](https://www.nature.com/articles/nmeth.4642) differentiates statistical testing from supervised machine learning by arguing that the two approaches address different tasks: namely, _inference_ and _prediction_ respectively. The article does not provide a rigorous definition for these tasks, but let me take a stab at it. In an inference task, we are presented with some set of data $$X$$ and we seek to use $$X$$ to make some claim about some unknown variable $$Y$$. For example, we might be interested in the fraction of voters in a given state that support a political candidate. We have access to polling data $$X$$ with the voting intentions for some limited number of voters and we wish to make some claim about the fraction of _all_ voters that support the candidate. We use the polling data $$X$$ to _infer_ the value of $$Y$$.

In the prediction task, we are again presented with some set of data $$X$$, and we wish to use $$X$$ to predict the future value of some variable $$Y$$.  For example, in a healthcare setting, $$X$$ might be a patient's clinical data and we want to predict whether the patient will suffer from some adverse health event. That is, we can let $$Y$$ be the patient's binary outcome as to whether they do or do not suffer the event.


In both prediction and inference we are simply using data to make a claim about an unknown variable. Whether that variable exists in the present, but is unobserved (inference), or exists in the future (prediction) is, in my opinion, not an important distinction. Both problems have the same structure and can be addressed with the same methods!

Making claims about unknown binary variables
---------------

The problem we're interested in addressing is the following: we're given data, $X$, describing some object, or sample, and we want to use $X$ in order to make some kind of binary decision between two choices $C_0$ or $C_1$. We'll use the variable $Y$ to denote the correct choice and thus, we are attempting to determine whether $Y = C_0$ or $Y = C_1$.  

There are many scenarios that fit this description. For example, $X$ might be an image of either a cat or a dog and we are interested in classifying which it is. In this case, $Y$ is the decision regarding whether the image is of a cat or dog. A very different example would be that $X$ is a sample of datapoints -- for example, test scores from two groups of students, and we are interested in deciding whether the true (unobserved) means of the two groups' scores are equal based upon our observed, but limited data $X$.  Here, $C_0$ might be the conclusion that the two groups of students have the same underlying test scores whereas $C_1$ is the conclusion that the two groups' mean scores differ.

Traditionally, machine learning is used for examples like the former (classifying images as either cats or dogs) and hypothesis testing is used for the latter (deciding whether the mean scores between two populations of students are equal). While indeed machine learning is usually a better fit for problems similar to the former and statistical testing for the latter (see the [article](https://doi.org/10.1016/j.patter.2020.100115) by Li and Tong), this does not necessarily have to be the case. Both of these problems can be cast as the problem of making a binary decision between two choices, which can be addressed by either hypothesis testing or machine learning.

A brief review of hypothesis testing  
-----------

In hypothesis testing, we summarize our data $X$ using a summarization function $T$ called a **statistic**. For example, if $X$ consists of test scores for a sample of students, then $T$ might be a function that simply computes the mean test score.  When performing hypothesis testing, one makes the very strong assumption that if one of the two choices, say $C_0$, is correct, then $T(X)$ will follow a specified distribution.  In hypothesis testing parlance, this distribution is called the [null distribution](https://en.wikipedia.org/wiki/Null_distribution#:~:text=Null%20distribution%20is%20a%20tool,is%20said%20to%20be%20true) which we'll denote as $P_{\text{null}}$.  In hypothesis testing, one computes the probability of drawing a sample from the null distribution that is "at least as extreme" as $T(X)$.  This probability is called a [p-value](https://en.wikipedia.org/wiki/P-value): 

$$\text{p-value} := \int P_{\text{null}}(x) \ \mathbb{I}(x \ \text{is more extreme than} \ T(X)) \ dx$$

where $\mathbb{I}$ is the indicator function.

A low p-value means that the null distribution is a poor explanation for our observed $T(X)$ and that we should look elsewhere for an explanation of $X$.  That is, a low p-value supports the choosing the alternate category, $C_1$, for $X$ rather than $C_0$ (making this choice is called "rejecting the null hypothesis"; the null hypothesis is the hypothesis that the null distribution produced $T(X)$). Traditionally, one pre-specifies a threshold, $\alpha$, such that if the p-value is below $\alpha$, one chooses $C_1$ rather than $C_0$.

In mathematical notation, the decision function, $f$, that outputs our choice of $C_0$ versus $C_1$ is:

$$f(T(X)) := \begin{cases}C_1  \ \text{if} \ \text{p-value} < \alpha \\  C_0  \ \text{otherwise} \end{cases}$$

A brief review of supervised machine learning
-----------------

In supervised machine learning for binary classification, our data $X$ is summarized using a summarization function $T$ in a similar manner to hypothesis testing.  In machine learning, $T(X)$ are called [features](https://en.wikipedia.org/wiki/Feature_selection) of $X$ and are usually a numerical vector.  Furthermore, to use machine learning, one is required to have on hand a set of *training examples* consisting of items and their associated correct decisions. We denote these item-decision pairs as 

$$\mathcal{D} := (X_1, Y_1), (X_2, Y_2), \dots, (X_n, Y_n)$$ 

Then, given these training examples, we employ a **learning algorithm** that looks at these data and finds a decision function, $f$, that will perform the binary decision when given some $T(X)$.  

If one views the learning algorithm itself as a function, $\mathcal{A}$, that takes as input a training set $\mathcal{D}$ and outputs a decision function $f$, then we can formulate the complete machine learning-based decision making algorithm as:

$$f(T(X)) := \mathcal{A}(\mathcal{D})(T(X))$$

where $\mathcal{A}(\mathcal{D})$ is the decision function output by the learning algorithm $\mathcal{A}$ when trained on dataset $\mathcal{D}$.

Both approaches may require "training" data
-----------------

The use of training data in machine learning is obvious; training models using examples is the entire premise of the field! On the other hand, the use of training data in hypothesis testing is much less obvious, but I would argue is still present, at least in the development of hypothesis tests for complex problems.  Here, I use "training data" in a very loose sense to mean all data that was used by either person or machine to formulate the decision function $f$.  Im machine learning, $f$ is output by the learning algorithm $\mathcal{A}$.  In hypothesis testing, $f$ is handcrafted by a person. This handcrafting of $f$ almost always requires data. 

As an illustrative example, let's look at the problem of [identifying differentially expressed genes]() in [RNA-seq](https://mbernste.github.io/posts/rna_seq_basics/) data.  In this problem, one is given two conditions on which we measure the expression of a set of genes. We are interested in identifying the subset of genes whose mean expression differs between the two conditions.  This fundamental problem has been addressed by a multitude of approaches in bioinformatics.

Both approaches require assumptions about the data
-----------------

It is obvious that hypothesis testing requires one to make strong assumptions about the data. These assumptions take the form of the null distribution -- that is, we assume a probability distribution over $T(X)$ conditioned on $Y = C_0$.  If data as extreme as $T(X)$ looks unlikely under the null distribution, we choose $C_1$.

In supervised machine learning, the assumptions made about the data are less obvious, but they are always present. In fact, their presence is a mathematical certainty! The [No Free Lunch Theorem]() in statistical learning theory states that no machine learning algorithm will work for every possible distribution of data. That is, ANY algorithm will work well on some distributions and poorly on others. One can view the distributions on which the model works well as the assumptions that the model is making about the data. These assumptions are often called the **inductive bias** of the algorithm.  

Here are a few examples of some inductive biases of well-known algorithms:
* [Logistic regression](https://en.wikipedia.org/wiki/Logistic_regression) assumes that the individual elements of $T(X)$ (assuming $T(X)$ is a feature vector) contribute additively and independently to the likelihood that $C_1$ is a better choice than $C_0$. 
* [Convolutional neural networks](https://en.wikipedia.org/wiki/Convolutional_neural_network) assume that useful groups of elements within $T(X)$ ($T(X)$ is assumed to be a tensor) are invariant to spatial shifts and rotations. If this is not the case, then convolutional neural networks might not be the best choice.

Inference vs. prediction: are these two different things?
-----------------

A [recent article by Bzdok et al.](https://www.nature.com/articles/nmeth.4642) differentiates statistical testing from supervised machine learning by arguing that the two approaches address different tasks: namely, _inference_ and _prediction_ respectively. The article does not provide a rigorous definition for these tasks, but let me take a stab at it. In an inference task, we are presented with some set of data $$X$$ about some system that in some way helps us make a claim about an unobserved characteristic of the system, call it $$Y$$. In the prediction task, we are again presented with some set of data $$X$$ about the system, and we wish to use $$X$$ to predict the future value of some variable $$Y$$.  For example, in a healthcare setting, $$X$$ might be a patients clinical data and we want to predict whether the patient will suffer from some adverse health event. That is, we can let $$Y \in \{\text{True}, \text{False}\}$$ be the patient's binary outcome as to whether they do or do not suffer the event.





Nonetheless, there are problems for which the best method is not so obvious. Such problems are often found in computational biology. For example, inferring [gene regulatory networks](https://en.wikipedia.org/wiki/Gene_regulatory_network) is a problem that has been addressed using [both hypothesis testing and supervised machine learning](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2217-z). On the surface, the biggest difference between hypothesis testing and supervised machine learning is that one approach requires training data while the other does not.  That is, machine learning requires training data, but (seemingly) few assumptions about the data whereas hypothesis testing requires (seemingly) no training data, but requires strong assumptions about the data (in the form of the null distribution). This appears to be a huge difference! 

In the remainder of this blog post, I will argue that this difference is not as vast as it seems.  When dealing with complex data, such as for applications in computational biology, the development of a novel hypothesis test requires looking at a lot of data!  In some sense, one can view this as "learning" or "training", even though it isn't being performed by a machine, rather, it's being performed by a statistician.  Conversely, all machine learning algorithms make assumptions about the data; they just do so a bit more implicitly than hypothesis testing.  These implicit assumptions, sometimes called *inductive biases* , are are made by all learning algorithms.

