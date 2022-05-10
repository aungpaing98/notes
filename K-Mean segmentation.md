## Steps for K-Mean segmentation
- Step 1 : Randomly generate the initial centriods (*means*) of the k cluster.
- Step 2 : Create k clusters by assigning each feature point to the nearest mean.
- Step 3: Recompute the mean of each cluster.
- Step 4 : Repeat steps 2 and 3 until convergence.


### K-Means Initialization methods
- method 1: Select k random feature points as initial centriods. If two points are very close, resample.
- method 2 : Select k uniformly distributed means within the range of the distribution.
- method 3:  Perform k-means clustering on a subset of pixels and use the result as the initial means.