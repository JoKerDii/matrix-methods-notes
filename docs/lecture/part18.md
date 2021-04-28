# Counting Parameters in SVD, LU, QR, Saddle Points

## Number of Free Parameters

$$
A = LU \quad X\Lambda X^{-1} \quad Q\Lambda Q^T \quad QS \quad SVD
$$

* $L$ = triangular / diagonal matrix; # of free parameters: $\frac{1}{2}n(n-1)$
* $U$ = triangular matrix; # of free parameters: $\frac{1}{2}n(n+1)$
* $Q$ = orthogonal matrix; # of free parameters: $(n-1) + (n -2) + ... = \frac{1}{2}n(n-1)$
* $\Lambda$ = diagonal matrix; # of free parameters: $n$
* $X$ = eigenvectors matrix; # of free parameters: $n^2 - n$
* $S$ = symmetric matrix; # of free parameters: $\frac{1}{2}n(n+1)$

For SVD, suppose $m \leq n$, the matrix has full rank $m$. From matrix $A$ we know there are $mn$ parameters.
$$
A_{m \times n} = U \Sigma V^T =  (m \times m)(m \times n)(n \times n)
$$
From SVD, we calculate the number of parameters
$$
\frac{1}{2} m (m-1) + m + (n-1)+ (n-2) + ... + (n-m) = \frac{1}{2} m (m-1) + m + mn - \frac{1}{2}m(m+1) = mn
$$
Therefore, let SVD for any matrix of rank 1: $A = U_{mr} \Sigma_{rr} V_{rm}^T$, the # of free parameters is 
$$
mr - \frac{1}{2}r(r+1)+r + rm - \frac{1}{2} r(r+1) = mr + nr - r^2
$$

## Saddle Points

The largest eigenvalue of $S + T$ matrix satisfies: 
$$
\lambda_{max}(S + T) \leq \lambda_{max}(S) + \lambda_{max}(T)
$$
where $\lambda_{max}(S + T)$ is the largest value of $\frac{\mathbf{x}^T(S + T)\mathbf{x}}{\mathbf{x}^T\mathbf{x}}$, $ \lambda_{max}(S)$ is the largest value of $\frac{\mathbf{x}^T S\mathbf{x}}{\mathbf{x}^T\mathbf{x}}$, $\lambda_{max}(T)$ is the largest value of $\frac{\mathbf{x}^T T\mathbf{x}}{\mathbf{x}^T\mathbf{x}}$. 

Similarly,
$$
\lambda_{min}(S + T) \geq \lambda_{min}(S) + \lambda_{min}(T)
$$
The eigenvectors $q_2, ..., q_{n-1}$ that correspond to eigenvalues $\lambda_2$ to $\lambda_{n-1}$, are **saddle points** of the function $R(\mathbf{x}) = \frac{\mathbf{x}^TS\mathbf{x}}{\mathbf{x}^T\mathbf{x}}$. The first derivatives of $R(\mathbf{x})$ are all zero at the eigenvectors $q_2, ..., q_{n-1}$. Saddle points make the eigenvalues hard to estimate / calculate in that the second derivatives of $R(\mathbf{x})$ are symmetric but **indefinite** (eigenvalues with opposite signs) at these points. 

## Lagrange Solution

Lagrange can be used to solve many saddle point problems. Let minimize a positive definite energy $\frac{1}{2} \mathbf{x}^TS\mathbf{x}$ with $m$ constraints $A\mathbf{x} = b$. The Lagrange function is 
$$
\text{Lagrangian} \quad L(x, \lambda) = \frac{1}{2} \mathbf{x}^TS\mathbf{x} + \lambda^T(A\mathbf{x} - \mathbf{b})
$$
By solving  $\partial L /\partial\mathbf{x} = 0$ and $\partial L /\partial\lambda = 0$ we have an indefinite block matrix
$$
\begin{bmatrix} \partial L /\partial\mathbf{x}\\ \partial L /\partial\lambda \end{bmatrix} = \begin{bmatrix} S \mathbf{x} + A^T \lambda \\ A\mathbf{x} - b \end{bmatrix} \quad \text {and} \quad H \begin{bmatrix} x \\ \lambda \end{bmatrix} = \begin{bmatrix} S&A^T \\ A&0 \end{bmatrix}\begin{bmatrix} \mathbf{x} \\ \lambda \end{bmatrix} = \begin{bmatrix} 0 \\ b \end{bmatrix}
$$
The matrix $H$ has negative determinant, and its eigenvalues have opposite signs. The solution $(x, \lambda)$ is a saddle point of Lagrange's function $L$.

## Saddle Points from Rayleigh Quotients

The maximum and minimum of the Rayleigh quotient $R(\mathbf{x}) = \mathbf{x}^TS\mathbf{x}/\mathbf{x}^T\mathbf{x}$ are $\lambda_1$ and $\lambda_n$.
$$
\text{Maximum } \frac{\mathbf{q}_1^TS\mathbf{q}_1}{\mathbf{q}_1^T\mathbf{q}_1} = \mathbf{q}_1^T \lambda_1 \mathbf{q}_1 = \lambda_1\\
\text{Minimum } \frac{\mathbf{q}_n^TS\mathbf{q}_n}{\mathbf{q}_n^T\mathbf{q}_n} = \mathbf{q}_n^T \lambda_n \mathbf{q}_n = \lambda_n\\
$$
Applying Lagrange
$$
\max \frac{\mathbf{x}^TS\mathbf{x}}{\mathbf{x}^T\mathbf{x}}  = \max \mathbf{x}^TS\mathbf{x} \text{ subject to }\mathbf{x}^T\mathbf{x} = 1
$$
With Lagrange multiplier
$$
L(x, \lambda) = \mathbf{x}^TS\mathbf{x} - \lambda(\mathbf{x}^T\mathbf{x} - 1)
$$
By solving  $\partial L /\partial\mathbf{x} = 0$ and $\partial L /\partial\lambda = 0$ we get **max-min-saddle points**

> #### Example 19
>
> What the max-min-saddle points of 
> $$
> R = \frac{\mathbf{x}^TS\mathbf{x}}{\mathbf{x}^T\mathbf{x}} = \frac{5 u^2 + 3v^2 + w^2}{ u^2 + v^2 + w^2}
> $$
>
> > **Answer**: maximum value 5 at $x = (1,0,0)$, minimum value 1 at $x = (0,0,1)$, saddle point value 3 at $x = (0,1,0)$.
>
> > **Solution**: All partial derivatives are zero at those three points, which are eigenvectors of the diagonal matrix $S$, and the eigenvalues corresponding to those eigenvectors are 5, 1, 3.

