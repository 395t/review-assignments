---
layout: summary
title: Summary
paper: li2018pointcnn
# Please fill out info below
author: liyanc
score: 6
---


* What is the core idea?

Point cloud representation learning suffers from poor topology-preservation and permutation variances.
In order to take advantage of the current CNN works, the authors propose a learned $\chi$-transformation for both weighting and permuting the features, which is named as $\chi$-Conv.

* How is it realized (technically)?

### $\chi$-Conv operator

  - Project to a local frame
  - Project the local coordinates to a local feature
  - Concatenate local feature with input feature
  - Learn a K x K matrix from local coordiantes, namely $\chi$-transform
  - Apply $\chi$ on concatenated features, therefore, weighting and permuting
  - Finally convolute with kernel K
  
  Implementation details are illustrated in following figures. 
  ![TU3 3_J_7PN0@{S4FW9)6VM](https://user-images.githubusercontent.com/25853995/139913210-9672880e-c457-496f-be73-b3bc4926099e.png)
  ![M _N5L8{8)I1Z@VFS}0QQW1](https://user-images.githubusercontent.com/25853995/139913295-46515021-6bb9-4501-9f16-3f9eab055e16.png)
  ![RU Y89N6GY~FY5( S %D4J6](https://user-images.githubusercontent.com/25853995/139913345-c2f25ec6-a5df-415c-8e91-bc6564634d83.png)

### Permutation invariance and orientation invariance

  Since the neighboring points are projected into a local frame and the reweighting matrix is learned on input, the combined $\chi$-transformation handles the orientation variance by reorienting the patch.
  Additionally, the permutation is explicitly rearanged by the $\chi$-transformation, it's supposed to be permutation invariant as well.
  
### Putting together

  Raw points are grouped by their centers and processed layerwisely.
  If it's a classification task, the network is constructed in a contrastive manner.
  On the other hand, a segmentation network would be constructed in a first constrastive and then expanding manner (hourglass).
  The following figure shows the architecture.
![{CO}6LTKE8Y (6UMDKHM%TS](https://user-images.githubusercontent.com/25853995/139914172-95106584-49c7-43f2-96ab-8b51a1e2258e.png)



* How well does the paper perform?
The authors perform experiments on both classification and segmentation.
The classification task runs on ModelNet40 and ScanNet with the results shown below, which is on par with the SOTA.
![U898AYW9J8RD{(QF614VG_Q](https://user-images.githubusercontent.com/25853995/139914594-33018753-8583-43a1-8db4-7fe7e42841c0.png)

The segmentation task runs on ShapeNet parts, S3DIS, ScanNet, with the results shown below, which is leading the SOTA.
![VA3K2C)B K$SHR%EXYWT165](https://user-images.githubusercontent.com/25853995/139914930-566cf7e7-60fd-48a8-99fe-413245f09891.png)


* What interesting variants are explored?
The authors ablate the $\chi$-transformation and analyze the effects on the feature separation with T-SNE as shown below.
It's clear that the proposed transformation improves the feature separation.
![@ MU5)IPJ( _OZ)N8NMZ~CI](https://user-images.githubusercontent.com/25853995/139915019-99699082-0296-46de-b17d-6581323849b4.png)


## TL;DR
* Group points wrt to centers and project them in to the local frame
* Learn a permuation and reweighting transformation on the local framed points
* Build hierachical models like CNN


