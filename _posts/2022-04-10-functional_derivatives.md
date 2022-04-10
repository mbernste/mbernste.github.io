---
title: 'Functionals and functional derivatives'
date: 2022-04-10
permalink: /posts/functionals/
tags:
  - tutorial
  - mathematics
  - calculus of variations
---

_The calculus of variations is a field of mathematics that deals with the optimization of functions of functions, called functionals, not often taught in computer science curricula, but lays the foundation for a number of important concepts and algorithms in machine learning and statistical inference. In this post, I will provide a high-level overview of functionals and the definition of the functional derivative._

Introduction
------------

Multivariate calculus, as taught in most high school and undergraduate courses, concerns itself with infitesimal changes either in the input or output of numerical functions. That is, functions that accept a vector of real-numbers and output a real number:

$$f : \mathbb{R}^n \rightarrow \mathbb{R}$$

In this blog post, we discuss the **calculus of variations**, a field of mathematics that generalizes the ideas in multivariate calculus from traditional numeric functions to _functions of functions_.  Functions of functions are called **functionals**. That is, if $\mathcal{F}$ is a set of functions, then 

$$F : \mathcal{F} \rightarrow \mathbb{R}$$

is a functional.

Functionals are quite prevalent in machine learning and statistical inference. For example, [information entropy](https://mbernste.github.io/posts/entropy/) can be considered a functional on probability mass functions. For a given [discrete random variable](https://mbernste.github.io/posts/measure_theory_2/), $X$, entropy can be thought about as a function that accepts as input $X$'s probability mass function, $p_X$, and outputs a real number:

$$H(p_X) := -\sum_{x \in \mathcal{X}} p_X(x) \log p_X(x)$$

where $\mathcal{X}$ is the [support](https://en.wikipedia.org/wiki/Support_(mathematics)) of $p_X$. 

Another example of a functional is the [evidence lower bound (ELBO)](https://mbernste.github.io/posts/elbo/), a function that, like entropy, operates on probability distributions. The ELBO is a foundational quantity used in the popular [EM algorithm](https://mbernste.github.io/posts/em/) and [variational inference](https://mbernste.github.io/posts/variational_inference/), two frameworks used to perform  statistical inference with probabilistic models. 

In this blog post, we will review some concepts in traditional calculus such as partial derivatives, gradients, and directional derivatives in order to introduce the definition of the **functional derivative**, which is simply the generalization of the derivative of numeric functions to functionals!

A review of partial derivatives, gradients, and directional derivatives
-----------------------------------------------------------------------

In this section, we will introduce a few important concepts in multivariate calculus: partial derivatives, gradients, and directional derivatives. For the remainder of this section, we will consider a continous function $f$ that maps real-valued vectors $\mathcal{x} \in \mathbb{R}^n$ to real-numbers. That is,

$$f: \mathbb{R}^n \rightarrow \mathbb{R}$$

### Partial derivatives

Given $\boldsymbol{x} \in \mathbb{R}^n$, the **partial derivative** of $f$ with respect to the $i$th component of $\boldsymbol{x}$, denoted $\frac{\partial f(\boldsymbol{x})}{\partial x_i}$ is simply the derivative of $f$ if we hold all the components of $\boldsymbol{x}$ fixed, except for the $i$the component. Said differently, it tells us the rate of change of $f$ with respect to the $i$th dimension of the vector space in which $\boldsymbol{x}$ resides! This can be visualized below for a function $f : \mathbb{R}^2 \rightarrow \mathbb{R}:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/partial_derivative.png" alt="drawing" width="450"/></center>

As seen above, the partial derivative $f(\boldsymbol{x})}{\partial x_1}$ is simply the derivative of the function $f(x_1, x_2)$ when holding $x_1$ as fixed. That is, it is the slope of the line tangent to the function of $f(x_1, x_2)$ when $x_1$ is fixed.

### Gradients

The **gradient** of $f$ at $\boldsymbol{x}$, denoted $\nabla \boldsymbol{x}$ is simply the vector 

$$\nabla f(\boldsymbol{x}) := \begin{bmatrix}\frac{\partial f(\boldsymbol{x})}{\partial x_1} & \frac{\partial f(\boldsymbol{x})}{\partial x_2} & \dots & \frac{\partial f(\boldsymbol{x})}{\partial x_n}] \end{bmatrix}$$

That is, it is the vector formed by taking the partial derivatives of $f$ with respect to each dimension! Geometrically, this vector will point in the direction of _steepest ascent_ along $f$'s surface at $\boldsymbol{x}$. 


### Directional derivatives



Functional derivatives
----------------------

As previously stated, a functional is a function of functions. Specifically, it is a function that maps functions to real numbers. The function $L$ above can be viewed as a functional because it takes a function $f \in \mathcal{H}$ and maps it to a real number. That real number, of course, corresponds to the average value of the loss function when evaluating $f$ on all of the $(x_i, y_i)$ pairs.

Now, we need a way to think about the derivative of $L$ at a given $f$. Recall that for a plain old function on the real numbers $g: \mathbb{R} \rightarrow \mathbb{R}$, the derivative of $g$ at $x$, denoted $g'(x)$ tells us how much $g$ is changing at $f$. Said differently, it asks, if we change $x$ by an infinitesimal amount, how much does $g$ change? The functional derivative of $L$ addresses this same question. That is, if we change $f$ by an infinitesimal amount, how does $L$ change? This concept is rigorously addressed by the functional derivative, denoted $\nabla L(f)$.

Now, to define the functional derivative, we must ask the question, what does it mean to "change $f$ by an infinitesimal amount"? To define this rigorously, we'll consider an arbitrary real number $\epsilon \in \mathbb{R}$ and an arbitrary function $\eta: \mathcal{X} \rightarrow \mathcal{Y}$. Then, we'll consider the functional evaluated at $f + \epsilon\eta$:

$$L(f + \epsilon \eta)$$

Notice that $f + \epsilon \eta$ is a function and thus, can be "fed" to $L$. Let's now go a step further and consder $f$ and $\eta$ to be fixed, but we'll let $\epsilon$ vary. That is, we will let $\epsilon$ be a variable that is free to be changed. We thus see that $L(f + \epsilon \eta)$ is a function of $epsilon$ and thus, an ordinary function mapping numbers to numbers. That is, we can let $\mathcal{L}(\epsilon) := L(f + \epsilon \eta)$ and realize that $\mathcal{L} : \mathbb{R} \rightarrow \mathbb{R}$.  


