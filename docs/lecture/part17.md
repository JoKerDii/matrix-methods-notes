# Rapidly Decreasing Singular Values

[咕咕咕 TOO tough, only got some intuitions]

Given a real matrix $X_{n \times n}$, its singular values $\sigma_1(x) \geq \sigma_2(x) \geq ... \geq \sigma_n(x) \geq 0$ give information: suppose $\sigma_{k+1}(x) = 0, \sigma_k(x)>0$, 

* $\text{rank}(x) = k$
* $X = \mathbf{u_1}\mathbf{v_1}^T + ... + \mathbf{u_k}\mathbf{v_k}^T$
* dim(col space) = dim(row space) = k

## Low-rank Matrix

**Definition** **of low-rank matrix** is that, $X = $ low rank if $2kn < n^2 \implies k< n/2$. In practice, we demand $k << n/2$.

Intuitively visualized low-rank matrix:

* Rank 1: matrices are highly **aligned** with the coordinates/ grid.

  * A counter example of a matrix that is bad for low rank: ("Triangular Flag")

    Suppose a triangular matrix $X = \begin{bmatrix} 1&0&...&0 \\ 1&1&0& \\ ...&...&...&\\1&...&...&1\\\end{bmatrix}$, the inverse of $X$ is $X^{-1} = \begin{bmatrix} 1&&& \\ -1&1&& \\ &-1&...&\\&&...&1\\\end{bmatrix}$, the inverse of $X^TX$ is $(X^TX)^{-1} = \begin{bmatrix} 1&-1&& \\ -1&2&-1& \\ &-1&...&...\\&&...&2\\\end{bmatrix}$, the singular values can be written as
    $$
    \sigma_k(x) = [2\sin(\frac{\pi(2k-1)}{2(2n+1)})]^{-1}
    $$
    We solve for the first singular value and the $n$th (last) singular value
    $$
    \sigma_1(x) \approx \frac{2n}{\pi}\\
    \sigma_n(x) \approx \frac{1}{2}
    $$
    These singular values are all large and not approximate to zero, this is why triangular matrix is bad for low rank.

  * A circle is convenient for low rank ("Japanese Flag")

    because by getting rid of the inscribed rank-one square, the small part left won't have large rank.

## Numerical Rank

Suppose $k$ is the last singular value above $\epsilon$ (tolerance, $0<\epsilon<1$). i.e.
$$
\sigma_{k+1} \leq \epsilon \sigma_1(x)\\
\sigma_{k} > \epsilon \sigma_1(x)
$$
We define the rank of this matrix as
$$
\text{rank}_\epsilon(X) = k
$$
when $\epsilon = 0$, the rank is 
$$
\text{rank}_0(X) = \text{rank}(X)
$$

## Eckart-Young

Eckart-Young tells how to approximate the matrix $X$ by a low rank matrix. In particular, how a matrix $X$ can be approximated by a rank $k$ matrix $X_k$.
$$
\sigma_{k+1}(X) = \|X-X_k\|_2
$$
where $X_k$ is the best rank-$k$ matrix to approximate $X$. When $X$ has exactly $k$ rank, the $\sigma_{k+1}(X)$ should be 0.

## Matrices of Numerical low rank

* All low-rank matrices

* Full-rank matrices that have singular values decaying rapidly - that is, full-rank matrices with low numerical rank.

  * e.g. Hilbert Matrix is full rank but has extreme low numerical rank.
    $$
    H_{jk} = \frac{1}{j+k+1}
    $$

  * e.g. Vandermonde Matrix

## The World is Smooth

Reason why many numerical low rank matrices exist.

Suppose a polynomial of two variables:  $p(x,y) = 1 + x + xy$
$$
X_{jk} = p(j,k) = 1 + j + jk
$$
The matrix $X_{jk}$ has rank of (1 + 1 + 1) = 3. (Note that the final term is a column vector times a row vector)

Now we show that this matrix $X$ is a numerical low rank matrix. In general, suppose we have polynomial of degree of $m$,
$$
p(x,y) = \sum^{m-1}_{s=0} \sum^{m-1}_{t=0} a_{st} x^s y^t
$$
Let $X_{jk} = p(j,k)$, the rank is very low whereas the matrix $X$ is very large
$$
\text{rank}(X) \leq m^2
$$
In the case of Hilbert Matrix $X_{jk} = \frac{1}{j+k+1}$, we define a function $f(x,y) = \frac{1}{x+y-1}$ and we want to find an approximation $p$ by sampling to $f$ that
$$
|f(x,y) - p(x,y)| \leq \epsilon/n \|x\|
$$
Let matrix $Y_{jk} = p(j,k)$ which has finite rank, so the previous inequation can be written as
$$
\|X-Y\|_2 \leq \epsilon \|X\|_2
$$

## The World is Sylvester

Theorem: If $X$ satisfies $AX - XB = C$, and $A,B$ are normal, then 
$$
\sigma_{k+1}(x) \leq Z_k(E,F) \sigma_1(x)\\
\text{rank}(c) = r
$$
where $Z_k(E,F)$ is Zolotarev number, $E$ is a set of eigenvalues of $A$, $F$ is a set of eigenvalues of $B$. The key fact is that the sets $E$ and $F$ are separated. 