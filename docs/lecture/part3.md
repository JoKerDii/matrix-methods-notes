# Orthogonal Columns in $Q$ Give $Q'Q = I$

### Five Key Ideas about **Orthogonality**

#### 1. Orthogonal vectors $x$ and $y$: $x^Ty = x \cdot y = 0$

> #### Example 4: 
>
> Dot product $x^Ty$ and $y^Tx$ always equal $\|x\|\|y\|cos\theta$, where $\theta$ is an angle between $x$ and $y$. So in all cases we have the Law of Cosines:
> $$
> c^2 = a^2 + b^2 - 2abcos\theta\\
> \|x-y\|^2 = \|x\|^2 + \|y\|^2 -2\|x\|\|y\|cos \theta
> $$
> Orthogonal vector have $cos\theta = 0$ and that last term disappears.

#### 2. Orthogonal basis for a subspace: Every pair of basis vectors has $v_i^Tv_j = 0$; Orthonormal basis: orthogonal basis of unit vectors.

> #### Example 5:
>
> The standard basis is orthogonal (even orthonormal) in $R^n$.
>
> Standard basis in $R^3$: $i = [1,0,0]^T$, $j = [0,1,0]^T$, $k = [0,0,1]^T$.

> #### Example 6:
>
> Every subspace of $R^n$ has an orthogonal basis.
>
> A plane in 3D space $R^3$. The plane has vector $a$ and $b$. Substract away from $b$ its component in the direction of $a$ gives an orthogonal basis.
> $$
> c = b - \frac{a^Tb}{a^Ta} a\\
> a^Tc = a^Tb - a^Tb = 0
> $$
> This is the idea of **orthogonalizing**, making basis to orthogonal basis. 

#### 3. Orthogonal subspaces R and N. The row space and null space are orthogonal.

**Four fundamental subspaces**: ($A$ matrix ($m \times n$), rank $r$)

* Column space $C(A)$ : dimension = $r$
* Row space $C(A^T)$: dimension = $r$
* Null space $N(A)$: dimension = $n-r$
* Null space $N(A^T)$: dimension = $m-r$

Recall that **null space** is a set of solution to $Ax = 0$.

Key points: [Two subspaces in $R^n$ and two subspaces in $R^m$]

* $C(A^T)$ and $N(A)$ are in $R^n$ space, and they are orthogonal.
* $C(A)$ and $N(A^T)$ are in $R^m$ space, and they are orthogonal.

> #### Example 7: 
>
> Given $A = \begin{bmatrix}  1&2&3\\ 4&7&9 \end{bmatrix}$ is a ($2\times 3$) matrix.
>
> $C(A^T)$ is the row space, each row has 3 elements or in 3 dimension. $N(A) = \begin{bmatrix}  x_1\\ x_2 \\x_3 \end{bmatrix}$ that satisfies $\begin{bmatrix}  1&2&3\\ 4&7&9 \end{bmatrix} \begin{bmatrix}  x_1\\ x_2 \\ x_3 \end{bmatrix} = 0$, where every row of $A$ is orthogonal to vector $x$. $C(A^T)$ and $N(A)$ are in $R^3$.
>
> $C(A)$is the column space, each column has 2 elements or in 2 dimension. $N(A^T) = \begin{bmatrix}  x_1\\ x_2 \end{bmatrix}$ that satisfies $\begin{bmatrix}  1&4\\ 2&7\\ 3&9 \end{bmatrix}\begin{bmatrix}  x_1\\ x_2 \end{bmatrix} = 0$, where every row of $A^T$ is orthogonal to vector $x$. $C(A)$ and $N(A^T)$ are in $R^2$.

> #### Example 8:
>
> **Singular Value Decomposition (SVD)** finds orthonormal bases $v_1, ..., v_r$ for the row space of $A$ and $u_1, ..., u_r$ for the column space of $A$. Each pair of $v$ and $u$ is connected by $A$. Multiplying by $A$ takes an orthogonal basis of $v$'s to an orthogonal basis of $u$'s.
> $$
> \text{Singular vectors } Av_1 = \sigma_1 u_1, Av_2 = \sigma_2 u_2, ... , Av_r = \sigma_r u_r
> $$

#### 4. Tall thin matrix $Q$ with orthonormal columns: $Q^TQ=I$ .

All the matrices $P= QQ^T$ have $P^2 = P$ (which signals a **projection matrix**), because 
$$
P^2 = (QQ^T)(QQ^T) = Q(Q^TQ)Q^T = QQ^T=P
$$
If $P^2 = P = P^T$ then $Pb$ is the **orthogonal projection** of $b$ onto the column space of $P$. 

> #### Example 9:
>
> To project $b$ on the $Q_1$ line , multiply by $P_1 = Q_1Q_1^T$. We got projection $P_1b$ and error $e = (I-P_1)b$.  We can also project $b$ on the $Q_2$ plane or $Q_3$ space.
>
> Note that $P_3 = Q_3Q_3^T = I$, we got
> $$
> P_3b = Q_3Q_3^Tb\\
> P_3b=b
> $$
> The error is now 0.

**The eigenvectors of a real matrix $A$ are orthogonal if and only if $A^TA = AA^T$.**

#### 5. Orthogonal (this word assumes square) matrices $Q$ have orthonormal columns $Q^T = Q^{-1}$. Since $Q^TQ = I$.

For square matrices $Q^TQ = I$ leads to $QQ^T = I$. The columns of $Q$ are an orthonormal basis for $\R^n$. The rows of $Q$ are an orthonormal basis for $R^n$. 

Multiplying orthogonal matrices produces an orthogonal matrix:

$$
Q_1 Q_2\text{ is orthogonal}: (Q_1 Q_2)^T(Q_1 Q_2) = Q_2^TQ_1^T Q_1 Q_2 = Q_2^TQ_2 = I
$$

Multiplying vector $x$ by $Q$ does not change the length of $x$. $\|Qx\| = \|x\|$ because
$$
(Qx)^T(Qx) = x^TQ^TQx = x^Tx
$$
Moreover, for every vector $x$ and $y$, the l**engths and angles are not changed by** $Q$:  
$$
(Qx)^T(Qy) = x^TQ^TQy = x^Ty \\
x^Ty = \|x\|\|y\| cos \theta
$$
Thus, computation with $Q$ never overflow !

> ####  Example 10: 
>
> For 2 by 2 orthogonal matrices, they are **rotations** of the plane or **reflections**. The columns of $Q$ are orthogonal unit vectors, with $cos^2\theta + sin^2\theta = 1$:
> $$
> Q_{rotate} = \begin{bmatrix}  cos\theta&-sin\theta\\ sin\theta&cos\theta \end{bmatrix} = \text{rotation through an angle }\theta
> $$
> By multiplying one column by -1, the two columns are still orthogonal of length 1
> $$
> Q_{rotate} = \begin{bmatrix}  cos\theta&sin\theta\\ sin\theta&-cos\theta \end{bmatrix} = \text{reflection across the }\frac{\theta}{2}-\text{line}
> $$
> Note that rotation $\times$ rotation = reflection $\times$ reflection = rotation, Rotation $\times$ reflection = reflection.

**Orthogonal basis = orthogonal axes in $R^n$.**

Given a squared orthogonal matrix $Q$ with columns $q_1, ..., q_n$, every vector $v$ can be written as a combination of the basis vector $q$'s.
$$
v = c_1q_1 + ... + c_nq_n
$$
Each $c_nq_n$ is the component of $v$ along the axes, or the projection of $v$ onto the axes. 

$c_1, ..., c_n$ are the **coefficients** in an orthonormal basis (**which can be found separately when basis vectors are orthonormal**)
$$
c_1 = q_1^Tv, c_2 = q_2^Tv, ..., c_n = q_n^Tv
$$

* A vector proof: 

  Multiply the two sides by $q_1^T$:
  $$
  q_1^Tv = c_1q_1^Tq_1 + ... + c_nq_n^Tq_n = c_1\\
  c_1q_1^Tq_1 = c_1\\
  q_1^Tv = c_1
  $$
  Thus every $c_k = q_k^Tv$.

* A matrix proof:
  $$
  Q^Tv = Q^TQc = c \text{ gives all the coefficients } c_k = q_k^T
  $$
  

> #### Example 11:
>
> **Householder matrix**
> $$
> H_n = I-2uu^T = I - \frac{2}{n} ones(n,n)\\
> H^TH = H^2 = I
> $$
> **Permutation matrix**: is the reordering of identity matrix. Every permutation matrix has unit vectors in its columns.
> $$
> e.g. \begin{bmatrix}  0&1&0\\0&0&1\\ 1&0&0 \end{bmatrix}
> $$

Note that **when a matrix is symmetric or orthogonal, it will have orthogonal eigenvectors**.









