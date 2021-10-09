---
layout: summary
title: Summary
paper: jaegle2021perceiver
# Please fill out info below
author: jordi1215
score: 9
---
### Introduction
Perceiver is a transformer architecture that can process data including images, point clouds, audio, video, and their combinations but its limited to simple tasks such as classification.
### Problem
1. Biological systems perceive the world by various inputs such as vision, audition, touch, etc. The perception models used in deep learning on the other hand are designed for individual modalities, often relying on domain specific assumptions such as the local grid structures exploited by virtually all existing vision models. These priors introduce helpful inductive biases, but also lock models to individual modalities.
2. Most transformer models have been mostly effective in scenarios with inputs of maximum a few thousand elements. Data types such as images, videos or books can contain millions of elements which makes the use of transformers a bit challenging.

### Solution
To address this, Perceiver builds upon Transformers and hence relies on a general attention layer that does not make any domain-specific assumptions about the input. Specifically, the Perceiver attention model first encodes the input into smaller latent arrays which processing cost is independent of the size of the input. This allow the Perceiver model to scale gracefully with the inputs.

### Implementation

![](jaegle2021perceiver_1a.png)



## TL;DR
* Perceiver is one of the first large scale architectures able to process different input types.
* Perceiver can scale well by attending to the inputs iteratively and channel its limited capacity to the most relevant inputs
* The paper demonstrate competitive performance in image classification comparing to ResNet-50, AudioSet sound event classification benchmark(audio and video), and cloud classification comparing to ModelNet-40.
