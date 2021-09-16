---
layout: summary
title: Summary for Layer Normalization (Ba et al, 2016)
paper: ba2016layer
author: jaywhang
score: 8
---

## Core Idea

In this paper, the authors propose _Layer Normalization_, an alternative to Batch Normalization (BN) for improving training stability and convergence.
The core idea is to derive the shift and scale parameters for normalization **within the layer itself**, unlike BN which relies on batch statistics.
An important distinction to BN is that all hidden units of a layer share the same normalization terms, but may be normalized differently across training examples.

### What issues does it solve?

Layer Normalization solves three major drawbacks of BN:
1. BN's normalization terms are computed from the minibatch, so it cannot be used when batch size is 1 or small.
2. BN's normalization terms are updated as an running mean/stddev during training, so there is a mismatch between training and test time.
3. When applied to a Recurrent Neural Network (RNN), BN requires keeping track of separate batch statistics for each time step. This is problematic when the sequence length is longer at test time, as there would not be a corresponding statistics to normalize with.

In short, Layer Normalization can be applied regardless of the batch size, has identical behavior at training and test time, and can be seamlessly applied to RNNs.

## Technical Description

For a layer $$a$$ with $$H$$ neurons, Layer Normalization computes the mean and standard deviation across the neurons themselves:

$$
\mu = \frac{1}{H}\sum\limits_{i=1}^{H} a_i, \hspace{3em} \sigma = \sqrt{\frac{1}{H}\sum\limits_{i=1}^{H}(a_i-\mu)^2}
$$

Note that all neurons ($$a_1, \ldots, a_H$$) share the same scalar parameters $$\mu$$ and $$\sigma$$.

## Invariance Properties

Layer normalization makes different trade-offs compared to the two related techniques, namely Batch Normalization and Weight Normalization.
The following table summarizes the trade-offs clearly:
![Table 1: Trade-off comparison to BN and WN.](ba2016layer_2_table1.png)

## Experimental Results

The paper presents six evaluation results showcasing the effectiveness of Layer Normalization, with a focus on RNNs.
We present two particularly interesting results here.
The first is a comparison to different BN variants considered by [Cooijmans et al., 2016].

(TODO: Make the plot little smaller)
![Figure 1: Comparison to Batch Normalization for a LSTM network.](ba2016layer_2_figure2.png)
As shown in the above figure, using Layer Normalization significantly increases the convergence speed of the LSTM-based Attentive Reader model [Vendrov et al., 2016].

Secondly, the authors also consider a feed-forward network by training a permutation-invariant MNIST classification network.

(TODO: Make the plot little smaller)
![Figure 2: Evaluation on the Permutation MNIST task.](ba2016layer_2_figure6.png)

While the plot is a bit noisy, it clearly shows that using Layer Normalization leads to gains in both training loss and test error compared to both the baseline and BN.

<!-- ## Theoretical Results -->

<!-- (Note: still deciding if the summary should discuss Section 5.2: Geometry of parameter space) -->

## References

* [Cooijmans et al., 2016] Tim Cooijmans, Nicolas Ballas, Cesar Laurent, and Aaron Courville. Recurrent batch normalization. _arXiv preprint arXiv:1603.09025_, 2016.
* [Vendrov et al., 2016] Ivan Vendrov, Ryan Kiros, Sanja Fidler, and Raquel Urtasun. Order-embeddings of images and language. _ICLR_, 2016.
* [Gregor et al., 2015] K. Gregor, I. Danihelka, A. Graves, and D. Wierstra. DRAW: a recurrent neural network for image generation. _arXiv:1502.04623_, 2015.

## TL;DR
* Unlike BN, Layer Normalization computes normalization terms within a hidden layer rather than batch statistics.
* Layer Normalization is agnostic to batch size, has identical training/test time behavior, and is directly applicable to RNNs.
* Experimental results show that Layer Normalization improves the performance of the network across several different tasks and architectures.
