---
layout: summary
title: Summary
paper: lang2018pointpillars
# Please fill out info below
author: joshpapermaster
score: 7
---

<!-- TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored? -->

## What is the core idea?

Previous solutions for 3D object detection were too slow. PointPillars is a solution for 3D object detection that uses only 2D convolution layers in the end to end learning process. It does this by using "pillars", which is basically looking at the 3D object from a bird's eye view and interpreting each space of the 2D bird's eye view as a vertical column (providing 3D depth). PointPillars then predicts 3D boxes for the objects.

There are several benefits to PointPillars over other common approaches
- Uses full information provided by point cloud by learning features 
- Using pillars instead of voxels saves time since voxels have to be vertically tuned
- All important layers are done in 2D which is more efficient
- Can easily use multiple lidar scans or radar point clouds 

## How is it realized technically?

There are three stages

![pointpillars](lang2018pointpillars_1b.png)

1. Encoder that takes the point cloud and maps it to a sparse pseudo-image
- point cloud input is x,y,z,r where r is reflectance
- point cloud is turned into a grid
- The points within each pillar are then additionally described by their distance to the pillar arithmetic mean and offset to the x,y center
- Sparse nature of pillar taken advantage of to create dense tensor representation
    - Random sampling if too many points
    - Zero padding if not enough
- Apply simple version of PointNet
- Following encoding, pesudo-image created from features being brought back to original locations

2. 2D convolutional backbone network that takes in the pseudo-image and learns a high-level representation
- Similar backbone to VoxelNet
- There's two networks:
    - Creates features from smaller spatial resolution images (harder to tell when objects are close)
    - Concatenates and upsamples features from previous network

3. Detection head predicts 3D boxes
- Single Shot Detector
- Uses 2D Intersection over Union (IoU)
- Box height was an additional regression target

Loss was the same as used in SECOND
- Combination of localization loss, object classification loss, and discretized direction loss

## How well does the paper perform?
- Uses KITTI object detection benchmark dataset
    - Only trains on lidar point clouds

<!-- image 1 bird's eye view mean average precision -->
Bird's eye view results:

![pointpillars](lang2018pointpillars_1a.png)

<!-- image 2 3d detection results -->
3D detection results:

![pointpillars](lang2018pointpillars_1d.png)

Object orientation results:
<!-- image 3 orientationr results -->
![pointpillars](lang2018pointpillars_1e.png)

Ablation results: 

![pointpillars](lang2018pointpillars_1f.png)

![pointpillars](lang2018pointpillars_1g.png)

## What interesting variants are explored?

Not any significant variants.

- Minimal box augmentation was found to be better, which differed from SECOND and VoxelNet
- Additional point features than VoxelNet allowed for better performance

## TL;DR
- PointPillars provides a faster and better solution to both the 3D object detection and bird's eye view detection problems when using lidar point clouds
- PointPillar encoder learns point clouds in vertical columns, which allows for 2D convolutional layers and faster computation
- Encoded image is mapped back to point cloud location and Single Shot Detector used to compute 3D box
