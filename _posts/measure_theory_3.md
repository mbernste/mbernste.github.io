


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

When $f$ is smooth (i.e. both continuous and differentiable), we can approximate the area under $f$ within a given interval $(a,b)$ by summing the areas of rectangles of even width that span $(a,b)$. If we keep shrinking the rectangles then, in the limit, this becomes the Reimann integral, which is taught in advanced high school and introductory undergraduate calculus courses.  The figure below demonstrates this process:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/Reimann.png" alt="drawing" width="600"/></center>

The Lebesgue integral also forms rectangles, but it does so in a different way than the Reimann integral. For the Lebesgue integral, a rectangle is formed *for each value* in the function's codomain (i.e., each unique height that the function ever reaches). For each value, a recangle is formed with a height equal to this value and a width equal to the length of all intervals along $\mathbb{R}$ where the function reaches this height.  The figure below displays this alternate stratagy:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/Lebesgue.png" alt="drawing" width="600"/></center>

A crucial difference between the Reimann integral and the Lebesgue integral is that the Lebesgue integral works for functions whose domain is non-numeric. We'll see how this works as we define the Lebesgue integral more rigorously.

Defining the Lebesgue integral through a sequence of definitions
---------

I find the full, rigorous definition of the Lebesgue integral to be quite complex. It helped me to break this definition down in a sequence of simpler definitions, each building on the next:
1. Simple functions
2. The Lebesgue integral of a simple function
3. The Lebesgue integral of a positive function
4. The Lebesgue integral

**1. Simple functions**

A **simple function** is a measure-theoretic generalization of a [step-function](https://en.wikipedia.org/wiki/Step_function).   Given a measurable space $(F, \mathcal{F})$, a simple function $g$ is any function that can be expressed as a finite, linear combination of indicator functions on these sets:

**Definition 8: Given a measurable space $(F, \mathcal{F})$, a function $g$

$$g : F \rightarrow \mathbb{R}$$

is a **simple function** if there exists a finite sequence of sets $A_1, A_2, \dots, A_n \in \mathcal{F}$ and a finite sequence of numbers $h_1, h_2, \dots, h_n \in \mathbb{R}$ such that $g$ can be expressed as 

$$g(x) = \sum_{i=1}^n h_i\mathbb{I}_{A_i}(x)$$

where $\mathbb{I}_{A_i}(x)$ is an indicator function such that $\mathbb{I}_{A_i}(x) := 1$ if $x \in A_i$ and $\mathbb{I}_{A_i}(x) := 0$ otherwise.


