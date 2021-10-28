---
layout: summary
title: Summary
paper: niemeyer2020giraffe
# Please fill out info below
author: chengchunhsu
score: 9
---

## What is the core idea?

* <u>Problem:</u> content creation needs to be controllable
* <u>Solution:</u> 
  * interpret the scene in the 3D domain rather than 2D
  * disentangle the scene by multiple "feature fields" (i.e., h_1 ~ h_N)

![1](niemeyer2020giraffe_1_1.png)

## How is it realized (technically)?



![1](niemeyer2020giraffe_1_5.png)



<u>Object as Neural Feature Fields</u>

How to represent multiple objects?

- Using a separate feature filed in combination with an affine transformation for each object.
- Transform points from object to scene space by:
  - ![1](niemeyer2020giraffe_1_3.png)
  - **s**: scale parameter
  - **t**: translation parameter
  - **R**: rotation matrix
  - **x**: 3D points



Volume rendering

- The **generative neural feature field (h_θ)** maps (x, d, z_s, z_a) to volume density and scene features which are used to construct the scene
  - ![1](niemeyer2020giraffe_1_4.png)
  - **σ**: volume density
  - **f**: features (for scene generation)
  - **x**: 3D points
  - **d**: view direction
  - **z_s**: shape code
  - **z_a**: appearance code



<u>Scene composition</u>

Summation of all feature fields

![12](niemeyer2020giraffe_1_12.png)

- **σ**: volume density
- **f**: features (for scene generation)

<u>Training</u>

- Generator objectives: 
  - ![1](niemeyer2020giraffe_1_8.png)
  - **N**: number of entities (i.e., objects and background)
  - **N_s**: number of sample points along each ray
  - **d_k**: ray for *k*-th pixel
  - **x_jk**: the *j*-th sample point for the k-th pixel / ray
- Discriminator objectives: binary cross entropy



## How well does the paper perform?

<u>**Disentangled Scene Generation**</u>

- Which degree our model learns to generate disentangled scene representations?
  - "disentangled scene": are objects disentangled from the background?

![1](niemeyer2020giraffe_1_9.png)



<u>**Controllable Scene Generation**</u>

- How well the scene can be controlled?

![1](niemeyer2020giraffe_1_10.png)



**<u>Generalization Beyond Training Data</u>**

- Do the compositional scene representations allow us to generalize outside the training distribution?

![1](niemeyer2020giraffe_1_11.png)





<u>**Comparison to baselines**</u>

![1](niemeyer2020giraffe_1_13.png)



## TL;DR
* Compositional 3D scene representation leads to more controllable image synthesis
* The neural rendering pipeline brings us faster inference and more realistic images
* The proposed method allows for controllable image synthesis for single-/multi-object scenes given training on raw unstructured image collections

