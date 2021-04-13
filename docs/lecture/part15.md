# Matrices $A(t)$ Depending on $t$, Derivative = $dA/dt$

## Interlacing

We are interested in how eigenvalues $\lambda$ and singular values $\sigma$ change when there is a slightly addition in matrix $A$. 

Suppose a symmetric matrix $S$ changes to $S + \mathbf{uu}^T$, $\mathbf{uu}^T$ is a positive change of rank 1. Its eigenvalues change from $\lambda_1 \geq \lambda_2 \geq ...$ to $z_1 \geq z_2 \geq ...$. We expect increases in eigenvalues since $\mathbf{uu}^T$ is **positive semidefinite**. Therefore, we have **interlaced** $\lambda$'s and $z$'s
$$
\lambda_1 \geq z_1 \geq \lambda_2 \geq z_2 \geq ... \geq z_n \geq \lambda_n
$$

## Derivative of Eigenvalue

Suppose a matrix $A(t)$ changing with time $t$, its eigenvalues $\lambda(t)$ are also changing. We know that

* $A^T(t)$ also has eigenvalue $\lambda(t)$ because the determinants won't change. 
* Probably $A^T$ has a different eigenvector $\mathbf{y}(t)$.
* The length of $\mathbf{x}$ and $\mathbf{y}$ are normalized by $X^{-1}X = I$ so that $\mathbf{y}^T(t)\mathbf{x}(t) = 1$ for all $t$.

So the facts we have are
$$
\begin{aligned}
A(t)\mathbf{x}(t) &= \mathbf{\lambda}(t)\mathbf{x}(t)\\
\mathbf{y}^T(t)A(t) &= \mathbf{\lambda}(t)\mathbf{y}^T(t)\\
\mathbf{y}^T(t)\mathbf{x}(t) &= 1
\end{aligned}
$$
From which we obtain
$$
\mathbf{\lambda}(t) = \mathbf{y}^TA(t)\mathbf{x}(t)
$$
Take the derivative with respect to $t$ we have
$$
\begin{aligned}
\frac{d\mathbf{\lambda}}{dt} &= \frac{d\mathbf{y}^T}{dt}A\mathbf{x} + \mathbf{y}^T \frac{dA}{dt}\mathbf{x} + \mathbf{y}^TA\frac{d\mathbf{x}}{dt}
\end{aligned}
$$
Since the first and third term cancelled out
$$
\begin{aligned}
\frac{d\mathbf{y}^T}{dt}A\mathbf{x}  + \mathbf{y}^TA\frac{d\mathbf{x}}{dt} &= \frac{d\mathbf{y}^T}{dt}\mathbf{\lambda}\mathbf{x}  + \mathbf{\lambda}\mathbf{y}^T\frac{d\mathbf{x}}{dt} \\ &= \mathbf{\lambda}(\frac{d\mathbf{y}^T}{dt}\mathbf{x}  + \mathbf{y}^T\frac{d\mathbf{x}}{dt})\\ &= \mathbf{\lambda}\frac{d}{dt}(\mathbf{y}^T\mathbf{x})\\ &= 0
\end{aligned}
$$
we get the derivative of eigenvalue
$$
\frac{d\mathbf{\lambda}}{dt} =\mathbf{y}^T(t)\frac{dA}{dt}\mathbf{x}(t)
$$

## Derivative of Singular Value

We know the facts

* $U^TAV = \Sigma$
* $A\mathbf{v} = \sigma \mathbf{u}, A^T\mathbf{u} = \sigma \mathbf{v}$
* $\mathbf{u}^T\mathbf{u} = \mathbf{v}^T\mathbf{v} = 1$

From which we have
$$
\mathbf{u}^T(t)A(t)\mathbf{v}(t) = \mathbf{u}^T(t)\sigma(t)\mathbf{u}(t) = \sigma(t)
$$
Take the derivative
$$
\begin{aligned}
\frac{d\sigma}{dt} &= \frac{d\mathbf{u}^T}{dt} A(t)\mathbf{v}(t) + \mathbf{u}^T(t) \frac{dA}{dt}\mathbf{v}(t) + \mathbf{u}^T(t) A(t) \frac{d\mathbf{v}}{dt} 
\end{aligned}
$$
Since
$$
\frac{d\mathbf{u}^T}{dt} A(t)\mathbf{v}(t) = \sigma(t)\frac{d\mathbf{u}^T}{dt}\mathbf{u}(t) = 0\\
\mathbf{u}^T(t) A(t) \frac{d\mathbf{v}}{dt} = \sigma(t)\mathbf{v}^T(t)\frac{d\mathbf{v}}{dt} = 0
$$


We get the derivative of a singular value
$$
\frac{d\sigma}{dt} = \mathbf{u}^T(t) \frac{dA}{dt}\mathbf{v}(t)
$$
