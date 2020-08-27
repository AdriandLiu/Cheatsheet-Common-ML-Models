# KNN

## What is it 

The KNN algorithm assumes that similar things exist in close proximity. In other words, **similar things are near to each other.**

### **Definition:**

KNN calculates the similiarity between different instances by distances and classifies them into K groups of user's choice. 

### How:

1. Initialize K to your chosen number of neighbors
2. For each example in the data
   1. Calculate the distance between the query example and the current example from the data.
   2. Add the distance and the index of the example to an ordered collection
3. Sort the ordered collection of distances and indices from smallest to largest \(in ascending order\) by the distances
4. Pick the first K entries from the sorted collection
5. Get the labels of the selected K entries
6. If regression, return the mean of the K labels
7. If classification, return the mode of the K labels

#### Training process:

When fitting to the data, KNN **does not have training process,** instead, after the input target value is given, KNN then calculates the distance between the target value and all other training data points and select Kth lowest distance, then if **regression**, return lowest Kth **mean**, if **classification**, return lowest Kth **mode**.



### Chose K value:

1. Firstly, there is no physical or biological way to determine the best value for “K”, so we have to try out a few values before settling on one. We can do this by pretending part of the training data is “unknown”
2. **Small values for K can be noisy and subject to the effects of outliers.**
3. **Larger values** of K will have smoother decision boundaries which mean **lower variance but increased bias.**
4. Another way to choose K is though **cross-validation.** First is using some kind of validation process\(cross-validation, leave-one-out,...\) for K=1, 2, 3, ... As K increases, the error usually goes down, then stabilizes, and then raises again. Set **optimum K at the beginning of the stable zone.** One way to select the cross-validation dataset from the training dataset. Take the small portion from the training dataset and call it a validation dataset, and then use the same to evaluate different possible values of K. This way we are going to predict the label for every instance in the validation set using with K equals to 1, K equals to 2, K equals to 3.. and then we look at what value of K gives us the best performance on the validation set and then we can take that value and use that as the final setting of our algorithm so we are minimizing the validation error .
5. In general, practice, choosing the value of **k is k = sqrt\(N\) where N stands for the number of samples in your training dataset.**
6. Try and **keep the value of k odd** in order to avoid confusion between two classes of data

### Example code:

```text
from collections import Counter
import math

def knn(data, query, k, distance_fn, choice_fn):
    neighbor_distances_and_indices = []
    
    # 3. For each example in the data
    for index, example in enumerate(data):
        # 3.1 Calculate the distance between the query example and the current
        # example from the data.
        distance = distance_fn(example[:-1], query)
        
        # 3.2 Add the distance and the index of the example to an ordered collection
        neighbor_distances_and_indices.append((distance, index))
    
    # 4. Sort the ordered collection of distances and indices from
    # smallest to largest (in ascending order) by the distances
    sorted_neighbor_distances_and_indices = sorted(neighbor_distances_and_indices)
    
    # 5. Pick the first K entries from the sorted collection
    k_nearest_distances_and_indices = sorted_neighbor_distances_and_indices[:k]
    
    # 6. Get the labels of the selected K entries
    k_nearest_labels = [data[i][1] for distance, i in k_nearest_distances_and_indices]

    # 7. If regression (choice_fn = mean), return the average of the K labels
    # 8. If classification (choice_fn = mode), return the mode of the K labels
    return k_nearest_distances_and_indices , choice_fn(k_nearest_labels)

def mean(labels):
    return sum(labels) / len(labels)

def mode(labels):
    return Counter(labels).most_common(1)[0][0]

def euclidean_distance(point1, point2):
    sum_squared_distance = 0
    for i in range(len(point1)):
        sum_squared_distance += math.pow(point1[i] - point2[i], 2)
    return math.sqrt(sum_squared_distance)

def main():
    '''
    # Regression Data
    # 
    # Column 0: height (inches)
    # Column 1: weight (pounds)
    '''
    reg_data = [
       [65.75, 112.99],
       [71.52, 136.49],
       [69.40, 153.03],
       [68.22, 142.34],
       [67.79, 144.30],
       [68.70, 123.30],
       [69.80, 141.49],
       [70.01, 136.46],
       [67.90, 112.37],
       [66.49, 127.45],
    ]
    
    # Question:
    # Given the data we have, what's the best-guess at someone's weight if they are 60 inches tall?
    reg_query = [60]
    reg_k_nearest_neighbors, reg_prediction = knn(
        reg_data, reg_query, k=3, distance_fn=euclidean_distance, choice_fn=mean
    )
    
    '''
    # Classification Data
    # 
    # Column 0: age
    # Column 1: likes pineapple
    '''
    clf_data = [
       [22, 1],
       [23, 1],
       [21, 1],
       [18, 1],
       [19, 1],
       [25, 0],
       [27, 0],
       [29, 0],
       [31, 0],
       [45, 0],
    ]
    # Question:
    # Given the data we have, does a 33 year old like pineapples on their pizza?
    clf_query = [33]
    clf_k_nearest_neighbors, clf_prediction = knn(
        clf_data, clf_query, k=3, distance_fn=euclidean_distance, choice_fn=mode
    )

if __name__ == '__main__':
    main()
```

## When/where to use it 

### Recommender system

such as recommend the movie based on the historical watch list.

## What it can do and what it can't do

### Pro:

1. The algorithm is simple and easy to implement.
2. There’s no need to build a model, tune several parameters, or make additional assumptions.
3. The algorithm is versatile. It can be used for classification, regression, and search \(as we will see in the next section\).

### Con:

The algorithm gets significantly slower as the number of examples and/or predictors/independent variables increase.

