---
layout: summary
title: Summary
paper: goodfellow2013maxout
# Please fill out info below
author: Zayne-sprague
score: 8
---

*TODO - how is this different than max-pooling for CNNs?  Adding this would be helpful to the review.
*TODO - add the visuals where marked
*TODO - add equations where marked
*TODO - break up sections a bit neater.


**_Main Idea_**

Taking the element-wise max of an input across multiple weight matrices produces a non-linear activation function
that can learn any convex function and take advantage of dropout layers while improving accuracy and allowing deeper networks.

**_How is it realized_**

Maxout networks use "Maxout Layers".  

Maxout Layers have multiple weight matrices and biases for the same input!  
(tip: Think of convolutional feature maps, in MLPs or linear layers they are just extra weight matrices and biases)

Maxout Layers takes the values from all the weight matrices in its layer, does the element wise multiplication with the
input per weight matrix, and then does an element wise maximum across all the different activations for that input.


TODO* {{A cool visual should go here}}


**_What does this mean_**

Because each input to the layer has a set of weights that are going to be Maxxed over, 
the activation function has "learnable weights".

Due to the max operator, and that the weights are learned, the maxout activations can learn any arbitrary convex function
(RELU, LeakyRELU, etc., they also have a more detailed proof in the paper)

TODO* {{equations should go here}}

**_Why is this important_**

Rectifiers (RELUs, etc.) suffer from dead activations, where they basically set the inputs to 0

This means Rectifiers use only a portion of the full potential of the model

Maxout Layers do not suffer from this as much because the values can be negative and rarely go to zero

Thus maxout layers will utilize more of the model than rectifiers will, which usually improves accuracy and allows for deeper networks

TODO* {{graphs on the activations switching between positive and negatives should go here}}


**_What are the costs_**

The major cost is that you now have many more weights per layer than you would if you used a rectifier.


**_How well does the paper perform?_**

They compare their model on various datasets incuding MNIST, CIFAR-10, CIFAR-100 and SVHN.  

They achieve state-of-the-art results in some cases reducing error by as much as 4%.

However, the biggest performance improvement is best shown by how much of the model is being utilized.  

Other models that use rectifiers suffered from dead neurons which made the gradient suffer and learning stall,
Maxout overcomes these issues.

Because of this, Maxout is able to support deeper models and make better use of the parameters, indicating that 
even better performance may be achievable.


**_Interesting Variants_**

They show how their model fairs with MLPs (linear layers) and CNNs.  

Beyond that, they mostly stick with the mathematical ramifications of why Maxout works, specifically on why it works best
with dropout.





## TL;DR
- Maxout requires a single layer to have multiple (k) weight matrices and takes the maximum values of those k activations as the final output
- Maxout Activations take advantage of Dropout more than any other activation function (at the time of the writing of the paper)
- Maxout Layers help use the entire model whereas rectifiers (or other activations) can "turn off" activations by being set to 0
