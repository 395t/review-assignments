---
layout: summary
title: Summary
paper: he2015delving
# Please fill out info below
author: jordi1215
score: 10
---

The paper introduces a new generalization of ReLU, called Parametric Rectified Linear Unit (PReLU), which adaptively learns the parameters of the rectifiers, and improves accuracy at negligible extra computational cost.
![image](https://user-images.githubusercontent.com/17770319/131951183-e94ad855-480d-4ed0-a5c5-c69b66127b05.png)
![image](https://user-images.githubusercontent.com/17770319/131951231-54edfeaa-6c8c-4bc1-bc82-67d64cf4efe5.png)

PReLU introduces a very small number of extra parameters. It can be trained using backpropagation and opptimized simultaneously with other layers.

ReLU expedites convergence of the training procedure and leads to better solutions than conventional sigmoid like units.

The paper also studies the difficulty of training rectified models that are very deep. By explicitly modeling the nonlinearity of rectifiers (ReLU/PReLU), the team derives a theoretically sound initialization method, which helps with convergence of very deep models (e.g., with 30 weight layers) trained directly from scratch. This gives more flexibility to explore more powerful network architectures.

Parametric Rectified Linear Unit (PReLU) surpass human-level performance for the classification task in the 1000-class ImageNet dataset.

## TL;DR
* Parametric Rectified Linear Unit (PReLU) with parameter that learns from backpropagation
* ReLU is better than sigmoid
* surpass human-level performance
