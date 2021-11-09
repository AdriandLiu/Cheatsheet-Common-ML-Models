# K-means

## What is it&#x20;

K-means is an unsupervised algorithm that was used to cluster different class

### Procedure:

1. Randomly select K points as centroids&#x20;
2. Calculate the _Euclidean_ distance between the centroids and other points and get mean
3. Assign other points to the class that is closest to them (lowest distance to the specific centroid) (calculate the distance between this point to all centroid, whichever smaller/closer, assign it)
4. Repeat 2 - 3 until the centroids and assigned data points don't change any further.

### Loss

K-均值最小化问题，是要最小化所有的数据点与其所关联的聚类中心点之间的距离之和，因

此 K-均值的代价函数（又称**畸变函数** Distortion function）为：![](broken-reference)

![](<.gitbook/assets/image (85).png>)

其中μc(i)代表与 x(i)最近的聚类中心点。

我们的的优化目标便是找出使得代价函数最小的 c(1),c(2),...,c(m)和μ1,μ2,...,μk：

![](<.gitbook/assets/image (86).png>)

回顾刚才给出的 K-均值迭代算法，我们知道，第一个循环是用于减小 c(i)引起的代价，而第二个循环则是用于减小μi 引起的代价。迭代的过程一定会是每一次迭代都在减小代价函数，不然便是出现了错误。

### Select K

#### Elbow method

Calculate the Within-Cluster-Sum of Squared Errors (WSS) for diﬀerent values of k, and choose the k for which WSS becomes ﬁrst starts to diminish. In the plot of WSS-versus-k, this is visible as an elbow.

#### Silhouette method

The silhouette value measures how similar a point is to its own cluster (cohesion) compared to other clusters (separation).

A high value is desirable and indicates that the point is placed in the correct cluster. Pick the k value with highest silhouette value

## When/where to use it&#x20;

## What it can do and what it can't do
