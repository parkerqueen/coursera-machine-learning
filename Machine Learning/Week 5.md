# Week 5

## Section 1
* The cost function for a neural network is going to be a generalization of the cost function we used for binary logistic regression. Concretely
$$J(\theta)=-\frac{1}{m}\times\sum_{i=1}^{m}\sum_{k=1}^{K}((y(x^i))_k\log((h(x^i))_k)+(1-(y(x^i))_k)\log(1-(h(x^i))_k))+\frac{\lambda}{2m}\sum_{l=1}^{L-1}\sum_{i=1}^{s_l}\sum_{j=1}^{s_{l+1}}(\theta_{j,i}^l)^2$$
* The double sum simply adds up the logistic regression costs calculated for each cell in the output layer.
* The triple sum simply adds up the squares of all the individual Θs in the entire network.
* The i in the triple sum does not refer to training example i.

## Section 2
* To perform gradient descent or one of the other advanced optimization algorithms, we have to calculate the partial derivatives of our cost function for each weight.
* The way we'll do that in Neural Networks is through an algorithm which is known as the Backpropagation algorithm. The overall process of the neural network training is described below.
* Given a training set of $m$ examples as $(x^1,y^1)....(x^m,y^m)$.
  * Set $\Delta_{i,j}^l=0$ for all $l$, $i$ and $j$.
  * For each training example $t=1..m$.
    * Set $a^1=x^t$.
    * Perform forward propagation and calculate $a^l$ for all $l$ upto $L$.
    * Using $y^t$, compute $\delta^L=a^L-y^L$
    * Compute $\delta^{L-1}$, $\delta^{L-2}$, $\cdots$, $\delta^2$ using the formula: ($.*$ represents element wise multiplication) 
    $$\delta^l=((\theta^l)^T\delta^{l+1}).*a^l.*(1-a^l)$$
    * Calculate $\Delta^l$ for each $l$ upto $L-1$ using: ($\delta^{l+1}$ should not contain the bias unit)
    $$\Delta^l=\Delta^l+\delta^{l+1}(a^l)^T$$
  * Compute $D_{i,j}^l$ for each $l$, $i$ and $j$.
    $$D_{i,j}^l=
    \begin{cases}
        \frac{1}{m}(\Delta_{i,j}^l+\lambda\theta_{i,j}^l) & j\ne0 \\
        \frac{1}{m}(\Delta_{i,j}^l) & j=0 \\
    \end{cases}$$
  * By mathematics, it can be proven that $\frac{\partial}{\partial\theta_{i,j}^l}J(\theta)=D_{i,j}^l$.

## Section 3
* Backpropagation is a complicated algorithm and hence it is very much possible to introduce subtle bugs which you may not even realize are present.
* Gradient Checking is a method to ensure that your implementation of backpropagation to calculate the partial derivatives is in fact correct.
* The idea behind gradient checking is to numerically approximate the partial derivatives of the cost function for each parameter at the initial values of the parameters and compare the result with the backpropagation produced result.
* Make sure to turn off gradient checking after the verification and not run it in every iteration because numerically computing the partial derivatives is very slow.
* To numerically approximate the partial derivative of a parameter $\theta_j$
$$\frac{\partial}{\partial\theta_j}=\frac{J(
\begin{bmatrix}
  \theta_0 \\
  \theta_1 \\
  \theta_2 \\
  \vdots \\
  \theta_j+\epsilon \\
  \vdots \\
  \theta_n
\end{bmatrix}
)-J(
\begin{bmatrix}
  \theta_0 \\
  \theta_1 \\
  \theta_2 \\
  \vdots \\
  \theta_j-\epsilon \\
  \vdots \\
  \theta_n
\end{bmatrix}
)}{2\epsilon}$$

## Section 4
* While the inital values of each parameter coule be set to $0$ in linear or logistic regression, doing the same for Neural Networks will prevent them from learning interesting hypothesis.
* If all the weights emerging from a neuron are identical and this is true for each neuron of each layer, then $a^l$ will just be a vector of the same value being repeated over and over. Consequently, during backpropagation, the same pattern will be observed for all $\delta^l$. Hence; after gradient descent, the same update will be applied to each weight emerging from a neuron, effectively persisting the symmetry. This is known as the problem of symmetric weights.
* To break this symmetry, we must randomly initialize all the parameters within some boundary such as $[-\epsilon,\epsilon]$.
* One good way for choosing $\epsilon$ is to base it on the number of units in the network. Let $L_{in}=s_l$ and $L_{out}=s_{l+1}$ and to populate $\theta^l$:
$$\epsilon = \frac{\sqrt{6}}{\sqrt{L_{in}+L_{out}}}$$ 