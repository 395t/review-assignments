layout: summary
title: Summary
paper: wang2018pseudo-lidar_2
# Please fill out info below
author: biofizzatreya
score: 9/10
---

TODO: Summarize the paper:
The paper proposes a method to convert convolutional network based object detection in stereo to LIDAR type point cloud representations. They do this because objects far away are smaller and traditional conv-nets fail to detect them properly.
* How is it realized (technically)?
The algorithm first uses a pair of stereoscopic images to first construct a depth map of the image using the following equation. 
![image](https://user-images.githubusercontent.com/13065170/140244235-deb7c6c4-b7f1-43ae-ade7-31c667e7eb90.png)
![image](https://user-images.githubusercontent.com/13065170/140244266-53549376-c12b-4643-ad35-f17361870c16.png)

Then, this depth map is used to calculate the x,y and z coordinates and converted into a point cloud representation.
![image](https://user-images.githubusercontent.com/13065170/140244306-91a4b66d-8c55-40ad-b555-57224f381083.png)

The point-cloud is called a pseudo-LIDAR signal. The pseudo-LIDAR representation along with the monocular images are fed into 3d-object detection pipelines.

* How well does the paper perform?
* ![image](https://user-images.githubusercontent.com/13065170/140244340-7297b915-caeb-46ec-b00a-a5a94cba2647.png)

 The paper does not develop any neural network architecture, instead it applies existing 3d object detection architectures on the pseudo-LIDAR point-cloud data.
 They evaluate their approach on the KITTI dataset. The pseudo-LIDAR is also back projected to LIDAR data to compare the accuracy.
 ![image](https://user-images.githubusercontent.com/13065170/140244380-ba0fceb1-f436-4cf1-b75a-4e2f1fc234ed.png)
![image](https://user-images.githubusercontent.com/13065170/140244405-548c722e-13cd-4d17-906f-ac0d21318da3.png)
![image](https://user-images.githubusercontent.com/13065170/140244436-02618178-75d6-42e8-a671-0e0b58665fc3.png)


* What interesting variants are explored?
The paper also attempts to detect pedestrians and cyclists which is a much harder task given the small size of the images of pedestrians and cyclists compared to cars. In this case pseduo-LIDAR has an accuracy of 0.5 compared to 0.7 in cars.
![image](https://user-images.githubusercontent.com/13065170/140244463-302b0e02-c002-43fc-a48f-3a62882a6046.png)



## TL;DR
* A method to convert images to LIDAR like point clouds
* Pseudo-LIDAR brings 3d object detection to the level of LIDAR data
* Combined with monocular images, makes 3d object detections less expensive
