## Linear Regression

Allows non-linear functions in the input, x, but the model is still
linear in the weights! WOW!

$$
\begin{aligned} f(\bm{x}; \bm{w}) &= w_0 + w_1 x_1 + \ldots + w_M x_M \\
&= \sum_{j=0}^M w_j x_j \\
&= \tilde{x}^T \bm{w} && \tilde{x} = (1, x_1, \ldots, x_M)^T \\
&= \bm{w}^T \tilde{x} \\
\end{aligned}
$$

Note that $x_0 = 1$ is a dummy variable to account for the bias term $w_0$.

### Average loss

$$
\begin{aligned}
E(\bm{w}) &= \frac{1}{N} \sum_{i=1}^N (y_i - f(\bm{x}_i; \bm{w}))^2 \\
&= \frac{1}{N} \|\bm{y} - \tilde{\bm{X}} \bm{w}\|^2 \\
\end{aligned}
$$

We can use $L_1$ or $L_2$ loss. For $L_2$, we get the RSS (Residual Sum of Squares).

### Classic least squeares solution

$$
\begin{aligned}
\bm{w}^* &= \arg\min_{\bm{w}} E(\bm{w}) \\
&= \boxed{(\tilde{\bm{X}}^T \tilde{\bm{X}})^{-1} \tilde{\bm{X}}^T \bm{y}} \\
\end{aligned}
$$

> [!exam]
> Probably $(X^TX)^{-1}$ is gonna be given.

### MAP Approach

We want to find the most probable weights given the data.

We assume for each data point $(\bm{x}_i, y_i)$ that the target $y_i$ is generated from a Gaussian distribution with mean $f(\bm{x}_i; \bm{w})$ and variance $\sigma^2$:
$$p(y_i | \bm{x}_i, \bm{w}) = \mathcal{N}(y_i | f(\bm{x}_i; \bm{w}), \sigma^2)$$

Assume that the outputs are conditionally independent given the inputs and weights:

$$
p(\bm{y} | \bm{X}, \bm{w}) = \prod_{i=1}^N p(y_i | \bm{x}_i, \bm{w})
$$

Further, assume that the prior does not depend on the inputs:
$$p(\bm{w} | \bm{X}) = p(\bm{w})$$

Then, for the posterior, we have:

$$
\begin{aligned}
p(\bm{w} | \bm{X}, \bm{y}) &= \frac{p(\bm{y} | \bm{X}, \bm{w}) p(\bm{w})}{p(\bm{y} | \bm{X})} \\
&= \frac{\prod_{i=1}^N p(y_i | \bm{x}_i, \bm{w}) p(\bm{w})}{p(\bm{y} | \bm{X})} \\
\end{aligned}
$$

Now, maximising the posterior is equivalent to minimising the log-posterior:

$$
\begin{aligned}
\bm{w}^* &= \arg\min_{\bm{w}} E(\bm{w})
\end{aligned}
$$

**We modelled the likelihood $p(y_i | \bm{x}_i, \bm{w})$ as a Gaussian**

Now we need to minimise $$E(\bm{w}) = \frac{1}{N} \left[ - \sum_{i=1}^N \log p(y_i | \bm{x}_i, \bm{w}) - \log p(\bm{w}) \right]$$.

## Logistic Regression

Use the Bernouilli distribution to model the likelihood of the data.

-   Problem: $\tilde{w}^T \bm{x}$ can be any real number, but we need a probability in $[0,1]$.
-   Solution: use the sigmoid function to squash the output to $[0,1]$:
    $$\theta_i = \sigma(f(\bm{x}_i; \bm{w})) \qquad \text{with } \sigma(z) = \frac{1}{1 + e^{-z}}$$

Now we compute the negative log-likelihood, because minimising the negative log-likelihood is equivalent to maximising the likelihood, which is equivalent to maximising the posterior (if we assume a flat prior).

> [!exam]
> Maximising the posterior is equivalent to minimising the negative log-posterior.

> [!exam]
> Maximising the posterior is equivalent to maximising the likelihood **if we assume a flat prior**.

Why? Because we can ignore $p(\bm{w})$ if it's constant in $\arg\min_{\bm{w}} E(\bm{w})$.

Now we get that

$$
\theta_i = \sigma(\tilde{\bm{x}}_i^T \bm{w}) = \frac{1}{1 + e^{-\tilde{\bm{x}}_i^T \bm{w}}} \iff \boxed{\theta_i = \frac{1}{1 + \exp(-x_0 + x_1 w_1 + \ldots + x_M w_M)}}
$$

## General Linear Model

We have seen two different (average) losses for regression and classification, and add a general framework to handle both:

![[images/8-general-linear-model.jpg]]

![[images/8-general-linear-model-2.jpg]]
