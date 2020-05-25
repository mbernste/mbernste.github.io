
*The evidence lower bound is an important quantity at the core of a number of important algorithms used in statistical inference including expectation-maximization and variational inference. In this post, I describe where it comes from and how it relates to other concepts in probabilistic modeling.*

Introduction
----------

The **evidence lower bound (ELBO)** is an important quantity that lies at the core of the theoretical foundations of a number of important algorithms in probabilistic inference such as [expectation-maximization]() and variational infererence. To understand these algorithms, it is helpful to understand the ELBO.

Before digging in, let's review the probabilistic inference task for a latent variable model. In a latent variable model, we posit that our observed data $x$ is a realization from some random variable $X$. Moreoever, we posit the existence of another random variable $Z$ where $X$ and $Z$ are distributed according to a joint distribution $P(X, Z)$.  Unfortunately, our data is *only* a realization of $X$, not $Z$, and therefore $Z$ remains unobserved (i.e. latent).

To understand the evidence lower bound, we must first understand what we mean by "evidence".  The **evidence**, quite a simply, just a name given to the likelihood function evaluated at a fixed $\theta$:

$$\text{evidence} := \log p(x ; \theta)$$

Why is this quantity often called the "evidence"? Intuitively, if we have chosen the right model $p$ and $\theta$, then we would expect that the marginal probability of our observed data $x$, would be high. Thus, a higher value of $\log p(x ; \theta)$ indicates, in some sense, that we may be on the right track with the model $p$ and parameters $\theta$ that we have chosen.

If we happen to also know (or posit) that $Z$ follows some distribution given by $q$ (and that $p(x, z; \theta) := p(x \mid z ; \theta)q(z)$), then the evidence lower bound is, well, a lower bound on the evidence that makes use of $q$.  Specifically, 

$$\log p(x ; \theta) \geq E_{Z \sim q}\left[\log \frac{p(x,Z; \theta)}{q(Z)} \right]$$

where the ELBO is simply the right-hand side of the above equation:

$${ELBO} := E_{Z \sim q}\left[\log \frac{p(x,Z; \theta)}{q(Z)} \right]$$
