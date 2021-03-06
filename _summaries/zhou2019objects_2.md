---
layout: summary
title: Summary
paper: zhou2019objects
# Please fill out info below
author: timchen0618
score: 10
---

TODO: Summarize the paper:
## What is the core idea?
Previous object detection methods identify objects as bounding boxes. However, it is not efficient as it required the model to enumerate all possible bounding boxes; that is, the model need to consider object at all possible location and of all possible sizes. 

This paper detect the center point of each object using keypoint estimation, and then regress to the size of the bounding box.
The same framework also applies to tasks like 3D detection and human pose detection where they regress to other properties such as 3D size and pose.

## How is it realized (technically)?

### Keypoint Estimation
They try to produce a keypoint heatmap $$\hat{Y} \in [0,1]^{\tfrac{W}{R} \times \tfrac{H}{R} \times C} $$, where R is the output stride and C is number of keypoint types. (C=17 human joints in pose detection and C=80 object classes in object detection) Essentially this is like dividing the image into patches of dimension RxR and predict the probability of each patch as a keypoint. $$\hat{Y}_{x,y,c}=1$$ stands for a detected keypoint, and $$\hat{Y}_{x,y,c}=0$$ represents background. 

Ground truth heatmap $$Y \in [0,1]^{\tfrac{W}{R} \times \tfrac{H}{R} \times C} $$ is then constructed using a Gaussian kernel $$Y_{xyc} = exp(-\tfrac{(x-\tilde{p_x})^2+(y-\tilde{p_y})^2}{2{\sigma_p}^2})$$, where each ground truth keypoint $$(\tilde{p_x}, \tilde{p_y})$$ is the center of the Gaussian. Each gaussian kernel has different standard deviation since the object can be of various sizes.

The training objective is penalty-reduced pixel-wise logistic regression with focal loss: (N is the number of keypoints in the image.)

![image](https://user-images.githubusercontent.com/35536646/138367795-b3711374-dcac-4c97-bc52-99abec63d40b.png)


To account for where the center point is in the RxR patch, they predict a offset $$\hat{O} \in R^{\tfrac{W}{R} \times \tfrac{H}{R} \times 2}$$ for each of the center point. All classes share the same offset prediction. 

### Objection Detection
For each center point, the model also regresses to the size of the object . 

![image](https://user-images.githubusercontent.com/35536646/138610393-41ba34c5-ebbd-41f8-b47a-5f4a8a4c332c.png)

So for each location, the model produce C+4 outputs at each location; C for the heat map, 2 for the offset and 2 for the size of the object.

The inference of this method is simple. First, we extract all the peaks (responses whose value is highest among 8 neighbors) and keep the top 100. 
For each keypoint prediction at location $$(x_i, y_i)$$, the coordinates of the 4 corners of bounding box is represented as follows:

![image](https://user-images.githubusercontent.com/35536646/138375399-9f3e033c-845f-4b35-a294-e28c81717177.png)


where $$(\delta \hat{x_i}, \delta \hat{y_i}) = \hat{O}_{\hat{x_i}, \hat{y_i}}$$ is the offset prediction and $$(\hat{w_i}, \hat{h_i}) = \hat{S}_{\hat{x_i}, \hat{y_i}}$$ is the size of the object.




### 3D Detection

For 3D detection, the model additionally predicts the depth, 3D dimension and orientation of the object. Three separate heads are added accrodingly on top of the backbone. The depth d is a scalar, the 3D dimensions are 3 scalars, and the orientation is represented by 8 scalars. The details of how to construct the 3D bounding box from the predictions can be found in Appendix B in the paper. 

### Human Pos Estimation
Here we want to estimate k(=17) human joints location in the image. During inference, the model first identify the keypoint, and then regress to the location of each joint, modeled as offset to the keypoint. To refine the prediction, it also outputs a heatmap for each joint, and use this as a correction to the regressed location. Specifically, the model finds the keypoint which is closest to the regressed joint location on the heatmap and use this as final prediction.

![image](https://user-images.githubusercontent.com/35536646/138610477-69fec021-4695-4c5d-b124-809109b27dd7.png)

## What interesting variants are explored?
They experiment with different backbone CNN structure including ResNet-18, ResNet-101, DLA-34, and Hourglass-104. 


## How well does the paper perform?

The model CenterNet with Hourglass-104 outperforms all other one-stage detectors. It did not beat the two-stage models, but is a lot faster. 

![image](https://user-images.githubusercontent.com/35536646/138371324-529b8d82-4b2f-47c0-83f4-4c52f676df8a.png)

They also report results on 3D bounding box estimation (Table 4) and pose estimation (Table 5). The model performs on par with the baselines but faster on 3D estimation, and it performs slightly worse than state-of-the-art models on pose estimation.

![image](https://user-images.githubusercontent.com/35536646/138610510-1b81dedb-8afc-4f96-8d25-a898e397f3d0.png)

![image](https://user-images.githubusercontent.com/35536646/138610490-6818aab3-8a36-4a62-959b-ce9a4f6c7b5f.png)

## TL;DR
- The paper propose CenterNet, which represents objects using their keypoints and regresses to other values such as size of bounding box, 3D location, orientation, and pose.
- The novel idea of representing objects as points is simple and can be generalized to other application.
- CenterNet is simpler and faster than other object detectors. It also achieves best performance among one-stage detectors.
