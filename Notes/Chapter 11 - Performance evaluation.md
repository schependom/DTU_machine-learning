## Two setups

**Setup I**:

-   Statistical test of performance considering the **specific** training dataset $\mathcal{D}$
-   If $z_\mathcal{D} < 0$, it means that $\mathcal{M}_A$ is better than $\mathcal{M}_B$ **when trainined on** $\mathcal{D}$

**Setup II**:

-   Statistical test of performance considering a **dataset of size $N$**
-   If $z < 0$, it means that $\mathcal{M}_A$ is better than $\mathcal{M}_B$ **using a typical trianing set**

## Comparing two classifiers: McNemar's test

**McNemar's test**

-   compare two classifiers
-   **same dataset**
-   **paired test**

Assume predictions from both classifiers

$$
\begin{align*}
\hat{\mathbf{y}}^A & = \{\hat{y}_1^A, \hat{y}_2^A, \ldots, \hat{y}_n^A\} \\
\hat{\mathbf{y}}^B & = \{\hat{y}_1^B, \hat{y}_2^B, \ldots, \hat{y}_n^B\}
\end{align*}
$$

Then, we can count how many times both classifiers are correct:

$$
\begin{align*}
c_i^A & = \begin{cases}1 & \text{if } \hat{y}_i^A = y_i \\0 & \text{otherwise} \end{cases} \\
c_i^B & = \begin{cases}1 & \text{if } \hat{y}_i^B = y_i \\0 & \text{otherwise} \end{cases}
\end{align*}
$$

$$
\begin{align*}
n_{11} &= \sum_{i=1}^{n} c_i^A c_i^B && =\text{\{both classifiers are correct\}} \\
n_{22} &= \sum_{i=1}^{n} (1-c_i^A) (1-c_i^B) && =\text{\{both classifiers are wrong\}} \\
n_{12} &= \sum_{i=1}^{n} c_i^A (1-c_i^B) && =\text{\{classifier A is correct, classifier B is wrong\}} \\
n_{21} &= \sum_{i=1}^{n} (1-c_i^A) c_i^B && =\text{\{classifier A is wrong, classifier B is correct\}} \\
\end{align*}
$$

We want to compare the accuracy difference:

$$
\theta = \theta_A - \theta_B
$$

where $\theta_A$ and $\theta_B$ are the true accuracies of classifiers A and B, respectively.

The expected value $E_\theta$ can be computed as follows:

$$
E_\theta = \frac{n_{12} + n_{21}}{n} = \hat{\theta} = \hat{\theta}_A - \hat{\theta}_B
$$

## Confidence interval for a regression model

Use cross-validation to obtain $\hat{y}_i$ for each data point $i$. Then, compute the loss as

$$
z_i = L(y_i, \hat{y}_i) = |\hat{y}_i - y_i| \text{ or } z_i = (\hat{y}_i - y_i)^2
$$

Now the estimated error is $$\hat{z} = \frac{1}{n} \sum_{i=1}^{n} z_i$$

If we assume that each error is normally distributed, the likelihood over the dataset $D$ is

$$
p(D | u, \sigma^2) = \prod_{i=1}^{n} \mathcal{N}(z_i | u, \sigma^2)
$$

Where $u$ is the true mean error and $\sigma^2$ is the true variance of the error.
And $u$ follows from the **generalized Student's $t$-distribution**.

## Comparing two regression models

Use cross-validation to obtain $\hat{y}_i^A$ and $\hat{y}_i^B$ for each data point $i$. Then, compute the per-observation losses $z_i^A$ and $z_i^B$. Note that

$$
\begin{align*}
z &= E_{A,\mathcal{D}}^\text{gen} - E_{B,\mathcal{D}}^\text{gen} \\
 &\approx \hat{z} \\
 &= \left(\frac{1}{n} \sum_{i=1}^{n} z_i^A\right) - \left(\frac{1}{n} \sum_{i=1}^{n} z_i^B\right) \\
    &= \frac{1}{n} \sum_{i=1}^{n} (z_i^A - z_i^B) \\
    &= \frac{1}{n} \sum_{i=1}^{n} z_i
\end{align*}
$$

Now assume that each difference in error $z_i$ is normally distributed:

$$
z_i \sim \mathcal{N}(\mu = u, \sigma^2)
$$

We can compare the models with the null hypothesis $H_0$ that model $\mathcal{M}_A$ and model $\mathcal{M}_B$ have the same performance and alternative hypothesis $H_1$ that they have different performance:

$$
\begin{cases}
H_0: u = 0 \\
H_1: u \neq 0
\end{cases}
$$

**EXAM**:

![[images/11-posterior-mcnemar.jpg]]

## Class imbalance

![[images/11-confusion-matrix.jpg]]

$$
\begin{align*}
\textbf{Precision} &= \text{Fraction true positive among positive predictions} \\
& = \frac{TP}{TP + FP} \\
& = p
\hfill \\
\hfill \\
\textbf{Recall} &= \text{Fraction positive predictions among all positive examples} \\
& = \frac{TP}{TP + FN} \\
& = r \\
& = TPR \\
& = \textbf{True Positive Rate}
\end{align*}
$$

p1 = 1/3 = 18/54
r1 = 9/10

p2 = 14/16 = 7/8
r2 = 7/10

## Receiver Operating Characteristic (ROC) curve

The ROC curve plots the True Positive Rate (TPR) against the False Positive Rate (FPR) at various threshold settings.

![[images/11-roc.jpg]]

The **Area Under the Curve (AUC)** is a measure of the classifier's ability to distinguish between classes. An AUC of 0.5 indicates no discrimination (random guessing), while an AUC of 1 indicates perfect discrimination.

$$\boxed{\text{AUC} = \int_0^1 \text{TPR} \, d\text{FPR}}$$

-   A random classifier has $\int_0^1 \text{TPR} \, d\text{FPR} = 0.5$.
-   A perfect classifier has $\int_0^1 \text{TPR} \, d\text{FPR} = 1$.

![[images/11-auc.jpg]]
