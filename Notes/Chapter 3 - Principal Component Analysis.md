## 1. Centered data matrix $\tilde{\mathbf{X}}$

Subtract the column-wise mean of the dataset:
$$\tilde{X}_{ij} = X_{ij} - \frac{1}{N} \sum_{i=1}^{N} X_{ij} \quad \iff \quad \tilde{\bm{x}}_i = \bm{x}_i - \bm{m} = \bm{x}_i - \frac{1}{N} \sum_{j=1}^{N} \bm{x}_j$$

## 2. Singular Value Decomposition (SVD)

$$
\boxed{\tilde{\bm{X}} = \bm{U} \bm{\Sigma} \bm{V}^T} = \bm{U} \begin{bmatrix}
\sigma_1 & 0 & \ldots & 0 \\
0 & \sigma_2 & \ldots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \ldots & \sigma_M \\
0 & 0 & \ldots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \ldots & 0 \\
\end{bmatrix} \begin{bmatrix}
- &\bm{v}_1^T &- \\
- &\bm{v}_2^T &- \\
&\vdots& \\
- &\bm{v}_M^T &- \\
\end{bmatrix} = \bm{U} \begin{bmatrix}
\sigma_1 & 0 & \ldots & 0 \\
0 & \sigma_2 & \ldots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \ldots & \sigma_M \\
0 & 0 & \ldots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \ldots & 0 \\
\end{bmatrix} \begin{bmatrix}
| & | & & | \\
\bm{v}_1 & \bm{v}_2 & \cdots & \bm{v}_M \\
| & | & & | \\
\end{bmatrix}^T
$$

### Eigenvectors

$$\bm{V}_{(K)} = \begin{bmatrix}| & | & & | \\\bm{v}_1 & \bm{v}_2 & \cdots & \bm{v}_K \\| & | & & | \\\end{bmatrix} \in \mathbb{R}^{M \times K} \qquad \text{with } \bm{V}^T\bm{V} = \bm{I}_K, \bm{V} = \bm{V}^{-1}$$

First $K$ columns of $\bm{V}$ (or rows of $\bm{V}^T$) are the **top $K$ principal components**.

-   $\text{PC}_1 = \bm{v}_1, \ldots, \text{PC}_K = \bm{v}_K$
-   These vectors capture the **directions of maximum variance** in the data.
-   These vectors form an **orthonormal basis** for a $K$-dimensional subspace
    -   $\tilde{\bm{V}} = \text{span}(\bm{v}_1, \ldots, \bm{v}_K) = \mathbb{R}^K \subseteq \mathbb{R}^M$

### Projected data

We can project the original data points $\bm{x}_i$ onto the subspace spanned by the first $K$ principal components:
$$\bm{b}_i^T = \tilde{\bm{x}}_i^T \bm{V}_{(K)} \quad \iff \quad \boxed{\bm{b}_i = \begin{bmatrix} \tilde{\bm{x}}_i^T \bm{v}_1 \\ \vdots \\ \tilde{\bm{x}}_i^T \bm{v}_K \end{bmatrix}} \quad \iff \quad \bm{B} = \tilde{\bm{X}} \cdot \bm{V}_{(K)}$$

![[images/3-subspace.jpeg]]

### Reconstructed data

We can reconstruct an approximation $\bm{\hat{x}}_i$ of the original data points $\bm{x}_i$ from their projections $\bm{b}_i$:
$$\bm{\hat{x}}_i = \bm{V}_{(K)} \bm{b}_i + \bm{m} \quad \iff \quad \boxed{\hat{\bm{x}}_i = (\bm{v}_1 b_{i,1} + \ldots + \bm{v}_K b_{i,K}) + \bm{m}}$$

-   Scalars/coefficients $b_{i,j} \in \R$
-   Vectors $\bm{v}_j, \bm{m} \in \R^M$ = dimension of original data

![[images/3-projection-reconstruction.png]]

## 3. Variance explained by each principal component

-   Variance explained by the $j$-th principal component: $\lambda_j = \sigma_j^2$
-   Total variance in the data: $\sum_{j=1}^{M} \sigma_j^2$
-   Fraction of variance explained by the first $K$ principal components:
    $$\text{Fraction of variance explained} = \boxed{\frac{\sum_{j=1}^{K} \sigma_j^2}{\sum_{j=1}^{M} \sigma_j^2}}$$
    -   This is the variance retained in reconstructed data using only the first $K$ principal components.

## Alternative to find principal components: eigenvalues of $\bm{\hat{S}}$

-   Compute the covariance matrix of the centered data:$$\bm{\hat{S}} = \frac{1}{N} \tilde{\bm{X}}^T \tilde{\bm{X}} \in \mathbb{R}^{M \times M}$$
-   Diagonalize $\bm{\hat{S}}$:
    $$\bm{\hat{S}} = \bm{V} \bm{\Lambda} \bm{V}^T$$
    where $\bm{\Lambda} = \text{diag}(\lambda_1, \ldots, \lambda_M)$ with $\lambda_1 \geq \lambda_2 \geq \ldots \geq \lambda_M \geq 0$
-   The eigenvectors $\bm{v}_1, \ldots, \bm{v}_M$ of $\bm{\hat{S}}$ corresponding to the largest eigenvalues $\lambda_1, \ldots, \lambda_M$ are the principal components
