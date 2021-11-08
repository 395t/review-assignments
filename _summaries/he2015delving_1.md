---
layout: summary
title: Summary
paper: he2015delving
# Please fill out info below
author: TongruiLi # Your GitHub id
score: 10 # How did you like this paper 0(dislike) to 10(love)
---

* What is the core idea?

The paper presents two contributions - PReLU, a parametrizied activation fuction that allows for more efficient convergence without the risk of overfitting, and He Initialization, an initialization method that allows training with deep models without risk of stalled gradient.



* How is it realized (technically)?

PReLU is defined as $$f(y_i) = max(0, y_i) + a_i min(0, y_i)$$ - this formulation basically replaces the cosntant weight in leaky ReLU with a trainable parameter. during training, the gradient of $$a_i$$ exists when $$y_i$$ is non positive. This activation function allows for the coefficient in convolution layer to gradually increase, thus enabling the model to retain more early stage information and make the discrimination at later stages.

He initialization method is an improvement over the previous Xavier method. In the derivation, it considered the effect of non linear activation and thus yield promising result when training deep models by preserving the magnitude of variance in forward/backward propagation. 

* How well does the paper perform?

PReLU's experimental result shows a consistant performance improvement over ReLU on ImageNet Classification task on multiple scale of images. This effect can be seen across variety of model structures, with no reported drastic increase in computation time.

He initialization method has a noticable improvement over xavier, the previous state of the art initialization method. Over the reported 22 and 30 layer model, He initialization gurantees a faster convergence over xavier, which converged more slowly in the 22 model case and did not converge at all in the 30 model case. 

With these two method combined, the best reported result over ImageNet2012 is a 4.94% error rate, which defeats the previously reporrted 5.1% human error rate, thus making this paper achieve superhuman result.

* What interesting variants are explored?

As previously explained, the paper focuses on PReLU, which is a variant of Leaky ReLU and by extension from the default ReLU. He initialization is basically a improvement over the previous xavier initialization. 

## TL;DR
* PReLU, a paramaterized ReLU activation function, is able to improve performance without added penalty.
* He initialization, an initialization method that preserves the magnitude of variance with non linear activation units, is able to gurantee a faster convergance when training on deeper models (<30 weighted layers).
* With PReLU and He initialization together, the paper is able to out-achieve human on ImageNet classification tasks.
