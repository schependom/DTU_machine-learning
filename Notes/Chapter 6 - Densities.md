-   We **can not** talk about the probability of a single point (**exact value**) in continuous space.
-   We **can** talk about the probability of a point falling within a certain region (**between two values**).

## Probability density function (pdf)

$p(x)$ is called a **probability density function (pdf)** or simply **density**.

## Continuous random variable

$$P(x \in [a,b]) = \int_a^b p(x) dx$$

$$P((x,y) \in D) = \iint_D p(x,y) dx dy$$

## Rules from Chapter 5 still apply

![[images/6-continuous.png]]

### Expected value

$$\E[f] = \int_{-\infty}^{\infty} f(x) p(x) dx$$

### Mean

$$\bar{x} = \E[x] = \int_{-\infty}^{\infty} x p(x) dx$$

### Covariance

$$\text{cov}(x,y) = \E[(x - \bar{x})(y - \bar{y})] = \iint (x - \bar{x})(y - \bar{y}) p(x,y) dx dy$$

### Variance

$$\text{var}[x] = cov(x,x) = \E[(x - \bar{x})^2] = \int_{-\infty}^{\infty} (x - \bar{x})^2 p(x) dx = \E[x^2] - (\E[x])^2$$

### Standard deviation

$$\text{std}(x) = \sqrt{\text{var}[x]}$$

## The multivariate normal distribution

A distribution of $M$-dimensional vectors $\bm{x} \in \mathbb{R}^M$ is a **multivariate normal distribution** with mean $\bm{\mu} \in \mathbb{R}^M$ and covariance matrix $\bm{\Sigma} \in \mathbb{R}^{M \times M}$ if its **pdf** is given by:
$$\mathcal{N}(\bm{x}|\bm{\mu}, \bm{\Sigma}) = \frac{1}{(2\pi)^{M/2} |\bm{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}(\bm{x} - \bm{\mu})^T \bm{\Sigma}^{-1} (\bm{x} - \bm{\mu})\right)$$
with
$$\bm{\mu} = \E[\bm{x}], \qquad \Sigma_{ij} = \text{cov}(x_i, x_j)$$

---

**NOTE:** the covariance matrix $\bm{\Sigma}$ must be:

-   **Symmetric**$$\text{cov}(x_i, x_j) = \text{cov}(x_j, x_i)$$
-   **Positive semi-definite** (all eigenvalues $\lambda_i \geq 0$): $$\forall \bm{z} \in \mathbb{R}^M : \bm{z}^T \bm{\Sigma} \bm{z} \geq 0$$

$\Sigma$ is not PSD if it has at least one negative eigenvalue.

---

### 2-dimensional example ($M=2$)

Assume $$\bm{\mu} = \begin{bmatrix} \bar{x}_1 \\ \bar{x}_2 \end{bmatrix} = \begin{bmatrix}0 \\ 0\end{bmatrix}, \qquad \bm{\Sigma} = \begin{bmatrix} \text{var}[x_1] & \text{cov}(x_1, x_2) \\ \text{cov}(x_1, x_2) & \text{var}[x_2] \end{bmatrix} = \begin{bmatrix}a & c \\ c & b\end{bmatrix}$$

![[images/6-2d-gaussian.png]]
