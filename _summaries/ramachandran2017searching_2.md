---
layout: summary
title: Summary
paper: ramachandran2017searching
# Please fill out info below
author: liaojh1998
score: 6
---

* What is the core idea?

    This paper proposed a reinforcement learning-based search method for finding good activation functions, then analyzed and evaluated the best found function, Swish, which is defined as $$x \cdot \sigma(\beta x)$$. According to evaluations, Swish is found to reliably outperform ReLU and multiple other activation functions in a wide variety of tasks and networks.

* How is it realized (technically)?

    * _Activation Function Search_

        The authors restricted the search space to functions composed from functions that takes in 1 or 2 scalar values and output a scalar. This is done by composing from multiple repetitions of the "core unit":

        <p align="center">
            <img src="https://d3i71xaburhd42.cloudfront.net/c8c4ab59ac29973a00df4e5c8df3773a3c59995a/2-Figure1-1.png" width="30%" height="30%">
        </p>

        Note that the inputs of the unary functions are restricted to the preactivation $$x$$ and the binary function outputs. This way, the activation function can always take a scalar value as input and output a single scalar value, like ReLU.

        The choice of the search algorithm depends on the size of the search space. For small search spaces, the algorithm exhaustively enumerate the entire search space, and maintain a list of top performing activation functions ordered by validation accuracy. For large search spaces, the algorithm use an RNN controller to "predict" components of the activation function:

        <p align="center">
            <img src="https://d3i71xaburhd42.cloudfront.net/c8c4ab59ac29973a00df4e5c8df3773a3c59995a/3-Figure2-1.png" width="30%" height="30%">
        </p>

        The RNN predicts a single component of the activation function at each timestep, and each prediction is fed back as input to "predict" the component of the next timestep in an autoregressive fashion. This network is trained with reinforcement learning (Proximal Policy Optimization, [Schulman et al., 2017](https://arxiv.org/abs/1707.06347)) to output functions that have high validation accuracies by using validation accuracy as the reward. To reduce search time, the search algorithm batched candidate functions and aggregated their validation accuracies to update the search algorithm.

    * _Search Evaluations_
        
        The searches are conducted by training ResNet-20 ([He et al., 2016a](https://ieeexplore.ieee.org/document/7780459)) on the CIFAR-10 ([Krizhevsky & Hinton, 2009](https://www.cs.toronto.edu/~kriz/learning-features-2009-TR.pdf)) by substituting each activation function instead of ReLU. Every network is trained for 10K steps.

        The top performing functions are tested on larger networks, specifically ResNet-164 (RN) ([He et al., 2016b](https://arxiv.org/abs/1603.05027)), Wide ResNet 28-10 (WRN) ([Zagoruyko & Komodakis, 2016](http://www.bmva.org/bmvc/2016/papers/paper087/index.html)), and DenseNet 100-12 (DN) ([Huang et al., 2017](https://arxiv.org/abs/1608.06993)), again by replacing ReLU. The authors used the same hyperparameters described in each model.

        The authors found the Swish activation to outperform all other activation functions, so they extensively tested Swish (with both trainable $$\beta$$ and $$\beta = 1$$) and several other famous activation functions (especially variants of ELU and Softplus) on challenging real world datasets. For the image classification task, CIFAR-10, CIFAR-100 ([Krizhevsky & Hinton, 2009](https://www.cs.toronto.edu/~kriz/learning-features-2009-TR.pdf)), and ImageNet 2012 classification set ([Russakovsky et al., 2015](https://arxiv.org/abs/1409.0575)) were used. For the machine translation task, the standard WMT 2014 English→German dataset was used.

* How well does the paper perform?

    For the top activation function search, $$x \cdot \sigma(\beta x)$$ (Swish) and $$\max(x, \sigma(x))$$ were found to consistently match or outperform ReLU in the RN, WRN, and DN network on the CIFAR-10 set. Swish consistently achieved about 0.2% better than ReLU.

    The following figure summarizes Swish's performance against other activation functions in different models:

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/c8c4ab59ac29973a00df4e5c8df3773a3c59995a/6-Table3-1.png" width="40%" height="40%">
    </p>

    In general, Swish matches or outperforms other activation functions most of the time by about 0.1%-2% in accuracy in CIFAR-100, by about 0.1-1% in top-5 accuracy in ImageNet, and by about 0.1-4.3 in BLEU score in the WMT datasets.

* What interesting variants are explored?

    The authors found that complicated activation functions consistently underperform simpler activation functions during search. The best activation functions are usually the one that use the preactivation $$x$$ as input to the final binary function: $$b(x, g(x))$$.

    TODO: add comment on Swish analysis for allowing small gradients propagation.

    From a glance, Softplus generally matched Swish in performance for image classification tasks and PReLU and LReLU generally matched Swish in performance for translation tasks.

## TL;DR
* Swish ($$x\cdot \sigma(\beta x))$$) can replace ReLU as activation functions in networks for slightly better performance.
* Activation function search by using reinforcement learning to maximize validation accuracy.
* Functions that perform well in smaller networks will generally perform well in larger networks as well. 
