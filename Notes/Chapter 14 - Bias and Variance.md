$$
\boxed{E_\lambda(\bm{w}) = \sum_{i=1}^{N} \left\{ \hat{y}_i - w_0 - \hat{\bm{x}}_i^T \bm{w} \right\}^2 + \lambda \|\bm{w}\|_2^2}
$$

where $\lambda \geq 0$ is a regularization parameter that controls the trade-off between fitting the training data and keeping the model weights small. The term $\lambda \|\bm{w}\|_2^2$ penalizes large weights, which helps to prevent overfitting by discouraging complex models that may fit the noise in the training data rather than the underlying pattern.

The expected generalization error can be decomposed into bias, variance, and irreducible error components as follows:

$$
\boxed{\mathbb{E}_{\mathcal{D}} [E^\text{gen}] = \mathbb{E}_\bm{x}\left[ \text{Var}_{y \mid \bm{x}}[y] \right] + (\bar{y}(\bm{x}) - \bar{f}(\bm{x}))^2 + \text{Var}_{\mathcal{D}}[f(\bm{x})]}
$$

Where

-   $\bar{f}(\bm{x}) = \mathbb{E}_{\mathcal{D}}[f(\bm{x})]$ is the expected prediction of the model over different training datasets $\mathcal{D}$
-   $\bar{y}(\bm{x}) = \mathbb{E}_{y \mid \bm{x}}[y]$ is the true mean response for input $\bm{x}$
