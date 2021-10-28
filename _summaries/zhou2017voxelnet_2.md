---
layout: summary
title: Summary
paper: zhou2017voxelnet
author: TL25693
score: # How did you like this paper 0(dislike) to 10(love)
---

TODO: Summarize the paper:
* What is the core idea?

The paper introduced VoxelNet, an end to end deep network that goes from raw 3d point cloud (from lidar) to object detection. It eliminates the need of traditionally hand craft features from the raw representation

* How is it realized (technically)?

**Voxel Partitioning** From a raw 3d point cloud input, VoxelNet first partitions the points to voxels.

**Grouping** Points are grouped according to the voxels. Some voxels may contain significantly more points than others

**Random Sampling** Randomly Sample at most T points for voxels that have more than T points. This have drastic effect on computation speed and decrease imbalance of points

**Stacked Voxel Feature Encoding** A novel way of encoding the points in raw input (per voxel) to feature space. It feeds **points, reflectance, and mean of points** to encode the **surface shape**, as stacked encoder layer aggragrates information from surronding points.

**Sparse Tensor Representation**  Due to majority (90%) of the voxels beeing empty, we can represent the entire voxels as a sparse 4D tesnor of size CxD'xH'xW'

**Region Proposal Network** The algorithm then feed the feature map to the RPN, which is modified from the origional network

**Loss Function** Loss on 3d ground truth box.

* How well does the paper perform?

* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
