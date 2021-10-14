---
layout: summary
title: Summary
paper: niemeyer2020giraffe_1
# Please fill out info below
author: chengchunhsu
score: 9/10
---

## What is the core idea?

* <u>Problem:</u> content creation needs to be controllable
* <u>Solution:</u> disentangle the scene by multiple "feature fields"

![1](niemeyer2020giraffe_1_1.png)

## How is it realized (technically)?



![1](niemeyer2020giraffe_1_5.png)









<u>Object as Neural Feature Fields</u>

Represent each object using a separate feature filed in combination with an affine transformation.

![2](niemeyer2020giraffe_1_2.png)

* s: scale parameter
* t: translation parameter
* R: rotation matrix



Transform points from object to scene space by

![1](niemeyer2020giraffe_1_3.png)

Volume rendering

![1](niemeyer2020giraffe_1_4.png)



<u>Scene composition</u>

Summation of all feature fields

![12](niemeyer2020giraffe_1_12.png)



<u>Neural Rendering</u>

![1](niemeyer2020giraffe_1_6.png)

![1](niemeyer2020giraffe_1_7.png)





<u>Objectives</u>

![1](niemeyer2020giraffe_1_8.png)



## How well does the paper perform?

<u>**Disentangled Scene Generation**</u>

- Which degree our model learns to generate disentangled scene representations?
- Are objects disentangled from the background?

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

