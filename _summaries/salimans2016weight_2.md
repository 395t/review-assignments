---
layout: summary
title: Summary
paper: {{salimans2016weight}}
# Please fill out info below
author: samatharhay
score: 9
---

The paper introduces weight normalization, a reparameterization of the weight vectors of a neural network, to speed up convergence of stocastic gradient descent.

In standard neural networks the weighted sum computed by each neuron is as follows:
**intsert equation 1**
where w (weights) and x (input) are both k-dimensional vectors and b is a scalar bias term.

In weight normalization each w vector is reparameterized in terms of a parameter vector v, of dimensionality k, and a scalar parameter g: 
**insert equation 2**

Since the mean of the neuron activations are still dependent on v a varient of batch normalization, called mean-only batch normalization, was introduced.

Similarly to to full batch normalization, the minibatch means are subtracted out, but the minibatch standard deviations are not divided by when computing neuron activations.  The activations are computed as follows:
**insert equation 7**

The gradient of the loss with respect to preactivation t is:
**insert equation 8**

The prove the usefulness of their model the authors conducted experiments using 4 different models.

 Supervied Classification: CIFAR-10
* Model based off of the ConvPool-CNN-C architecture, with the modifications of replacing the first drop out layer with a layer that adds Gaussian noise, expanding the last hidden layer from 10 to 192 units and using a 2X2 max-pooling layer instead of a 3X3.
* Batch nomalization preformed 16% slower than the baseline, while weight normalization was not noticable slower
* Mean-only batch normalization with weight normalization preformed the best (7.31% error)

**insert Figure 1 and 2**

Generative Modelling: Convolutional VAE: 
* Similar to the CVAE architecture, with the modification of encoder and decoder blocks were parameterized with ResNet blocks and teh diagonal posterior is replaced with auto-regressive variational inference.
* Weight normalization had lower variance and converges to a better optimum

**insert Figure 3**

Generative Modelling: Draw
* use DRAW model
* Unclear how batch normalization would be applied to the model due to the LSTMs, WN is trivially applied to the weight vectors of each LSTM unit
* WN presents a signification speed up on convergence.

**insert Figure 4**

Reinforcment Learning: DQN
* Deep Q-Network
* Not suited for BN, WN was easily applied.
* WN was able to improve preformace.

**insert Figure 5**


The authors were able to show that weight normalization can help improve convergance speed in several different models, as well as several were batch normalization was not implimentable. 

They also clearly explained how to implement WN and proposed a varient of batch normalization to go along with it.

## TL;DR
* Weight normalization was proposed to increase convergence rate when using SGD
* Models, such as LSTMs, where batch normalization is not easily applied benifit from WN
*  mean-only batch normalization was proposed
