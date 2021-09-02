---
layout: summary
title: Summary
paper: {{clever2015fast}}
# Please fill out info below
author: joshpapermaster
score: 8/10
---

<!-- TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored? -->

This paper introduces an activation function called the exponential linear unit (ELU), which has faster learning properties than the previous most common activation functions such as ReLU, LReLU, and PReLU.


ELU maintains the nice properties of ReLU by maintaining f(x) = x for x >= 0. 

- This is important to avoid the vanishing gradient property of sigmoid and tanh. 
- The gradient at almost any point in those functions is less than 1. This means at each step the gradient is becoming closer to zero. 
- Since ReLU uses the identity function for positive inputs, the gradient is always 1, which avoids the previously mentioned problem. 


ELU expands on the improvements made by LReLU and PReLU by exponentially including negative inputs. 

- As seen from LReLU and PReLU, it's useful for these functions to include negative inputs to help bring the mean closer to 0. 
- The mean should be closer to 0 to help the speed of the training computation. 
- ReLU has the potential for too many inputs to be negative and drop to zero. By keeping some negative values, more inputs can remain being trained. 
- The improvement over LReLU and PReLU is that ELU allows the gradient to smoothly approach zero as the input becomes more negative. 
- This is important because it maintains a consistent method for reducing noise. 
- The 2 previous functions linearly introduce negative values, while ELU brings them in exponentially. This allows for a deactivation state of inputs similar to ReLU, while maintaining negative values. 


* include better looking math to represent ELU
* include image from paper of differences of activation functions


ELU performs well on the major image recognition sets they tested on. The authors proved ELU had significantly lower activation means and training loss than other activation functions when testing with the MNIST dataset. At the time of their evaluations and publication, ELU held the best test score of CIFAR-100 and second best of CIFAR-10. The CIFAR-100 test error used in their evaluation is 24.28%, which is soundly lower than the previous best of 27.62%.


Their evaluations proved ELU is adaptable to many different image recognition CNN's. ELU on its own scored higher than ReLU, LReLU, PReLU, and SReLU with and without batch normalization.


## TL;DR
- ELU provides an easily implementable improvement to ReLU, LReLU, PReLU, SReLU, etc.
- Uses an exponential function for negative values to slowly reduce gradient to zero 
- ELU increases speed of training and precision of results
