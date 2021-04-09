# Randomized Matrix Multiplication

## 1. Basics

* **Problem**: multiplying big matrices $C = AB$ is expensive

* **Solution**: sample $A$ and $B$ instead of using the complete matrices.  Specifically, 

  * We first sample $s$ columns from $A$ and $s$ corresponding rows from $B$ using a sampling matrix $S$. Each column of $S$ has only one non-zero value.
    $$
    C = AS = s_k\mathbf{a}_k \\ R = S^TB= s_k\mathbf{b}_k^T \\ CR = ASS^TB = \sum s_k^T \mathbf{a}_k \mathbf{b}_k^T\approx AB
    $$

    * The expected value of $SS^T$ is $I$. This shows the key to randomization.
    * $ASS^TB$ gives a sum of column-row products $\mathbf{a}_k \mathbf{b}_k^T$ weighted by the numbers $s_k^2$. $\sum s_k^T \mathbf{a}_k \mathbf{b}_k^T$ can be seen as $AB$ is approximated by the weighted sum of a random selection of $s$ rank-one matrices.
    * Since sampling matrix $S$ transforms $A$ and $B$ to lower dimensions, $ASS^TB$ is a more uniform approximation to $AB$.
    * The selection is random, but the weights can be chosen by us.

  * By outer product (columns-row products), we get $s$ rank one matrices $a_k b_k^T$. 

  * We can then multiply their sum by $n/s$ to estimate the true $AB = $ sum of $n$ products.

* **Goal**: we aim to have correct expected value and the lowest variance. 

## 2. Computing Mean and Variance

Suppose we start with a vector $\mathbf{v} = (a,b)$, sample it twice (2 independent trials), and then compute the mean $m = E[(x_1, x_2]$ and the variance $\sigma^2 = E[(x - \text{mean})] = E[x^2] - (\text{mean})^2$.
$$
\begin{aligned}
m &= E[(x_1, x_2)] = \frac{1}{2}(a,b) + \frac{1}{2}(a,b) = (a,b)\\
\sigma^2 &= E[(x - \text{mean})] = E[x^2] - (\text{mean})^2 = \frac{1}{2}(a^2, b^2)
\end{aligned}
$$
Note that if $b$ is larger than $a$, we could keep the correct mean $(a,b)$ and reduce the variance $\sigma^2$ by giving greater probability to choosing the larger samples $(0,b)$.

## 3. Random Matrix Multiplication with the Correct Mean AB

These $s_{kj}$ are chosen from probabilities by random sampling. The steps are

1. assign probabilities $p_j$ to all of the $n$ columns of $A$ with $\sum_{i=1}^n p_i = 1$.
2. choose $s$ columns **with replacement**
3. multiply both the chosen $k$ columns of $A$ and chosen $k$ rows of $B$ by $1/\sqrt{sp_k}$, we get  (column $k$ of $A$)(row $k$ of $B$) /$sp_k$ .

* Proof of random sampling computes the matrix product with the correct mean $AB$:

  Suppose there are $s$ identical trials, each chooses a column-row pair of $A$ and $B$ with probabilities $p_1$ to $p_n$, then the expected value from **each trial** is 
  $$
  p_1 \frac{\text{(column 1 of A)(row 1 of B)}}{sp_1} + ... + p_n \frac{\text{(column n of A)(row n of B)}}{sp_n}
  $$
  which is exactly $AB/s$. And since there are $s$ trials, the expected value for the randomized multiplication $(AS)(S^TB)$ is $AB$.

Note that the probabilities $p_1$ to $p_n$ should be chosen by us and can strongly affect the variance. There are several options:

* **Uniform sampling** would choose equal probability $p = 1/n$. This is reasonable if the columns of $A$ (and also the rows of $B$) have similar lengths.
* **Unequal probabilities** $p_j$ is better in that it can avoid missing important columns.
* A different option: introduce a mixing matrix $M$ and work with $AM$ and $M^{-1}B$, then use probabilities $p_j$for the random mixed columns of $A$ and rows of $B$.

## 4. Norm-squared Sampling Minimizes the Variance

Norm-squared sampling chooses the probabilities $p_j$ proportional to the numbers $||\text{column j of A}||~~||\text{row j of B}||$, with a scaling constant $1/C$ to ensure $\sum p_j = 1$.
$$
p_j = \frac{1}{C}||\text{column j of A}||~~||\text{row j of B}|| = \frac{||a_j||~~||b_j^T||}{C} \text{ with }C = \sum^n_{j=1} ||a_j||~~||b_j^T||
$$
It is best to choose large columns and rows more often. The choice of $p_j$'s above minimizes the variance. This is proved below:

Each of the $s$ trials produces a matrix $X_j = \mathbf{a}_j \mathbf{b}_j^T/sp_j$ with probability $p_j$. Its $i,k$ entry is $(X_j)_{ik} = a_{ij}b_{jk}/sp_j$.The mean for each trial is 
$$
E[X]= \sum^n_{j=1}p_jX_j = \frac{1}{s} \sum^n_1 \mathbf{a}_j \mathbf{b}_j^T = \frac{1}{s}AB
$$
The variance for one trial by definition is $E[X]^2 - (E[X])^2$ , which can be computed in the **Frobenius norm** (sum of squares of matrix entries)
$$
\begin{aligned}
E[||AB-CR||^2_F] &= \sum_{i,k} \sum_{j=1}^n p_j \frac{a_{ij}^2b_{jk}^2}{sp_j^2} - \frac{1}{s}||AB||^2_F\\
&= \sum_{j=1}^n \frac{||a_{j}||^2||b_{j}^T||^2}{sp_j} - \frac{1}{s}||AB||^2_F
\end{aligned}
$$
Now we multiply the constraint $\sum_1^n p_j = 1$ by a **Lagrange multiplier** $\lambda$ to  prove that $p_j = \frac{||a_j||~~||b_j^T||}{C}$ minimizes the variance:
$$
L(p_1,...,p_n, \lambda) = \sum^n_{j=1}\frac{||a_j||^2~~||b_j^T||^2}{sp_j} - \frac{1}{s}||AB||^2_F + \lambda (\sum^n_1 p_j - 1)
$$
Take the partial derivatives $\partial L/\partial p_j$, set it to zero, and solve for $p_j$:
$$
\begin{aligned}
\frac{\partial L}{\partial p_j} = 0 &\implies \frac{1}{sp_j^2}||a_j||^2~~||b_j^T||^2 = \lambda\\
&\implies p_j = ||a_j||~~||b_j^T||/\sqrt{s\lambda}
\end{aligned}
$$
We choose $\lambda$ to make sure $\sum_1^n p_j = 1$, 
$$
\sum_1^n p_j =\sum^n_1\frac{||a_j||~~||b_j^T||}{\sqrt{s\lambda}} = 1 \implies \sqrt{s \lambda} = C \text{ and } p_j = \frac{||a_j||~~||b_j^T||}{C}
$$
To compute the smallest variance, we substitute  $p_j = \frac{||a_j||~~||b_j^T||}{C}$ to the variance to get
$$
\begin{aligned}
E[||AB-CR||^2_F] &= \sum_{j=1}^n \frac{||a_{j}||^2||b_{j}^T||^2}{sp_j} - \frac{1}{s}||AB||^2_F \\
 &= \frac{1}{s} [\sum^n_{j=1}||a_j||~~||b_j^T||]^2 - \frac{1}{s}||AB||^2_F 
 \end{aligned}
$$
Since $\sum^n_{j=1}||a_j||~~||b_j^T|| = C$, we get the smallest variance
$$
\begin{aligned}
E[||AB-CR||^2_F] &= \frac{1}{s} [\sum^n_{j=1}||a_j||~~||b_j^T||]^2 - \frac{1}{s}||AB||^2_F \\
&=\frac{1}{s} (C^2 - ||AB||^2_F)
 \end{aligned}
$$
