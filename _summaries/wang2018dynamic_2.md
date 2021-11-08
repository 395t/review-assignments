---
layout: summary
title: Summary
paper: wang2018Ddynamics
# Please fill out info below
author: specfazhou
score: 8
---

TODO: Summarize the paper:
* What is the core idea? <br/>
In this paper, the authors come up with a new neural network module called EdgeConv that can use local geometric information of point clouds, which is permutational invariant and partially translational invariant. By dynamically updating a graph of relationships, EdgeConv is able to perform semantic segmentation task. EdgeConv can also easily be integrated into other point cloud processing pipelines. The following picture shows the entire model architecture for classification and segmentation,<br/>
<img src = 'wang2018dynamic_2_model_arch.png'>


* How is it realized (technically)? <br/>
<img src = 'wang2018dynamic_2_Edgeconv.png'>
EdgeConv module is essentially one MLP together with two operations called edge feature and aggregation operation. The edge feature $$h_\Theta(x_i,x_j)$$ is a non-linear function with learnable parameters, and the aggregation operation can either be $$\Sigma$$ or $$max$$. There are five different choices of edge features and aggregation operations that have important different influences. These five different choices are shown as follows:<br/>
<img src = 'wang2018dynamic_2_first_choice.png'> The first choice is standard convolution <br/>
<img src = 'wang2018dynamic_2_second_choice.png'> The second choice only has global information, and is used in PointNet <br/>
<img src = 'wang2018dynamic_2_third_choice.png'> $$g$$ is Gaussian kernel and $$u$$ is distance between two points in Euclidean space <br/>
<img src = 'wang2018dynamic_2_forth_choice.png'> This method only provides local information <br/>
<img src = 'wang2018dynamic_2_fifth_choice.png'> This is the best that has both local and global information


* How well does the paper perform? <br/>
EdgeConv has achieved great results in classification, part segmentation, and semantic segmentation. For classification, the authors evaluate their model on the ModelNet40, which not only achieved the state-of-the-art result, but also cost much shorter time to train. For segmentation, their model archieved competitive results to other point cloud processing methods. The following three pictures show how their model performs:
<img src = 'wang2018dynamic_2_dyn_result1.png'>
<img src = 'wang2018dynamic_2_dyn_result2.png'>
<img src = 'wang2018dynamic_2_dyn_result3.png'>




* What interesting variants are explored?<br/>
One very interesting point is that you can regard PointNet, PointNet++, MoNet, and PCNN as special cases with special choices of edge features and aggregation operations. 

## TL;DR
* The EdgeConv module gives both global and local information of point clouds
* EdgeConv can be easily used to other different point clouds processing methods
* using dynamic graph of relationships
