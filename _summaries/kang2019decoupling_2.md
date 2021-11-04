---
layout: summary
title: Summary
paper: kang2019decoupling
# Please fill out info below
author: joshpapermaster
score: # How did you like this paper 0(dislike) to 10(love)
---

<!-- TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored? -->
## What is the core idea?
Visual recognition solutions can struggle when there is a long-tailed distribution, which is also known as the class imbalance problem. This paper separates the this problem into two processes: representation learning and classification. 

Representation learning
- trained with different sampling techniques and losses

Classification
- the long tailed classes are recognized by the model from various classifiers  

The paper determined the following findings from using their decoupled process:
- instance based sampling provided really good generalized results
- during representation learning it's beneficial to adjust decision boundaries of classifier 
    - done by sampling or weight normalization
- Can apply to any standard network 

## How is it realized technically?

Experiments were done covering the different decoupled techniques to determine which were most effective

Representation Learning:
- Instance-balanced sampling
    - All examples have same chance of being sampled
- Class-balanced sampling
    - Each class has same chance of being sampled and then example uniformly sampled within the class
- Square-root sampling
    - Middle ground between the two previous sampling techniques. Square-roots the total number of images in each class when calculating the ratio of images in specific class / total images
- Progressively-balanced sampling
    - Uses instance-balanced sampling for some epochs and then switches to class-balanced sampling
- Loss re-weighting
    - Not tested in this paper, but the approaches they did test produced better results

Classification:
- Classifier Re-training (cRT)
    - Use class-balanced sampling and re-initialize and optimize the weights for a few epochs 
- Nearest Class Mean classifier (NCM)
    - First get the mean feature representation for each class, then run nearest neighbors using cosine similarity or Euclidean distance
- τ -normalized classifier (τ -normalized)
    - Normalize the weights with a hyperparameter factor τ
- Learnable weight scaling (LWS)
    - Variant of previous method - keeps the representations and weights fixed and learns scaling factors

## How well does the paper perform?

Experiments done on three datasets
- Places-LT (artificially unbalanced from original)
- ImageNet-LT (artificially unbalanced from original)
- iNaturalist 2018 (natural)


The many, medium, few, all titles below refer to the number of images trained on from the dataset

![decoupling](kang2019decoupling_2a)



## TL;DR
* Three
* Bullets
* To highlight the core concepts
