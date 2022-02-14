# Using Neural nets to recognize handwritten digits


## Perceptrons

### - What is a neural network?
- A type of artificial neuron called a perceptron.


### - How do perceptrons work?
  - A perceptron takes several binary inputs, x1, x2, ..., and produce 
a **single** binary output.
  - Introduce weights, w1, w2, ..., real numbers expressing the importance 
of the respective inputs to the output.
  - The neuron's output, **0 or 1**, is determined by whether the weighted sum ∑jwjxj 
is less than or greater than some threshold value.![img.png](chapter1img/img.png)
  - In this network, first layer of perceptrons is making three simple decisions, by weighing the input evidence.
Each of the perceptrons from second layer is making a decision by weighing up the results  from the first layer. In this way
the second layer can make a complex and abstract decision. More complex decisions can be made by the third layer.
  - Two changes for simplify the description:
    - write ∑jwjxj as a dot product: **w⋅x**, where w and x are *vectors* 
    - move threshold to the other side of the inequality and replace it by *bias*: **b**
    - ![img.png](chapter1img/img2.png)
    - Bias is like a measure of how easy it is to get the perceptron to output a 1


## Sigmoid neurons

### - How can we devise algorithms for a neural network?
- **Suppose we have a network of perceptrons that we'd like to use to learn to solve some problem**
- The inputs to the network might be the raw pixel data from a scanned, handwritten image of a digit
- We'd like the network to learn **weights and biases** so that the output from the network correctly classifies the digit
![img.png](chapter1img/img3.png)
- Problem: A small change in the weights or bias of any single perceptron in the network can sometimes 
cause the output of that perceptron to **completely flip**, say from 0 to 1. And the flip may then cause the behaviour of **the rest of the 
network to completely change** is some very complicated way.

### - Then we have sigmoid neurons
- Similar to perceptrons, but modified so that *small changes in weights and bias cause only a small change* in their output
- Output is not 1 or 0, but σ(w⋅x+b) , where σ is called the sigmoid function* and is defined by:
![img_1.png](chapter1img/img_1.png)
- To be more explicitly, the output is![img.png](chapter1img/img5.png)
- Suppose **z ≡ w⋅x+b**  is a large positive number. Then e−z≈0  and so σ(z)≈1.
- Shape of the sigmoid function:![img.png](chapter1img/img7.png)
- The smoothness of σ means that small changes Δwj in the weights and Δb in the bias will produce a small change Δoutput in the output from the neuron. In fact, calculus tells us that Δoutput is well approximated by
![img.png](chapter1img/img8.png) where the sum is over all the weights, wj, and ∂output/∂wj and ∂output/∂b denote *partial derivatives* of the output with respect to wj and b, respectively.


## The architechture of neural networks

### - Explain some terminology that lets us name different parts of a network
- ![img.png](chapter1img/img9.png)
The "hidden" layer just means that its neither input layer nor output layer
- To recognize digit, assume the image is a 64 by 64 greyscale image, then there are 4096 input neurons with the intensities scaled appropriatedly between 0 and 1
- The output layer contain a single neuron, with output values of less than 0.5 indicating "input image is not a 9" and ...
- Such networks are called **feedforward neural networks**, which means there are no loops in the network - information is always fed forward and never fed back
- For models which feedback loops are possible are called **recurrent neural networks**. 


## A simple network to classify handwritten digits

- To recognize individual digits we will use a three-layer neural network:![img.png](chapter1img/img10.png)
- Out training images are 28 x 28 pixel images and so the input layer contains 784 neurons. 
- The second layer of the network is a hidden layer. The number of neurons in this hidden layer is n, and we'll experiment with different values for n
- The output layer contains 10 neurons. The neuron has the highest activation value will indicate what number the digit is.
- As 4 neurons are enough to encode the answer, why we use 10:
  - the network with 10 output neurons learns to recognize digits better than the network with 4 output neurons.