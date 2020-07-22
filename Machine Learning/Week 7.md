# Week 7

## Section 1
* Another algorthm for classification problems is known as Support Vector Machine.
* Let the parameters of the model be defined as $\theta$ and the input vector of features be $x$. The hypothesis/model of a support vector machine is
$$h(x)=
\begin{cases}
    1 & \theta^Tx\ge0 \\
    0 & otherwise \\
\end{cases}$$
* The cost function is
$$J(\theta)=C\sum_{i=1}^{m}(y(x^i)cost_1(\theta^Tx^i)+(1-y(x^i))cost_0(\theta^Tx^i))+\frac{1}{2}\sum_{j=1}^{n}(\theta_j^2)$$
* $cost_1(\theta^Tx^i)=0$ when $\theta^Tx^i\ge1$ and $cost_0(\theta^Tx^i)=0$ when $\theta^Tx^i\le-1$. Both of these functions increase linearly in 'otherwise' cases.
* What $\lambda$ served in the optimization objective of logistic regression can be gained by $C$.
* You'd notice that the cost function gives a cost of zero only when something is greater than or less than 0 by a margin of more than 1. It's just acting as a safety factor.
* In SVM, there is the concept of Large Margin Classification. Concretely, If $C$ is very large, an SVM will pick such a decision boundary which will have as large as possible minimum distance to any of the training examples.

## Section 2
* A vector inner product of two vectors $u$ & $v$ is equal to $u^Tv$ and $u^Tv=p\times||u||$ where $p$ is the length of orthognal projection of $v$ onto $u$ (can be both positive & negative). Lastly, $u^Tv=v^Tu$.
* Consider that $C$ is very large and that $\theta$ has 3 entries with $\theta_0=0$. The optimization objective of SVM boils down to
$$J(\theta)=\frac{1}{2}(||\theta||)^2\;\;\;s.t.\;\;\;p^i||\theta||\ge1\;\;if\;\;y^i=1\;\;\;and\;\;\;p^i||\theta||\le-1\;\;if\;\;y^i=0$$
* Our optimization objective is to get as small a value as possible for $\theta$ but at the same time get $abs(p^i||\theta||)$ greater than 1 (a large value). The only way to be able to achieve that is to maximize the value of $p^i$. Graphically, it can be shown that $p^i$ represents the distance from the training example $i$ to the decision boundary.
* Hence, SVM is known as a large margin classifier in that it tries to choose the maximum margin decision boundary from each training example under a very large value of $C$. We can use this $C$ to tune this behavior.

## Section 3
* For learning complex non-linear hypothesis, we usually took higher order polynomials of the same features.
* For SVMs, we have the concept of kernels. In the vector space of features, we can randomly choose landmarks. Let's say I choose 3 landmarks $l^1$, $l^2$, $l^3$.
* In this way, I've defined 3 new features each corresponding to one of the landmarks. For instance:
$$f_1=similarity(x,l^1)=exp(-\frac{(||x-l^1||)^2}{2\sigma^2})$$
* The $similarity$ function is known as the kernel function. In the above example, I'm using a Gaussian Kernel.
* As $x$ gets closer to $l^1$, $f_1$ approaches $1$ and vice versa.
* $\sigma$ manages the steepness with which $f_1$ reaches $1$ after a certain distance threshold. The less the value of $\sigma$, the steeper the ascent will be.

## Section 4
* We choose $m$ landmarks with $m$ being equal to the number of training examples with $ith$ landmark being the same as the feature vector of example $x^i$.
* For each training example, calculate its feature vector $f^i$. Add a first entry $1$.
* Instead of using $\theta^Tx^i$, we'll now use $\theta^Tf^i$. In this way, we've introduced non-linear decision boundaries for SVMs.
* If we don't use a kernel, it's known as SVM with a linear kernel. We'll simply proceed with using $\theta^Tx^i$
* Larger $C$: Lower Bias, Higher Variance
* Smaller $C$: Higher Bias, Lower Variance
* Larger $\sigma^2$: Features $f^i$ vary more smoothly. Higher Bias, Lower Variance.
* Smaller $\sigma^2$: Features $f^i$ vary less smoothly. Lower Bias, Higher Variance.

## Section 5
* Not all similarity functions make valid kernels. A valid kernel should satisfy a technical condition called "Mercer's Theorem" which enables the SVM packages to execute a wide class of optimizations.
* If $n$ (features) is very large relative to $m$ (training examples), use logistic regression or a linear-kernel SVM.
* If $n$ is small and $m$ is intermediate, use SVM with a Gaussian Kernel.
* If $n$ is small and $m$ is very large, add features and use a linear-kernel SVM (or logistic regression).
