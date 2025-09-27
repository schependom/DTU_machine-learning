## Term-document matrix

$$
\mathbf{X} = \begin{bmatrix}
    x_{11} & x_{12} & \cdots & x_{1t} \\
    x_{21} & x_{22} & \cdots & x_{2t} \\
    \vdots & \vdots & \ddots & \vdots \\
    x_{n1} & x_{n2} & \cdots & x_{nt} \\
\end{bmatrix} = \begin{bmatrix}
    - & \text{Document $1$} & - \\
    - & \text{Document $2$} & - \\
     & \vdots & \\
    - & \text{Document $n$} & -
\end{bmatrix} = \begin{bmatrix}
    | & | & & | \\
    \text{Term $1$} & \text{Term $2$} & \cdots & \text{Term $t$} \\
    | & | & & |
\end{bmatrix}
$$

-   $n$ documents
-   $t$ terms (words)
-   $x_{ij} = 1$ if term $j$ occurs in document $i$

## Measures of distance

$$
\begin{cases}
    \textbf{Non-negativity}: & d(\bm{x}, \bm{y}) \geq 0 \\
    \textbf{Identity}: & d(\bm{x}, \bm{y}) = 0 \Leftrightarrow \bm{x} = \bm{y} \\
    \textbf{Symmetric}: & d(\bm{x}, \bm{y}) = d(\bm{y}, \bm{x}) \\
    \textbf{Triangle inequality}: & d(\bm{x}, \bm{z}) \leq d(\bm{x}, \bm{y}) + d(\bm{y}, \bm{z}) \\
\end{cases}
$$

### Norms

![[images/4-norms.png]]

$$
\begin{cases}
\textbf{Non-negativity}: & ||\bm{x}|| \geq 0 \\
\textbf{Scaling}: & ||\alpha \bm{x}|| = |\alpha| \cdot ||\bm{x}|| \\
\textbf{Triangle inequality}: & ||\bm{x} + \bm{y}|| \leq ||\bm{x}|| + ||\bm{y}||
\end{cases}
$$

#### L$_p$ norm

$$
d_p = \|\bm{x} - \bm{y}\|_p = \begin{cases}
    \left(\sum_{i=1}^{m} |x_i - y_i|^p\right)^{1/p} & \text{if } p \geq 1 \\
    \max_{i} |x_i - y_i| & \text{if } p = \infty
\end{cases}
$$

#### Frobeniusnorm

Measures the **magnitude of the entire dataset**:

$$
\|\mathbf{X}\|_F = \sqrt{\sum_{i=1}^{N} \sum_{j=1}^{M} x_{ij}^2} = \sqrt{\text{trace}(\mathbf{X}^T \mathbf{X})} = \sum_{i=1}^N \|\bm{x}_i\|_2^2
$$

#### Mahalanobis distance

Takes into account the **correlations** of the data set and **scales** the axes based on the variance of each variable.

$$
d_M(\bm{x}, \bm{y}) = \sqrt{(\bm{x} - \bm{y})^T \bm{\Sigma}^{-1} (\bm{x} - \bm{y})}
$$

If the EVD of $\hat{\bm{S}}=\frac{1}{N} \tilde{\bm{X}}^T \tilde{\bm{X}}$ is $\hat{\bm{S}} = \bm{V} \bm{\Lambda} \bm{V}^T$, then

$$
d_M^2(\bm{x}, \bm{y}) = (\bm{x} - \bm{y})^T \bm{V} \bm{\Lambda}^{-1} \bm{V}^T (\bm{x} - \bm{y})
$$

For the special case $\bm{\Sigma} = \mathbf{I}_M$, we get the Euclidean distance $d_E(\bm{x}, \bm{y})$.

## Dissimilarities

We want that
$$\text{similarity} = s \in [0, 1]$$

We could base dissimilarity on distance and choose $s(\bm{x}, \bm{y}) = \frac{a}{d(\bm{x}, \bm{y}) + a}$ for some $a > 0$, but for some types of data, **measures of similarity may be easier than measures of distance**.

Assume $\bm{x}$ is **binary** and **$M$-dimensional**:
$$\forall i \in \{1, \ldots, M\} : x_i \in \{0, 1\}$$
We can define $$\begin{cases}
f*{11} &= \text{\#entries where } x_i = 1 \text{ and } y_i = 1 \\
f*{10} &= \text{\#entries where } x*i = 1 \text{ and } y_i = 0 \\
f*{01} &= \text{\#entries where } x*i = 0 \text{ and } y_i = 1 \\
f*{00} &= \text{\#entries where } x*i = 0 \text{ and } y_i = 0 \\
M &= f*{11} + f*{10} + f*{01} + f\_{00}
\end{cases}

$$

Then we can define the following **similarity measures**:

-   **Simple Matching Coefficient (SMC)**:
    -   Zeros and ones are a **convention**
        -   _Male/female_
            $$\text{SMC}(\bm{x}, \bm{y}) = \frac{f_{11} + f_{00}}{M}$$
-   **Jaccard Coefficient**:
    -   0/1 has **asymmetric** meaning
        -   Presence/absence
        -   E.g. term-document, disease / no disease
            $$\text{Jaccard}(\bm{x}, \bm{y}) = \frac{f_{11}}{f_{01} + f_{10} + f_{11}}$$
-   **Cosine Similarity**:
    -   Some vectors have much larger norm than others
        -   E.g. term-document
        -   Document length matters
            $$\text{cos}(\bm{x}, \bm{y}) = \frac{f_{11}}{\|\bm{x}\| \cdot \|\bm{y}\|}$$
$$
