---
layout: summary
title: Summary
paper: {{paper_tag}}
# Please fill out info below
author: # dalmeraz
score: 7
---

TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored?

## Core Idea
View synthesis is the task of given a set of images of a specific scene, generating a 3d representation of that scene. An innovative model in this task is NeRF, however this model is slow and intensive. This paper presents SNeRG, a model thats two orders of magnitude faster than NeRF. This is done by trading computation for storage through pre-training.

<p align="center"> <img src="hedman2021baking_2_a.png" height="300"/> </p>

## How This is Realized
This is done by precomputing and storing ("baking") a trained NeRF into a Sparse Neural Radiance Grid which is represented as a sparce 3d voxel grid data structure.

During training, the model uses a "deferred" NeRF model which computes environmental features but differs view-dependent features to render time. During testing, a method  of storing the model in a sparse 3D data structue is used which allows for quick speed ups when executing the model. From here diffuse color features volume densities and specular features are passed to generate alpha-composite colors and features. The features are then passed though a neural network along with the viewing direction to generate a specular color which is finally concatenated to the colors to generate an output.

<p align="center"> <img src="hedman2021baking_2_b.png" height="300"/> </p>

Comparing to NeRF, NeRF has a lot of forward passes needed to be done which are just completely avoided in SNeRG.

<p align="center"> <img src="hedman2021baking_2_c.png" height="300"/> </p>

## Results:

<p float="middle">
  <img src="hedman2021baking_2_g.png" width="49%"/>
  <img src="hedman2021baking_2_h.png" width="49%" /> 
</p>

As can be seen on the image above, the quality of the model remains extremely competitive with other models and the table shows us the large improvements gained in terms of speed.

## Interesting variants
Opacity regularization
Time and space for volumetric representation was strongly associated with sparsity of opacity in the model.  To encourage this sparsity, the model uses a regulazier that calculates loss for  predicted densities based on Cauchy loss.

<p align="center"> <img src="hedman2021baking_2_f.png" height="100"/> </p>

## TL;DR
* Storing geometry data in a precomputed data structure leads to high speed improvements
* Real time rendering is enabled though the use of said data strucute
* regularizing NeRF's opacity predictions during  training encourages sparsity which leads to speed and time  improvements.
