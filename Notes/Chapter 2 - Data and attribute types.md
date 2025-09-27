## Attribute Types

-   **Discrete**
-   **Continuous**
-   **Binary**
-   **Categorical**

-   **Nominal**:
    -   Not ordered
    -   Only **uniqueness** matters
    -   _E.g. colors, types_
-   **Ordinal**:
    -   Ordered
    -   _E.g. "small", "medium", "large"_
-   **Interval**:
    -   Ordered
    -   **Relative magnitude** has physical meaning
    -   _E.g. year, longitude (Greenwich = arbitrary zero point)_
    -   "New civilization" may not choose the same zero point (Greenwich, year 0)
-   **Ratio**:
    -   **Value 0** has specific physical meaning
    -   "Twice as big/much/..."
    -   _E.g. age, weight, nb of ..., meters above sea level_

### Hierarchy

-   Nominal < Ordinal < Interval < Ratio
-   Ratio $\Rightarrow$ Interval $\Rightarrow$ Ordinal $\Rightarrow$ Nominal
-   But we classify as the **most specific**

## Imputation

> [!term] Imputation
> The process of replacing missing data with substituted values.

-   Mean
-   Median
-   Mode (Most frequent value)

## Feature transformations

-   **Linear**
    -   Standardise with $\hat{\mu}_j$ and $\hat{\sigma}_j$
-   **Non-linear**
    -   $\tilde{X}_j = g(X_j)$, where $g$ is a non-linear function
    -   E.g. $\tilde{X}_j = log(X_j)$ for weight differences
-   **Adding new features based on existing ones**
    -   E.g. BMI = weight / height$^2$
-   **One-out-of-$K$ encoding**
    -   Replace a nominal variable with 3 binary ones
    -   $K=3$: $$\begin{bmatrix}
        3 \\
        1 \\
        1 \\
        2 \\
        \vdots \\
        3 \\
        2\\
    \end{bmatrix} \leftrightarrow \begin{bmatrix}
        0 & 0 & 1 \\
        1 & 0 & 0 \\
        1 & 0 & 0 \\
        0 & 1 & 0 \\
        \vdots & \vdots & \vdots \\
        0 & 0 & 1 \\
        0 & 1 & 0 \\
    \end{bmatrix}$$
    -   Advantage: **no ordering assumed**
        -   Mapping categorical var to discrete integers implies **unwanted order**!
-   **Binarizing / thresholding**
    -   With **indicator function**: $\mathbf{1}_{A}(x) = \begin{cases}1 & \text{if } x \in A \\ 0 & \text{if } x \notin A\end{cases}$ $$x \leftrightarrow \begin{bmatrix}
        \mathbf{1}_{[0,\infty)}(x_1) \\
        \mathbf{1}_{[0,\infty)}(x_2) \\
        \vdots \\
        \mathbf{1}_{[0,\infty)}(x_N) \\
    \end{bmatrix}$$
