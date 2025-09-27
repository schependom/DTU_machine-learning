The quality of a question is high when:

-   The question is **balanced**: roughly equal number of examples for each answer
-   The question is **pure**: each answer leads to examples of **(mostly) one class**

## Purity gain $\Delta$

-   Question creates a split: $$\text{node } r \rightarrow K \text{ branches } v_1, \ldots, v_K$$
-   The purity gain $\Delta$ of the question is the difference in impurity before and after the split.
-   The impurity in a branch $v_k$ is weighted by the fraction of examples that go into each branch.
    -   $N(v_k)$: number of examples in branch $v_k$
    -   $N(r)$: number of examples in node $r$
        $$\Delta = I(r) - \sum_{i=1}^{k} \frac{N(v_i)}{N(r)} I(v_i)$$

---

## CLASSIFICATION: Decision Trees

### Purity Function $I(v)$

-   Suppose $C$ classes
-   $p(c|v)$: fraction of examples in branch $v$ that belong to class $c$

1. **Entropy**:$$\text{Entropy}(v) = - \sum_{c=1}^{C} p(c|v) \log_2 p(c|v)$$
2. **Gini impurity**:$$\text{Gini}(v) = 1 - \sum_{c=1}^{C} p(c|v)^2$$
3. **Misclassification error**:$$\text{ClassError}(v) = 1 - \max_{c} p(c|v)$$

### Hunt's algorithm for building a decision tree

1. All examples in root ($D_r$ = all examples)
2. $D_r$ = dataset in current branch
3. If stop criterion met, make leaf node:
    - Assign most common class in $D_r$ to leaf
4. Else:
    - Find question with highest purity gain $\Delta$
    - Split $D_r$ into $K$ branches $v_1, \ldots, v_K$
    - Recurse on each branch with corresponding dataset $D_{v_k}$

Stop criteria:

-   Pure split (one class) encountered
-   Early stopping
    -   E.g. branch contains less than specific \# examples
    -   E.g. max tree depth reached
    -   E.g. purity gain $\Delta$ of the best split is below a threshold
    -   DISADVANTAGE:
        -   **horizon effect**
        -   i.e. future splits could have high purity gain, but we stop too early

### $\bm{X}$ has continuous features

-   Binary, two-way splits
-   Consider each of the $M$ continuous features $X_j$
-   Attempt different splits$$x_m < x^* \qquad \text{where } x^* \text{ is a threshold value}$$
-   This leads to $M$ different questions, each with a different purity gain $\Delta$
-   Choose the question with highest $\Delta$
-   Problem: many possible thresholds $x^*$
    -   Need for **early stopping** in Hunt's algorithm

---

## REGRESSION: Regression Trees

-   We want to **predict the <u>mean</u> response** (continuous) of an observation
-   Allows for flexible prediction that is **piecewise constant**

### Purity function $I(v)$

Denote $y(v)$ the **mean response** of examples in branch $v$:
$$y(v) = \frac{1}{N(v)} \sum_{i=1}^{N(v)} y_i$$
Then the **average sum-of-squares** error in branch $v$ is
$$I(v) = \frac{1}{N(v)} \sum_{i=1}^{N(v)} (y_i - y(v))^2$$
