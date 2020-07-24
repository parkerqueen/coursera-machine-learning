# Neural Networks (3B1B)

## Section 1
* A Neural Network is just a layered architecture in which each layer consists of a set of neurons.
* For now, think of a neuron as just a box holding a number known as its 'activation'.
* The activation of each neuron of a layer determines the activation of the subsequent layer neurons. This is loosely analogous to the biological neurons, in which the firing of a set of neurons (through their axons) cause other neurons to fire (by receiving signals through their dendrites).

## Section 2
* To solve a problem through DL, the goal might be to choose a good NN architecture (number of layers, neurons in each layer etc.).
* We can then represent the input to our problem as some set of activations applied to the first layer of our NN and the output of our problem as the set of activations being received on the last layer.

## Section 3
* Consider a `28x28` grid of pixels and each pixel has a grayscale value associated with it. We want to find out what digit is present on the grid.
* What we might do is have a layer of $28\times28=784$ neurons and then have some arbitrary hidden layers and an output layer of 10 neurons, each corresponding to one digit. We will also constraint the activation of any single neuron to be within `0` & `1`.
* Given a picture, the activations of the neurons of the first layer will be the grayscale values of the grid. 
* The hope is that the next layer might have neurons associated with all the possible edges when writing a digit and that the activations of the neurons here will be set based on inferences from the previous layer.
* In the same vein, the next layer might have neurons associated with all the possible patterns when writing a digit whose activations will be set based on inferences from the previous layer. This continues until the last layer which will represent one of the 10 possible digits.

## Section 4
* A neuron will have its activation set by taking a weigted sum of the activation values of all the previous layer neurons and adding it to some `bias` value (usually negative). We can then squish the sum into our expected range by using a function such as the `sigmoid` function. The `bias` value controls the meaningfulness of the weighted sum.
* Forget that a neuron is a box which holds a number. It really is just a function that spits out some output (activation) based on an input composed of the activations of all the neurons of the previous layer. This concept then generalizes and we're able to see our whole NN as just one giant mammoth function that takes as input some set of activations and produces another set as the output.

## Section 5
* Let $a^k$ denote a vector comprising of the activations of all neurons of layer $k$.
* Let $W$ be a $m\times n$ matrix where $m$ denotes the number of neurons of layer $k$ and $n$ denotes the number of neurons of layer $k-1$. Each row of $W$ holds weights through which each neuron of layer $k-1$ connect with a particular neuron of layer $k$.  
* Let $b^k$ be a vector comprising of all the biases of the neurons of layer $k$.
$$a^k=sigmoid(Wa^{k-1}+b^k)$$

## Section 6
* The parameters of our NN function are all the weights and biases. We start out by setting them as random values. 
* Imagine now that we pass a labelled training example through our NN and get an output. We can then compare the output to the expected activation of the output neurons and compute a cost. The cost can be computed as a sum of the squared error of all the output neurons.
* Using the technique above, we can calculate an average cost over all of our training data. To represent this idea, think of a function that takes as input a vector of all the weights and biases, uses the input to caculate the cost of each trianing example and finally spits out an average cost (a scalar).

## Section 7
* The intuition behind being able to fine tune our NN function is to minimize the cost function mentioned above. We can then use the input vector of the said weights and biases at that minimum point as parameters of our NN function.
* Quite obviously, gradient descent seems like a good choice for such an optimization problem. (Refer to Machine Learning notes for more information).
* For each iteration of gradient descent when you increase one of the weight parameters, you are compelled to think that probably to our neuron, the activation of the neuron associated with that weight parameter is of greater importance and vice versa.

## Section 8
* In section 3, we discussed our hopes for what each layer might do. But does that happen in reality? No. It just turns out that our network, in the unfathomably large dimensional space, finds itself a happy little corner of some local minimum which plays out well for the training examples.
* The above is apparent in the fact that if you give our trained network some random noise, it might quite confidently predict it as one of the digits. 

## Section 9
* For gradient descent, we have to calculate the negative of the gradient vector at paricular values of the parameters.
* Backpropagation is a way to calculate this negative gradient. 
* Although the cost function is just the average cost over all the training examples, consider just one training example $x^i$ from the set for now.
  * For $x^i$, we can label each output layer neuron with the adjustment and the magnitude of such an adjustment needed to produce the desired result (and thus minimize the cost function).
  * Picking just one neuron from the above, we can do the following things to increase (vice versa to decrease) its activation:
    * Increase its bias.
    * Increase weights of its incoming edges, especially those which come from more active neurons.
    * Change activations of the previous layers proportional to the corresponding weights (+ve & -ve weights).
  * But this is just one neuron. Each neuron of the output layer will have its own desire about the activations of the previous layer as well its weights and its bias.
  * By adding together all the desired effects for the neurons of the previous layer, we get a list of nudges that should happen to its neurons.
  * And now we can recursively apply the same phenomenon for each neuron of the previous layer.
* But this is just one training example from which we can get a 'desired value' about each parameter (weights & biases). We can just average these desired values of each parameter over all the trianing examples.
* For the calculus of Backpropagation, refer to the Machine Learning notes.
