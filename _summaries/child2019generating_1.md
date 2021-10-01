---
layout: summary
title: Summary
paper: child2019generating
# Please fill out info below
author: ishank-arora
score: 9
---

TODO: Summarize the paper:
* What is the core idea?
  * This paper introduces Spare Transformers. 
  * Sparse transformers are a variation on Transformers
  * Sparse Transformers introduce sparse factorizations of the attention matrix which reduces the time and memory required by transformers from $$O(n^2)$$ to $$O(n\sqrt{n})$$.
  * The paper also introduces
    1. A variation of the Transformer archietecture and initialisation for training Sparse Transformers on even deeper networks
    2. Recomputing attention matrices
    3. Fast attention kernels for training
* Background
  * Let's consider the task of autoregressive sequence generation
    * An autoregressive model predicts future behavour based on past behaviour
  * The joint probability of a sequence $$\mathbf{x} = \{x_1, x_2, x_3, ..., x_n\}$$ can be modeled as the product of conditional probability distributions and parameterized by a network $$\theta$$.
    * $$p(x) = \prod_{i=1}^{n} p(x_i \mid x_1, ..., x_{i-1};\theta)$$
    * The network $$\theta$$ takes in the sequence of tokens and outputs a categorical distrubition using softmax over a vocabulary of size $$v$$.
    * $$\theta$$ is typicall a Transformer in decode-only mode.
      * The self-attention portion computes $$n$$ weightings for each of the $$n$$ elements. 
      * This is intractable as the sequence length grows
* How is it realized (technically)?
  * Factorized Self-Attention
  * Sparse Transformer
* How well does the paper perform?
  * 
* What interesting variants are explored?
  * No variants were explored, except of course, Sparse Transformer as a variant of the Transformer model

## TL;DR
* Three
* Bullets
* To highlight the core concepts
