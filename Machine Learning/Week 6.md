# Week 6

## Section 1
* What to do if a machine learning algorithm is not working?
* Get more training data. (high variance)
* Introduce more features. (high bias)
* Reduce features. (high variance)
* Introduce polynomial features by mixing and matching the current features. (high bias)
* Increase lambda. (high variance)
* Decrease lambda. (high bias)

## Section 2
* To evaluate our learned hypothesis, we divide the dataset into a trining set and a test set (usually a 70/30 split). We then train our hypothesis on the training set using $J(\theta)$. Once we're done, we can then calculate the test error either with the same metric used for training or another metric. For example, in logistic regression, we can use the "0/1 Misclassification Error" to denote the test set error.
* Usually, $J(\theta)$ contains add-ons, things like regularization term and modified optimization-sake error (our optimization objective). $J_{train}(\theta)$, $J_{validation}(\theta)$, $J_{test}(\theta)$ refer to the errors calculated without regularization terms and optimization-sake modifications. They're just there to give the simplest numerical error.
* Given many models with different polynomial degrees, we can use a systematic approach to identify the 'best' model. We split our data into a training set, a validation set and a test set (usually a 60/20/20 split). We can train each model by minimizing its cost $J(\theta)$. We can then calculate $J_{validation}(\theta)$ on each of the trained model and pick the model with the least cost. Lastly, to evaluate this model, we can calculate $J_{test}(\theta)$ for it.
* To understand why we do the above procedure, think of it this way: the polynomial degree of each model can itself be considered a parameter. We learn a set of parameters $\theta$ from the training set and learn this 'degree' parameter from the validation set (because we use $J_{validation}(\theta)$ to choose this 'degree').

## Section 3
* In case of a high bias problem, both $J_{train}(\theta)$ and $J_{test}(\theta)$ will be high.
* In case of a high variance problem, your $J_{train}(\theta)$ will be much low but your $J_{test}(\theta)$ will be much high.
* In models with regularization, we have to choose just the right $\lambda$ or the problems above will remain.
* Create a set of reasonale lamdas.
* Create a set of different models as described in Section 2.
* For each lamdba, go through each model to learn some $\theta$.
* Compute cross-validation errors without regularization.
* Select the best combo of the model & the lambda.
* Calculate test set error without regularization.

## Section 4
* We can use learning curves to detect if a learning process is suffering from high bias or high variance.
* Learning curves can be taken as: $J_{train}(\theta)$ & $J_{validation}(\theta)$ plotted against number of examples $m$.
* High Bias, Small Training Set
  * $J_{train}(\theta)$ is low and $J_{validation}(\theta)$ is high.
* High Bias, Large Training Set
  * $J_{train}(\theta)$ & $J_{validation}(\theta)$ are high and approximately equal.
* High Variance, Small Training Set
  * $J_{train}(\theta)$ is low and $J_{validation}(\theta)$ is high.
* High Variance, Large Training Set
  * $J_{train}(\theta)$ increases with training set size and $J_{validation}(\theta)$ continues to decrease without leveling off. Also, $J_{train}(\theta)\le J_{validation}(\theta)$ but the difference between them remains significant.
* If a learning algorithm is suffering from high bias, getting more training data will not (by itself) help much.
* If a learning algorithm is suffering from high variance, getting more training data is likely to help.
* The error value will plateau out after a certain m or training set size for any given model.

## Section 5
* The recommended way to approach a Machine Learning problem is to
  * Have a numerical evaluation metric for your algorithm.
  * Start out with a simple, quick and dirty algorithm.
  * Plot learning curves to decide if more data, more features, etc. are likely to help.
  * Manually examine the errors on examples in the cross validation set and try to spot a trend where most of the errors were made.

## Section 6
* In classification problems, we may encounter the problem of skewed classes.
* To correctly identify such problems, we've to use different evaluation metrics.
* We can use the concept of precision and recall. In case of binary classification:
$$Precision=\frac{TruePositives}{TruePositives+FalsePositives}$$
$$Recall=\frac{TruePositives}{TruePositives+FalseNegatives}$$
* In logistic regression, if drop the value of threshold, we get higher recall and lower precision.
* On the contrary, if we incrase the threshold value, we get higher precision but lower recall.
* If we've multiple algorithms and for each we've precision as well as recall on their cross validation sets, how do we compare them?
* We can use the $F_{1}$ score. ($P$: Precision, $R$: Recall)
$$F_{1}=\frac{2PR}{P+R}$$

## Section 7
* If we've a problem, in which given a set of input features, a human expert can confidently predict $y$, then we can choose an algorithm with a massive number of features and train on it on a huge/mammoth data to get very good results.
* By the human expert being able to confidently predict the output, I mean that the feature vectors capture sufficient information to be confident about the output.
* Since we're choosing a huge amount of data, the algorithm is unlikely to overfit enabling us to use so many features.