


*In this series of posts, I present my understanding of some basic concepts in measure theory — the mathematical study of objects with “size”— that have enabled me to gain a deeper understanding into the foundations of probability theory.*

*In part 3, we will build from the measure-theoretic definitions for probability and random variables towards the measure-theoretic definition for the expectation of a random variable.*

Introduction
-------

So far, we have laid out some foundational definitions for a measure-theoretic treatment of probability. By doing so, we have unified the concepts of discrete random variables and continuous random variables, as are often taught in introductory courses.  Furthermore, this rigorous definition of random variables can describe non-numeric random variables.  

Now, we will discuss how expectation is defined for the more rigorous, measure-theoretic definition of a random variable. First, let's review the basic notion for the expected value of a random variable. 

Intuitively, the expected value of a random variable is the "average" value we would expect to see if we were able to repeatedly observe the random value of the random variable.  The expected value for a random variable $X$ is denoted $E(X)$.

In introductory courses, it is taught that the expectation for a discrete random variable is given by

$$E(X) := \sum_x xP(X = x)$$

whereas if $X$ is continuous its expectation is given by

$$E(X) := \int_x x f(x) \ dx$$

where $f(x)$ is $X$'s density function (see [part 2](https://mbernste.github.io/posts/measure_theory_2/) of this series for a description of a density function).  

Both of these definitions carry the same intuition -- that is, to compute the expectation of $X$ we take a weighted-average of all of the values of the random variable where the weights correspond to how likely that value is. Can we unify these two definitions using our new measure-theoretic definition for a random variable?

Expectation
---------

Recall, that measure-theoretic probability defines a random variable $X$ as a measurable function from some probability space $(\Omega, E, P)$ to a measurable space $(H,\mathcal{H})$.  The measure-theoretic treatment of probability then defines its expectation $E(X)$ as the following **Lebesgue integral**:

 $$E(X) := \int_{\omega \in \Omega} X(\omega) dP(\omega)$$
 
This may look pretty strange -- nothing like the Reimann integral that is usually taught in introductory calculus classes. Let's dig in.

Intuition behind Lebesgue integration
---------

Intuitively, for a given function $f$ whose codomain is numeric (i.e. the real numbers or a subset thereof), an integral measures the area under the function's surface.

When $f$ is smooth (i.e. both continuous and differentiable) within a given interval along its domain, we can approximate this area by summing rectangles under the curve. If we keep shrinking the rectangles then, in the limit, this becomes the Reimann integral, which is taught in advanced high school and introductory undergraduate calculus courses.
