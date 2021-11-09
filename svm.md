# SVM

## What is it&#x20;

### Definition:

SVM, also stand by Support Vector Machine, can be used in both classification and regression problems. It uses the technique of maximizing two class's margin to get the optimal separator to classify the classes.

### Margin:

![](<.gitbook/assets/image (24).png>)

![](<.gitbook/assets/image (23).png>)

### Hard margin:

![](<.gitbook/assets/image (25).png>)

![](<.gitbook/assets/image (26).png>)

![](<.gitbook/assets/image (27).png>)

### Soft margin:

allow points inside the margin and on the wrong side but penalize them

![](<.gitbook/assets/image (28).png>)

![](<.gitbook/assets/image (29).png>)

### Kernels:

{% embed url="https://zhuanlan.zhihu.com/p/45223109" %}

Due to that some data are not linearly separable, based on the theory: when the dimension is finite, there will a linear separator in dimension hat so we use projection function to project them to higher dimension space in SVM

However, it is computationally expensive to get both projection to higher dimension and dot product of features and response. So after a complex mathematical derivation, we realize that as long as one mathematical function satisfies the Kernal function requirement

$$
K(x,z) = \phi(x).\phi(z)
$$

it can be used to replace the dot product of&#x20;

$$
\phi(x).\phi(z)
$$

&#x20;which is the **projection function** that project data to higher dimension.&#x20;



_**In other words, as kernel is used to replace the projection function, SVM is still doing higher dimension projection but no longer computationally expensive (lower dimension computation in higher dimension space)**_

_****_

### **Definition: **

![](<.gitbook/assets/image (30).png>)

### **Kernel functions example:**

![](<.gitbook/assets/image (31).png>)

### **Final function:**

![](<.gitbook/assets/image (32).png>)

Where

$$
t_n
$$

means Nth training data

### **Formula derivation:**

![](<.gitbook/assets/image (35).png>)

![](<.gitbook/assets/image (34).png>)

![](<.gitbook/assets/image (33).png>)

### Hinge loss

Why hinge loss:

We will punish the misclassified data points, which are located either inside the margin or wrong side of the margin, the margin is _distance from boundary._ If classify correctly, then no punishment.

![](<.gitbook/assets/image (39).png>)

![](<.gitbook/assets/image (40).png>)

![](<.gitbook/assets/image (41).png>)

In hard margin SVM there are, by definition, no misclassifications

### Perceptron vs SVM

![](<.gitbook/assets/image (42).png>)

* The Perceptron does not try to optimize the separation "distance". As long as it finds a hyperplane that separates the two sets, it is good. SVM on the other hand tries to maximize the "support vector", i.e., the distance between two closest opposite sample points.
* The SVM typically tries to use a "kernel function" to project the sample points to high dimension space to make them linearly separable, while the perceptron assumes the sample points are linearly separable.

The major practical difference between a (kernel) perceptron and SVM is that **perceptrons can be trained online (i.e. their weights can be updated as new examples arrive one at a time)** whereas SVMs cannot be. See this question for information on whether SVMs can be trained online. So, even though a SVM is usually a better classifier, perceptrons can still be useful because they are cheap and easy to re-train in a situation in which fresh training data is constantly arriving.

## Support Vector Regression

![](<.gitbook/assets/image (36).png>)

![](<.gitbook/assets/image (37).png>)



###

## When/where to use it&#x20;

Any classification problem with linear or non-linear but the complex data transformations and resulting boundary plane are very difficult to interpret. This is why it's often called a black box.

## What it can do and what it can't do



### Pros:&#x20;

1. Can Perform well on a range of datasets&#x20;
2. Guaranteed Optimality: Due to the nature of Convex Optimization, the solution is guaranteed to be the global minimum not a local minimum.
3. Work in linear separable and non-linear separable with appropriate kernel selection
4. Work well for both low and high-dimensional data&#x20;
5. Memory efficient, as long as the support vectors are determined, other points can be omitted for now while predicting

Explanation of 2:

SVM loss:

![](<.gitbook/assets/image (38).png>)

both of hinge and L2 loss are convex, so their sum is convex, take the partial derivate will result in global minimum

### Cons:&#x20;

1. Efficiency decreases as training set size increases&#x20;
2. Not interpretable: no probability
