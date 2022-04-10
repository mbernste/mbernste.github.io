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

Calculus, as taught in most high school and undergraduate courses, concerns itself with infitesimal changes either in the input or output of numerical functions. That is, functions that accept a vector of real-numbers and output a real number:

$$f : \mathbb{R}^n \rightarrow mathbb{R}$$

In this blog post, we discuss a different category of function: the set of functions that accept as input _a function_ and output a real number. Such functions are called **functionals**. Functionals are quite prevalent in machine learning and statistical inference. For example, [Shannon entropy]() can be considered a functional on probability mass functions. Recall, entropy is a function that, for a given [discrete random variable](), $X$, accepts as input a probability mass function and outputs a real number:

$$H(p_X) := -\sum_{x \in \mathcal{X}} p_X(x) \log p_X(x)$$

where $p_X$ is the probability mass function for $X$ and $\mathcal{X}$ is the [support](https://en.wikipedia.org/wiki/Support_(mathematics)) of $p_X$.

The **calculus of variations** is the field of mathematics that generalizes the ideas in calculus from traditional numeric functions to functionals.


In the calculus of variations, functions of functions are referred to as [functionals](https://en.wikipedia.org/wiki/Functional_(mathematics)). The derivative of a functional is called a **functional derivative**.

Functionals? Functional derivatives? Let's step through this slowly.

As previously stated, a functional is a function of functions. Specifically, it is a function that maps functions to real numbers. The function $L$ above can be viewed as a functional because it takes a function $f \in \mathcal{H}$ and maps it to a real number. That real number, of course, corresponds to the average value of the loss function when evaluating $f$ on all of the $(x_i, y_i)$ pairs.

Now, we need a way to think about the derivative of $L$ at a given $f$. Recall that for a plain old function on the real numbers $g: \mathbb{R} \rightarrow \mathbb{R}$, the derivative of $g$ at $x$, denoted $g'(x)$ tells us how much $g$ is changing at $f$. Said differently, it asks, if we change $x$ by an infinitesimal amount, how much does $g$ change? The functional derivative of $L$ addresses this same question. That is, if we change $f$ by an infinitesimal amount, how does $L$ change? This concept is rigorously addressed by the functional derivative, denoted $\nabla L(f)$.

Now, to define the functional derivative, we must ask the question, what does it mean to "change $f$ by an infinitesimal amount"? To define this rigorously, we'll consider an arbitrary real number $\epsilon \in \mathbb{R}$ and an arbitrary function $\eta: \mathcal{X} \rightarrow \mathcal{Y}$. Then, we'll consider the functional evaluated at $f + \epsilon\eta$:

$$L(f + \epsilon \eta)$$

Notice that $f + \epsilon \eta$ is a function and thus, can be "fed" to $L$. Let's now go a step further and consder $f$ and $\eta$ to be fixed, but we'll let $\epsilon$ vary. That is, we will let $\epsilon$ be a variable that is free to be changed. We thus see that $L(f + \epsilon \eta)$ is a function of $epsilon$ and thus, an ordinary function mapping numbers to numbers. That is, we can let $\mathcal{L}(\epsilon) := L(f + \epsilon \eta)$ and realize that $\mathcal{L} : \mathbb{R} \rightarrow \mathbb{R}$.  


