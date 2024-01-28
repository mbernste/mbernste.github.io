

Introduction
------------

Throughout many of my prior linear algebra posts, we have seen theorems of the form "A matrix has property X if and only if it is an invertible matrix". In this post, we will bring these theorems into one place, and introduce a few more, in order to form a set of statements that all can be used to define an invertible matrix. We will also show that each of these statements imply all of the rest of the statemetns. Put together, these statements form what is called the **invertible matrix theorem**. Not only does this theorem provide a [multi-angled perspective](https://mbernste.github.io/posts/understanding_3d/) into the nature of invertible matrices, it is also practically useful because if one has some matrix, $\boldsymbol{A}$, then one needs only to prove a single one of the statements in the invertible matrix theorem in order to learn that _all of the remaining statements_ of the invertible matrix theorem are also true of the matrix. 

The invertible matrix therorem
------------------------------

The invertible matrix theorem is stated as follows:

<span style="color:#0060C6">**Theorem 1**: A square matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ is an invertible matrix if and only if _any_ of the following statements hold:</span>

<center><span style="color:#0060C6">1. There exists a square matrix $\boldsymbol{C} \in \in \mathbb{R}^{n \times n}$ such that $\boldsymbo{AC} = \boldsymbo{CA} = \boldsymbol{I}$</span></center>

<center><span style="color:#0060C6">2. The columns of $\boldsymbol{A}$ are linearly independent</span></center>

<center><span style="color:#0060C6">3. The rows of $\boldsymbol{A}$ are linearly independent</span></center>

<center><span style="color:#0060C6">4. The rank of $\boldsymbol{A}$ is $n$</span></center>

<center><span style="color:#0060C6">5. The linear transformation $T(\boldsymbol{x}) := \boldsymbol{Ax}$ is one-to-one and onto.</span></center>

<center><span style="color:#0060C6">6. The equation.</span></center>


<span style="color:#0060C6">is a **simple function** if there exists a finite sequence of sets $A_1, A_2, \dots, A_n \in \mathcal{F}$ and a finite sequence of numbers $h_1, h_2, \dots, h_n \in \mathbb{R}$ such that $g$ can be expressed as</span>

<center><span style="color:#0060C6">$$g(x) = \sum_{i=1}^n h_i\mathbb{I}_{A_i}(x)$$</span></center>

<span style="color:#0060C6">where $\mathbb{I}_{A_i}(x)$ is an indicator function that equals one if $x \in A_i$ and equals zero otherwise.</span>

Axiom 2 for defining the determinant states that if two column vectors of a matrix are equal, then the determinant is zero. The intuition behind this axiom is that if a matrix has two equal column-vectors, then the parallelopided is, in a sense, flat and thus, its volume is zero. From this axiom, we derived Theorem 2, which states that any matrix whose column vectors are linearly dependent has a determinant that is zero. 

Now, recall Theorem 4 from our [previous blog post](https://mbernste.github.io/posts/inverse_matrices/) that a matrix is singular (i.e., not invertible) if and only if its columns are linearly dependent. Combining these two theorems, we arrive at the following conclusion: a matrix is invertible if and only if its determinant is non-zero:



Intuitively, this makes sense. Again, recall from our [discussion of invertible and singular matrices](https://mbernste.github.io/posts/inverse_matrices/) that a singular matrix collapses vectors down into a smaller dimensional subspace. What Theorem 10 tells us is that any such matrix that performs this dimensionality reduction has column vectors that form a flat parallelopiped, which has a volume, and hence determinant, of zero!
