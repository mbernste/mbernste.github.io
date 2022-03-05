---
title: 'Gradient boosting'
date: 2022-03-04
permalink: /posts/gradient_boosting/
tags:
  - tutorial
  - machine learning
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Boosting is a machine learning paradigm that entails constructing an ensemble of models in an iterative fashion where upon each iteration, a new model is added to the ensemble that compensates for the weaknesses of the previously selected models. 

Introduction
------------

Gradient boosting is a machine learning paradigm that involves training an ensemble of weak models to form a strong model. To understand gradient boosting, one must understand two central ideas: **gradient descent** and **boosting**.  In this post, we will first review the supervised learning task, boosting, and gradient descent. Then we will discuss how these ideas come together in gradient boosting. Lastly, we will contrast the gradient boosting paradigm with the standard gradient descent learning algorithm for fitting model parameters; they are actually quite different! 

Review of the supervised learning task
--------------------------------------

Before we get started, let's review the basic supervised learning task so that we are on the same page regarding both the problem setting and mathematical notation. 

In supervised learning, our goal is to learn a function $F$ that maps each element in a set $\mathcal{X}$ to a target element in a set $\mathcal{Y}$. That is, we seek a specific function 

$$F: \mathcal{X} \rightarrow \mathcal{Y}$$

The space of objects $\mathcal{X}$ depends on the problem being solved. It may consist of text numerical vectors, documents, images, or graphs. The space $\mathcal{Y}$ usually consists of real numbers (in the case of regression) or a set of finite labels (in the case of classification). 

We don't have access to the optimal function, $F$, directly. Instead, we have access to a finite set of pairs $\{(x_i, y_i)}_{i=1, \dots, n}$ where $x_i \in \mathcal{X}$ and $y_i \in \mathcal{Y}$ such that $F(x_i) = y_i$.  Our goal is to approximate the true $F$ by leveraging this finite sample. 

To perform this approximation, we search a space of functions $\mathcal{H}$ for a function $f \in \mathcal{H}$ that minimizes a function, called the [loss function](https://en.wikipedia.org/wiki/Loss_function), that tracks the correspondence between each $y_i$ and each $f(y_i)$. That is, the loss function $\ell(y_i, f(x_i))$ tells us how much $f(x_i)$ deviates from $y_i$.

Then, we seek to find an $f \in \mathcal{H}$ that minimizes the average loss over all of the samples:

$$\hat{f} := \text{arg min}_{f \in \mathcal{H}} \frac{1}{n} \sum_{i=1}^n \ell(y_i, f(x_i))$$

The hope is then that $\hat{f}$ is a good approximation to the "true" latent function $F$.

Gradient descent
----------------

Gradient descent is a numerical approach for solving an optimization problem that involves starting with an initial guess of the solution to the problem and then iteratively improving that solution by taking small steps in the direction of steepest descent down the objective function's surface.

Say we have an objective function $g : \mathcal{\mathbb{R}^m} \rightarrow \mathbb{R}$ and we wish to find the argument that minimizes $g$. That is, we wish to find the solution to the optimization problem

$$\hat{\boldsymbol{x}} := \text{arg min}_{\boldsymbol{x} \in \mathbb{R}^m} g(x)$$

In gradient descent, we find the $\boldsymbol{x}$ that minimizes $g$ by "walking" down $g$'s surface:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/gradient_descent_error_surface.png" alt="drawing" width="500"/></center>

More rigorously, gradient descent works as follows: We start with an initial guess of the solution $\boldsymbol{x}\_0 \in \mathbb{R}^m$ and iteratively update our estimate by following the direction of steepest descent.  Recall, the direction of steepest _ascent_ is given by the function's [gradient](https://en.wikipedia.org/wiki/Gradient), $\nabla g(\boldsymbol{x})$, and so the direction of steepest _descent_ is simply the direction of the negative gradient. Thus, at the $t$th iteration, the updated solution is given by

$$\boldsymbol{x}_t := \boldsymbol{x}_{t-1} - \alpha \nabla g(\boldsymbol{x}_{t-1})$$

The parameter, $\alpha$, is called the **learning rate** and simply dictates how far we will step in the direction of the negative gradient at each iteration.

Notice that gradient descent can really only be applied when $g$ is differentiable. Otherwise, we cannot compute a gradient and therefore do not how to update the solution! (A variant of gradient descent called [subgradient descent](https://en.wikipedia.org/wiki/Subgradient_method) can be applied to cases where $g$ is not differentiable, but we'll save that discussion for later.)

Functional gradient descent
---------------------------

As we will see, gradient boosting can be understood as a gradient descent algorithm for solving for 

$$\hat{f} := \text{arg min}_{f \in \mathcal{H}} L(f)$$

where 

$$L(f) := \frac{1}{n} \sum_{i=1}^n \ell(y_i, f(x_i))$$

Now this may seem a bit weird. In our explanation of gradient descent above, it was assumed that the objective function was numeric. That is, $g$ maps vectors of real numbers to a number: 

$$g: \mathbb{R}^m \rightarrow \mathbb{R}$$ 

Here, our objective function $L$ maps abstract functions to real numbers: 

$$L : \mathcal{H} \rightarrow \mathbb{R}$$ 

So how dow we compute gradients and how do we derive a gradient descent algorithm?

The answer to these questions requires a brief forray into functional analysis and the calculus of various. We will seek to derive a sort of generalization of gradient descent on spaces of functions that we will refer to as "functional gradient descent". 

The gradient boosting algorithm
-------------------------------

Gradient boosting can be understood as a generalization of gradient descent to the space of functions $\mathcal{H}$. That is, we solve the optimization problem

$$\hat{f} := \text{arg min}_{f \in \mathcal{H}} L(f)

where 

$$L(f) := \frac{1}{n} \sum_{i=1}^n \ell(y_i, f(x_i))$$

using gradient descent over $\mathcal{H}$. That is, we start with an initial model $f_0$ and iteratively update $f_0$ by taking small steps that improve $L(f)$. That is, at iteration $t$, we update our current estimate $f_t$ by

$$f_t := f_{t-1} + \alpha h_t$$

where $h_t$ is a function in $\mathcal{H}$ that represents a function that improves $L(f)$ the most. That is, $h_t$ is analogous to the gradient, $\nabla L(\theta)$, from traditional gradient descent. 


The question we now must answer is, how do we derive this "gradient function" $h_t$? Let's take a step back and take a look at traditional gradient descent. Specifically, let's look at the gradient:

$$\begin{align*}\nabla L(\theta) &= \partial \frac{1}{n} \sum_{i=1}^n \ell(y_i, f(x_i; \theta)) \end{align*}$$

**Here's the crucial insight:** if we want a function $h_t$ that acts like the gradient of $L(f_{t-1})$, then for all $x_i$, it should hold that

$$h_t(x_i) = \frac{\partial \ell(y_i, f(x_i))}{\partial f(x_i)}$$

That is, for any given $x_i$, $$h_t(x_i)$$ gives you the 

For simplicity of notation, let

$$r_i := \frac{\partial \ell(y_i, f(x_i)}{\partial f(x_i)}$$

Then, we simply need a function $h_t$ for which $h_t(x_i) = r_i$. How do we actually find such a function? One idea is to train a model to fit the pairs $(x_i, r_i)$! Once we fit this model, we can update our current estimate $f_{t-1}$ via

$$f_t := f_{t-1} + h_t$$

At the end of $T$ iterations, our full model $\hat{f}$ will have the form

$$\hat{f}(x) = \sum_{t=1}^T \alpha h_t(x)$$

Notice that $f(x)$ is actually an ensemble of models $h_1, \dots, h_T$! As we will show in the next section, this process can be viewed as a boosting algorithm!


Viewing gradient boosting as boosting
--------------------------------------



Calculating the pseudo-residuals for common loss functions
----------------------------------------------------------

