# Positive Definite and Semidefinite Matrices

## Specialty of Symmetric Matrices $S = S^T$

1. **All $n$ eigenvalues $\lambda$ of a symmetric matrix $S$ are real numbers.**

2. **The $n$ eigenvectors $q$ can be chosen orthogonal or rescaled orthonormal.**

   Thus, the **eigenvector matrix** of $S$ has $Q^TQ = I$ and $Q^T = Q^{-1}$. 

   **Spectral Theorem:** Every real symmetric matrix has the form $S = Q \Lambda Q^T$

   Also, every matrix of that form is symmetric: 
   $$
   (Q\Lambda Q^T)^T = Q^{TT}\Lambda^TQ^T = Q\Lambda^TQ^T = Q\Lambda Q^T
   $$
   Note that $\Lambda$ is a diagonal matrix $\Lambda^T = \Lambda$

## Tests for Positive Definite and Semi Definite Matrices

#### Five Tests for Positive Definite Matrices

1. All $\lambda_i > 0$.
2. Energy $x^TSx > 0$ (All $x \neq 0$)
3. $S = A^TA$ (columns of A are independent)
4. All leading determinants $> 0 $.
5. All pivots $> 0 $ in elimination

> #### Example 15
>
> $S$ is positive definite, what about $S^{-1}$, $Q^TSQ$?
>
> > **Answer**: They are positive definite, too.
>
> > **Solution**: 
> >
> > $S^{-1}$ has eigenvalue of $1/\lambda > 0$.
> >
> > $(Q^TSQ)^T = Q^TS^TQ$, as $S$ is symmetric $S = S^T$, $Q^TSQ$ is symmetric too. Since $Q^T = Q^{-1}$, $Q^TSQ = Q^{-1}SQ$. Since $S$ and $Q^{-1}SQ$ are "similar matrices", they have same eigenvalues. Therefore, $Q^TSQ$ is also positive definite.

#### Five Tests for Semi Definite Matrices

(**Semidefinite allows energy/ eigenvalues/ determinants/ pivots of $S$ to be zero.**)

1. All $\lambda_i \geq 0$.
2. Energy $x^TSx \geq 0$ (All $X \neq 0$)
3. $S = A^TA$ (columns of A are independent or dependent)
4. All leading determinants $\geq 0 $.
5. All pivots $\geq 0 $ in elimination

> #### Example 16
>
> A semi-definite case $\begin{bmatrix}3&4 \\4&16/3 \end{bmatrix}$ with zero determinant, there must be at least one eigenvalue is zero. How do we know other eigenvalues are positive?
>
> > **Answer**: Trace: 3 + 16/3  = $\lambda_1 + \lambda_2$. Since the determinant is 0, it is a singular matrix, $\lambda_2 = 0$. Thus, $\lambda_1 = 3+ 16/3 = 8\frac{1}{3}$.



## Energy-based Definition (2nd test)

$S$ is positive definite if the energy $x^TSx$ is positive for all vectors $x \neq 0$.

> #### Example 17
>
> $$
> E = x^TSx = \begin{bmatrix}x_1 x_2\end{bmatrix} \begin{bmatrix}2&4\\ 4&9\end{bmatrix} \begin{bmatrix}x_1 \\ x_2\end{bmatrix} = 2x_1^2 + 8x_1 x_2 + 9 x_2^2
> $$
>
> $E(x)$ is a positive energy. 

* The graph of $E(x)$ in above example is a **bowl opening upwards**. 
  * Property: The bottom point of the bowl has energy $E = 0$ when $x=y=0$.
  * Property: minimum at where the first derivative $\frac{df}{dx}$ is 0 and second derivative $\frac{d^2f}{dx^2}$ is **positive definite** at minimum point.
  * Property: the graph goes upwards whenever the second derivative matrix is positive definite.
    * If $S$ has a negative eigenvalue $\lambda < 0$, the graph goes below zero. 
    * There is a maximum if $S$ is negative definite (all $\lambda < 0$, upside down bowl)
    * There is a saddle point if $S$ has both positive and negative eigenvalues. A saddle point matrix is "indefinite".

* If $x^TSx > 0$ for the eigenvectors of $S$, then $x^TSx > 0$ for every nonzero vector $x$.  

  Since $x^TSx$ is a positive combination of the energies $\lambda_kx_k^Tx_k > 0$ for every nonzero vector x. 

$$
\begin{aligned}
x^TSx & = (c_1x_1^T + ... + c_nx_n^T)S(c_1x_1 + ... + c_nx_n) \\
& = (c_1x_1^T + ... + c_nx_n^T)S(c_1\lambda_1x_1 + ... + c_n\lambda_nx_n) \\
& = c_1^2\lambda_1x_1^Tx_1 + ... + c_n^2\lambda_nx_n^Tx_n > 0 \text{ if every } \lambda_i > 0
\end{aligned}
$$

* Connection between positive energy and positive eigenvalues: 

  If $Sx = \lambda x$ then $x^TSx = \lambda x^Tx$, so $\lambda > 0$ leads to $x^TSx > 0$.

* Test without knowing any eigenvalues or eigenvectors:

  If $S_1$ and $S_2$ are symmetric positive definite, so is $S_1 + S_2$.
  $$
  x^T(S_1 + S_2)x = x^TS_1x + x^TS_2x > 0 
  $$

## Three More Equivalent Tests (3,4,5th tests)

* $S = A^TA$ for a matrix $A$ with **independent** columns
  $$
  \text{Energy } = x^TSx = x^TA^TAx = (Ax)^T(Ax) = \|Ax\|^2
  $$
  The energy is the length squared of the vector $Ax$ which must be non-negative, meaning $S$ or $A^TA$ is at least semidefinite.

  * When energy is positive, $Ax$ have to be non-zero vector $Ax \neq 0 $ when $x \neq 0$, so the columns of $A$ must be **independent**. 
  * When energy is zero, there must be a $\lambda = 0$, so $A$ must have **dependent** columns. In this case, $S$ is a semi-definite matrix.

* **Leading determinants** are those start from the upper left of a matrix. 

* Leading determinants are closely related to **pivots** (the number on the diagonal after elimination)

  The $k$th pivot equals the ratio $\frac{D_k}{D_{k-1}}$ of the leading determinants (sizes $k$ and $k-1$).

  So the pivots are all positive when the leading determinants are all positive.

> #### Example 18
>
> $\begin{bmatrix}3&4 \\ 4&6 \end{bmatrix}$ is positive-definite with positive leading determinants.
>
> $\begin{bmatrix}-3&4 \\ 4&-6 \end{bmatrix}$ is not positive-definite, since the first leading determinant is negative.
>
> The first and second leading determinants of $\begin{bmatrix}3&4 \\ 4&6 \end{bmatrix}$ are 3 and $(3 \times 6) - (4 \times 4) = 2$. Thus the first and second pivots are 3 and $3/2$.

* $S = A^TA$ where $A$ can be 1) symmetric or 2) triangular

  1) If $S = Q^T\Lambda Q$, then $S = (Q\sqrt{\Lambda} Q^T)^T(Q\sqrt{\Lambda} Q^T)$, where $A = Q\sqrt{\Lambda}Q^T = A^T$ is a symmetric matrix.

  2) If $S = LU = LDL^T$ with positive pivots in $D$, then $S = (L\sqrt{D})(\sqrt{D}L^T) = A^TA$, where $A$ is upper triangular and $\sqrt{\text{pivot}}$ on the main diagonal of $A$.

  * Since elimination is triangular factorization $S = LU$, for symmetric matrix, it can be $S = LDL^T$, where pivots are on the diagonal of $D$. After sharing those pivots $S = (L\sqrt{D})(\sqrt{D}L^T) = A^TA$ -- "**Cholesky factorization**".

> #### Example 19
>
> Is this matrix $S = \begin{bmatrix}1&1&1 \\1&1&1 \\ 1&1&1 \end{bmatrix}$ positive definite or semi definite or none of both?
>
> > **Answer**: semi-definite
>
> > **Solution**: 
> >
> > Symmetric matrix $S$ can be written as $S = A^TA = \begin{bmatrix}1&1&1\end{bmatrix} \begin{bmatrix}1\\1\\1\end{bmatrix}$. Notice that the rank of $S$ is 1, so it only has one non-zero eigenvalues $\lambda_2 = \lambda_3 = 0$. Since Trace = $\lambda_1 + \lambda_2 + \lambda_3 = $ sum of values on the diagonal of $S$ = $1 + 1 + 1 = 3$, we got  $\lambda_1 = 3$. 
> >
> > $S$ can also be written as $S = Q\Lambda Q^T = \lambda_1 q_1 q_1^T + \lambda_2 q_2 q_2^T + \lambda_3 q_3 q_3^T = \lambda_3 q_3 q_3^T$ where $Q$ is orthonormal eigenvector matrix.  $\lambda_3 q_3 q_3^T = 3 \begin{bmatrix}1/\sqrt{3}&1\sqrt{3}&1\sqrt{3}\end{bmatrix} \begin{bmatrix}1\sqrt{3}\\1\sqrt{3}\\1\sqrt{3}\end{bmatrix}$.
> >
> > We can conclude that $S$ is semi-definite since it has zero eigenvalues as well as positive eigenvalues.
> >
> > Note that
> >
> > * If $S$ has zero eigenvalues, it is not positive definite.
> > * If all eigenvalues of $S$ are non-negative, it has a positive eigenvalue, it is semi-definite.

## Ellipse $ax^2 + 2bxy + cy^2 = 1$

$S = Q \Lambda Q^T$ is **positive definite** when all $\lambda_i > 0$. The graph of $x^TSx = 1$ is an **ellipse** (by cutting through the bowl at height $x^TSx = 1$), with its axes pointing along the eigenvectors of $S$.

$S = Q \Lambda Q^T$ is the "**Principal axis theorem**": it displays the **axes**'s **directions** (from the **eigenvectors**) and the axis **length** (from the **eigenvalues** $\lambda$'s). Length = $1/\sqrt{\lambda}$. The bigger eigenvalue gives shorter axis. 

> #### Example 20
>
> $S = \begin{bmatrix}5&4 \\ 4&5 \end{bmatrix}$ has $\lambda = 9$ and $1$. Energy ellipse $5x^2 + 8xy + 5y^2 = 1$. The eigenvectors are $q_1 = (1,1)$ and $q_2 = (1,-1)$. 
>
> To line up the ellipse to new coordinates $X$ and $Y$: Divided by $\sqrt{2}$ to get unit vectors. With those orthonormal eigenvectors $S = Q\Lambda Q^T$. Then get the energy $x^TSx = (x^TQ) \Lambda (Q^Tx)$. 
> $$
> 5x^2 + 8xy + 5y^2 =9(\frac{x+y}{\sqrt{2}})^2 + 1(\frac{x-y}{\sqrt{2}})^2
> $$
> Note that 9 and 1 are from $\Lambda$. Orthonormal eigenvectors are inside the squares $(1,1)/\sqrt{2}$ and $(1,-1)/\sqrt{2}$.
>
> Now we have lined up ellipse:
> $$
> \frac{x+y}{\sqrt{2}} = X, \frac{x-y}{\sqrt{2}} = Y, \text{ and } 9X^2 + Y^2 = 1
> $$
> The greater length of axis is 1 and the shorter length is 1/3.



