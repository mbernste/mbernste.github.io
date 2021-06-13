
Introduction
-----------

Statistical hypothesis testing and machine learning-based binary classification are two very different frameworks for making binary decisions with data. A [recent article](https://www.sciencedirect.com/science/article/pii/S2666389920301562) by Jingyi Jessica Li and Xin Tong discusses the differences between these two strategies and offers guidance on which one to choose for a given decision-problem at hand. Indeed, the two strategies are very different given that they were born from two different scientific fields (statistics and computer science). Understanding these differences as well as the strengths and weaknesses of each is vital for choosing the right strategy. Nonetheless, I also think it is helpful to understand how these two strategies are similar. In this post, I will create a unified framework for thinking about decision-making algorithms at large and will place statistical testing and machine learning into this common conceptual framework.

Hypothesis testing
----------

Let us quickly review the central mechanism behind hypothesis testing (this review will not serve as a complete description if you have not seen this material before). Born from the field of statistics, hypothesis testing is a framework for deciding whether the test statistic computed on a given data sample originated from a specified probability distribution, called the "null distribution".  More specifically, one computes the probability under the null distribution that data "at least as weird" as the observed data was sampled from the null (the phrase, "least as weird", depends on the problem and must be rigorously defined and quantified). This probability is called a p-value.  If the p-value is low, then one can proclaim that the observed data is not well explained by the null distribution and that one should look elsewhere for an explanation of the data. When this occurs, one "rejects" the "null hypothesis" -- that is, one rejects the hypothesis that the test statistic computed on the data was sampled from the null distribution. If on the other hand, the p-value is high, then null distribution serves as a reasonable explanation for the data.

Machine learning-based binary classification
----------

