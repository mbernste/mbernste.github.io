
Introduction
-----------

Statistical hypothesis testing and machine learning-based binary classification are two very different frameworks for making binary decisions with data. A [recent article](https://doi.org/10.1016/j.patter.2020.100115) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given decision-problem at hand. Indeed, the two strategies are very different given that they were born from two different scientific fields (statistics and computer science). Understanding these differences as well as the strengths and weaknesses of each is vital for choosing the right strategy. Nonetheless, I also think it is helpful to understand how these two strategies are similar. In this post, I will create a unified framework for thinking about decision-making algorithms at large and will place statistical testing and machine learning into this common conceptual framework.

Binary decision making with data
----------

The problem we're interested in addressing is the following: we're given data, $X$, describing some object or sample and we want to determine whether that sample belongs to one of two categories.  There are many scenarios that fit this description. For example, $X$ might be an image of either a cat or a dog and we are interested in classifying which it is. A very different example would be that $X$ is a sample of datapoints (e.g., test scores) from two populations (e.g., students from two different schools) and we are interested in deciding whether the true means of the two groups as a whole are equal based upon our observed, but limited sample $X$.  This is a binary classification problem in that we are interested in inferring whether the two means are or are not different. 

Traditionally, machine learning is used for examples like the former (classifying images as either cats or dogs) and hypothesis testing is used for the latter (deciding whether the mean score between two populations of students are equal). While indeed machine learning is usually a better fit for problems similar to the former and statistical testing for the latter, this does not necessarily have to be the case. Both of these problems can be cast as the problem of making a binary decision between two choices, which can be addressed by either machine learning or hypothesis testing.  The [article](https://doi.org/10.1016/j.patter.2020.100115) by Li and Tong discuss the strengths of both methods.



