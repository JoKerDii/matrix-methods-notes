# Eckart-Young: The Closest Rank k Matrix to A

## Principal Component Analysis (PCA)

The **PCA** uses the largest $\sigma$'s connect to the first $u$'s and $v$'s to understand the information in a matrix of data. $A_k$ is the most important part of matrix $A$.
$$
A_k = \sigma_1 u_1 v_1^T + ... + \sigma_k u_k v_k^T \text{ with rank } (A_k) = k
$$
The **principal components (PC)** of $A$ are its **singular vectors**. It is in the direction of the first singular vector $u_1$ of $A$.

#### Statistics behind PCA

Recall concepts: 

* The **variances** are the diagonal entries of the matrix $AA^T$
* The **covariances** are the off-diagonal entries of the matrix $AA^T$. High/positive covariance means that increased $y$ goes with increase $x$. Negative covariance means the opposite.

Steps: 

1. First we need to center the data by computing the mean of each row of the data, substracting the mean from each row. 

2. Second we need to compute sample covariance matrix.

   The **sample covariance matrix** is defined by 
   $$
   S = \frac{AA^T}{n-1}
   $$
   The factor is $n-1$ because one degree of freedom has already been used for mean = 0.

3. $S$ describes PCA

   * Two orthogonal eigenvectors of $S$ are $u_1$ and $u_2$, which are singular vectors (principal components) of $A$.
   * $u_1$ points to the direction that captures the most variance. $u_1$ also tells the slope or the direction by $u_{12}/u_{11}$ if $u = [u_{11}, u_{12}]$ for a 2 by 2 $S$.
   * The sum of eigenvalues $\sigma_i$ of $S$ is the trace of $S$. The first rank one piece $\sigma_1u_1v_1^T$ is the largest.

#### Geometry behind PCA

**The sum of squared distances from the data points to the $u_1$ line is a minimum.**

To see this, separate each column $a_j$ of $A$ into its components along $u_1$ and $u_2$:
$$
\sum^n_1 \|a_j\|^2 = \sum^n_1|a_j^Tu_1|^2 + \sum^n_1 |a_j^Tu_2|^2.
$$
On the RHS, $\sum^n_1|a_j^Tu_1|^2 = u_1^T(AA^T)u_1$. When we maximize that sum in PCA by choosing the top eigenvector $u_1$ of $AA^T$, we minimize the second sum.

#### Linear Algebra behind PCA

The **sample covariance matrix** is mentioned above $S = \frac{AA^T}{n-1}$.

The **total variance** comes from the Frobenius norm (squared) of $A$:
$$
T = \|A\|^2/(n-1) = (\|a_1\|^2 + ... + \|a_n\|^2)/(n-1)
$$
The numerator is the trace of $S$. As the trace of $S$ is the sum of eigenvalues $\sigma_i^2/(n-1)$ of $S$, the **total variance** can be written as
$$
T = \|A\|^2/(n-1) = (\sigma_1^2 + ... + \sigma_r^2)/(n-1)
$$
The first PC accounts for (explains) a fraction $\sigma_1^2/T$ of the total variance. 



## Eckart-Young

**Eckart-Young Theory: If $B$ has rank $k$ then $\|A - B\| \geq \|A - A_k\|$.**

**Eckart-Young Theory in $L^2$: If $\text{rank}(B)\leq k$ then $\|A - B\| = \max \frac{\|(A-B)x\|}{\|x\|} \geq \sigma_{k+1}$.**



Three types of matrix norm: 

* Spectral norm / $l_2$ norm

  $\|A\|_2 = \max \frac{\|Ax\|}{\|x\|} = \sigma_1$

* Frobenius norm

  $\|A\|_F = \sqrt{\sigma_1^2+ ... + \sigma_r^2}$

* Nuclear norm

  $\|A\|_N = \sigma_1 + ...+ \sigma_r$ 

Four properties of matrix norm:

* Different values for square identity matrix

  $\|I\|_2 = 1, \|I\|_F = \sqrt{n}, \|I\|_N = n$

* Replace $I$ by any orthogonal matrix $Q$ and the norms stay the same (because all $\sigma_i = 1$)

  $\|Q\|_2 = 1, \|Q\|_F = \sqrt{n}, \|Q\|_N = n$

* Those norms stay the same when $A$ is multiplied by an orthogonal matrix $Q$.

* All those norms have $\|Q_1 A Q_2^T\| = \|A\|$ for orthogonal $Q_1$ and $Q_2$.

