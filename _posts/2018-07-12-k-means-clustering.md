---
layout: post
title: k-mean clustering
---

k-means is a popular unsupervised machine learning algorithm for finding clusters in data.

In this article we will be learning the intuition behind the k-means algorithm and coding a basic implementation of it. Unfortunately I won’t be delving into the mathematics behind the algorithm (or else the article would be too long!) but there are lots of resources on that out there.

## Intuition
The algorithm starts by randomly initialising $$K$$ “centroids” which act as the centre of each cluster.



On each iteration there are two steps.

### Assignment

Each cluster is assigned the points that are “closest” (least squared Euclidean distance) to its centroid.

### Update

Each centroid is updated to be the mean of the points in its cluster.



We repeat this for $$N$$ iterations, and in this way the algorithm discovers “groupings” of observations.



## Implementation
The pseudocode for k-means goes as follows:

```
Input: The centroids K, 
       The number of iterations N, 
       Training set {x_1, x_2 ... x_m}

centroids = array of K randomly initialised points

Repeat:
    for i = 1 to i = m:
        cluster[i] = index of cluster centroid closest to x_i

    for i = 1 to i = K:
        centroids[i] = mean of points assigned to cluster i
```

We’re going to (very) minimally implement this algorithm with pure Python 3.6. We will also limit ourselves to 2 dimensions to make our code simpler. In reality, this algorithm can be applied to any number of dimensions.

First, let’s define how we will represent a single point in space. We can do this using a named tuple. This is a lot like a normal tuple, but the fields are named.

```
from collections import namedtuple

Point = namedtuple("Point", "x y")
This allows us to do things like

p1 = Point(3, 2)
print(p1.x)

>> 3
```

Now, from the pseudocode we can write some skeleton code.

```
from collections import namedtuple
import matplotlib.pyplot as plt
import random

Point = namedtuple("Point", "x y")

"""Our implementation of the k-means algorithm

Args:
    K (int): The number of centroids
    N (int): the number of iterations
    points (List[Point]): Our data points

Returns:
    (List[int]): The clusters list

"""

def kmeans(K, N, points):
    # Initialise centroids as a random sample of points
    centroids = random.sample(points, K)

    # Create an empty list of length len(points)
    # Recall that clusters contains which points are assigned to which cluster
    # e.g. clusters[3] = 2 means that points[3] is in cluster 3
    clusters = [None] * len(points)

    # Repeat N times
    # The _ denotes that we don't care about naming the variable.
    for _ in range(N):
        # ASSIGNMENT
        # The enumerate function adds a counter to the list
        # so we can get both the index and the value
        # e.g. enumerate([d, a, g]) = [(0, d), (1, a), (2, g)]
        for i, point in enumerate(points):
            dist_to_centroids = ...
            closest_centroid = ...
            clusters[i] = closest_centroid

        # UPDATE
        # For each centroid, set it to the mean of points in its cluster
        for k, centroid in enumerate(centroids):
            cluster = get_cluster(...)
            centroid = mean_point(...)

    return clusters
```

Let’s define a function that calculates squared distance. This is easy to implement.

```
def sqrdist(a, b):
    return (a.x - b.x)**2 + (a.y - b.y)**2
```

Now we can use this function in a list comprehension to compute the distance to each centroid.

```
dist_to_centroids = [sqrdist(point, centroid) for centroid in centroids]
```

To calculate the closest centroid we are going to use some neat properties of the min function.

```
closest_centroid, _ = min(enumerate(dist_to_centroids), key=lambda p: p[1])
```

There’s a few different parts to this so let’s break it down.

The `min(key=…)` argument allows you to sort an iterable (in this case a list of `Points`) by a particular key. So we first call `enumerate` on `dist_to_centroids` so we have a list of tuples in the form `[(index, distance), …]` and the lambda `lambda p: p[1]` selects the 2nd element from each tuple. This allows us to sort the list of tuples by distance. Then we can extract the centroid indexes using the syntax `closest_centroid, _` which puts the first element of each tuple into `closest_centroid` and discards the actual distances.

So now we have completed our assignment step.

```
for i, point in enumerate(points):
    dist_to_centroids = [sqrdist(point, centroid) for centroid in centroids]
    closest_centroid, _ = min(enumerate(dist_to_centroids), key=lambda p: p[1])
    clusters[i] = closest_centroid
```

For our update step, we need to implement two functions: `get_cluster` which returns the points in a particular cluster, and `mean_point` which calculate the mean of all the points in a cluster.

Both functions can be implemented simply using a for loop.

```
def get_cluster(k, clusters, points):
    new_cluster = []

for i, cluster in enumerate(clusters):
    if (clusters == k):
    new_cluster.append(points[i])

    return new_cluster
def mean_point(points):
    # If a cluster has 0 points assigned to it,
    # we can effectively delete that cluster
    if (len(points) == 0):
        return Point(0, 0)

    x = 0
    y = 0
    for point in points:
        x += point.x
        y += point.y

return Point(x/len(points), y/len(points))
Now we are done! We can test the function like so:

points = [Point(x=1, y=1),
Point(x=1, y=2),
Point(x=2, y=1),
Point(x=8, y=9),
Point(x=8, y=8),
Point(x=10, y=11),
Point(x=20, y=23),
Point(x=19, y=24),
Point(x=18, y=19),
Point(x=21, y=25),
Point(x=5, y=20),
Point(x=5, y=21),
Point(x=4, y=20)]

kmeans(4, 10, points)

>> [0, 0, 0, 2, 2, 2, 1, 1, 1, 1, 3, 3, 3]
```

These functions could probably be better implemented using functional programming or the like, but the one’s we’ve written are perfectly fine for our purposes.

## Considerations

How do we choose the number of clusters, $$K$$?

This is a rather extensive topic, so rather than discussing it here I will point you to this wikipedia page:

<https://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set>

Despite this, the number of clusters is most often simply chosen by human intuition.

## How do we initialise K?

If you run our implementation several times, you may find that the algorithm converges to different solutions (local optima) depending on the initialisation. Hence, it is important to maximise the chances of getting a “correct” initialisation. The most commonly used method is the one we used, to randomly sample our dataset. Other methods include steps to spread the centroids out. To reduce the effect of bad initialisations, it is recommended to run k-means many times.

Thanks for reading!


