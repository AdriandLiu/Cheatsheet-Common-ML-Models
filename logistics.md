# Logistics

## What is it&#x20;

### Definition:

Logistics is basically a linear classifier do the classification for linearly separable data but it is able to avoid the problem of that&#x20;

1. L2 loss may cause correct prediction can have higher loss than the incorrect one!
   *

![](<.gitbook/assets/image (19).png>)

Logistic solve the problems by squashing the loss:&#x20;

### Formula:

![](<.gitbook/assets/image (7).png>)

![](<.gitbook/assets/image (8).png>)

Decision boundary:&#x20;

![](<.gitbook/assets/image (20).png>)

### Loss function:

_Cross entropy:_

![](<.gitbook/assets/image (10).png>)

![](<.gitbook/assets/image (16).png>)

![](<.gitbook/assets/image (17).png>)

![](<.gitbook/assets/image (18).png>)

![](<.gitbook/assets/image (21).png>)

!!! Derived from log-likelihood of **Bernoulli** PDF

Minimizing logistic loss corresponds to maximizing **Bernoulli** likelihood. Minimizing squared-error loss corresponds to maximizing **Gaussian** likelihood (it's just OLS regression; for 2-class classification it's actually equivalent to LDA).

## When/where to use it&#x20;

To predict the categorical variables/ outcome variable must be discrete

### Binary:

1. fit **one** logistic model
2. predict the class by the **highest** probability

### **Multi-class:**

more than one class:  y ∈ {0,1,…,C} (**multi-class**: logistics fit C number of classifier and make prediction based on the most confident result)

![](<.gitbook/assets/image (22).png>)



## What it can do and what it can't do

{% embed url="https://iq.opengenus.org/advantages-and-disadvantages-of-logistic-regression/" %}

1. Pros:
   1. Perform well on the linearly separable data
   2. Low dimension, less prone to overfit
   3. No distribution needed
   4. Easy to interpret - probability
   5. No need to worry about highly correlated
2. Cons:
   1. **Non-linear problems can't be solved** with logistic regression **since it has a linear decision surface**
   2. Sensitive to outliers
   3. **difficult to capture complex relationships**
