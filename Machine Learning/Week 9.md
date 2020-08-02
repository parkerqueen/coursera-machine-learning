# Week 9

## Section 1
* A gaussian distribution ($\mathcal{N}(\mu,\sigma^2)$) is such in which the random variable assumes values with a probability given by the formula:
$$P(x;\mu,\sigma^2)=\frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{(x-\mu)^2}{2\sigma^2})$$
* A gaussian distribution represents a bell shaped cruve whose peak exists at $\mu$ and whose width of the peakness is defined by $\sigma$.
* "Parameter Estimation" problem is when we try to find $\mu$ and $\sigma^2$ for a likely gaussian distribution. If we're given a set of numbers which we think fit into a normal distribution, we can use the following estimation formulas:
$$\mu=\frac{1}{m}\sum_{i=1}^{m}(x^i)$$
$$\sigma^2=\frac{1}{m}\sum_{i=1}^{m}(x^i-\mu)^2$$

## Section 2
* Anomaly Detection is an unsupervised machine learning problem in which we try and identify outliers/anomalies in our dataset. 
* The idea is to find a model $P(x^i)$ which outputs the probability of $x^i$ being a non-issue. We can then set a threshold $\epsilon$ below which an $x^i$ can be classified as an anomaly.
* Assuming $x^i\in R^n$, we need to fit the parameters $\mu_1, \mu_2, \cdots, \mu_n$ and $\sigma_1^2, \sigma_2^2, \cdots, \sigma_n^2$ using the formulas mentioned in the section above.
* Our probability model $P(x)$ then becomes:
$$P(x)=\prod_{j=1}^{n}P(x_j;\mu_j,\sigma_j^2)$$

## Section 3
* To evaluate our Anomaly Detection algorithm, we've to move closer to a Supervised Learning setting.
* Given a set of labelled data with labels $1$ and $0$ denoting whether an example is an anomaly, we split the data into training, cross validation and test sets. Training set should not contain any anomaly examples. Furthermore, the number of anomalies are very very small compared to normal examples. (for instance 10000 to 50 ratio).
* From the unlabelled extract of the training set, we fit our model $P(x)$. 
* We can then use the cross-validation set to fit $\epsilon$ using F-1 Scoring metric. We can use the test set to get our final F-1 metric.
* This section brings up the question: When do we use a Supervised Learning algorithm or anomaly detection (unsupervised)? There are a couple guidelines. If we've a very very small number of anomalies and a large number of normal examples. Or if there are many different "types" of anomalies and it is hard for any algorithm to learn from anomaly examples to predict future anomalies. Or if future anomalies may look nothing like any of the provided anomalies. In all these cases, use anomaly detection.
* It's a good idea to plot each of your feature as a histogram and verify if it somewhat follows a gaussian distribution. If it doesn't, one can use transformations such as $\log(x)$ and/or $x^\frac{1}{c}$ to make the data attain a close gaussian form.
* It's a good idea to choose such features for an anomaly detection problem which take on very large or very small values for anamolous examples relative to the normal values.  

## Section 4
* Instead of the original model, we can also make use of multivariate gaussian distribution. Our probability model $P(x)$ becomes
$$P(x;\mu,\Sigma)=\frac{1}{(2\pi)^{0.5n}|\Sigma|^{0.5}}exp(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))$$
* Parameter estimation can be done as
$$\mu=\frac{1}{m}\sum_{i=1}^{m}(x^i)$$
$$\Sigma=\frac{1}{m}\sum_{i=1}^{m}((x^i-\mu)(x^i-\mu)^T)$$
* The non diagonal entries of $\Sigma$ represent the correlation between features whereas the main diagonal is just the variance of all the features.
* It can be proven mathematically that the original model we presented in the sections above is actually just a special case of multivariate gaussian distribution where all non diagonal entries of $\Sigma$ are 0.
* A multivariate gaussian model is able to capture the correlation between features automatically whereas in the original model we've to create a new feature to capture the correlation. (for instance $x_{new}=\frac{x_i}{x_j}$). The original model is also very computationally cheaper and works okay even if $m$ is small. For the multivariate model, $m\ge n$ or else $\Sigma$ will be singular. Similarly, the features must not be linearly dependent.

## Section 5
* Let $n_u$ be the number of users, $n_m$ be the number of movies, $r(i, j)$ be a boolean if a user $i$ has rated a movie $j$ and $y^{(i, j)}$ be the rating respectively. For recommender systems, we have an algorithm called the Content Based Recommendation system. Let $x^i$ be an $n\times1$ feature vector for a movie $i$ and $m^j$ be the number of movies rated by a user $j$. Let $\theta^j$ be a parameter vector to predict user rating of a movie for user $j$. Our objective for content based recommendation system is:
$$J(\theta^1,\theta^2,\cdots,\theta^{n_u})=\frac{1}{2}\sum_{j=1}^{n_u}\sum_{i:r(i,j)=1}((\theta^j)^Tx^i-y^{(i,j)})^2+\frac{\lambda}{2}\sum_{j=1}^{n_u}\sum_{k=1}^{n}(\theta_k^j)^2$$
* The gradient descent becomes ($\lambda\theta_k^j=0$ for $k=0$)
$$\theta_k^j=\theta_k^j-\alpha\sum_{i:r(i,j)=1}(((\theta^j)^Tx^i-y^{(i,j)})x_k^i+\lambda\theta_k^j)$$

## Section 6
* It's not always possible to have a proper feature vectors for each movie. Collaborative Filtering is a feature learning algorithm.
* Given an initial set of parameter vectors $\theta^1,\theta^2,\cdots,\theta^{n_u}$, we can use the following objective function to learn $x^1,x^2,\cdots,x^{n_m}$:
$$J(x^1,x^2,\cdots,x^{n_u})=\frac{1}{2}\sum_{i=1}^{n_m}\sum_{j:r(i,j)=1}((\theta^j)^Tx^i-y^{(i,j)})^2+\frac{\lambda}{2}\sum_{i=1}^{n_m}\sum_{k=1}^{n}(x_k^i)^2$$
* We can squash the above two objective functions together as:
$$J(x^1,x^2,\cdots,x^{n_u},\theta^1,\theta^2,\cdots,\theta^{n_u})=\frac{1}{2}\sum_{(i,j):r(i,j)=1}((\theta^j)^Tx^i-y^{(i,j)})^2+\frac{\lambda}{2}\sum_{j=1}^{n_u}\sum_{k=1}^{n}(\theta_k^j)^2+\frac{\lambda}{2}\sum_{i=1}^{n_m}\sum_{k=1}^{n}(x_k^i)^2$$
* Since the algorithm learns the feature itself, there is no need for the former symbolism that $x_0=1$ and $x^i\in R^{n+1}$. We will consider that $x^i\in R^n$ and no $x_0$/$\theta_0$ exist.
* The gradient descent updates become:
$$x_k^j=x_k^j-\alpha\sum_{j:r(i,j)=1}(((\theta^j)^Tx^i-y^{(i,j)})\theta_k^i+\lambda x_k^j)$$
$$\theta_k^j=\theta_k^j-\alpha\sum_{i:r(i,j)=1}(((\theta^j)^Tx^i-y^{(i,j)})x_k^i+\lambda\theta_k^j)$$

## Section 7
* Let $X$ be a $n_m\times n$ matrix where row $j$ is the transpose of the feature vector of movie $j$.
* Let $\Theta$ be a $n_u \times n$ matrix where row $i$ is the transpose of the parameters of user $i$.
* We can predict all the movie ratings by simply $\Theta X^T$. Hencewhy the collaboration filtering algorithm is also known as low rank matrix factorization algorithm ($\Theta X^T$ is a low rank matrix).
* A good strategy is to perform mean normalization on the matrix $Y$ where $Y$ is a $n_m\times n_u$ matrix of ratings. In essence, we need to substract the mean of each row from its individual components. And when a prediction in a certain row is being done, we should add the corresponding mean back. This has the advantage that if any user hasn't rated any movies, then his/her predictions of a movie is going to be the mean rating of that particular movie.
