# Logistics

## What is it 

### Definition:

Logistics is basically a linear classifier do the classification for linearly separable data but it is able to avoid the problem of that 

1. L2 loss may cause correct prediction can have higher loss than the incorrect one!
   * 

![](.gitbook/assets/image%20%2868%29.png)

Logistic solve the problems by squashing the loss: 

### Formula:

![](.gitbook/assets/image%20%2819%29.png)

![](.gitbook/assets/image%20%2839%29.png)

Decision boundary: 

![](.gitbook/assets/image%20%2820%29.png)

### Loss function:

_Cross entropy:_

![](.gitbook/assets/image%20%28105%29.png)

![](.gitbook/assets/image%20%28102%29.png)

![](.gitbook/assets/image%20%2824%29.png)

![](.gitbook/assets/image%20%2827%29.png)

![](.gitbook/assets/image%20%2810%29.png)

!!! Derived from log-likelihood of **Bernoulli** PDF

Minimizing logistic loss corresponds to maximizing **Bernoulli** likelihood. Minimizing squared-error loss corresponds to maximizing **Gaussian** likelihood \(it's just OLS regression; for 2-class classification it's actually equivalent to LDA\).

## When/where to use it 

To predict the categorical variables/ outcome variable must be discrete

### Binary:

1. fit **one** logistic model
2. predict the class by the **highest** probability

### **Multi-class:**

more than one class:  y ∈ {0,1,…,C} \(**multi-class**: logistics fit C number of classifier and make prediction based on the most confident result\)

![](.gitbook/assets/image%20%2885%29.png)



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

