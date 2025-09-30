## Discriminative analysis

In discriminative analysis, we **directly** come up with a mapping $p(y|\bm{x}, \bm{w})$

-   E.g. logistic regression

## Generative modelling

In generative modelling, we first **model the distribution of each class** and then consider how well a new instance corresponds to each of them.

## Bayes classifier

We want to classify a new instance $\bm{x}$ into one of $C$ classes $y \in \{1, \ldots, C\}$.

In general

$$
p(y|\bm{x}) = \frac{p(\bm{x}|y)p(y)}{p(\bm{x})} = \frac{p(\bm{x}|y)p(y)}{\sum_{c=1}^C p(\bm{x}|c)p(c)}
$$

and for binary classification ($C=2, y_i \in \{0, 1\}$):

$$
p(x_1, \ldots, x_M | y=k) = \frac{\text{Nr. obs. where } y=k \text{ and we measure } x_1, \ldots, x_M}{\text{Nr. obs. where } y=k}
$$

Problems with this approach:

-   We need to estimate $p(\bm{x}|y=k)$ for **each class** $y \in \{1, \ldots, C\}$
    -   So we need a lot of data
-   There is a high risk of 0-probabilities if we have many features
    -   Divide by zero in Bayes' rule

## Naive Bayes

We make the assumption that the features are **conditionally independent given the class**:

$$
p(x_1, \ldots, x_M | y=k) = \prod_{j=1}^M p(x_j | y=k)
$$

This leads to the **Naive Bayes classifier**:

$$
p(y=k | x_1, \ldots, x_M) = \frac{\left[p(x_1 | y=k) \cdots p(x_M | y=k)\right] \cdot p(y=k)}{\sum_{c=1}^C p(x_1 | y=c) \cdots p(x_M | y=c) p(y=c)}
$$

## Robust estimation

![[images/13-robust.png]]

## Non-binary data

If $y$ is not binary, we can't use the frequency estimator (nr of... divided by nr of ...). Instead, we can use a **gaussian estimator** for each feature $\bm{x}$ in each class $y=k$:

Compute class mean $\bm{\mu}_c$ and class covariance matrix $\bm{\Sigma}_c$ for each class $c \in \{1, \ldots, C\}$. Then$$
p(\bm{x} | y=c) = \mathcal{N}(\bm{x} | \bm{\mu}_c, \bm{\Sigma}_c)$$

We then classify using the Bayes classifier.

$$
p(y=c | \bm{x}) = \frac{P(\bm{x} | y=c) p(y=c)}{\sum_{c=1}^C P(\bm{x} | y=c) p(y=c)}
$$

![[images/13-non-binary.jpeg]]

The **<u>Naieve Bayes assumption</u> of conditional independence** of the attributes $x_1, \ldots, x_M$ given the class $y=c$, means that **$\bm{\Sigma}_c$ is diagonal** for each class $c$:

$$
\bm{\Sigma}_c = \begin{bmatrix}
\sigma_{c,1}^2 & 0 & \ldots & 0 \\
0 & \sigma_{c,2}^2 & \ldots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \ldots & \sigma_{c,M}^2 \\
\end{bmatrix}
$$

Where $\sigma_{c,j}^2 = \text{var}[x_j | y=c]$ is the variance of feature $j$ in class $c$.

For the two-dimensional case ($x_1$ = `height`, $x_2$ = `weight`):

$$
\textbf{Females: } \bm{\Sigma}_1 = \begin{bmatrix} \sigma_{f1}^2 & 0 \\ 0 & \sigma_{f2}^2 \end{bmatrix}, \qquad \textbf{Males: } \bm{\Sigma}_2 = \begin{bmatrix} \sigma_{m1}^2 & 0 \\ 0 & \sigma_{m2}^2 \end{bmatrix}
$$

We see that $x_1$ and $x_2$ are independent within each class:
$$\text{cov}(x_1, x_2 | y=\text{female}) = 0 = \text{cov}(x_1, x_2 | y=\text{female})$$

So, assuming that $x_1$ and $x_2$ are *conditionally* independent, the 2-dimensional Gaussian is the **product of two univariate gaussians**:
$$p(x_1, x_2 | y = \text{female}) = p(x_1 | y = \text{female}) p(x_2 | y = \text{female})$$

![[images/13-independent-gaussians.png]]
