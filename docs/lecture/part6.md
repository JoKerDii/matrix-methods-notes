# Singular Value Decomposition (SVD)

Reason why we need SVD $A = U\Sigma V^T$ rather than $S = Q \Lambda Q^T$:

* The best matrix -  symmetric matrix has real eigenvalues and orthogonal eigenvectors, but not all matrices are like that. Other matrices have complex eigenvalues or non-orthogonal eigenvectors. 
* If $A$ is not square then $Ax = \lambda x$ is impossible and eigenvectors fail.

## Basics of SVD

For a real $m \times n$ matrix $A$, $n$ right orthogonal ( in $R^n$, $V^T = V^{-1}$) **singular vectors** $v_1, ..., v_n$ and $m$ left orthogonal ( in $R^m$, $U^T = U^{-1}$) **singular vectors** $u_1, ..., u_m$ are connect (in **vector** form) by:
$$
Av_1 =\sigma_1 u_1, ..., Av_r =\sigma_r u_r\\
Av_{r+1} = 0, ..., Av_n = 0
$$
where $r$ is the **rank** of matrix $A$, the number of **independent** columns (and rows). Thus the last $n-r$ $v$' are in the null space of $A$, and the last $m-r$ $u$'s are in the null space of $A^T$. Those $r$ positive singular values are in descending order $\sigma_1 \geq \sigma_2 ... \sigma_r > 0$.

In **matrix** form: 
$$
AV = U\Sigma\\
A\begin{bmatrix} \\ v_1, ...,v_r, ..., v_n \\ \\ \end{bmatrix} = \begin{bmatrix} \\ u_1, ..., u_r, ..., u_m\\ \\ \end{bmatrix} \begin{bmatrix}\sigma_1 & & & \\ &...& &\\ & &\sigma_r&\\ & & & 0\end{bmatrix}
$$
Note that we can reduce it to $AV_r = U_r\Sigma_r$ since other parts produce zeros. Now $\Sigma_r$ is square.

[Recall that **eigenvectors** are connected in vector form by $Ax = \lambda x$, and in matrix form by $AX = X\Lambda$].

Therefore, the SVD of $A$ is 
$$
A = U\Sigma V^T = \sigma_1 u_1 v_1^T + ... + \sigma_r u_r v_r^T
$$
Note that those pieces of $A$ come in order of importance, $\sigma_1 u_1 v_1^T$ is the most important piece since the $\sigma_1$ is the largest.  **The sum of the first $k$ pieces is best possible for rank $k$**: $A_k = \sigma_1 u_1 v_1^T + ... + \sigma_k u_k v_k^T$ is the best rank $k$ approximation to $A$.

> #### Exercise 4
>
> Why are all eigenvalues of a square matrix $A$ less than or equal to $\sigma_1$?
>
> > **Answer:  $\|Ax\| = \|U \Sigma V^Tx\| = \|\Sigma V^Tx\| \leq \sigma_1 \|V^Tx\| = \sigma_1\|x\| \text{ for all } x$**
> >
> > Note that multiplying by orthogonal matrices $U$ and $V^T$ does not change vector lengths. Since an eigenvector has $\|Ax\| = |\lambda| \|x\|$, then $|\lambda| \|x\| \leq \sigma_1 \|x\|$ and $|\lambda| \leq \sigma_1$. 

## Two Proofs of SVD

1. With $A = U\Sigma V^T$, we form $A^TA$ and $AA^T$:
   $$
   A^TA = (V\Sigma^TU^T)(U\Sigma V^T) = V\Sigma^T\Sigma V^T\\
   AA^T = (U\Sigma V^T)(V\Sigma^TU^T) = U\Sigma\Sigma^T U^T
   $$
   Both RHS are **symmetric matrices** with the special form $Q \Lambda Q^T$. Non-zero eigenvalues $\sigma_1^2,...,\sigma_r^2$ are in $\Sigma^T\Sigma$ or $\Sigma\Sigma^T$ in same numbers. $V$ contains orthonormal eigenvectors of $A^TA$ ($V^TV = 1$). $U$ contains orthonormal eigenvectors of $AA^T$ ($U^TU = 1$). 

2. As $V$ contains orthonormal eigenvectors of $A^TA$, with $Av_k = \sigma_ku_k$, determine $u$'s.
   $$
   A^TAv_k = \sigma_k^2 v_k \text{ and then } \\ v_k = Av_k / \sigma_k \text{ for } k = 1,..., r
   $$
   Prove $u$'s are **eigenvectors** of $AA^T$
   $$
   AA^T u_k = AA^T(\frac{Av_k}{\sigma_k}) = A(\frac{A^TA v_k}{\sigma_k}) = A\frac{\sigma_k^2 v_k}{\sigma_k} = \sigma_k^2 u_k
   $$
   Prove $u$'s are **orthonormal**
   $$
   u_j^Tu_k = (\frac{Av_j}{\sigma_j})^T(\frac{Av_k}{\sigma_k}) = (\frac{v_j^T(A^TA v_k)}{\sigma_j \sigma_k}) = \frac{\sigma_k}{\sigma_j} v_j^Tv_k = \begin{cases}
         1, & \text{if }\ j = k \\
         0, & \text{if }\ j \neq k
       \end{cases}
   $$

> #### Example 18
>
> Find the matrices $U, \Sigma, V$ for $A = \begin{bmatrix}3&0\\4&5 \end{bmatrix}$.
>
> 1. Compute $A^TA, AA^T$.
>
>    $A^TA = \begin{bmatrix}25&20\\20&25 \end{bmatrix}$, $AA^T = \begin{bmatrix}9&12\\12&41 \end{bmatrix}$
>
>    They have same trace 50 and same eigenvalues $\sigma_1^2 = 45$ and $\sigma_2^2 = 5$. The determinant of $A$ is $\sigma_1 \sigma_2 = \sqrt{45 \times 5} = 15$.
>
> 2. Compute right singular vectors $V$ - the eigenvectors of $A^TA$
>    $$
>    A^TAv_1 = \sigma_1^2v_1\\
>    \begin{bmatrix}25&20\\20&25 \end{bmatrix}v_1 = 45 v_1\\
>    v_1 = \begin{bmatrix}1\\1 \end{bmatrix}
>    $$
>
>    $$
>    A^TAv_2 = \sigma_2^2v_2\\
>    \begin{bmatrix}25&20\\20&25 \end{bmatrix}v_2 = 5 v_2\\
>    v_2 = \begin{bmatrix}-1\\1 \end{bmatrix}
>    $$
>
> 3. Normalize right singular vectors $V$ as it is orthonormal
>    $$
>    v_1 = 1/\sqrt{2} \begin{bmatrix}1\\1 \end{bmatrix}, v_2 = 1/\sqrt{2} \begin{bmatrix}-1\\1 \end{bmatrix}
>    $$
>
> 4. Compute left singular vectors $U$ according to $u_i = \frac{Av_i}{\sigma_i}$.
>    $$
>    Av_1 = \sigma_1 u_1\\
>    \begin{bmatrix}3&0\\4&5 \end{bmatrix} 1/\sqrt{2} \begin{bmatrix}1\\1 \end{bmatrix} = \sqrt{45} u_1\\
>    u_1 = \begin{bmatrix}1\\3 \end{bmatrix}
>    $$
>
>    $$
>    Av_2 = \sigma_2 u_2\\
>    \begin{bmatrix}3&0\\4&5 \end{bmatrix} 1/\sqrt{2} \begin{bmatrix}-1\\1 \end{bmatrix} = \sqrt{5} u_1\\
>    u_2 = \begin{bmatrix}-3\\1 \end{bmatrix}
>    $$
>
> 5. Normalize left singular vectors $U$ as it is also orthonormal
>    $$
>    u_1 = 1/\sqrt{10} \begin{bmatrix}1\\3 \end{bmatrix}, u_2 = 1/\sqrt{10} \begin{bmatrix}-3\\1 \end{bmatrix}
>    $$
>
> 6. Finally we got $U, \Sigma, V$.
>    $$
>    U = 1/\sqrt{10} \begin{bmatrix}1&-3\\3&1 \end{bmatrix}, \Sigma = \begin{bmatrix}\sqrt{45}& \\ &\sqrt{5} \end{bmatrix}, V = 1/\sqrt{2} \begin{bmatrix}1&-1\\ 1&1 \end{bmatrix}
>    $$

## Geometry of SVD

As $U$ and $V^T$ are orthogonal, they can be rotation or possible reflection. As $\Sigma$ is diagonal, it can stretch the matrix.