Perspectives on Expectation Maximization

Expectation Maximization (EM) is a popular algorithm for performing maximum-likelihood estimation for the parameters in a latent variable model. Introductory machine learning and bioinformatics courses often teach the Expectation Maximization algorithms for estimating parameters in important models such as [Guassian Mixture Models](https://en.wikipedia.org/wiki/Mixture_model#Gaussian_mixture_model) and [Hidden Markov Models](https://en.wikipedia.org/wiki/Baum–Welch_algorithm).

After learning about this algorithm in introductory graduate school courses, the intuition was clear, but I still had several remaining questions.  When is EM preferred over some other method for estimating parameters?  What is EM really doing? Why is EM guaranteed to converge?

In this blog post, I'll describe my current understanding of the theory behind the EM algorithm, which helped me to answer the aformentioned questions. I'll also offer a few perspectives for intuiting this algorithm.

The Setting
---------

As mentioned previously, EM is used for performing maximum likelihood estimation on the parameters of a latent variable model. To review this task, let's say we have two sets of random variables $X$ and $Z$ and some parameterized joint distribution over these random variables:

$$P(X, Z; \theta)$$

Where $\theta$ parameterizes the distribution.
