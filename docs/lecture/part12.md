# Computing Eigenvalues and Singular Values

## 1. Compute Eigenvalues of S

**QR algorithm**:

1. Simplify original matrix $S$ by Lanczos to the **tridiagonal** $T = Q^TSQ = Q^{-1}SQ$ leaving eigenvalues alone. Now we have $T = T_0$.
2. By Gram-Schmidt or Householder, factor $T_0$ into $QR$. Notice $R = Q^{-1}T_0$.
3. Reverse those factors $Q$ and $R$ to produce $T_1 = RQ = Q^{-1}T_0Q$.
4. Repeat over and over again.

Note that the new $T_1 = Q^{-1}T_0Q$ still **tridiagonal** and is **similar** to $T$ with same eigenvalues. Those similar matrices $T, T_1, T_2,...$ approach a diagonal matrix $\Lambda$, which reveals the unchanged eigenvalues of the original matrix $T$. The first eigenvalue is in the last entry $T_{nn}$.

**Improved QR algorithm**:

Shift $QR$ by substracting a multiple $s_k I$ of the identity matrix before the $QR$ step, and adding it back after the $RQ$ step.

1. Simplify original matrix $S$ by Lanczos to the tridiagonal $T = Q^TSQ = Q^{-1}SQ$ leaving eigenvalues alone. Now we have $T = T_0$.
2. Choose a shift $s_k$ at step $k$
3. Factor $T_k - s_kI = Q_kR_k$
4. Reverse factors and shift back: $T_{k+1} = R_kQ_k + s_kI$

Similar to the previous $QR$ method, the $T$'s are similar matrices, which is proved by
$$
T_{k+1} = Q_k^{-1}(T_k - s_kI)Q_k + s_kI = Q_k^{-1}T_kQ_k
$$
$T_{k+1}$ is still symmetric because $T_{k+1} = Q_k^{-1}T_kQ_k$ and $Q_k^{-1} = Q_k^T$.

Note that well-chose shifts $s_k$ will greatly speed up the approach of the $T$'s to a diagonal matrix $\Lambda$. A good shift is $s_k=T_{nn}$ suggested by Wilkinson.

## 2. Compute Singular Values of S

Singular values are the same for $\Lambda$ and $Q_1AQ_2^T$ even if $Q_1$ is different from $Q_2$, because multiplying two orthogonal matrices produces an orthogonal matrix. And this $ Q_1AQ_2^T$ gives a **bidiagonal** matrix. 

The Golub-Kahan algorithm for the SVD works directly on $A$, in two steps

1. Find $Q_1$ and $Q_2$ so that $Q_1 AQ_2^T$ is bidiagonal
2. Adjust the shifted $QR$ algorithm to preserve singular values of this bidiagonal matrix.

Note that singular values of $A$ are the square roots of the eigenvalues of $S = A^TA$. And the unchanged singular values of $Q_1AQ_2^T$ are the square roots of the unchanged eigenvalues of $(Q_1AQ_2^T)^T(Q_1AQ_2^T) = Q_2A^TAQ_2^T$. **Multiply (bidiagonal)^T(bidiagonal) to get tridiagonal**.

