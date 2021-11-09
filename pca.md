# PCA

## What is it&#x20;

Principle Component Analysis is the most commonly used dimension reduction algorithm by minimizing the projection error, which is also called projection spread.

It firstly normalize the data in case of different magnitute (square feet of house/number of house), then calculate the eigenvector for the direction of data dispersed and eigenvalue for the relative importance of these different direction. So overall, PCA combines our predictors and allows us to drop the Eigenvectors that are relatively unimportant.

主要成分分析是最常见的降维算法。

在 PCA 中，我们要做的是找到一个**方向向量**（Vector direction），当我们把所有的数据都投射到该向量上时，我们希望投射平均均方误差能尽可能地小。方向向量是一个经过原点的向量，而投射误差是从特征向量向该方向向量作垂线的长度。

![](<.gitbook/assets/image (94).png>)

下面给出主要成分分析问题的描述：

*
  * 问题是要将 n 维数据降至 k 维
  * 目标是找到向量 u(1),u(2),...,u(k)使得总的投射误差最小主要成分分析与线性回顾的比较：

**主要成分分析与线性回归是两种不同的算法**。主要成分分析最小化的是**投射**误差而线性回归尝试的是最小化**预测**误差。线性回归的目的是预测结果，而主要成分分析不作任何预测。

![](<.gitbook/assets/image (95).png>)

上图中，左边的是线性回归的误差，右边则是主要成分分析的误差。

第一步是均值归一化 normalization。我们需要计算出所有特征的均值，然后令 $$x_j=x_j-μ_j$$ 。如果特征是在不同的数量级上 (square feet of house/number of house)，我们还需要将其除以标准差 $$σ^2$$ 。

if we don't do the normalization:

**A common answer is to suggest that covariance is used when variables are on the same scale, and correlation when their scales are different. However, this is only true when scale of the variables isn't a factor. **Otherwise, why would anyone ever do covariance PCA? It would be safer to always perform correlation PCA.

Imagine that your variables have different units of measure, such as meters and kilograms. It shouldn't matter whether you use meters or centimeters in this case, so you could argue that correlation matrix should be used.

Consider now population of people in different states. The units of measure are the same - counts (number) of people. Now, the scales could be different: DC has 600K and CA - 38M people. Should we use correlation matrix here? It depends. In some applications we do want to adjust for the size of the state. Using the covariance matrix is one way for building factors that account for the size of the state.

**Hence, my answer is to use covariance matrix when variance of the original variable is important, and use correlation when it is not.**

第二步是计算**协方差矩阵**（covariance matrix）Σ for two variables X, Y：

![](<.gitbook/assets/image (96).png>)

bottom-left and upper-right are the covariance matrix



第三步是计算协方差矩阵的**特征向量**（eigenvectors）:

在 Octave 里我们可以利用**奇异值分解**（singular value decomposition）来求解，\[U, S, V] = svd(sigma)。

对于一个 n×n 维度的矩阵，上式中的U 是一个具有与数据之间最小投射误差的方向向量构成的矩阵。如果我们希望将数据从 n 维降至 k 维，我们只需要从 U 真呢个选取前 K 个向量，获得一个 n×k 维度的矩阵，我们用 U\_reduce 表示，然后通过如下计算获得要求的新特征向量 z(i)：

![](<.gitbook/assets/image (97).png>)

其中 x 是 n×1 维的，因此结果为 k×1 维度。注，我们不对偏倚特征进行处理。

### Why choose maximum variance as first principle component

![](https://i.stack.imgur.com/Q7HIP.gif)

If you stare at this animation for some time, you will notice that "the maximum variance (projection spread)" and "the minimum error" are reached at the same time, namely when the line points to the magenta ticks I marked on both sides of the wine cloud. This line corresponds to the new wine property that will be constructed by PCA.

### Why eigenvector

{% embed url="https://zhuanlan.zhihu.com/p/32412043" %}

part. 6

![](<.gitbook/assets/image (98).png>)

### Why does PCA work?

While PCA is a very technical method relying on in-depth linear algebra algorithms, it’s a relatively intuitive method when you think about it.

* First, the covariance matrix $$Z^TZ$$ is a matrix that contains estimates of how every variable in _**Z**_ relates to every other variable in _**Z**_. Understanding how one variable is associated with another is quite powerful.
* Second, Eigenvalues and Eigenvectors are important. **Eigenvectors represent directions**. Think of plotting your data on a multidimensional scatterplot. Then one can think of an individual Eigenvector as a particular “direction” in your scatterplot of data. **Eigenvalues represent magnitude, or importance**. Bigger Eigenvalues correlate with more important directions.
* Finally, we make an assumption that more variability in a particular direction correlates with explaining the behavior of the dependent variable. Lots of variability usually indicates signal, whereas little variability usually indicates noise. Thus, the more variability there is in a particular direction is, theoretically, indicative of something important we want to detect. (The [setosa.io PCA applet](http://setosa.io/ev/principal-component-analysis/) is a great way to play around with data and convince yourself why it makes sense.)

Thus, PCA is a method that brings together:

1. **A measure of how each variable is associated with one another. (Covariance matrix.)**
2. **The directions in which our data are dispersed. (Eigenvectors.)**
3. **The relative importance of these different directions. (Eigenvalues.)**

PCA combines our predictors and allows us to drop the Eigenvectors that are relatively unimportant.

### How PCA transform data

{% embed url="https://medium.com/analytics-vidhya/understanding-principle-component-analysis-pca-step-by-step-e7a4bb4031d9" %}

![](<.gitbook/assets/image (110).png>)

After transforming, we obtained the data with reduced dimension but relatively large variance w.r.t. the original data

### When to use PCA

* Reduce the number of features but cannot identify the unimportant ones that can be ignored, and
* Ensure that the features of the data are independent of one another even if the features become less interpretable

### Results Interpretation&#x20;

K numbers of variables explains  ...% of variance of data&#x20;

### References

{% embed url="https://stats.stackexchange.com/a/140579" %}



### Extension: Covariance vs Correlation

Correlation \[-1,1] is the normalized format of Covariance $$[-\inf, \inf]$$&#x20;

#### What is Covariance?

Covariance measures how two variables move with respect to each other and is an extension of the concept of variance (which tells about how a single variable varies). It can take any value from -∞ to +∞.

* Higher this value, more dependent is the relationship. A positive number signifies positive covariance and denotes that there is a direct relationship. Effectively this means that an increase in one variable would also lead to a corresponding increase in the other variable provided other conditions remain constant.
* On the other hand, a negative number signifies negative covariance which denotes an inverse relationship between the two variables. Though covariance is perfect for defining the type of relationship, it is bad for interpreting its magnitude.

#### What is Correlation?

Correlation is a step ahead of covariance as it quantifies the relationship between two random variables. In simple terms, it is a unit measure of how these var

| **Basis**        | **Covariance**                                                                                                                               | **Correlation**                                                                                                                                                                      |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Meaning**      | Covariance is an indicator of the extent to which 2 random variables are dependent on each other. A higher number denotes higher dependency. | Correlation is an indicator of how strongly these 2 variables are related provided other conditions are constant. The maximum value is +1 denoting a perfect dependent relationship. |
| **Relationship** | Correlation can be deduced from covariance                                                                                                   | Correlation provides a measure of covariance on a standard scale. It is deduced by dividing the calculated covariance with standard deviation.                                       |
| **Values**       | The value of covariance lies in the range of -∞ and +∞.                                                                                      | Correlation is limited to values between the range -1 and +1.                                                                                                                        |
| **Scalability**  | Affects covariance                                                                                                                           | Correlation is not affected by a change in scales or multiplication by a constant.                                                                                                   |
| **Units**        | Covariance has a definite unit as it is deduced by the multiplication of two numbers and their units.                                        | Correlation is a unitless absolute number between -1 and +1 including decimal values.                                                                                                |

![](<.gitbook/assets/image (99).png>)

## When/where to use it&#x20;



## What it can do and what it can't do
