

Boosting is a machine learning paradigm that entails constructing an ensemble of models in an iterative fashion where upon each iteration, a new model is added to the ensemble that compensates for the weaknesses of the previously selected models. 

Review of the supervised learning task
--------------------------------------

Before getting into the meat of gradient boosting, let's review the basic supervised learning task so that we are on the same page regarding both the problem setting and mathematical notation. 

In supervised learning, our goal is to map each element in a set $\mathcal{X}$ to a target variable in a set $\mathcal{Y}$. That is, we seek a specific function 

$$F: \mathcal{X} \rightarrow \mathcal{Y}$$

The space of objects $\mathcal{X}$ depends on the problem being solved. It may consist of text documents, images, graphs, or DNA sequences. The space $\mathcal{Y}$ usually consists of real numbers, in the case of regression, or a set of finite labels, in the case of classification. 

We don't have access to the optimal function, $F$, directly. Instead, we have access to a finite set of pairs $(x_i, y_i)$ where $x_i \in \mathcal{X}$ and $y_i \in \mathcal{Y}$ such that $F(x_i) = y_i$.

Our goal is to recover $F$ from this finite sample. To do so, we search a space of functions $\mathcal{H}$ for a function $f \in \mathcal{H}$ that minimizes a function, called the [loss function], that tracks the correspondence between each $y_i$ and each $F(y_i)$.


Overview of boosting
--------------------

$$S := \{(x_1, y_1), (x_2, y_2), \dots, (x_2, y_2) \}$$ where $x_i$ is a given item and $y_i$ is the target variable that we are trying to learn. Specifically, boosting entails building a classifier of the form:

$$F(x) := \sum_{t=1}^T \alpha h_t(x)$$

where $h_t(x)$ 
