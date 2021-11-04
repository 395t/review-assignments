---
layout: summary
title: Summary
paper: he2019momentum
# Please fill out info below
author: elampietti
score: 9
---

Traditionally, computer vision tasks are more effective with supervised pre-training while tasks in natural language processing (NLP) are successful with unsupervised representation learning.
This is because NLP tasks build tokenized dictionaries in their discrete signal spaces that unsupervised learning can be applied to.
However, computer vision has a continuous, high-dimensional space that makes it more challenging for dictionary building.
This paper focuses on how to build dynamic dictionaries for unsupervised visual representation learning using their Momentum Constrast (MoCo) for training.

The keys in this dynamic dictionary are images or patches and are put into an encoder network allowing dictionary look-up for a matching key.
The goal of this learning would be to minimize contrastive loss when training the visual representation encoder.
This training process is visualized in the below figure.

![train_encoder](https://user-images.githubusercontent.com/7085644/140272389-b0ec71d8-e51e-4dbd-a67f-1ba9607cac21.PNG)

The optimal dynamic dictionary should be large to represent the continuous, high-dimensional visual space and they should also be consistent.
The dictionary has a queue of samples where the current mini-batch encodings are enqueued while the older are dequeued.
Consistency is then maintained with a key encoder that slowly progressed as a momentum-based moving average of the query encoder.

Contrastive learning is used to train the encoder for a dictionary look-up task.
This is done by finding the key that has the smallest contrastive loss with the query, meaning it is the most similar.
This similarity loss function is shown below.

![contrastive_loss](https://user-images.githubusercontent.com/7085644/140273552-d1d51632-da7f-4f34-bdd8-19a91c9e7cc0.PNG)

Momentum Contrast is employed to make sure that the dynamic dictionary being built is large and the encoder of the keys is consistent during its evolution.
This is done by using a queue for the dictionary data samples so that the dictionary size can be larger than the mini-batch size and set as a hyper-parameter.
A momentum update is then employed during back-propagation to solve the issue for updating keys when using a queue for samples.
This means that the encoder will evolve slowly, therefore keeping it consistent.
This momentum update is shown below.

![momentum_update](https://user-images.githubusercontent.com/7085644/140274470-4a219377-7e3d-4043-a2f4-d7faf5b09120.PNG)

Pseudocode of Momentum Constrast is shown below where the pretext tasks has positive sample pairs for a query and key if they are from the same image, and negative sample pairs otherwise.

![moco_pseudocode](https://user-images.githubusercontent.com/7085644/140274698-97e02ac7-d913-4b82-b8b7-13e42019ef72.PNG)

The encoder was built with a ResNet that outputs a fixed 128-D vector for the representation of the query or the key.
The ecoders also have shuffling Batch Normalization to prevent them from cheating the pretext task and benefits training.

Momentum Contrast performance is studied on ImageNet-1M and Instagram-1B with an SGD optimizer.
Three variations of contrastive loss are visualized below along with their results using the linear classification protocol.

![loss_variations](https://user-images.githubusercontent.com/7085644/140275575-0af2d328-263c-4c6d-a10e-97256fee5991.PNG)

![contrastive_loss_variation_results](https://user-images.githubusercontent.com/7085644/140275560-d8fd836c-0938-47e9-8588-a46ae0898c64.PNG)

All three methods show that larger K is beneficial, and therefore a larger dictionary is always better.
Additionally, the results of using a larger momentum value are shown below and reveal that slow evolution is best.

![momentum_results](https://user-images.githubusercontent.com/7085644/140275813-4f6cbc3d-fb3c-45f0-bcdd-3bf162a5041a.PNG)

Comparison with previous unsupervised learning methods are done with accuracy vs. #parameters trade-offs.
MoCo is able to achieve 60.6% accuracy compared to competitors of similar model sizes and also does best with large models as shown below.

![lcp_results](https://user-images.githubusercontent.com/7085644/140276299-f4da7a64-cf85-4740-834b-517a80fa7e23.PNG)

Unsupervised learning should learn features that are transferrable to downstream tasks.
Feature normalization and schedules for fine-tuning MoCo are performed so that MoCo uses the same hyper-parameters and schedule as the supervised ImageNet counterpart.
PASCAL VOC object detection was used to evaluate Moco vs. ImageNet supervised pre-training.
The results below show that MoCo is able to beat the supervised learning counterpart for VOC object detection.

![VOC_results](https://user-images.githubusercontent.com/7085644/140277865-a8416ec7-578b-46ad-9c57-9ab2b86f513a.PNG)

And here are results showing MoCo beating the supervised counterpart with a C4 backbone.

![VOC_results_2](https://user-images.githubusercontent.com/7085644/140277998-3b55cf93-a2f8-442e-96a3-18da9bf20fe0.PNG)

Here are the results for the COCO dataset showing that MoCo is better than the supervised counterpart for both backbones.

![COCO_results](https://user-images.githubusercontent.com/7085644/140278250-957a2f3a-652c-4551-8849-67da4a24acdd.PNG)

Finally, downstream task evaluation reveals that MoCo is competitive with ImageNet supervised pre-training.

![downstream_evaluation](https://user-images.githubusercontent.com/7085644/140278379-59d5c698-4c63-4d7b-84d9-c641b941d64c.PNG)

The better results with MoCo pre-trained on the less curated dataset IG-1B compared to IN-1M shows that MoCo is good for real-world unsupervised learning.

## TL;DR
* Unsupervised visual learning is challenging due to the continuous, high-dimensional space.
* A dynamic dictionary that is large and consistent can be built using Momentum Contrast for unsupervised visual learning.
* A queue of data samples for the dictionary allows for a large dictionary size while a momentum update allows for slow evolution and therefore consistency.
