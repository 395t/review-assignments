---
layout: summary
title: Summary
paper: qi2016pointnet
# Please fill out info below
author: elampietti
score: 9
---

Point clouds were traditionally difficult to process as input because of their irregular format.
They would be transformed to either 3D voxel grids or image collections for easier processing.
The downside to these transformations is that it makes the data voluminous compared to keeping them in point clouds.
This paper uses their unified PointNet architecture to process point cloud inputs and classify them as a whole or by segments.

![applications of pointnet](https://user-images.githubusercontent.com/7085644/139198884-6e2c1d1a-427b-46b2-bfe4-7af92a2344c9.PNG)

Each point is represented by (x,y,z) and are processed independently and identically during the first stage. 
The novel approach in this paper is to use a single symmetric max pooling to select informative points from the point cloud
The network is able to detect objects or segments with this sparse set of points from the point cloud that outline the object. 
This behavior allows the network to handle outliers or missing data from the point cloud well.

For object classification, PointNet outputs a score for each of the possible classes and for semantic segmentation it outputs a score for each semantic subcategory for each point.

The input point sets are unordered, therefore the network must be able to handle permutations of the input as well as transformations such as rotating all the points.
The point sets also make up structures so distance information between them is important.

The architecture visualized in the below figure shows that it consists of a classification network with an extension of a segmentation network.
The max pooling layer aggregates the information of all the points and makes it invariant to permutations of the input.
The network also have a local and global information combination structure and two joint alignment networks.

![pointnet architecture](https://user-images.githubusercontent.com/7085644/139199188-1508e0f1-189a-4784-a2ac-56f8127678b0.PNG)

The following is the symmetric function that is a applied to transformed elements of the point set.

![symmetric function](https://user-images.githubusercontent.com/7085644/139201274-05ec4b3c-2563-4c69-9ddf-878f5c87d7f2.PNG)

'h' is approximated with a multi-layer perceptron network and 'g' is approximated with a single variable function and a max pooling function.
With a set of 'h's, the network can learn 'f's for properties of the point set.

The global point cloud feature vector is fed back into the network with each point feature to capture new per point features that have both local and global information.
This allows for good shape part and scene segmentation.
The joint alignment network predicts an affine transformation matrix to apply to the input coordinates allowing the network to be invariant to geometric transformations of the point cloud.

The following figure show that PointNet is effective at part segmentation for a task with 16 object categories.
The table shows that PointNet achieves state-of-the-art results for part segmentation with the higher average mean intersection over union for all the categories.

![segmentation results](https://user-images.githubusercontent.com/7085644/139202877-248f9ddc-bac8-434b-b3f9-f2abf62bdd7c.PNG)
![segemntation quantitative results](https://user-images.githubusercontent.com/7085644/139203261-4d272a0e-a11a-4bd4-ac89-cc15a76beb62.PNG)

PointNet also achieves state-of-the-art results for point classification and ties the Subvolume model for the highest accuracy of 89.2.

![classification results](https://user-images.githubusercontent.com/7085644/139203060-965a0560-dbe0-4685-a6cf-95e83c93c4c2.PNG)

For classification and segmentation problems in scenes, PointNet beats the baselines in overall accuracy and mean intersection over union (mIoU).

![scene results](https://user-images.githubusercontent.com/7085644/139204127-63d75b62-b86d-485b-9c54-c0cd582abffb.PNG)
![scene results visualized](https://user-images.githubusercontent.com/7085644/139204116-93a1d0d1-e70c-4448-82cc-eda1168c5220.PNG)

The robustness of PointNet was tested by corrupting the input by removing points and adding outliers.
The model is still accurate as seen below.

![robustness](https://user-images.githubusercontent.com/7085644/139204427-bb231886-a58f-439c-ab04-872aa1766f98.PNG)

PointNet is also much faster than other state-of-the-art models such as Subvolume and uses much fewer FLOPs and less space for 3D classification.

![time and space complexity](https://user-images.githubusercontent.com/7085644/139204788-f16ea7a4-e067-4775-a8ac-ebcc6f4f6cf9.PNG)

## TL;DR
* PointNet is a deep network that can process 3D point sets for shape classification, shape part segmentation, and scene semantic parsing. 
* Being able to process unordered point sets allows for faster performance and can transferred to other domains.
* The max pooling layer in the network is key as it allows PointNet to be invariant to unordered point sets as input.
