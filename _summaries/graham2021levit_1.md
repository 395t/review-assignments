---
layout: summary
title: Summary
paper: graham2021levitt
# Please fill out info below
author: biofizzatreya
score: 8
---

TODO: Summarize the paper:

The paper attempts to combine, convolutional networks and training principle from CNNs with vision transformers.
![image](https://user-images.githubusercontent.com/13065170/136635751-c21a6e5d-c6ce-4813-bda9-4f3ef884e265.png)
![image](https://user-images.githubusercontent.com/13065170/136635765-4209a6b7-7e90-436c-a96f-2cb958586416.png)

The transformer layers are stacked like a ResNet. The ResNet extracts features from the transformer layers and the gradients are back-propagated. Thus all CNN operations can be applied on the intermediate representations.
![image](https://user-images.githubusercontent.com/13065170/136635772-1c66741e-e1f9-4927-af8c-df03e3d3ad3b.png)
![image](https://user-images.githubusercontent.com/13065170/136635778-6ab9bdbe-7889-4779-b60a-204815006999.png)

LeVit is 1.5 to 5 times faster than competition. 
![image](https://user-images.githubusercontent.com/13065170/136635784-094d7434-e487-40a4-b3fa-a14a7eb44a4e.png)


## TL;DR
* CNN strategies applied to vision transformers
* Convolutional operations applied to transformer stacks
* Results in much faster object detection
