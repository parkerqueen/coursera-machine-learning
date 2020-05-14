# Week 4

## Section 1
* We know that our brain does millions of amazing things and it might seem that to mimic our brain we will need to write tons of different softwares for distinct functionalities. But there is this 'one learning algorithm' hypothesis that states the brain works using just one algorithm. An example of this is that if you use neuro-rewiring to cut the auditory nerve signals to your auditory cortex and instead send visual nerve signals to it, the auditory cortex will eventually learn to see.
* Neural Networks came about with the motivation to mimic the most amazing learning algorithm i.e. the brain. And that this will someday help us to achieve the big AI dream of truly intelligent machines.
* But in the more practical sense, why do I need a NN? We've done Linear & Logistic regression which work very well for linear hypothesis but are not feasible for very complex non linear hypothesis. Many problems have millions of features requiring a very complex hypothesis. It turns out that a NN is perfect for learning such complex hypothesis.

## Section 2
* A NN just a layered architecture in which each layer comprises of a number of neurons. The first layer is the input layer while the last layer is the output layer. 
* Each neuron in a layer usually outputs an activation number by calculating a weighted sum of the activations of all the neurons of the previous layer (including a 'bias unit' neuron whose activation is `1`) and then possibly passing it through some function such as the logistic function. 
* Consequently, the neural network is seen as a giant hypothesis that takes in a set of activations and outputs another set and the weights in the NN become the parameters of our hypothesis.

## Section 3
* $a_j^k$ represents the activation of the $jth$ neuron in the $kth$ layer. $a^k$ represents the vector of activations of the $kth$ layer.
* $\theta^k$ is an $m\times n$ matrix where $m$ denotes the number of neurons in the $(k+1)th$ layer while $n$ denotes the number of neurons in the $kth$ layer. $\theta^k$ denotes the matrix of weights controlling function mapping from $k$ to $k+1$.

## Section 4
* Forward propagation is the procedure of computing activations of each neuron of a layer based on the activations of the neurons of the previous layer and continuing this process till the output layer.
* For forward propagation, one may use the following vectorized formula to calculate the activation vector of a layer.
$$a^k=g(\theta^{k-1}a^{k-1})$$
* $g$ can be a function such as the logistic function.

## Section 5
* 