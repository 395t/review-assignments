---
layout: summary
title: Summary
paper: dai2017deformable
# Please fill out info below
author: nilesh2797
score: 9
---

## What is the core idea?
* Standard CNNs use fixed geometric shape: a convolution unit samples the input feature map at fixed locations; a pooling layer reduces the spatial resolution at a
fixed ratio
* This paper proposes Deformable Convolution Networks (`DCN`) which enables convolution/RoI pooling units to **learn to deform the sampling locations (grid)**
<p align='center'><img src="dai2017deformable_1/deformed-convolution.png" height="200"/></p>

## How is it realized (technically)?
### Deformable Convolution
Composed of two convolution layers:
* Regular convolution layer to generate output features but the n x n sampling grid is augmented with offsets 
* Offsets are obtained by applying a separate convolutional layer over the same input and is learned simultaneously
<p align='center'><img src="dai2017deformable_1/deformable-convolution.png" height="300"/></p>

### Deformable Region of Interest (`RoI`) Pooling
Similar idea as deformable convolution, offsets are now added to the spatial binning positions
* Regular RoI pooling first generates the pooled feature maps, a Fully-connected layer then generates normalized offsets
* Normalized offsets are scaled back to RoI's width and height, this enables offset learning invariant to RoI size
<p align='center'><img src="dai2017deformable_1/deformable-roi.png" height="300"/></p>

## How well does the paper perform?
### Object Detection on COCO Dataset
<p align='center'><img src="dai2017deformable_1/dcn-results.png" width="800"/></p>

### Sample Visualization
<p align='center'><img src="dai2017deformable_1/dcn-vis-conv.png" width="900"/></p>
<p align='center'><img src="dai2017deformable_1/dcn-vis-roi.png" width="900"/></p>

## TL;DR
* Enables convolution units to learn to sample input spatial location
* End to end trainable without additional supervision
* Gets significant improvements over traditional CNNs on object detection task
