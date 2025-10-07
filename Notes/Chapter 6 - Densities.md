# Densities

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

---

# Bayesian Inference

## Beta distribution $\text{Beta}(\theta | \alpha, \beta)$

The **Beta distribution** is a distribution over the interval $[0, 1]$ and is parameterized by two positive parameters $\alpha$ and $\beta$:
$$\text{Beta}(\theta | \alpha, \beta) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \theta^{\alpha - 1} (1 - \theta)^{\beta - 1}$$

> [!exam]
> Don't remember formula, but maybe question about the graph.

![[images/6-beta.jpg]]

## Prior

The **prior** distribution $p(\bm{w})$

-   Represents our beliefs about the parameter $\theta$ **before observing any data**
-   Encodes our **initial knowledge** or assumptions about the parameter.

---

We can use the Beta distribution as a **prior** for the parameter $\theta$ of a Bernoulli distribution, because both are defined on the interval $[0, 1]$
$$p(\bm{w}) = p(\theta) = p(\theta | \alpha, \beta) = \text{Beta}(\theta | \alpha, \beta)$$

_E.g. if we would know that for two different situations (dog in doghouse vs. friend flipping coin), we have upfront knowledge about the parameter $\theta$ (probability of success) based on past experience or expert opinion, we can encode this knowledge in the prior distribution by choosing appropriate values for the hyperparameters $\alpha$ and $\beta$._

-   _E.g._, if we have no prior knowledge about $\theta$, we can use a uniform prior $\text{Beta}(\theta | 1, 1)$.
-   _E.g._, if we believe that $\theta$ is likely to be small, we can use a prior like $\text{Beta}(\theta | 2, 5)$.
-   _E.g._, if we believe that $\theta$ is likely to be large, we can use a prior like $\text{Beta}(\theta | 5, 2)$.

## Posterior

The **posterior** distribution $p(\bm{w} | \bm{X}, \text{hyperparams})$

-   Represents our beliefs about the parameters $\bm{w}$ **after observing the data** $\bm{X}$.
-   It is obtained by using **Bayes' theorem**
-   We use the prior and the likelihood:
    -   **Prior** = $p(\bm{w}|\bm{X}, \text{hyperparams})=p(\bm{w} | \text{hyperparams})$
    -   **Likelihood** = $p(\bm{X} | \bm{w})$ = joint probability of the data given the parameters
        $$p(\bm{w} | \bm{X}, \text{hyperparams}) = \frac{p(\bm{X} | \bm{w}) p(\bm{w} | \text{hyperparams})}{p(\bm{X} | \text{hyperparams})}$$

---

_E.g. for the Bernouilli_:
$$p(\theta | N=..., m=..., \alpha, \beta) = \frac{p(N,m | \theta)p(\theta | \alpha, \beta)}{p(N,m)}$$

---

## Notation

![[images/6-notation-bayesian.jpg]]

## Bayesian Inference

The process of updating our beliefs about a parameter $\bm{w}$ after observing data $\bm{X}$ using Bayes' theorem is called **Bayesian Inference**. It involves the following steps:

1. **Choose a prior** distribution $p(\bm{w})$ that reflects our initial beliefs about the parameter.
2. **Collect data** $\bm{X}$
3. Compute the likelihood $p(\bm{X} | \bm{w})$
    - = joint probability of the data given the parameter.
    - E.g. for Bernouilli trials:$$p(N,m | \theta) = \theta^m (1 - \theta)^{N - m}$$
4. **Apply Bayes' theorem** to compute the posterior distribution $p(\bm{w} | \bm{X})$
    - Based on the prior $p(\bm{w} | \text{hyperparameters like } \alpha, \beta)$
    - Based on the likelihood $p(\bm{X} | \bm{w})$
      $$p(\bm{w} | \bm{X}) = \frac{p(\bm{X} | \bm{w}) p(\bm{w})}{p(\bm{X})}$$
5. **Make inferences** about the parameter $\bm{w}$ using the posterior distribution, such as finding the mean, mode, or credible intervals.

## Maximum a posteriori (MAP) estimation as a Learning principle

In Bayesian inference, the **Maximum a posteriori (MAP)** estimation is a method used to estimate the parameters $\bm{w}$ that maximizes the posterior distribution $p(\bm{w} | \bm{X})$. It combines both the prior beliefs about the parameter and the observed data to find the most likely value of $\bm{w}$.

### Difference between MLE and MAP

-   **MLE** focuses solely on the likelihood of the observed data given the parameter, **ignoring any prior beliefs**.
    -   It finds the value of $\bm{w}$
    -   To maximize the **likelihood** $p(\bm{y} | \bm{X}, \bm{w})$ of the observed data.
        $$\bm{w}_{MLE} = \arg\max_{\bm{w}} p(\bm{y} | \bm{X}, \bm{w})$$
-   **MAP incorporates prior beliefs about the parameter** through the prior distribution $p(\bm{w})$.
    -   It finds the value of $\bm{w}$
    -   To maximize the **posterior distribution** $p(\bm{w} | \bm{X}, \bm{y})$.
        $$\bm{w}_{MAP} = \arg\max_{\bm{w}} p(\bm{w} | \bm{X}, \bm{y}) = \arg\max_{\bm{w}} \frac{p(\bm{y} | \bm{X}, \bm{w}) p(\bm{w})}{p(\bm{y} | \bm{X})} = \boxed{\arg\max_{\bm{w}} p(\bm{y} | \bm{X}, \bm{w}) p(\bm{w})}$$

## General Bayesian Inference

1. Consider the data
    - $\bm{X} = (\bm{x}_1, \ldots, \bm{x}_N)^\top$
    - $\bm{y} = (y_1, \ldots, y_N)^\top$
    - $\bm{w}$ are the parameters of the model
2. Make assumptions - Assume that the likelihood $p(\bm{y} | \bm{X}, \bm{w})$ factorizes over the data points
   $\quad \Rightarrow$ the **data** points are **<u>conditionally independent given the parameters</u>** $\bm{w}$:
   $\quad \Rightarrow$ When we know the parameters $\bm{w}$ and $\bm{x}_i$, the other observations are irrelevant in terms of predicting $y_i$:$$\boxed{p(\bm{y} | \bm{X}, \bm{w}) = \prod_{i=1}^N p(y_i | \bm{x}_i, \bm{w})}$$ - The prior $p(\bm{w})$ doesn't depend on the data $\bm{X}$:$$\boxed{p(\bm{w} | \bm{X}) = p(\bm{w})}$$
3. Apply Bayes' theorem to compute the **posterior distribution of the parameters given the data**:
   $$\boxed{p(\bm{w} | \bm{X}, \bm{y}) = \frac{p(\bm{y} | \bm{X}, \bm{w}) p(\bm{w} | \bm{X})}{p(\bm{y} | \bm{X})} = \frac{\prod_{i=1}^N p(y_i | \bm{x}_i, \bm{w}) p(\bm{w})}{p(\bm{y} | \bm{X})}}$$
4. Find the most likely parameters given the data (**MAP** estimation):
    - Maximise the posterior:$$\bm{w}^* = \arg\max_{\bm{w}} p(\bm{w} | \bm{X}, \bm{y})$$
    - Or, equivalently, **minimize the negative log-posterior**:$$\bm{w}^* = \arg\min_{\bm{w}} E(\bm{w}) \qquad \text{with } E(w) = \frac{1}{N} \left[\sum_{i=1}^N - \log p(y_i | \bm{x}_i, \bm{w}) - \log p(\bm{w})\right ]$$
      Because the average negative log-posterior is easier to work with than the posterior itself:
        $$
          \begin{aligned}
          E(\bm{w}) &= \frac{1}{N} \left[- \log \left[ p(\bm{y} | \bm{X}, \bm{w}) p(\bm{w}) \right] \right] \\
          &= \frac{1}{N} \left[- \log p(\bm{y} | \bm{X}, \bm{w}) - \log p(\bm{w}) \right] \\
          &= \frac{1}{N} \left[- \log \left[\prod_{i=1}^N p(y_i | \bm{x}_i, \bm{w})\right] - \log p(\bm{w})\right] && \text{by conditional independence} \\
          &= \frac{1}{N} \left[- \sum_{i=1}^N \log p(y_i | \bm{x}_i, \bm{w}) - \log p(\bm{w})\right] \\
          &= \frac{1}{N} \left[\sum_{i=1}^N - \log p(y_i | \bm{x}_i, \bm{w}) - \log p(\bm{w})\right ]
          \end{aligned}
        $$

## Summary of Bayesian Inference

![[images/6-mle-summary.jpg]]

We multiply the prior with the likelihood to get the posterior.

-   If we assume nothing upfront (flat prior), then the posterior $p(\bm{w} | \bm{X}, \bm{y})$ is equal to the likelihood $p(\bm{y} | \bm{X}, \bm{w})$ (=what our model predicts), which is what MLE does.
-   If we have prior knowledge, we can encode it in the prior $p(\bm{w})$, and the posterior will be a compromise between the prior and the likelihood. In this case, we don't use MLE, but MAP estimation: maximize the posterior instead of the likelihood.
