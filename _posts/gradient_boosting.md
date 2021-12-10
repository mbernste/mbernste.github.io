

Boosting is a machine learning paradigm that entails constructing an ensemble of models in an iterative fashion where upon each iteration, a new model is added to the ensemble that compensates for the weaknesses of the previously selected models. 

Review of the supervised learning task
--------------------------------------

Before getting into the meat of gradient boosting, let's review the basic supervised learning task so that we are on the same page regarding both the problem setting and mathematical notation. 

In supervised learning, our goal is to map each element in a set $\mathcal{X}$ to a target variable in a set $\mathcal{Y}$. That is, we seek a specific function 

$$F: \mathcal{X} \rightarrow \mathcal{Y}$$

The space of objects $\mathcal{X}$ depends on the problem being solved. It may consist of text numerical vectors, documents, images, or graphs. The space $\mathcal{Y}$ usually consists of real numbers (in the case of regression) or a set of finite labels (in the case of classification). 

We don't have access to the optimal function, $F$, directly. Instead, we have access to a finite set of pairs $\{(x_i, y_i)}_{i=1, \dots, n}$ where $x_i \in \mathcal{X}$ and $y_i \in \mathcal{Y}$ such that $F(x_i) = y_i$.  Our goal is to approximate $F$ from this finite sample. 

To perform this approximation, we search a space of functions $\mathcal{H}$ for a function $f \in \mathcal{H}$ that minimizes a function, called the [loss function](https://en.wikipedia.org/wiki/Loss_function), that tracks the correspondence between each $y_i$ and each $F(y_i)$. That is, the loss function $L(y_i, f(x_i))$. That is, we seek to find an $f \in \mathcal{H}$ that minimizes the average loss over all of the samples:

$$\hat{f}(x) := \text{arg min}_{f \in \mathcal{H}} \frac{1}{n} \sum_{i=1}^n L(y_i, f(x_i))$$

Gradient descent
----------------

Gradient descent is a numerical approach for solving an optimization problem that involves iteratively improving our solution by taking small steps along the direction of steepest descent down the loss function's surface. Recall, the direction of steepest ascent of a continuous function is given by the [gradient vector]() at a given point and thus, gradient descent entails iteratively computing the gradient of the objective function at the current solution and then slightly changing the solution in the direction of the gradient. 

Specifically, let's say that each model in the space $\mathcal{H}$ is characterized by set of parameters $\phi \in \mathbb{R}^r$. That is, we can write each $f \in \mathcal{H}$ as $f(x; \theta)$. Then, the problem

$$\text{arg min}_{f \in \mathcal{H}} \frac{1}{n} \sum_{i=1}^n L(y_i, f(x_i))$$

becomes

$$\text{arg min}_{\theta \in \mathbb{R}^r} \frac{1}{n} \sum_{i=1}^n L(y_i, f(x_i; \theta))$$

Moreover, if we assume that $f(x_i, \theta)$ is differentiable with respect to $\theta$, then we can compute the gradient:

$$\frac{\partial \sum_{i=1}^n L(y_i, f(x_i; \theta)))}{\partial \theta}$$

Then, we can update our current solution 

$$\theta_{t+1} := \theta_t + \gamma \frac{\partial \sum_{i=1}^n L(y_i, f(x_i; \theta)))}{\partial \theta}$$


Boosting
--------


Gradient boosting
-----------------
