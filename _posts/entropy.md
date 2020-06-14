
Foundations of information theory: what is information? (part 2)

*The mathematical field of information theory attempts to mathematically describe the concept of “information”. In this series of posts, I will attempt to describe my understanding of how, both philosophically and mathematically, information theory defines the polymorphic, and often amorphous, concept of information. In the first post, we discussed the concept of self-information. In this second post, we will build on this foundation to discuss the concept of information entropy.*

Introduction
-----------

In the [first post](https://mbernste.github.io/posts/self_info/) of this series, we discussed how Shannon's Information Theory defines the information content of an event as the degree of surprise that an agent experiences when the event occurs. We discussed how surprise intuitively should correspond to probability in that an event with low probability elicits more surprise because it is unlikely to occur.  Thus, in information theory, information is a function, $I$, called **self-information**, that operates on probability values $p \in [0,1]$:

$$I(p) := -\log p$$

One strange thing about this equation is that it seems to change with respect to the base of the logarithm. Why is that? In this post, we will connect this idea of "information as surprise" to another angle from which we can view information: "information as an efficiency of communication".  This perspective starts to take more shape when we introduce the concept of information **entropy**.  After introducing this concept, it will become clear that the base of the logarithm used in $I$ corresponds to the number of symbols that we assume we are utilizing to communicate the outcome of the event.

Introducing information entropy
-----------

Given an event within a [probability space](), self-information describes the information content inherent in that event occuring. The concept of **information entropy** extends this idea to discrete random variables.  Given a random variable $X$, the entropy of $X$, denoted $H(X)$ is simply the expected self-information over its outcomes:

$$H(X) := E\left[I(P(X))\right] = -\sum_{x \in \mathcal{X}}P(X)\log P(X)$$

where $P$ is the probability mass function of $X$ and $\mathcal{X}$ is the codomain of $X$.

Said differently, the entropy of $X$ is simply the average self-information over all of the possible outcomes of $X$.  Intuitively, since self-information describes the degree of surprise of an event, the entropy of a random variable tells us, on average, how surprised we are going to be by the outcome of the random variable.

A discrete random variable that is certain to be only one value (e.g., with probability 1 $X = a$), the outcome of this random variable would not be surprising at all -- we already know its outcome! Therefore, it's entropy should be zero.

In contrast, a uniform discrete random variable (such as one describing a fair-coin), will always surprise us because we have no idea which of the outcomes will occur -- they are all equally likely!  Intuitively, a uniform random variable should have a high entropy.  In fact, the entropy of a discrete random variable $X$ is maximal when probabilities is uniformly distributed over its outcomes.

In the figure below, we plot the entropy of a Bernoulli random variable (i.e. a coin flip) over its parameter $\theta$ (i.e. the probability that the coin comes up heads):






