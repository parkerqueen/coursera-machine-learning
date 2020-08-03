# Week 10

## Section 1
* If we have a dataset of 100 million examples, we can train our model on a small subset, say 1000 and use learning curves to verify that the algorithm has high variance when $m$ is small and more data is likely to help. 
* If $m$ is very large, stochastic gradient descent is a much more efficient alternative to batch gradient descent. (Assume we're discussing linear regression)
  * Randomly shuffle the training set.
  * Repeat until convergence for each variable $\theta_j$ of $J(\theta)$
    * for $i=1:m$
      * for all $j$
$$\theta_j=\theta_j-\alpha(h(x^i)-y(x^i))x_j^i$$
* Another algorithm is known as the mini-batch gradient descent. 
  * Choose a paramter $b$. A typical range is between 2 & 100.
  * Repeat until convergence for each variable $\theta_j$ of $J(\theta)$
    * for $i=1:m$ with a step of $b$
      * for all $j$
$$\theta_j=\theta_j-\frac{\alpha}{b}\sum_{k=i}^{i+b}((h(x^k)-y(x^k))x_j^k)$$
* It's important to note that stochastic gradient descent won't actually converge to a global minimum but will meander around it.
* To check if the stochastic gradient descent is working, plotting the cost function over the number of iterations would defeat the efficiency. Instead what we try and do is calculate the average cost of last 1000 (or any other constant) training examples and plot it against the number of iterations in 1000s. If the plot is very noisy and doesn't seem to be decreasing, try the plot with on an avergage of a greater number of training examples to smoothen the curve.

## Section 2
* If we have a continuous stream of data available, then we can make use of Online Learning. In Online Learning, as soon as we get a training example we train our hypothesis on that training example just once and then throw that example away. In essence, soon as we get one training example, we do:
    * for all $j$
$$\theta_j=\theta_j-\alpha(h(x)-y(x))x_j$$
* Normally we continue doing the above infinitely and always training our model. One advantage of this is that our model adapts to the changes automatically.
* MapReduce is a distributed data processing algorithm. We can use it to speed up the training of our model. In the context of linear regression with batch gradient descent, we can divide our dataset into $k$ equal parts and then assign $k$ computing resources to compute the partial derivative terms for each $\theta_j$ over distinct $1/k$ parts of the original training set. In the end, we can add up all the $k$ results and calculate new values for each $\theta_j$.
* In essence, whenever and at any level if we can split up our algorithm and express it in terms of two functions we can map each function's computation to a separate machine/computing resource and reduce the results into one useful figure. 
