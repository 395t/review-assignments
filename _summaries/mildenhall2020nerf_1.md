---
layout: summary
title: Summary
paper: martin-brualla2020nerf
# Please fill out info below
author: mattkelleher
score: # How did you like this paper 0(dislike) to 10(love)
---

## Core Idea
This paper introduces a fully connected deep network that synthesizes 2D views of complex 3D scenes given a location $$(x,y,z)$$ and direction $$(\Theta , \Phi )$$. 
The scene is represented by the network and 

## Technical Implementation

~in progress

## Results

Evaluation Metrics:
- Peak Signal-to-Noise Ratio (PSNR) 
- Structural Similarity Index (SSIM)
- Learned Perceptual Image Patch SImilarity (LPIPS)  


<img src="mildenhall2020nerf_1_results.PNG" width="815" />

<img src="mildenhall2020nerf_1_examples.PNG" width="650" />

## Ablations

Ablation studies were conducted using the Real Synthetic 360. 

<img src="mildenhall2020nerf_1_ablation.PNG" width="660"/>

THe authors explored the affects of each of the three main compentents (positional encoding, view dependencem heirarchical sampling) of the system design as seen in rows 1-4 above. 
As we would expect intuitively a lack view dependence was more determintal to model performance than a lack of positional encoding or a a lack of heirarchical sampling.
They also show (rows 5-6) that with less views of the object (training data) the network is not able to optimize as wel and suffers decreases in performance as expected.
Finally the authors show that the choice of maximum frequence used (rows 7-8) in the postional encoding step is in fact a sweet spot as increasing or decreasing this value hurts performance.
They state that they believe that the benefit of increasing $$L$$ is capped when $$2^L$$ e      

TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
