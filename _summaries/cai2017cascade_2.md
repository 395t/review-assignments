---
layout: summary
title: Summary
paper: cai2017cascade
# Please fill out info below
author: mmcinnestaylor # Your GitHub id
score: 8 # How did you like this paper 0(dislike) to 10(love)
---

## Core Idea  
* In object detection, an intersection over union (IoU) threshold is used to define positives and negatives.  
* Cascade R-CNN uses a sequence of detectors with increasing IoU thresholds, leading to higher selectivity against false positives.  
* The detectors are trained stagewise, since the output distribution of a lower quality detector is sufficient input for a higher quality detector.  
* The cascade procedure helps reduce overfitting during training, and leads to closer matches between the hypothesis and detector quality at each stage during inference  

## Technical Implementation  
* The architecture is framed as a cascaded regression problem:  
	* $$f(x,\textbf{b}) = f_T\circ f_{T-1}\circ...\circ f_1(x,\textbf{b})$$  
		* Here, $$T$$ is the total number of cascade stages.  
	* Each regressor $$f_t$$ is optimized w.r.t. the sample distribution $$\{\textbf{b}^t\}$$ which which arrives at stage $$t$$ instead of the iitial distribution $$\{\textbf{b}^1\}$$  

![2D](cai2017cascade_2_a.png)  

* Each stage $$t\in T$$ includes a classifier $$h_t$$ and regressor $$f_t$$ which are optimized for an IoU threshold $$u^t$$ where $$u^t>u^{t-1}$$  
* The above is achieved by minimizing the following loss:  
	* $$L(x^t, g) = L_{cls}(h_t(x^t),y^t) + \lambda[y^t\geq 1]L_{loc}(f_t(x^t,\textbf{b}^t),\textbf{g})$$  
		* $$\textbf{b}^t = f_{t-1}(x^{t-1},\textbf{b}^{t-1})$$  
		* And where $$g$$ is the ground truth object for $$x^t$$, $$\lambda = 1$$ is the tradeoff coefficient, $$[\cdot]$$ is the indicator function, and $$y^t$$ is the label of $$x^t$$ given $$u^t$$  
## Variants  
* Experiments were performed implementing the architecture while varying the number of cascade stages, which results of which were:  

![Results](cai2017cascade_2_d.png)

## Results  

![Results](cai2017cascade_2_b.png)
![Results](cai2017cascade_2_c.png)

## TL;DR
* Cascade R-CNN uses a series of connected stages with increasing IoU thresholds to achieve state of the art detection performance  
* Experiments demonstrate the detection performance comes as a small increase in computational cost  
* Experiments also demonstrate the architecture to be effective across a number of different backbones
