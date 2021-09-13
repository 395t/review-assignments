Mish: A Self Regularized Non-Monotonic Activation Function, Misra; 2019 – Summary

author: Shivi Agarwal
score:

Core idea:  Efficiency of Mish Activation functions over Relu, Leaky Relu.


This paper discusses Mish, a novel self regularized non-monotonic activation function inspired by the self gating property of Swish. Mish is mathematically defined as: f(x) = x tanh (softplus(x)). It is used to overcome the problem of Dying ReLU which leads to gradient information loss due to collapse in negative inputs to zero. For tasks in Computer Vision,  Mish tends to match or improve the performance of neural network architectures. 

Experiment setup
Task: Validate Activation functions on Image classification
Data: The networks were trained for  runs for 50 epochs each
Model: RMSPro as the optimizer
Evaluation metric: training issues and divergence in deeper architects.
Side note: the authors validate that Mish performs better when compared to other validation functions. 


<img src="pics1.png">

First derivation of Mish that is closely related to swish an it helps to optimize the deep neural  networks :
f 0 (x) = sech2 (so ft plus(x))xsigmoid(x) + f(x) x 			(1)
 = ∆(x) swish(x) + f(x) x						 (2) 
where so ft plus(x) = ln(1+e x ) and sigmoid(x) = 1/(1+e −x ).
∆(x) parameter is a pre conditioner. It provides a strong regularization effect and helps make gradients smoother and easier to optimize.
The 1st derivative of Mish is:
f 0 (x) = e xω δ 2
Where, ω = 4(x + 1) + 4e 2x + e 3x + e x (4x + 6) and δ = 2e x + e 2x + 2.
Self-Gating property is where the non-modulated input is multiplied with the output of a non-linear function of the input. Due to the preservation of a small amount of negative information, Mish eliminated by design the preconditions necessary for the Dying ReLU phenomenon.


<img src="pics2.png">

The loss landscape for the ResNet20 equipped with Mish is much smoother and conditioned as compared to that of ReLU and Swish activation function. Mish has a wider minima which improves generalization compared to that of ReLU and Swish, with the former having multiple local minimas. Mish obtained the lowest loss as compared to the networks equipped with ReLU and Swish, and thus, validated the preconditioning effect of Mish on the loss surface.

TL;DR
Mish activation function overcomes the problem of dying Relu.
It gives Smoother output landscapes which help in easier optimization and better generalization.
Mish obtained the lowest loss.



```python

```
