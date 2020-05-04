# Week 1

## Section 1
* Tom Mitchell defines Machine Learning as:
  *  a computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E
* Machine Learning Algorithms:
  * Supervised Machine Learning (Starred)
  * Unsupervised Machine Learning (Starred)
  * Other algorithms such as Reinforcement Learning, Recommender Systems etc.

## Section 2
* Supervised Machine Learning is where you provide such a data to an algorithm which is 'labelled', a data set in which right answers are given
  * Regression Problem -> Problem with a continuous valued output
  * Classification Problem -> Problem with a discrete valued output
* An algorithm is trained to predict the output based on a input vector of features (attributes)
  * An interesting tidbit: we use Support Vector Machines to deal with problems that operate on infinitely many features
* The output is a function `f` mapping some input(s) to some output(s)

## Section 3
* Unsupervised Machine Learning is where 'unlabelled' data is given to the algorithm
  * We just throw the data towards the algorithm and ask: 'Can you automatically find any sort of structure in the given data?'
  * Clustering Algorithms
  * Non Clustering Algorithms (ex: Cocktail Party Algorithm)
* The output is the structure found in the data

## Section 4
* The output function of a Supervised ML Algorithm is denoted by `h` (hypothesis)
* For a univariate linear regression with one feature $x$
$$h(x)=\theta_0+\theta_1x$$
* The thetas here are called 'parameters'

## Section 5
* For linear regression, the most commonly used cost function is the squared error cost function. For univariate linear regression
$$J(\theta_0,\theta_1)=\frac{1}{2m}\times\sum_{i=1}^{m}(h(x^i)-y(x^i))^2$$
* The mean is being halved (note: we divide by $\frac{1}{2m}$) to aid in computation (when we calculate derivative)
* Our goal is to find the theta values when the cost function is minimum

## Section 6
* Gradient descent is an algorithm used to find the local minimum of some arbitrary function `J`
* For a function `J` of two variables $\theta_0$ & $\theta_1$, the gradient descent algorithm is
  * Repeat until convergence for each variable of `J`
$$\theta_j=\theta_j-\alpha\times\frac{\partial}{\partial \theta_j}(J(\theta_0,\theta_1))$$
  * Note that we perform simultaneous updates
  * The $\alpha$ is called the learning rate and it controls how big a step do we table towards the local minimum
  * If $\alpha$ is too small, it may take a long time to achieve convergence
  * If $\alpha$ is too big, the algorithm may overshoot the local minima and is likely to fail to converge
  * A good thing is that we do not have to reduce the value of $\alpha$ as we approach the local minima to ensure convergence. This is because we're multiplying the learning rate with the slope (slope automatically decreases as we approach the local minima). Hence the algorithm will automatically take smaller and smaller steps as we approach the minimum

## Section 7
* The squared error cost function is a convex function i.e. the only local minima is also the global minima
* To perform gradient descent on the squared error cost function discussed in Section 5, the gradient descent rule translates to
  * Repeat until convergence for $\theta_0$ & $\theta_1$
$$\theta_0=\theta_0-\alpha\times\frac{1}{m}\times\sum_{i=1}^{m}(h(x^i)-y(x^i))$$
$$\theta_1=\theta_1-\alpha\times\frac{1}{m}\times\sum_{i=1}^{m}((h(x^i)-y(x^i))\times x^i)$$
* Since we're looking at the entire training set at every step of the gradient descent, we call it the batch gradient descent