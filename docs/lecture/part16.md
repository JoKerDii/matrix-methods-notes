# Derivatives of Inverse and Singular Values

## Derivative of Singular Value

We know the facts

* $\sigma = \mathbf{u}^TA\mathbf{v}$
* $A\mathbf{v} = \sigma \mathbf{u}$
* $(\sigma \mathbf{v})^T \mathbf{v} = (A^T\mathbf{u})^Tv \implies A^T\mathbf{u} = \sigma \mathbf{v}$
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
Since the first and third terms are zero
$$
\frac{d\mathbf{u}^T}{dt} A(t)\mathbf{v}(t) = \sigma(t)\frac{d\mathbf{u}^T}{dt}\mathbf{u}(t) = 0\\
\mathbf{u}^T(t) A(t) \frac{d\mathbf{v}}{dt} = \sigma(t)\mathbf{v}^T(t)\frac{d\mathbf{v}}{dt} = 0
$$


We get the derivative of a singular value
$$
\frac{d\sigma}{dt} = \mathbf{u}^T(t) \frac{dA}{dt}\mathbf{v}(t)
$$

## Derivative of Squared Matrix $A$

The $\frac{dA^2}{dt}$ is not $2A\frac{dA}{dt}$, but $A \frac{dA}{dt} + \frac{dA}{dt} A$
$$
\frac{dA^2}{dt} = \frac{(A+\Delta A)^2 - A^2}{\Delta t} = \frac{A(\Delta A) + (\Delta A)A + (\Delta A)^2}{\Delta t} = A \frac{dA}{dt} + \frac{dA}{dt} A
$$

## Large Perturbation

Let define the perturbation to the symmetric matrix $S$ as
$$
S + \theta \mathbf{u}\mathbf{u}^T
$$
Suppose there is a large perturbation $20 \mathbf{q}_2 \mathbf{q}_2^T$ to matrix $S$, then
$$
(S + 20 \mathbf{q}_2\mathbf{q}_2^T)\mathbf{q}_2 = (\lambda_2 + 20)\mathbf{q}_2
$$
the second eigenvalue $\lambda_2$ become very large and seem not follow the interlacing pattern. 

However, the $\lambda_2$ becomes the largest eigenvalue and the interlacing pattern still holds in the form
$$
z_1 \geq \lambda_1 \geq z_2 \geq ...
$$
where $z_1$ is the new eigenvalue changed from $\lambda_2$.