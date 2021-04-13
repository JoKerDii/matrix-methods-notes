# Low Rank Changes in $A$ and Its Inverse



## Overview

**Matrix inversion lemma**, a.k.a, **Sherman-Morrison-Woodbury formula**, gives the exact formula for the changes in $A^{-1}$ when substracting a low rank matrix (a rank perturbation) from $A$.

This formula is the key to updating the solution to a linear system $Ax=b$.

## Basic Case 1

Suppose $A = I$ and there is a small perturbation $\mathbf{uv}^T$ with rank=1. The inverse of  $M = I-\mathbf{uv}^T$ is 
$$
M^{-1} = I+ \frac{\mathbf{uv}^T}{1-\mathbf{v}^T\mathbf{u}}
$$
 Two features of the formula:

* The correction to $M^{-1}$ is also rank one, which is $\frac{\mathbf{uv}^T}{1-\mathbf{v}^T\mathbf{u}}$.
* This correction term can become infinite, then $M$ is not invertible (no $M^{-1}$). This occurs if the number $\mathbf{v}^T\mathbf{u}$ happens to be 1. In this case the formula fails.

Prove this formula by easily checking $MM^{-1} = I$. 
$$
MM^{-1} = (I-\mathbf{uv}^T)(I+\frac{\mathbf{uv}^T}{1-\mathbf{v}^T\mathbf{u}}) = I-\mathbf{uv}^T+\frac{(I-\mathbf{uv}^T)\mathbf{uv}^T}{1-\mathbf{v}^T\mathbf{u}} = I - \mathbf{uv}^T + \mathbf{uv}^T = I
$$
Find the key of this formula by column eliminating and row eliminating **extended matrix**: 
$$
E = \begin{bmatrix} I&\mathbf{u}\\\mathbf{v}^T&1\end{bmatrix} \text{ has determinant }\mathbf{D} = 1-\mathbf{v}^T\mathbf{u}
$$

## Basic Case 2

Now suppose we have a perturbation $U_{(n\times k)}V^T_{(k \times n)}$ of rank $k$. The inverse of $M = I-UV^T$ is 
$$
M^{-1} = I_n+ U(I_k - V^TU)^{-1}V^T
$$
We are exchanging an inverse of size $n$ for an inverse of size $k$.

Similarly, prove this formula by easily checking $MM^{-1} = I$. 
$$
\begin{aligned}
(I_n-UV^T)(I_n+U(I_k-V^TU)^{-1}V^T) &= I_n - UV^T+(I_n - UV^T)U(I_k-V^TU)^{-1}V^T\\
&= I_n - UV^T+U(I_k - U^TV)(I_k-V^TU)^{-1}V^T\\
&= I_n - UV^T+UV^T\\
&= I_n
\end{aligned}
$$
Find the key of this formula by column eliminating and row eliminating **extended matrix** of size $(n+k)$:
$$
E = \begin{bmatrix} I_n&\mathbf{U}\\\mathbf{V}^T&I_k\end{bmatrix} \text{ has determinant } det(I_n-UV^T) = det(I_k - V^TU)
$$
When $k<<b$, the inverse that we should compute would be much faster and easier.

## Sherman-Morrison-Woodbury Formula

Perturb any invertible $A$ by a rank $k$ matrix $UV^T$. Now the inverse of $M = A-UV^T$ is 
$$
M^{-1} = (A-UV^T)=A^{-1} + A^{-1}U(I-V^TA^{-1}U)^{-1}V^TA^{-1}
$$
Now we are exchanging an inverse of $n$ by $n$ matrix $A$ for an inverse of $k$ by $k$ inverse of $C = I-V^TA^{-1}U$.

## Updating Least Squares

This is an application of Sherman-Morrison-Woodbury Formula. Recall the least squares equation $A^TA\widehat{x} = A^Tb$ - the "normal equations" to minimize $||\mathbf{b}- A\mathbf{x}||^2$. Suppose a new equation arrives, then $A$ has a new row $\mathbf{r}$ (1 by $n$) and there is a new measurement $b_{m+1}$ and a new $\widehat{x}$. So the perturbation here is rank one ( it can also be higher ranks)
$$
\begin{aligned}
\begin{bmatrix}A^T &\mathbf{r}^T \end{bmatrix}\begin{bmatrix}A\\ \mathbf{r}^T \end{bmatrix}\widehat{\mathbf{x}} &=\begin{bmatrix}A^T &\mathbf{r}^T \end{bmatrix}\begin{bmatrix}\mathbf{b}\\ b_{m+1} \end{bmatrix}\\
\implies[A^TA + \mathbf{r}^T\mathbf{r}]\widehat{\mathbf{x}} &= A^T\mathbf{b} + \mathbf{r}^Tb_{m+1}
\end{aligned}
$$
The new matrix in the normal equation is a rank one correction to the original $A^TA$. We update $\widehat{\mathbf{x}}$ by
$$
[A^TA + \mathbf{r}^T\mathbf{r}]^{-1} = (A^TA)^{-1}-c(A^TA)^{-1}\mathbf{r}^T\mathbf{r}(A^TA)^{-1} \text{ with }
\\c = \frac{1}{1+\mathbf{r}(A^TA)^{-1}\mathbf{r}^T}
$$
To find $c$ quickly we only need to solve $(A^TA)\mathbf{y} = \mathbf{r}^T$. 

Updating $\widehat{\mathbf{x}}$ is called **recursive least squares**. The steps are

1. Solve $A\mathbf{x} = \mathbf{b}$ and $A\mathbf{z} = \mathbf{u}$. Compute $\mathbf{D} = 1- \mathbf{v}^T\mathbf{z}$
2. Then $\mathbf{y} = \mathbf{x} + \frac{\mathbf{v}^T\mathbf{x}}{\mathbf{D}}\mathbf{z}$ is the solution to $M\mathbf{y} = (A-\mathbf{u}\mathbf{v}^T)\mathbf{y} = \mathbf{b}$.

## The derivative of $A^{-1}$

We are interested in the change $\Delta f(x)$ in a function $f(x)$ when $x$ is moved slightly $\Delta x$. We define $B = A + \Delta A$ and we have the fact
$$
B^{-1} - A^{-1} = B^{-1}(A-B)A^{-1}
$$
Suppose $A = A(t)$ changes with time $t$ and so as $A^{-1}$, we have
$$
\begin{aligned}
\Delta A &= B - A\\
\Delta A^{-1} &= B^{-1} - A^{-1}
\end{aligned}
$$
Now let $\Delta t \rightarrow 0$ and then we find the derivative
$$
\begin{aligned}
\frac{\Delta A^{-1}}{\Delta t} &= -(A + \Delta A^{-1})\frac{\Delta A}{\Delta t}A^{-1}\\
\frac{dA^{-1}}{dt} &= -A^{-1}\frac{dA}{dt} A^{-1}
\end{aligned}
$$
