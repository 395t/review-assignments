---
layout: summary
title: Point Transformer
paper: zhao2020point
# Please fill out info below
author: kelseyball
score: 10
---

# What is the core idea?
- Self-attention is fundamentally a set operator (permutation-invariant) and thus a natural fit for modeling 3D point clouds, which are sets of 3D points
- The authors investigate how to apply self-attention/transformers to 3D point cloud processing
- "Point Transformer" networks outperform a variety of models in large- and small-scale 3D image understanding tasks

# How is it realized (technically)?
## Point Transformer Layer
- Point transformer layer uses vector self-attention (rather than scalar dot-product attention) with learnable position encoding function
- Attention is computed per point over its k nearest neighbors
<img width="500px" src="zhao2020point_1h.png"/>
<img width="500px" src="zhao2020point_1i.png"/>

### Position Encoding Function
- Learnable position encoding function
- The difference of two 3D point coordinates (anchor point and neighboring point) is passed into a 2-layer MLP with ReLU
<img width="200px" src="zhao2020point_1a.png"/>

## Point Transformer Block
- Comprised of: linear projections, point transformer layer, and a residual connection
- Input **x** is a set of feature vectors with associated coordinates **p**
<img width="200px" src="zhao2020point_1b.png"/>

## Point Transformer Network
- Point transformer blocks are combined with downsampling and interpolation modules which reduce and increase the cardinality of the point set as needed
<img width="1000px" src="zhao2020point_1c.png"/>

# How well does the paper perform?

## Semantic Segmentation
- Task/Dataset: S3DIS -- 271 rooms, each point has a semantic label (floor, chair, etc.). The task is to label each point.
- Eval metrics: mean classwise accuracy (mAcc), overall pointwise accuracy (OA), and mean classwise Intersection over Union (IoU) (IoU computes the ratio of (1) the intersection of the predicted and true points for a class and (2) their union)
<img width="500px" src="zhao2020point_1d.png"/>

## Shape Classification
- Task/Dataset: ModelNet40; classify 12,311 CAD models into 40 object categories
- Eval metrics: mean classwise accuracy (mAcc) and overall accuracy over all classes (OA)
<img width="500px" src="zhao2020point_1e.png"/>

## Object Part Segmentation
- Task/Dataset: ShapeNetPart; 16k models of 16 shape types, each annotated with 2-6 parts, 50 part types total. Classify each point with a part.
- Eval metrics: IoU averaged over part category (cat. mIoU) and IoU averaged per instance over parts (inst. mIou)
<img width="500px" src="zhao2020point_1f.png"/>

# What interesting variants are explored?
<img width="500px" src="zhao2020point_1g.png"/>

# TL;DR
* Point transformer layers apply vector attention to local KNN neighborhoods of a point in a 3D point cloud; this operation is the basis of Point Transformer networks
* The authors experiment with different values of k, types of attention, and types of position encoding functions
* Point Transformer Networks achieve new SoTA on semantic segmentation, shape classification, and object-part segmentation
