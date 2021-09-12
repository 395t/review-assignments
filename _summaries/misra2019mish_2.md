---
layout: summary
title: Summary
paper: misra2019mish
# Please fill out info below
author: biofizzatreya
score: 7
---

TODO: Summarize the paper:
This paper attempts to fix the vanishing gradient problem of Relu activation functions by using, what they call Mish. 
Relu is a conditionally defined function. It has a fixed value 0 for $$ x<0 $$ and is linear for $$ x>0 $$. Since Relu has a fixed value of 0 for $$ x<0 $$ this results in a problem of vanishing gradients, where negative gradients in one layer do not propagate to the next layer. Moreover, Relu itself is not a smooth function as it is condtionally defined at 0. This creates rugged training landscapes.
An alternative to using Relu is a function called Swish. Swish is defined as $$ x\cdot \text{sigmoid}(\beta\cdot x) $$, where the sigmoid function is defined as $$ \frac{1}{1+e^{-x}} $$. This function makes a smooth-activation function with a shape similar to Relu. This also reduces the vanishing-gradient problem.

Mish is influenced by swish and is defined as $$ x\cdot tanh\left(\text{ln}(1+e^x)\right) $$. The $$ \text{ln}(1+e^x) $$ is also called a softplus function. The authors compare the effect of using different activation functions such as Relu, Swish and Mish. 

![Picture1](https://user-images.githubusercontent.com/13065170/132050780-f3438c1c-a2b6-433d-a3de-2d9279d81cce.png)

Understandably Mish is differentiable and not as rough compared to Relu

![Picture2](https://user-images.githubusercontent.com/13065170/132051192-10e6a969-44fb-42b1-b1b2-ff45573533d1.png)

Mish compares well with other activation functions.

![Picture3](https://user-images.githubusercontent.com/13065170/132051510-42e39ced-5bb2-4589-a94c-fcef71cd8077.png)

Mish seems to work quite well when it comes to overfitting. Compared to other activation functions, Mish does not increase its loss as much as number of layers are increased. Mish also performs more accurately when it comes to training data corrupted by gaussian noise. They have performed other comparisons as well. To distinguish itself from Swish, they show that Swish decreases Top-1 accuracy in larger models, unlike Mish. Mish was also able to seriously reduce the runtime for object detection training, possibly due to its differentiability and lack of conditional statements.

![Picture4](https://user-images.githubusercontent.com/13065170/132052717-1e3aa06d-364c-4d74-b705-a0e057a1e30c.png)




## TL;DR
* A smooth activation function Mish
* Proposed as an alternative to Swish and Relu
* Performs well especially in larger models
