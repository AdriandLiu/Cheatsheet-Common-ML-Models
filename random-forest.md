# Random Forest

## What is it&#x20;

### Definition:

Random forest is an ensemble method that uses the idea of bootstrap and bagging (bootstrap aggregating) to&#x20;

1. firstly sample the training data with replacement, **K times**, these subset of data are independent
2. subset the features with dimension of $$\sqrt{D}$$
3. build **K number of weak learner** (accuracy slightly over 50% ,usually shallow decision tree) based on the subset of data points and features.&#x20;
4. vote (**mode**) for the classification return; **mean** for the regression return (All models have equal importance).

### Out of bag:

* the instances not included in a bootstrap dataset can be used for validation
* simultaneous validation of decision trees in a forest
* no need to set aside data for cross validation

### Variable importance:

#### Mean decrease Gini

Determining the feature importance can be done with different methods, the Gini Importance method or the Mean Decrease Accuracy method, depending on if the Random Forest purpose was either classification or regression. **The Gini method is based on the Gini Index which is a measure for impurity in a population, a low Gini coefficient represents more purity in a data set.** Now, if we think about the trees in a Random Forest, every node contains a certain distribution of the response variable. After a split, the child nodes should have a lower Gini coefficient, because the goal of the splits is to make the class distributions in the child nodes as pure as possible, all observations in a node should be as similar as possible. So the variable that was used to make the split has decreased the Gini. **Now if we evaluate the mean decrease in Gini that every feature used in the trees of the forest has realized, we know how much each feature has contributed to the performance of the model. **

#### Mean decrease accuracy

The Mean Decrease Accuracy method uses observations that have not been used to train the model. These observations with known outcomes are scored by the model and the accuracy is then recorded. Next a random permutation is done for the values of one feature of these unused observations, then the model scores these observations again (with noise in one feature) and calculates how much the accuracy of the model has decreased. When this is done for all features we can rank the features on importance.&#x20;

## Why

Random forest reduces the correlation of individual trees by sampling the training data and features. (Individual better than random as long as they are uncorrelated)

**So in our random forest, we end up with trees that are not only trained on different sets of data (thanks to bagging) but also use different features to make decisions.**

**Reduce correlation will reduce variance (uncertainty), more trees, more stable.**

****

## When/where to use it&#x20;

Classification

Regression

**But not time-series data as both training data and features will be subsampled.**

## What it can do and what it can't do

### Pro:

* It is unexcelled in accuracy among current algorithms.
* It runs efficiently on large data bases. (subset of data and features)
* It can handle thousands of input variables without variable deletion. (same above)
* It gives estimates of what variables are important in the classification. (feature importance)
* It generates an internal unbiased estimate of the generalisation error as the forest building progresses. (out of bag)
* It has an effective method for estimating missing data and maintains accuracy when a large proportion of the data are missing.
* It has methods for balancing error in class population unbalanced data sets.
* Generated forests can be saved for future use on other data.
* Prototypes are computed that give information about the relation between the variables and the classification.
* It computes proximities between pairs of cases that can be used in clustering, locating outliers, or (by scaling) give interesting views of the data.
* The capabilities of the above can be extended to unlabeled data, leading to unsupervised clustering, data views and outlier detection.
* It offers an experimental method for detecting variable interactions
