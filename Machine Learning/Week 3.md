# Week 3

## Section 1
* The usual way to solve classification problem is to use some regression model and set up a threshold (or a set of thresholds) around which you can classify an input.
* Linear regression does not work very well for such a scenario. For a classification problem, there are better functions available which fit the data more suitably that linear lines. For instance, a linear regression model will output values larger than 1 and smaller than 0 for some inputs (binary classification) but a logistic model won't.
* A logistic regression model is usually used for binary classification.

## Section 2
* For binary classification, we try to fit an S-shaped curve through our data. A function called the sigmoid function (or the logistic function) is perfect for such an S-shaped curve.
$$sigmoid(x)=\frac{1}{1+exp(-x)}$$
* The sigmoid function gives output less than `0.5` for $x<0$ and output greater than `0.5` for $x>0$.
* To fit the sigmoid function, we find a linear function (usually, can be non-linear too) which is known as the decision boundary (see Section 3) and compose that function into the sigmoid function to get a hypothesis as
$$h(x)=\frac{1}{1+\exp(-\theta^Tx)}$$
* The output of a logistic model delineates the probability of our classification being `1`. Concretely
$$h(x)=P(y=1|x;\theta)$$
* If the probability is greater than or equal to `0.5`, we classify it as belonging to category `1` and vice versa.

## Section 3
* The input to the sigmoid function is $\theta^Tx$ which represents some linear equation. This is the line we're trying to fit into the graph as a decision boundary i.e. something that separates our binary classes.
* The essence is that putting our input features into the decision boundary curve will give us a positive or a negative value.
  * For positive values, we will get our hypothesis value to be greater than `0.5`
  * For negative values, we will get our hypothesis value to be less than `0.5`
  * The bigger the positive value or the smaller the negative value, the far away our hypothesis will be from `0.5`
* So our decision boundary is some curve that should output a positive value for one category and a negative value for the other category.
* Just like we studied how we can generalize linear regression to polynomial regression, we can also fit non-linear decision boundaries into the data in case of logistic regression. All depends on what type of equation we're trying to input into our sigmoid function.

## Section 4
* The cost function for logistic regression is
$$J(\theta)=\frac{1}{m}\times\sum_{i=1}^{m}(cost(h(x^i),y(x^i)))$$
$$cost(h(x),y(x))=
\begin{cases}
    -\log(h(x)) & y(x)=1 \\
    -\log(1-h(x)) & y(x)=0 \\
\end{cases}$$
* Case 1: $y(x)=1$
  * The plot of $\log(x)$ between `0` & `1` (because our h(x) can only ever output values between `0` & `1`) shows that
    * $-\log(1)=0$
    * $-\log(0)=\infty$ (vertical asymptote)
    * So; the cost is 0 if $h(x)=1$ and as $h(x)\to0$, the cost is increased rapidly towards $\infty$
* Case 2: $y(x)=0$
  * The plot of $\log(1-x)$ between `0` & `1` shows that
    * $-\log(0)=0$
    * $-\log(1)=\infty$ (vertical asymptote)
    * So; the cost is 0 if $h(x)=0$ and as $h(x)\to1$, the cost is increased rapidly towards $\infty$
* The squared error cost function for linear regression was convex and local optima free but if we used the same cost function for our logistic regression model, it would not be a convex function. But our new cost function is convex.

## Section 5
* The simplified cost function for logistic regression is
$$J(\theta)=-\frac{1}{m}\times\sum_{i=1}^{m}(y(x^i)\log(h(x^i))+(1-y(x^i))\log(1-h(x^i)))$$
* The gradient descent algorithm for logistic regression is
  * Repeat until convergence for each $\theta_j$ of the vector $\theta$
$$\theta_j=\theta_j-\alpha\times\frac{\partial}{\partial\theta_j}(J(\theta))$$
$$\theta_j=\theta_j-\alpha\times\frac{1}{m}\times\sum_{i=1}^m((h(x^i)-y(x^i))\times x_j^i)$$

## Section 6
* There are more advanced optimization algorithms than Gradient Descent such as
  * Cojugate Gradient
  * BFGS
  * L-BFGS
* These algorithms converge more quickly and do not need a learning rate to be chosen.

## Section 7
* For a multi-class classification problem, we can use the one-versus-all (aka one-versus-rest) algorithm.
* For example, say we have a problem to classify an item into three categories: `0`, `1` & `2`.
* What we will do is train `3` binary classification logistic models. We will end up training three hypothesis functions.
$$h^k(x)=P(y=k|x;\theta)$$
* We can then choose the category whose hypothesis function yields the maximum probability.

## Section 8
* The problem of overfitting and underfitting arises in the context of what type of curve (what degree polynomial) is to be used to fit the data.
* Generally, the higher order a polynomial is, the more flexibility it has in fitting the data.
* In underfitting, the function can not account for all the data values and has high bias but low variance. Underfitting occurs when using lower degree polynomials. An underfit model does not capture all the training values properly as well as fails to generalize to unseen problems.
* In overfitting, the function tries too hard to account for the data values and has low bias but high variance. Overfitting occurs when using higher order polynomials. An overfit model does capture all the training values properly but fails to generalize to previously unseen problems.
* There are two ways to address overfitting:
  * Reduce the number of features (manually or using a model selection algorithm)
  * Regularization (Reduce the magnitude of each $\theta_j$) 

## Section 9
* One way to achieve regularization is to modify our cost function to penalize large values for each $\theta_j$ except $\theta_0$. We dont penalize $\theta_0$ conventionally but you may very wall decide to do that. For linear regression
$$J(\theta)=\frac{1}{2m}\times(\sum_{i=1}^{m}(h(x^i)-y(x^i))^2+\lambda\sum_{j=1}^{n}(\theta_j)^2)$$
* The above mentioned cost function delineates two goals. We have to fit the data perfectly while also keeping the parameters lower in magnitude.
* The $\lambda$ is called the regularization parameter and controls the balance between the two goals mentioned above. Bear in mind that too high a value for $\lambda$ will furnish an underfit model.
* Lower magnitude parameters result in smoother function and are less prone to overfitting.

## Section 10
* For linear regression, the updated cost function has been mentioned in Section 9.
* For gradient descent of the updated cost function
  * Repeat until convergence for each $\theta_j$ of the vector $\theta$ (2nd equation holds for $j\ge1$)
$$\theta_0=\theta_0-\alpha\times\frac{1}{m}\times\sum_{i=1}^{m}(h(x^i)-y(x^i))$$
$$\theta_j=\theta_j-\alpha\times(\frac{1}{m}\times\sum_{i=1}^{m}((h(x^i)-y(x^i))\times x_j^i)+\frac{\lambda}{m}\theta_j)$$
* We can rewrite the 2nd equation to gain a better intuition about what's happening.
$$\theta_j=\theta_j(1-\alpha\frac{\lambda}{m})-\alpha\times\frac{1}{m}\times\sum_{i=1}^{m}((h(x^i)-y(x^i))\times x_j^i)$$

## Section 11
* The normal equation method for the updated cost function becomes
$$minarg(J(\theta))=(X^TX+\lambda
\begin{bmatrix}
  0 & 0 & 0 & \cdots & 0 \\
  0 & 1 & 0 & \cdots & 0 \\
  0 & 0 & 1 & \cdots & 0 \\
  \vdots & \vdots & \vdots & \vdots & \vdots \\
  0 & 0 & 0 & \cdots & 1
\end{bmatrix}
)^{-1}X^Ty$$
* The above newer equation also solves the non-invertability issue that we encountered before.

## Section 12
* For logistic regression, the updated cost function becomes
$$J(\theta)=-\frac{1}{m}\times\sum_{i=1}^{m}(y(x^i)\log(h(x^i))+(1-y(x^i))\log(1-h(x^i)))+\frac{\lambda}{2m}\sum_{j=1}^{n}(\theta_j)^2$$
* The gradient descent for the updated cost function goes as
  * Repeat until convergence for each $\theta_j$ of the vector $\theta$ (2nd equation holds for $j\ge1$)
$$\theta_0=\theta_0-\alpha\times\frac{1}{m}\times\sum_{i=1}^{m}(h(x^i)-y(x^i))$$
$$\theta_j=\theta_j-\alpha\times(\frac{1}{m}\times\sum_{i=1}^{m}((h(x^i)-y(x^i))\times x_j^i)+\frac{\lambda}{m}\theta_j)$$
