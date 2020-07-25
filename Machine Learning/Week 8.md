# Week 8

## Section 1
* In unsupervised learning, we are given unlabelled data and the goal is to find some structure in the data.
* One type of unsupervised learning algorithms is the clustering algorithms in which we try and find clusters in data. The goal in clustering to is to form groups having "high cohesion but low coupling".

## Section 2
* Consider a dataset ${x^1,x^2,x^3,\cdots,x^m}$ where $x^i\in R^n$. In essence, the data consists of n-dimensional vectors (n features).
* In K-Means Algorithm, we randomly initialize $K$ cluster centroids $\mu_1,\mu_2,\mu_3,\cdots,\mu_K$ where $\mu_i\in R^n$.
* Repeat
  * for $i=1$ to $m$: 
    * $c^i=minarg_k(||x^i-\mu_k||)^2$
    * This is the cluster assignment step. Each data point is assigned to the closest cluster centroid.
  * for $k=1$ to $K$:
    * $\mu_k=\frac{1}{n}(x^a+x^b+x^c+\cdots+x^n)$
    * This is the cluster move step. Each cluster centroid is moved to newer position: the mean of all the points assigned to that cluster.
* The optimization objective of K-Means Clustering is known as the distortion function:
$$J(c^1,c^2,\cdots,c^m,\mu_1,\mu_2,\cdots,\mu_K)=\frac{1}{m}\times\sum_{i=1}^{m}(||x^i-\mu_{c^i}||)^2$$

## Section 3
* To randomly initialize $K$ cluster centroids, we randomly pick $K$ data points and set them as our centroids.
* It turns out that using different initializations may result in different solutions, each representing a local optima.
* The recommended way is to try out lots of random initializations to make sure that our algorithm doesn't get stuck in a bad local optima. In the end, the clustering with the least distortion cost can be chosen. This makes a huge difference when the $K$ is between 2 and 10. As $K$ increases, we're already likely to have a decent solution in the first run.
* To choose $K$, most of the times it is done manually or by human intuition. One automatic way is the "Elbow Method". In Elbow Method, you plot a graph betweek the number of clusters on x-axis against the distortion cost on the y-axis. As you move along the x-axis, the graph decreases until it almost plateaus out after a certain $K$. The best $K$ is usually where the curve forms a shape similar to human elbow.

## Section 4
* Another facet of non-supervised learning is called 'Dimensionality Reduction'. In dimensionality reduction, we reduce an n-dimensional data set to an m-dimensional approximation where $m\le n$.
* Think of a 2D dataset where each point $x^i\in R^2$. We can think of a line and project each $x^i$ onto that line. We need only one number to represent the projection of each point on the line. In essence, we've created a 1D approximation of our dataset. This concept scales to bigger dimensions. 
* Dimensionality reduction is used when our features are highly correlated or dependent.

## Section 5
* Principal Component Analysis is an algorithm used to perform dimensionality reduction. In PCA, if we're reducing from $n$ dimensions to $k$ dimensions, then we need to find $k$ vectors ($u^1$, $u^2$, $\cdots$, $u^k$) such that the projection (orthogonally) of all our data points onto the linear subspace spanned by these vectors yields the minimum projection error.
* First we perform mean normalization and feature scaling.
* Calculate covariance matrix $\Sigma$ as
$$\Sigma=\frac{1}{m}\sum_{i=1}^{n}(x^i\times (x^i)^T)$$
* Perform singular value decomposition to obtain $U$, $S$ & $V$ of $\Sigma$. The eigenvectors contained in $U$ correspond to the principal components of variation in out data.
* The first $k$ columns of $U$ are our vectors $u^1$, $u^2$, $\cdots$, $u^k$ (principal components). Call the relevant $n\times k$ sub-matrix of $U$ as $U_{reduce}$. 
* Our reduced feature vector for $x^i$ becomes
$$z^i=U_{reduce}^Tx^i$$
* For decompression
$$x^i\approx U_{reduce}z^i$$
* To retain 99% data variance in our compressed data, we choose the smallest value of $k$ such that:
$$\frac{\frac{1}{m}\sum_{i=1}^{m}(||x^i-x_{approx}^{i}||)^2}{\frac{1}{m}\sum_{i=1}^{m}(||x^i||)^2}\le0.01$$
* To calculate the expression above for different $k$s in an efficient manner:
$$1-\frac{\sum_{i=1}^{k}(S_{ii})}{\sum_{i=1}^{n}(S_{ii})}$$
* If using PCA to speed up a supervised learning problem, the mapping of $x^i\to z^i$ should be learned from the training set only.
* Using PCA to prevent over-fitting alone is not a good idea. Use regularization instead.