# Eigenvalues and Eigenvectors

## Usefulness

$x$ is the eigenvector of $A$, $\lambda$ is the eigenvalue of $A$. According to the equation below, **the eigenvectors of $A$ don't change direction when multiplied by $A$.**
$$
A x = \lambda x
$$
$x$ is also an eigenvector of $A^2$ , and certainly $A^k$ for all $k = 1,2,3,...$. And $A^{-1}x = \frac{1}{\lambda} x$ provided $\lambda \neq 0$.
$$
A(Ax) = A(\lambda x) = \lambda(Ax) = \lambda^2 x\\
\text{Certainly }A^k x = \lambda^k x \text{ for all } k = 1,2,3,...
$$
Most square matrix (n by n) have $n$ independent eigenvectors $x_1$ to $x_n$ with $n$ different eigenvalues $\lambda_1$ to $\lambda_n$. Thus every n-D vector $v$ will be a combination of the eigenvectors
$$
\begin{aligned}
A^kx & = \lambda^k x\\
v & = c_1x_1 + ... + c_nx_n\\
v_2 = Av & = c_1 \lambda_1 x_1 + ... + c_n \lambda_n x_n\\
v_{k} = A^kv & = c_1 \lambda_1^k x_1 + ... + c_n \lambda_n^k x_n\\
v_{k+1} = A^{k+1}v & = c_1 \lambda_1^{k+1} x_1 + ... + c_n \lambda_n^{k+1} x_n = A(A^k v) = Av_k\\
v_{k+1} & = A v_k
\end{aligned}
$$

#### Properties of Evalues and Evectors

Suppose a **symmetric** matrix $S = \begin{bmatrix}  2&1\\1&2 \end{bmatrix}$ has eigenvectors $3 \begin{bmatrix}  1\\1\\ \end{bmatrix}$ and $\begin{bmatrix} 1\\-1 \end{bmatrix}$ thus $\lambda_1 = 3, \lambda_2 = 1$.

* **Trace** of $S$: $\lambda_1 + \lambda_2 = 4$ equals the sum of diagonal elements $2+2 = 4$.

* **Determinant** of $S$: $\lambda_1 \lambda_2 = 3 \times 1 = 3$ equals the determinant $(2 \times 2) - (1 \times 1) = 3$.
* **Real** eigenvalues of $S$: Symmetric matrices $S = S^T$ always have real eigenvalues.
  * The powers $S^k$ will grow ($S$ is like real numbers with every $\lambda$ real), while the power of orthogonal matrix $Q$ ($Q$ is like complex numbers $e^{i\theta} = \cos \theta + i \sin \theta$ of magnitude 1, since every $|\lambda| = 1$) never grow or decay because $Q^2, Q^3$ are orthogonal matrix too.
* **Orthogonal eigenvectors**: $x_1 \cdot x_2 = 0$.

#### Warnings of Evalues and Evectors

* $\lambda (A+B) \neq (\lambda(A) + \lambda(B))$
* $\lambda(AB) \neq \lambda(A)\lambda(B)$

## Review of Computing Eigenvalues

$$
\begin{aligned}
Ax & = \lambda x\\
(A-\lambda I)x & = 0 
\end{aligned}
$$

$(A - \lambda I)$ is not invertible ( we couldn't have null space unless the determinant is 0 ), which means it is singular, and the determinant of $(A - \lambda I)$ must be 0. 
$$
det(A - \lambda I) = 0
$$

> #### Exercise 1
>
> If $A$ is shifted to $A+sI$, what happens to the $x$'s and $\lambda$'s?
>
> > **Answer**: If $A$ is shifted to $A + sI$, the eigenvectors $x$ stay the same, every eigenvalue $\lambda$ shifts by the number $s$.
>
> > **Solution**: $(A+sI)x = \lambda x + s x = (\lambda + s)x$

## Similar Matrix

Matrix $A$ and $B$ are similar if $B = M^{-1}AM$ ($M$ is an invertible matrix), because $A$ and $B$ have same **eigenvalues**. The eigenvector of $B$  is $My$, which has a different basis of eigenvector $y$ of $A$.
$$
\begin{aligned}
M^{-1}AMy & = \lambda y\\
AMy & = \lambda My\\
A(My) & = \lambda (My)
\end{aligned}
$$
We use this idea to compute eigenvalues of large matrices $A$ - **the eigenvalues of any triangular matrix $M^{-1}AM$ show up on the main diagonal. **For example the eigenvalues of $\begin{bmatrix} a&b\\0&d \end{bmatrix}$are $\lambda_1 = a, \lambda_2 = d$

> #### Exercise 2
>
> Show $AB$ has same non-zero eigenvalues as $BA$.
>
> > **Answer**: $M^{-1}(BA)M = AB$ shows $AB$ and $BA$ are similar.
>
> > **Solution**: 
> >
> > This question is equivalent to "Show $AB$ and $BA$ are similar matrices". i.e. $M^{-1}(BA)M = AB$
> >
> > Take $M=B$, we got $B^{-1}(BA)B = AB$.

## Diagonalizing a Matrix

Suppose matrix $A$ has a full set of $n$ independent eigenvectors $x_1, ..., x_n$ and we put them into an **invertible eigenvector matrix** $X$, we have
$$
AX = X\Lambda
$$
where $\Lambda$ is a **diagonal matrix** with eigenvalues on the main diagonal. It tells that
$$
A = X\Lambda X^{-1}
$$
It is significant in that if we know eigenvectors and eigenvalues, we know matrix $A$.

When matrix $A$ is squared, the eigenvectors do not change, while eigenvalues are also squared. Similarly, the eigenvalues of $A^k$ are $\lambda_1^k, ... \lambda_n^k$.
$$
A^2 = X\Lambda^2 X^{-1}\\
A^k = X\Lambda^k X^{-1}
$$

> #### Exercise 3
>
> $A = \begin{bmatrix}0.8 & 0.3 \\ 0.2 & 0.7 \end{bmatrix}$ is a **Markov matrix**, with positive columns adding to 1. Compute $A^k v$.
>
> > **Answer**:  $A^kv = c_1(1)^kx_1 + c_2(1/2)^kx_2$
>
> > **Solution**: 
> >
> > Find eigenvalues $\lambda_1$ and $\lambda_2$: $(0.8 - \lambda)(0.7-\lambda) - 0.2 \times 0.3 = 0 \implies \lambda_1 = 1, \lambda_2 = 0.5$ and plug in $A^kv = X \Lambda^k X^{-1} v = c_1 \lambda_1^k x_1 + ... + c_n \lambda_n^k x_n$.
> >
> > From $A^kv$ we know, **as $k$ increases, $A^kv$ approaches $c_1x_1 = $ steady state.**

