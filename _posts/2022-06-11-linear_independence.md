

Introduction
------------

An extremely important concept in the study of vector spaces is that of _linear independence_. At a high level, a set of vectors are said to be **linearly independent** if you cannot form any vector in the set using a weighted sum of any combination of the other vectors in the set. If a set of vectors does not have this quality -- that is, a vector in the set can be formed from some combination of other vectors in the set -- then the set is said to be **linearly dependent**.

Linear independence
-------------------

A set of vectors $\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_n \in \mathcal{V}$ are said to be **linearly independent** if you cannot form any of the vectors in the set using a weighted combination of any of the other vectors.

For example, say we have three vectors in a Euclidean space:

$$\boldsymbol{x}_1 := \begin{bmatrix}1 \\ 2 \\ 3\end{bmatrix}$$

$$\boldsymbol{x}_2 := \begin{bmatrix}2 \\ 1 \\ 3\end{bmatrix}$$

$$\boldsymbol{x}_3 := \begin{bmatrix}5 \\ 4 \\ 9\end{bmatrix}$$

These vectors are NOT linearly independent becase we can see that $\boldsymbol{x}_3$ is simply a weighted sum of $\boldsymbol{x}_1$ and $\boldsymbol{x}_2$:

$$\begin{align*}\boldsymbol{x}_3 &= \boldsymbol{x}_1 + 2\boldsymbol{x}_3 \\ \begin{bmatrix}5 \\ 4 \\ 9\end{bmatrix} &= \begin{bmatrix}1 \\ 2 \\ 3\end{bmatrix} + 2 \begin{bmatrix}2 \\ 1 \\ 3\end{bmatrix}\end{align*}$$

A set of vectors are not linearly independent are called **linearly dependent**.
