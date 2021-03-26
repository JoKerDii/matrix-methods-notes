# Norms of Vectors and Matrices

Every norm for vectors or functions or matrices must share these properties:

* The norm of a nonzero vector $v$ is a positive number $\|v\|$.
* All norms multiply $v$ by $c$ (**Rescaling**): $\|cv\| = |c| \|v\|$
* All norms add $v$ to $w$ (**Triangle inequality**): $\|v + w\| \leq \|v\| + \|w\|$

Three special norms of $l^p$ norm: $\|v\|_p = (|v_1|^p + ... + |v_n|^p)^{1/p}$.

* $l^2$ norm: Euclidean norm
  $$
  \|v\|_2 = \sqrt{|v_1|^2 + ... + |v_n|^2}
  $$

* $l^1$ norm: 
  $$
  \|v\|_1 = |v_1| + ... + |v_n|
  $$

* $l^{\infty}$: max norm
  $$
  \|v\|_{\infty} = \text{maximum of }|v_1|, ..., |v_n|
  $$

Note that minimization in $l^1$ produces sparse solutions. There are few nonzero components. By contrast, $l^2$ solution has many small components. $l^0$ norm is not a true norm as the geometry is not convex in 2D.

 $l^2$ norm connects to the ordinary geometry of inner products $(v,w) = v^Tw$ and angles $\theta$: 

* Inner product = length squared 
  $$
  v \cdot w = v^Tv = \|v\|^2
  $$

* Angle $\theta$ between vectors $v$ and $w$
  $$
  v^Tw = \|v\|\|w\| cos\theta
  $$

* The most important inequalities in mathematics

  * **Cauchy-Schwarz**
    $$
    |v^Tw| \leq \|v\|\|w\|
    $$

  * **Triangle Inequality**
    $$
    \|v+w\| \leq \|v\| + \|w\|
    $$

#### Matrix Norms $\|A\|$ from Vector Norms $\|v\|$

The largest **growth factor**:
$$
\|A\| = \max_{v \neq 0}\frac{\|Av\|}{\|v\|}
$$
Vector norm leads to a matrix norm.

* $l^2$ norm: $\|A\|_2 = $ largest singular value $\sigma_1$ of $A$

  * Coming from $A = U\Sigma V^T$, the orthogonal matrices $U$ and $V^T$ have no effect on $l^2$ norm
    $$
    \frac{\|Av_1\|}{\|v_1\|} = \frac{\|\sigma_1u_1\|}{\|v_1\|} = \sigma_1 \frac{\|u_1\|}{\|v_1\|} = \sigma_1
    $$

* $l^1$ norm: $\|A\|_1=$ largest $l_1$ norm of the columns of $A$

* $l^{\infty}$ norm $\|A\|_{\infty} =$ largest $l_1$ norm pf the rows of $A$ 

Note that those three norms are all not affected by $U$ and $V$ ("unitary invariance"), instead, we just take the vector $\sigma = (\sigma_1, \sigma_2, ..., \sigma_r)$ on the main diagonal of $\Sigma$
$$
\begin{aligned}
\|A\|_{Nuclear} & = \sigma_1 + ... + \sigma_r\\
\|A\|_F & = \sigma_1^2 +...+ \sigma_r^2\\
\|A\|_2 & = \sigma_1
\end{aligned}
$$
