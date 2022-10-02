The general linear group
------------------------

Now, we will note a few important observations about elementary row matrices and invertible matrices in general:

First, notice that each elementary matrix is invertible. The inverse of an elementary matrix that row-scales by a constant $c$ is simply the elementary matrix that scales the row by $\frac{1}{c}$. The inverse of an elementary matrix that row swaps is simply the elementary matrix that swaps the rows back to their original configuration. The inverse of an elementary matrix that performs a row sum is simply the elementary matrix that performs the subtraction. Thus we see that not only are elementary matrices invertible, but their inverses are also elementary matrices!

Because these elementary row matrices are invertible, instead of starting with some invertible matrix $\boldsymbol{A}$ and producing the identity matrix $\boldsymbol{I}$ via some sequence of multiplications, 

$$\boldsymbol{I} = \boldsymbol{E}_n \dots, \boldsymbol{E}_1\boldsymbol{A}$$

we can instead start with the identity matrix and produce $\boldsymbol{A}$:

$$\boldsymbol{A} = \boldsymbol{E}^{-1}_1 \dots \boldsymbol{E}^{-1}_n\boldsymbol{I} $$

From this fact, we can see that we can go from any invertible matrix to another by multiplying the matrix with some series of elementary matrices. For example, say we have two different invertible matrices $\boldsymbol{A}$ and $\boldsymbol{B}$. Then we can transform $\boldsymbol{A}$ into the identity matrix via some some sequence of multiplications by elementary matrices:

$$\boldsymbol{I} = \boldsymbol{E}_n \dots, \boldsymbol{E}_1\boldsymbol{A}$$

We can also transform $\boldsymbol{B}$ into the identity matrix via some some sequence of multiplications by elementary matrices:

$$\boldsymbol{I} = \boldsymbol{E}_{n+m} \dots, \boldsymbol{E}_{n+1}\boldsymbol{B}$$

We can convert $\boldsymbol{A}$ to $\boldsymbol{B}$ by converting $\boldsymbol{A}$ to $\boldsymbol{I}$ and then convert $\boldsymbol{I}$ to $\boldsymbol{B}$ via the inverses of the elementary matrices used to convert $\boldsymbol{B}$ to $\boldsymbol{I}$:

$$\boldsymbol{B} = \boldsymbol{E}^{-1}_{n+1} \dots \boldsymbol{E}^{-1}_{n+m}\boldsymbol{E}_n \dots, \boldsymbol{E}_1\boldsymbol{A}

Let's let the matrix $\boldsymbol{C}$ be defined as:

$$\boldsymbol{C} := \boldsymbol{E}^{-1}_{n+1} \dots \boldsymbol{E}^{-1}_{n+m}\boldsymbol{E}_n \dots, \boldsymbol{E}_1$$

Then, we see that 

$$\boldsymbol{B} = \boldsymbol{CA}$$

Notably, $\boldsymbol{C}$ is also an invertible matrix because all of the elementary matrices we multiplied together to produce $\boldsymbol{C}$ are all invertible! 

The general linear group
------------------------

Now we can see that the set of all invertible matrices of shape $n \times n$, together with the matrix multiplication operation, form a [group](https://en.wikipedia.org/wiki/Group_(mathematics)). 

Recall, a group is a set $S$ together with a function $f$ that operates on pairs of objects in $S$ to produce a third object in $S$

$$f: S \times S \rightarrow S$$

such that $f$ is [associative](), there exists an object in $S$ called the **identity** object, denoted $s_{\text{identity}}$, and for each object $s \in S$, there exists another object $s^{-1} \in S$, called its **inverse** such that 

$$f(s, s^{-1}) = $s_{\text{identity}}$$

For example, the real numbers $\mathbb{R}$ together with the multiplication operation form a group. The operator $f$ in this case is simply 

$$f(x, y) := xy$$

The identity object is simply 1. That is, $s_{\text{identity}} := 1$ and the inverse for any number $x \in \mathbb{R}$ is simply its reciprocal $1 / x$. That is because 

$$f(x, 1/x) = x(1/x) = 1$$

Now, in the case of invertible matrices, we have shown that every invertible matrix, $\boldsymbol{A}$, can be multiplied by a second invertible matrix $\boldsymbol{C}$ to produce a third $\boldsymbol{B}$. Thus, $f$ in the general linear group is simply matrix multiplication. That is, given two matrices $\boldsymbol{A}$ and $\boldsymbol{B}$, we have

$$f(\boldsymbol{A}, \boldsymbol{B}) := \boldsymbol{AB}$$

The identity of the general linear group is simply the identity matrix $\boldsymbol{I}. Finally, the general linear group's inverse for an invertible matrix $\boldsymbol{A}$ is simply its inverse matrix $\boldsymbol{A}^{-1}$.


