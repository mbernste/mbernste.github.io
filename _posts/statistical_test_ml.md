
Introduction
-----------

Statistical hypothesis testing and machine learning-based binary classification are two very different frameworks for making binary decisions with data. A [recent article](https://doi.org/10.1016/j.patter.2020.100115) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given binary decision problem at hand. Indeed, the two strategies are very different given that they were born from two different scientific fields (statistics and computer science). Understanding these differences, as well as the strengths and weaknesses of each, is vital for choosing the appropriate strategy for one's problem. Nonetheless, I also think it is helpful to understand how these two strategies are similar. In this post, I will create a unified framework for thinking about decision-making algorithms at large and will place hypothesis testing and machine learning into this common conceptual framework.  This post will take a more machine learning-centric perspective.

Binary decision making with data
----------

The problem we're interested in addressing is the following: we're given data, $X$, describing some object or sample and we want to determine whether that sample belongs to one of two categories.  There are many scenarios that fit this description. For example, $X$ might be an image of either a cat or a dog and we are interested in classifying which it is. A very different example would be that $X$ is a sample of datapoints (e.g., test scores) from two populations (e.g., students from two different schools) and we are interested in deciding whether the true means of the two groups as a whole are equal based upon our observed, but limited sample $X$.  This is a binary classification problem in that we are interested in inferring whether the two means are or are not different. 

Traditionally, machine learning is used for examples like the former (classifying images as either cats or dogs) and hypothesis testing is used for the latter (deciding whether the mean score between two populations of students are equal). While indeed machine learning is usually a better fit for problems similar to the former and statistical testing for the latter, this does not necessarily have to be the case. Both of these problems can be cast as the problem of making a binary decision between two choices, which can be addressed by either machine learning or hypothesis testing.  The [article](https://doi.org/10.1016/j.patter.2020.100115) by Li and Tong discuss the strengths of both methods.

A quick overview of hypothesis testing and machine learning-based classification
-----------

Before we get started, I will provide a very brief (and not comprehensive) description of the two frameworks.  The language I choose to use will attempt to highlight the similarities between the two approaches.  

In hypothesis testing, we summarize our data $X$ using a summarization function $T$, thereby computing $T(X)$.  In hypothesis testing, $T(X)$ is called the **test statistic**.  When performing hypothesis testing, one makes the very strong assumption that if $X$ belongs to one of the two categories, which we'll denote $C_0$, then $T(X)$ will follow a specified distribution.  In hypothesis testing parlance, this distribution is called the [null distribution](https://en.wikipedia.org/wiki/Null_distribution#:~:text=Null%20distribution%20is%20a%20tool,is%20said%20to%20be%20true). We'll denote the null distribution as $P_{C_0}$.  In hypothesis testing, one computes the probability of drawing a sample from the null distribution that is "at least as extreme" as $T(X)$.  This probability is called a [p-value](https://en.wikipedia.org/wiki/P-value). 

$$\text{p-value} := \int \text{extremeness}(x, T(X)) P_{C_0}(x) \ \dx$$

A low p-value means that the null distribution is a poor explanation for our observed $T(X)$ and that we should look elsewhere for an explanation of our data $X$.  That is, a low p-value supports the choosing the alternate category, $C_1$ for $X$ rather than $C_0$ (called "rejecting the null hypothesis"; the null hypothesis is the hypothesis that the null distribution produced $T(X)$). Traditionally, one pre-specifies a threshold such that if the p-value is below the given threshold, one chooses $C_1$ rather than $C_0$.

In machine learning-based binary classification, our data $X$ is also summarized using some summarization function $T$.  In machine learning, $T(X)$ are called [features](https://en.wikipedia.org/wiki/Feature_selection) of $X$. (Note, in hypothesis testing $T(X)$ is usually a single number and in machine learning $T(X)$ is usually a numeric vector).  




