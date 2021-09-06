---
layout: summary
title: Summary
paper: glorot2010understanding
author: elampietti
score: 8
---

The core idea of this paper is to challenge the effectiveness of asymmetric activation functions, such as sigmoid, with the traditional, random initialization for deep architecture.
The paper accomplishes this by providing improved results from their normalized initialization process and by using symmetric activation functions such as hyperbolic tangent and softsign. 

The Shapeset-3 x 2 dataset is used in this paper for the test models to predict 9 possible shape classifications.
Feedforward neural networks with a variation of one to five hidden layers each consisting of one thousand hidden nodes and an output layer of softmax logisitic regression was used for the following experiments. 

The paper makes a point that studying the changes in gradients and activation function values between epochs and network layers is informative towards the effectiveness of a model.

With deeper networks, the variance of the gradient will decrease using the standard initialization as you back-propagate through the network and ultimately result in slower learning, therefore they created a normalized initialization to make a more consistent varience in gradient/activation values throughout the network.

Here is the standard initialization that has a multiplicative effect of decreasing back-propagated gradients where 'n' is the number of nodes in the layer:

![standard](https://user-images.githubusercontent.com/7085644/132159731-98d1bf49-90c7-4873-9c02-a2882d287cd3.PNG)

Here is the equation for the normalized initialization to mitigate that multiplicative effect:

![equation](https://user-images.githubusercontent.com/7085644/132159455-d40e6655-e598-4f12-80af-82ac19a9e5f9.PNG)

The improvement resulting from the choice of an activation function is realized through experiements tracking the saturation levels of each layer and trying to minimize over-saturation.

The asymmetric activation function, sigmoid, with random initialization showed the highest saturation towards 0 in the top hidden layer compared to the hyperbolic tangent and softsign activation functions which did not encounter this pattern due to their symmetry around 0.
With unsupervised pre-training as initialization, the sigmoid activation function does not produce this high level of saturation.

The hyperbolic tangent activation did experience a saturation pattern from the bottom to the top of the network which needs to be investigated further to explain according to the paper, however it performed better than sigmoid and benefitted the most from the normalized initialization.

The softsign activation had the lowest saturation rate due to its quadratic polynomial tails which allow values to approach its asymptotes at a slower rate.

The paper provides an overall improvement of 9% in the test error from 59.47% to 50.47% with the normalized initialization on a five layer network with the hyperbolic tangent network.

I like how although the paper states that many of their observations are not currently explained, they provide key avenues to further explore these improvements by saying to focus on the varience of gradients and saturation of activation values throughout deep networks.

## TL;DR
* Random initialization combined with a sigmoid activation function is not effective for deep architecture.
* Symmetric activation functions and a normalized initialization is better suited for deep learning.
* Tracking the gradients/activation values between epochs/layers provides insight into the effectiveness of a model.
