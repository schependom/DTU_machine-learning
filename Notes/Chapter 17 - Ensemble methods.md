## Ensemble Methods

Combining multiple (weak) classifiers into one (strong) classifier.

## Bagging

-   bootstrap aggregating
-   new training sets drawn randomly from pool of training data **with replacement**

### Example: Random Forests

Each tree is generated as follows:

-   sample dataset with replacement (multiple datasets)
-   when generating each node in the tree, randomly select a subset of the features and only consider splits using these features (multiple classifiers)

This way, a large number of trees are generated and the trees are combined using majority voting (bagging).

![[images/17-random-forest.jpg]]

## Boosting

-   add weights to the pool of training data
-   train classifier $C_1$ on new training data set, obtained by sampling **with replacement according to weights**
-   classify all data objects
-   increase weights of misclassified objects
-   train classifier $C_2$ on re-weighted training data set
-   repeat

### AdaBoost

-   each classifier $C_m$ has weight $\alpha_m$ based on its accuracy
-   use majority vote weighted by $\alpha_m$ to classify new objects

![[images/17-adaboost-algo.jpg]]

![[images/17-adaboost.jpg]]
