## Train and test error

$$E_{\mathcal{M}_k}^{\text{train}} = \frac{1}{N^\text{train}} \sum_{i \in \mathcal{D}_{\text{train}}} (y_i - f(\bm{x}_i; \bm{w}_k))^2$$

$$E_{\mathcal{M}_k}^{\text{test}} = \frac{1}{N^\text{test}} \sum_{i \in \mathcal{D}_{\text{test}}} (y_i - f(\bm{x}_i; \bm{w}_k))^2$$

## Overfitting

For overly complex models

-   $E_{\mathcal{M}_k}^{\text{train}}$ is very low
-   $E_{\mathcal{M}_k}^{\text{test}}$ is very high

Test error is more representative of the true error.

## Generalisation error

> **The generalization error is the test error evaluated over an infinitely large test set**

-   Train model $\mathcal{M}$ on the available dataset $D$ to get prediction rule $f_{\mathcal{M}}$
-   Compute $$\boxed{E_{\text{gen}}^{\mathcal{M}} = \mathbb{E}_{(\mathbf{x},\mathbf{y})} [L(\mathbf{y}, f_{\mathcal{M}}(\mathbf{x}))]}$$
-   If we somehow had many test sets $D_1, \ldots, D_k$, we could estimate the generalization error as:
    $$\int L(\mathbf{y}, f_{\mathcal{M}}(\mathbf{x})) p(\mathbf{x}, \mathbf{y}) d\mathbf{x} d\mathbf{y} \approx \frac{1}{K} \sum_{i=1}^{K} L(\mathbf{y}_i, f_{\mathcal{M}}(\mathbf{x}_i))$$
    So:
    $$
    E_{\text{gen}}^{\mathcal{M}} \approx \frac{1}{K} \sum_{k=1}^{K} E_{\text{test}}^{\mathcal{M},D_k}
    $$

## Cross-validation

Purpose: **estimate the generalization error**

-   **HOLDOUT**
    -   $\mathcal{D} = \mathcal{D}_{\text{train}} \cup \mathcal{D}_{\text{test}}$
    -   $\boxed{E^{\text{gen}}_{\mathcal{M}} \approx E_{\text{test}}^{\mathcal{M}}}$
-   **K-FOLD CROSS-VALIDATION**
    -   Split $\mathcal{D}$ into $K$ disjoint subsets $\mathcal{D}_1, \ldots, \mathcal{D}_K$:$$\mathcal{D} = \mathcal{D}_1 \cup \ldots \cup \mathcal{D}_K$$
    -   Each part is a test set once, and a training set $K-1$ times
    -   $\boxed{E^{\text{gen}}_{\mathcal{M}} \approx \frac{1}{K} \sum_{k=1}^K E_{\text{test}}^{\mathcal{M}, \mathcal{D}_k}}$
-   **LEAVE-ONE-OUT CROSS-VALIDATION (LOOCV)**
    -   Special case of K-Fold CV where $K = N$
    -   Each test set has exactly one data point
    -   $\boxed{E^{\text{gen}}_{\mathcal{M}} \approx \frac{1}{N} \sum_{i=1}^N E^{\text{test}}_{\mathcal{M_k}}}$

## Select the best of $S$ models

-   For each model $\mathcal{M}_s$, estimate the generalization error $E^{\text{gen}}_{\mathcal{M}_s}$ using cross-validation
-   Select the model $\mathcal{M}_{s^*}$ with the lowest **estimated** generalization error:$$s^* = \arg\min_{s=1,\ldots,S} \hat{E}^{\text{gen}}_{\mathcal{M}_s}$$

## Which cross-validation method to use?

-   **Holdout**
    -   computationally **least intensive**
    -   **not very data efficient**
    -   $\boxed{\text{High bias, high variance}}$
-   **Leave-one-out**
    -   very computationally **intensive**
    -   **estimates are highly correlated**
    -   $\boxed{\text{Low bias, high variance}}$
-   **K-fold cross-validation**
    -   computationally **moderate**
    -   **more data efficient**
    -   $\boxed{\text{Moderate bias, moderate variance}}$

**Recommendation**:

-   $K$-fold for $K = 5, 10$ - holdout if problem very large
-   $K$-fold for $K = 5, 10$ - holdout if problem very large

## KNN with LOOV

For each observation $x_i$

-   Temporarily remove $x_i$
-   Find $K$ nearest neighbors around $x_i$ (not $x_i$ itself)
-   Determine whether $x_i$ is classified correctly based on this neighborhood:$$c_i = 0 \text{ or } c_i = 1$$
-   Compute **accuracy** as $$\frac{1}{N} \sum_{i=1}^{N} c_i$$

## Two-layer cross-validation

We have $S$ different models $\mathcal{M}_1, \ldots, \mathcal{M}_S$, $K_1$ outer folds and $K_2$ inner folds.

-   **OUTER FOLD** with $K_1$ folds (over $i = 1, \ldots, K_1$):
    -   Split the data into subset $\mathcal{D}^\text{par}_i$ and $\mathcal{D}^\text{test}_i$
    -   For each of the $S$ models, compute the estimated generalization error:$$\hat{E}^{\text{gen}}_s = \sum_{j=1}^{K_2} \frac{|\mathcal{D}^\text{val}_j|}{|\mathcal{D}^\text{par}_i|} E^{\text{val}}_{\mathcal{M}_s,j}$$
        $\rightarrow K_2 \cdot S$ models trained
    -   Select the best model $\mathcal{M}^* = \mathcal{M}_{s^*}$ with $s^* = \arg\min_{s=1,\ldots,S} \hat{E}^{\text{gen}}_s$
    -   Train the selected model $\mathcal{M}^*$ on the entire outer training set $\mathcal{D}^\text{train}_i$
        $\rightarrow 1$ extra model trained
    -   Let $E^{\text{test}}_i$ be the test error of $\mathcal{M}^*$ tested on $\mathcal{D}^\text{test}_i$
-   **INNER FOLD** with $K_2$ folds (over $j = 1, \ldots, K_2$):
    -   Split data $\mathcal{D}^\text{par}$ into subset $\mathcal{D}^\text{train}_j$ and $\mathcal{D}^\text{val}_j$
    -   For each of the models ($s=1, \ldots, S$)
        -   Train model $\mathcal{M}_s$ on $\mathcal{D}^\text{train}_j$
        -   Compute validation error $E^{\text{val}}_{\mathcal{M}_s, _j}$

Compute the overall estimated generalization error as:$$\hat{E}^{\text{gen}} = \sum_{i=1}^{K_1} \frac{|\mathcal{D}^\text{test}_i|}{N} E^{\text{test}}_i$$
$\rightarrow K_1(1 + K_2 S)$ models trained

---

In each inner fold, we train $S$ models, select the best one
$\quad \Rightarrow S \text{ models}$

We do this for each of the $K_2$ inner folds
$\quad \Rightarrow K_2 S \text{ models}$

Then, we train the selected model on the entire outer training set
$\quad \Rightarrow 1 \text{ model}$

In each outer fold, we test the selected model on the outer test set.

We do this for each of the $K_1$ outer folds
$\quad \Rightarrow \boxed{K_1(K_2 S+1) \textbf{ models trained}}$

## Forward and backward feature selection

-   **Forward selection**
    -   Start with no features
    -   Add one feature at a time, the one that gives the lowest cross-validation error
    -   Stop when adding more features does not decrease the cross-validation error
-   **Backward selection**
    -   Start with all features
    -   Remove one feature at a time, the one that gives the lowest cross-validation error
    -   Stop when removing more features does not decrease the cross-validation error

So, when asked a question about this, don't look at the validation error, but at the test error.
