# Survey of Difficulties with $Ax=b$

This is an introduction lecture to Chapter 2: Introduction to Computations with Large Matrices.

#### Here are 8 solutions to the difficulties of $Ax = b$

1. $x = A^+b$ pseudoinverse is an answer for almost all cases
2. Check size, condition $\frac{\sigma_1}{\sigma_n}$, and $ x = A/\ b$.
3. $m > n = \text{rank}$, $A^TAx = A^Tb$.
4. $m < n$, min norm $A^+b$ or min $l_1$ norm; undetermined/ many solutions/ deep learning
5. Columns in bad condition $\implies$ Gram-Schmidt: $A = QR$ gives either normal way or column pivoting way [See II - 2]
6. Near singular / Inverse problem $\implies$ Add a penalty term, apply  $\min \|Ax-b\|^2 + \delta^2 \|x\|^2 $ to regularize the problem [See II-2] 
7. Problem is too big. $\implies$ Iterative method [See II - 1] [See 2.3]
8. Problem is way too big $\implies$ Random Number Algebra [See 2.4]

## 6 - Add a Penalty Term

Add a $l_2$ norm penalty term:
$$
\min \|Ax-b\|^2_2 + \delta^2 \|x\|_2^2
$$
The problem is exactly the same as
$$
(A^TA + \delta^2I)x = A^Tb
$$
In an 1D example, we define a matrix $A = [\sigma]$ to solve the equation above.
$$
(\sigma^2 + \delta^2)x = \sigma b\\
x = (\frac{\sigma}{\sigma^2 + \delta^2}) b
$$
When $\delta \rightarrow 0$, 
$$
\begin{aligned}
x &\rightarrow \frac{1}{\sigma} b &\text{ if } \sigma \neq 0\\
x &\rightarrow 0 &\text{ if } \sigma = 0\\
\end{aligned}
$$
Therefore, when $\delta \rightarrow 0$, the solution $\rightarrow$ **pseudoinverse**.

Note that the penalty term can also be $l_1$ norm, named "**LASSO**"
$$
\min \|Ax-b\|^2_2 + \delta^2 \|x\|_1^2
$$
**Conclusion**: 

For any matrix $A$, the solution to the problem $Ax = b$ is 
$$
(A^TA + \delta^2I)^{-1}A^T
$$
which approaches to $A^+$ **pseudoinverse**.