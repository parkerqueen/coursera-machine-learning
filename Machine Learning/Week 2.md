# Week 2

## Section 1
* For multivariate linear regression, the hypothesis becomes
$$h_\theta(x_1,x_2,x_3,\cdots,x_n)=\theta_0+\theta_1x_1+\theta_2x_2+\theta_3x_3+\cdots+\theta_nx_n$$
* It's better to introduce new notations. Consider the following
$$x=
\begin{bmatrix}
    x_0 \\
    x_1 \\
    x_2 \\
    x_3 \\
    \vdots \\
    x_n
\end{bmatrix},
\theta=
\begin{bmatrix}
    \theta_0 \\
    \theta_1 \\
    \theta_2 \\
    \theta_3 \\
    \vdots \\
    \theta_n
\end{bmatrix},
x_0=1
$$
* Now, our equation becomes
$$h(x)=\theta^Tx$$

## Section 2
* The squared error cost function for multivariate linear regression
$$J(\theta)=\frac{1}{2m}\times\sum_{i=1}^m(h(x^i)-y(x^i))^2$$
* The gradient descent algorithm for multivariate linear regression
  * Repeat until convergence for each $\theta_i$ of the vector $\theta$
$$\theta_j=\theta_j-\alpha\times\frac{\partial}{\partial\theta_j}(J(\theta))$$
$$\theta_j=\theta_j-\alpha\times\frac{1}{m}\times\sum_{i=1}^m((h(x^i)-y(x^i))\times x_j^i)$$

## Section 3
* If the possible ranges of your features are very different, then gradient descent might take longer to find the minima
* An appropriate heuristic is to scale your feature ranges. A generally acceptable range is to get all of your features within `-1` & `+1`
* If $-0.0000001\le x_j\le+0.0000001$ holds true for some $x_j$, then even though $-1\le x_j\le+1$ is true, the difference between ranges of other features (having a more closely-packed `-1` to `+1` range) would still be large
* Another heuristic is mean normalization. Each feature value for $x_j$ is replaced by ($\mu_j$ is the mean for feature $x_j$)
$$\frac{x_j-\mu_j}{max(x_j)-min(x_j)}$$
* Instead of using range, we can also use the Standard Deviation in the above formula

## Section 4
* To make sure that the gradient descent is actually working properly
  * Debugging Convergence Test: Plot $J(\theta)$ against the number of iterations of the gradient descent. If the curve is decreasing after every iteration, then the algorithm is working properly. Look for the point where the curve flattens. This is where the gradient descent solution has most likely converged
  * Automatic Convergence Test: Use numerical analysis tools to ensure the difference between the previous value and the current value is less than some threshold $\epsilon$ to gauge convergence
* Try choosing different values for the learning rate and use the plot method above to find the best $\alpha$ that gives you a curve that has the greatest negative slope

## Section 5
* We're not bound to choosing the features that are provided explicitly in the dataset. We can combine two features to create a third feature and use it in our regression model
* We're also not bound to using a linear model of regression but can choose any polynomial regression model and run it just like the methods we've studied
* If our hypothesis were the following, we've effectively introduced a new feature $x_3=(x_2)^2$
$$h(x)=\theta_0+\theta_1x_1+\theta_2(x_2)^2$$

## Section 6
* A proper analytical alternative to Gradient Descent is the Normal Equation method
* The intuition behind it is that you can partial derivate the cost function $J(\theta)$ on each $\theta_j$ and set that derivative equal to zero and solve for $\theta_j$
* Mathematically, the above can be done by the following formula ($X$ is called the design matrix)
$$minarg(J(\theta))=(X^TX)^{-1}X^Ty$$
$$X=
\begin{bmatrix}
  vector (x^1)^T \\
  vector (x^2)^T \\
  vector (x^3)^T \\
  \vdots \\
  vector (x^m)^T
\end{bmatrix},
y=
\begin{bmatrix}
  y^1 \\
  y^2 \\
  y^3 \\
  \vdots \\
  y^m
\end{bmatrix}
$$
* Here, $X$ is a $m\times(n+1)$ matrix while $y$ is a m-dimensional vector
* Turns out that calculating inverses of bigger matrices is very costly (For an nxn matrix: $O(n^3)$). A general heuristic is to use the normal equation method if your number of features are 1000 or sometimes maybe even 10000

## Section 7
* The $(X^TX)$ matrix above might at times be non-invertible
  * If your have a feature which is linearly dependant on another feature
  * If $m\le n$ (where $n$ is the number of features)