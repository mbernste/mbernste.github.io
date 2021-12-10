---
title: 'Gradient boosting'
date: 2021-12-10
permalink: /posts/gradient_boosting/
tags:
  - tutorial
  - machine learning
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Boosting is a machine learning paradigm that entails constructing an ensemble of models in an iterative fashion where upon each iteration, a new model is added to the ensemble that compensates for the weaknesses of the previously selected models. 

Review of the supervised learning task
--------------------------------------

Before getting into the meat of gradient boosting, let's review the basic supervised learning task so that we are on the same page regarding both the problem setting and mathematical notation. 

In supervised learning, our goal is to map each element in a set $\mathcal{X}$ to a target variable in a set $\mathcal{Y}$. That is, we seek a specific function 

$$F: \mathcal{X} \rightarrow \mathcal{Y}$$

The space of objects $\mathcal{X}$ depends on the problem being solved. It may consist of text numerical vectors, documents, images, or graphs. The space $\mathcal{Y}$ usually consists of real numbers (in the case of regression) or a set of finite labels (in the case of classification). 

We don't have access to the optimal function, $F$, directly. Instead, we have access to a finite set of pairs $\{(x_i, y_i)}_{i=1, \dots, n}$ where $x_i \in \mathcal{X}$ and $y_i \in \mathcal{Y}$ such that $F(x_i) = y_i$.  Our goal is to approximate $F$ from this finite sample. 

To perform this approximation, we search a space of functions $\mathcal{H}$ for a function $f \in \mathcal{H}$ that minimizes a function, called the [loss function](https://en.wikipedia.org/wiki/Loss_function), that tracks the correspondence between each $y_i$ and each $F(y_i)$. That is, the loss function $\ell(y_i, f(x_i))$ tells us how much $f(x_i)$ deviates from $y_i$.

Then, we seek to find an $f \in \mathcal{H}$ that minimizes the average loss over all of the samples:

$$\hat{f}(x) := \text{arg min}_{f \in \mathcal{H}} \frac{1}{n} \sum_{i=1}^n \ell(y_i, f(x_i))$$

Boosting
--------

Gradient descent in machine learning
------------------------------------

Gradient descent is a numerical approach for solving an optimization problem that involves iteratively improving our solution by taking small steps along the direction of steepest descent down the objective function's surface.

Specifically, let's say we are attempting to minimize the function $L(\theta)$ where $\phi \in \mathbb{R}^p$ and $F(\theta)$ is differentiable. Then, gradient descent starts by choosing an initial guess of the solution $\phi_0 \in \mathbb{R}^p$ and iteratively updates our estimate by following the direction of steepest descent.  Recall, the direction of steepest _ascent_ is given by the function's [gradient](https://en.wikipedia.org/wiki/Gradient). Specifically, at the $t$th iteration, the update is

$$\phi_t := \phi_{t-1} - \nabla F(\theta)$$

In machine learning, it is common optimize the loss function using models that are characterized by a set of parameters $\phi \in \mathbb{R}^p$. That is, we can write each $f \in \mathcal{H}$ as $f(x; \theta)$. Then, if $f(x; \theta)$ is differentiable with respect to $\theta$, we can let 

$$L(\phi) := \frac{1}{n}\sum_{i=1}^n \ell(y_i, f(x_i; \phi))$$

and, with help from the [chain rule](https://en.wikipedia.org/wiki/Chain_rule), can apply gradient descent as described above to find the $\theta$ that minimizes $L(\phi)$. 

Gradient boosting
-----------------

In the previous section, we assumed that each model $f \in \mathcal{H}$ is parameterized by $\theta$. Furthermore, we assumed that $f(x; \theta)$ were differentiable with respect to $\theta$. With these two assumptions, we discussed how gradient descent could be applied over $\theta$.

Now, what happens if each $f \in \mathcal{H}$ is not parameterized by a real-valued vector $\theta$. For example, what if $\mathcal{H}$ is a space of [decision trees](https://en.wikipedia.org/wiki/Decision_tree)? Can we still apply gradient descent?

In fact, it turns out that we can indeed derive an approximate gradient descent algorithm. This algorithm is called *gradient boosting*. 

It works as follows: we start with our best guess function $f_0$ and at each iteration $t$, we calculate the derivative of the $L$ with respect to each $f(x_i)$: 

$$r_i := \frac{\partial \ell(y_i, f(x_i)}{\partial f(x_i)}$$

These values, are often called _pseudo residuals_ as will be explained later in this post. For now, note that $r_i$ is the gradient of our function $L$ with respect to the functions output at each input $x_i$. 


