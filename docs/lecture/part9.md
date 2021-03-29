# Four Ways to Solve Least Squares Problems

**Least Squares Problems**: To find $\hat{x}$ which minimizes $\|b - A\hat{x}\|^2$ by taking derivative and setting it to zero. Then the problem is now written as a **normal equation**: 
$$
A^TA \hat{x} = A^Tb
$$
**Four ways** to solve this normal equation:

1. The SVD of $A$ leads to its **pseudoinverse** $A^+$. Then $\hat{x} = A^+b$.
2. $A^TA\hat{x} = A^Tb$ can be solved directly when $A$ has **independent columns**.
3. The **Gram-Schmidt** idea produces orthogonal columns in $Q$. Then $A = QR$.
4. Minimize $\|b - Ax\|^2 + \delta^2 \|x\|^2$. With that **penalty**, we change the normal equations to $(A^TA + \delta^2I)x_{\delta} = A^Tb$.

## $A^+$ is the Pseudoinverse of $A$

Compute Pseudoinverse $A^+$:

* If $A$ is invertible, then $A^+$ is $A^{-1}$. If not:

  * **Rule 1**: If $A$ has independent columns, then $A^+ = (A^TA)^{-1}A^T$ and so $A^+A = I$.

  * **Rule 2**: If $A$ has independent rows, then $A^+ = A^T(AA^T)^{-1}$ and so $AA^+ = I$.

  * **Rule 3**: A diagonal matrix $\Sigma$ is inverted where possible - otherwise $\Sigma^+$ has zeros.

    * In row space and column space of $A$,
      $$
      \Sigma^+\Sigma = I;~~~\Sigma\Sigma^+ = I
      $$
      
* In null space of $A$ and $A^T$,
      $$
      \Sigma^+\Sigma = 0;~~~\Sigma\Sigma^+ = 0
      $$
    
* For all matrices, the pseudoinverse of $A = U\Sigma V^T$ is $A^+ = V \Sigma^+ U^T$.

Some properties of $A^+$: 

* If $A$ is m by n, then $A^+$ is n by m.
* $A^+$ inverts $A$.
  * $A$ multiplying a vector $x$ in its row space produces $Ax$ in the column space.
  * Row space of $A$ is column space of $A^+$. Column space of $A$ is row space of $A^+$.
  * Multiplying by $A$ transforms row space to column space. Multiplying by $A^+$ transforms column space to row space. 
  * $A^+Ax = x$ when $x$ is in the row space. $AA^+b = b$ when $b$ is in the column space.
* Null space of $A^T$ equals to null space of $A^+$.
* Pseudoinverses do not obey all the rules of inverse matrices
  * $(AB)^+ = B^+A^+$ does not always hold. If A has full column rank and $R$ has full row rank then it is true.
  * $(A^T)^+ = (A^+)^T$ and $(A^TA)^+ = A^+(A^T)^+$ hold.

#### $x^+ = A^+b $ solution

This pseudoinverse $A^+$ solves the least squares equation $A^TA \hat{x} = A^Tb$ that 
$$
x^+ = A^+b = V\Sigma^+U^Tb
$$
We write $\hat{x}$ as $x^+$ because of $x^+$'s two properties

1. **Least squares solution**: $x = x^+ = A^+b$ makes $\|b-Ax\|^2$ as small as possible.
2. **Minimum norm solution**: If another $\hat{x}$ achieves that minimum then $\|x^+\| < \|\hat{x}\|$.

#### Proof:

Squared error
$$
\|b-Ax\|^2 = \|b-U\Sigma V^Tx\|^2 = \|U^Tb - \Sigma V^Tx\|^2
$$
Set $w = V^Tx$ to get $\|U^Tb - \Sigma w\|^2$. The best $w$ is $\Sigma^+ U^Tb$. 
$$
\begin{aligned}
w &= V^Tx^+ = \Sigma^+ U^Tb \\ V^T &= V^{-1} 
\end{aligned}
$$
And finally we get
$$
x^+ = V \Sigma^+ U^Tb = A^+b
$$
The **merit** is that $A^TA$ does not need to be invertible. The **drawback** is computing eigenvalues and eigenvectors is costly. 

When $A^TA$ is **invertible**, we'd better resort to other ways that directly deals with $A^TA \hat{x} = A^Tb$. 

## Solve $A^TA \hat{x} = A^Tb$

To solve normal equation directly, note that $A^TA$ must be **invertible** ($A$ has **independent** columns) and **diagonal** (the columns of $A$ are **orthogonal**). 

$A^TA$ is invertible when $A$ has **independent columns**. And for all matrices, there holds some properties: 
$$
N(A^TA) = N(A) \text{ and } C(AA^T) = C(A) \text{ and } \text{ rank}(A^TA) = \text{ rank}(AA^T) = \text{ rank}(A)
$$

#### In Geometry

We project $b$ onto the column space of $A$ to get the projection $p = A\hat{x}$. The error vector from $b$ to $p$ is $e = b - p = b - A \hat{x}$. Since $b - A\hat{x}$ is perpendicular to all vectors $Ax$ in the column space, for all $x$:
$$
(Ax)^T(b - A\hat{x}) = x^TA^T(b - A\hat{x}) = 0\\
A^TA \hat{x} = A^Tb
$$
Where we can get:

* **Projection** of $b$ onto the column space of $A$: 
  $$
  p = A\hat{x} = A(A^TA)^{-1}A^Tb
  $$

* **Projection matrix** that multiplies $b$ to give $p$:
  $$
  P = A(A^TA)^{-1}A^T
  $$
  Projection matrices have the special property $P^2 = P$. When we project a second time, the projection $p$ stays the same.
  $$
  P^2 = A（A^TA）^{-1}A^T A（A^TA）^{-1}A^T = A（A^TA）^{-1}A^T = P
  $$

## Gram-Schmidt Idea

$A^TA$ is important but expensive to compute. Gram-Schmidt produces orthonormal $q$'s from independent $a$'s, then $A = QR$, where $Q$ is orthogonal and $R$ is triangular. Therefore,
$$
A^TA = (QR)^T(QR) = R^TQ^TQR = R^TR
$$
The normal equation can be solved by
$$
\begin{aligned}
A^TA\hat{x} &= A^Tb\\
R^TR\hat{x} &= R^TQ^Tb\\
R \hat{x} & = Q^Tb\\
\hat{x} & = R^{-1}Q^Tb
\end{aligned}
$$
Note that the columns of $A$ need to be **independent** with full rank but no need to be orthogonal (so $A^TA$ does not need to be diagonal ). The idea is to **orthogonalize** the columns of $A$ or producing orthogonal (even orthonormal ) columns. Start with $A$ and end with $Q$. Independent columns $a_1, ..., a_n$ lead to orthonormal $q_1, ..., q_n$.

#### Gram-Schmidt Steps

Step 1 (**Orthogonalize**): Compute $q_1 = a_1/\|a_1\|$ which is a unit vector with $\|q_1\| = 1$.

Step 2 (**Orthogonalize**): Substract from $a_2$ its component in the $q_1$ direction and get $A_2 = a_2 - (a_2^T q_1)q_1$ which is orthogonal to $q_1$

Step 3 (**Normalize**): $q_2 = A_2/\|A_2\|$

Step 4 (**Orthogonalize**): $A_3 = a_3 - (a_3^Tq_1)q_1 - (a_3^Tq_2)q_2$, with $A_3^Tq_1 = A_3^Tq_2 = 0$ and $\|q_3\| = 1$

Step 5 (**Normalize**): $q_3 = A_3/\|A_3\|$

...... (the algorithm goes onwards)

**Each $a_k$ is a combination of $q_1$ to $q_k$:**
$$
\begin{aligned}
a_1 & = \|a_1\|q_1\\
a_2 & = (a_2^Tq_1)q_1 + \|A_2\|q_2\\
a_3 & = (a_3^Tq_1)q_1 + (a_3^Tq_2)q_2 + \|A_3\|q_3\\
\end{aligned}
$$
So that the matrix $R=Q^TA$ with $r_{ij} = q_i^Ta_j$ is **upper triangular**.

## Least Square with a Penalty Term

Minimize $\|b - Ax\|^2 + \delta^2 \|x\|^2$. With that **penalty**, we change the normal equations to $(A^TA + \delta^2I)x_{\delta} = A^Tb$. In least squares, this is called "**ridge regression**".

**The limit of $(A^TA + \delta^2 I)^{-1}A^T$ is pseudoinverse $A^+$.**

**Proof**: 

Substitute $A = U\Sigma V^T$ into $(A^TA + \delta^2I)^{-1}A^T$.
$$
A^TA + \delta^2I = V\Sigma^TU^TU\Sigma V^T+ \delta^2I = V(\Sigma^T \Sigma + \delta^2 I)V^T\\
(A^TA + \delta^2I)^{-1}A^T = V\Sigma^TU^TU\Sigma V^T+ \delta^2I = V(\Sigma^T \Sigma + \delta^2 I)^{-1}V^T V\Sigma^TU^T = V[(\Sigma^T \Sigma + \delta^2 I)^{-1} \Sigma^T] U^T
$$
So when $\delta \rightarrow 0$,
$$
\text{limit}_{\delta \rightarrow 0} \text{ } V[(\Sigma^T \Sigma + \delta^2 I)^{-1} \Sigma^T] U^T = V\Sigma^+U^T = A^+
$$
