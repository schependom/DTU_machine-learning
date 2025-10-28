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

We now turn our attention towards boosting instead of bagging. In boosting we iteratively change the distribution that we sample the training examples from so that the classifiers will focus on examples that are hard to classify. A particularly well known boosting method is `AdaBoost` where the ensemble's prediction accounts for the error rate per learner when doing the prediction.

-   add weights to the pool of training data
-   train classifier $C_1$ on new training data set, obtained by sampling **with replacement according to weights**
-   classify all data objects
-   increase weights of misclassified objects
-   train classifier $C_2$ on re-weighted training data set
-   repeat

### AdaBoost

-   each classifier $C_m$ has weight $\alpha_m$ based on its accuracy
-   To make the final classification, take a weighted majority vote amongst the classifiers in the ensemble (weighted by $\alpha_m$)

![[images/17-adaboost-algo.jpg]]

![[images/17-adaboost.jpg]]
