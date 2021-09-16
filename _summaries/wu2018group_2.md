---
layout: summary
title: Summary
paper: {{wu2018}}
# Please fill out info below
author: # SShivang
score: # 10/10
---

Core Idea:

The batch norm introduced an optimization in which the outputs of the layers were normalized for a particular batch (scaled and recentered). This lead to significant improvement in performance for a lot of deep learning tasks (one of the most important improvements). However, the technique doesn't work as well for smaller batch sizes and when you want to optimize a single point. This may be the case if it is impossible to have large batch sizes (model such as BERT) and you have to train on a smaller portion. This paper introduces a group norm which works on smaller batches and has consistent improvements of performance across batch sizes.

Technical Realization:

The paper realizes that instance norm (where we normalize features across a singular instance ) is a strong idea. However, instance norm goes to far as it doesn't leverage the channels. Therefore it doesn't get strong statistical signals (use for normalizing) and is likely to over react accross a feature. It leverages the channels and allows for normalization between more channels.

Performance:

The group norm has similar performance to batch norm, however for larger batch sizes it doesn't do as well as batch norm. Regardless it provides an important alternative for smaller architectures.

Variants:

They don't have many variants instead they just test along many different tasks.


## TL;DR
* batch norm introduced an optimization in which the outputs of the layers were normalized for a particular batch
* the technique doesn't work as well for smaller batch sizes
* group norm which works on smaller batches and has consistent improvements of performance across batch sizes
