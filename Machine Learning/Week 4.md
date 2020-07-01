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
* For notation, assume that $L$ denotes the total number of layers in our network and $s_l$ denotes the number of neurons in $lth$ layer (not counting the bias unit). Also note that $s_L=K$.
* $z_j^l$ represents the value which when input into the activation function will generate the activation of the $jth$ neuron in the $lth$ layer. Hence, it does not contain any value for the bias unit's activation.
* $a_j^l$ represents the activation of the $jth$ neuron in the $lth$ layer including the bias unit. $a^l$ represents the vector of activations of the $lth$ layer.
* $\theta^l$ is an $m\times n$ matrix where $m$ denotes the number of neurons in the $(l+1)th$ layer while $n$ denotes the number of neurons in the $lth$ layer. $\theta^l$ denotes the matrix of weights controlling function mapping from $l$ to $l+1$.

## Section 4
* Forward propagation is the procedure of computing activations of each neuron of a layer based on the activations of the neurons of the previous layer and continuing this process till the output layer.
* For forward propagation, one may use the following vectorized formula to calculate the activation vector of a layer.
$$a^l=g(\theta^{l-1}a^{l-1})$$
* $g$ can be a function such as the logistic function.
