---
layout: summary
title: Summary
paper: rogers2020a
# Please fill out info below
author: timchen0618
score: 8
---
## Core Idea
It is basically a survey paper that try to identify how BERT works and what it captures to do the end tasks. They also investigate the training process of BERT and the overparameterization problem. 

## Knowledge That BERT Have
### Syntactic Knowledge
- BERT representations are hierarchical. (Somewhat similar to the tree structure in syntactic parsing.)
- BERT is found to have some kind of syntactic knowledge, but it is not similar to the syntactic rules people defined. 
- Syntactic structures are not encoded in attention heads but in token embeddings.
- It seems like BERT can do well on inputs without good syntactic formatting, since it might not need the information to solve end tasks.

### Semantic Knowledge
- BERT has some knowledge of semantic roles. When predicting a masked token, it prefers words that has proper semantic roles.
- BERT cannot do well with math and numbers.
- BERT did not capture much entity information during pretraining.

### World Knowledge
- There is some world knowledge in the model, which yield comparable results to methods using knowledge base in some tasks.
- But it cannot reason with these knowledge.
(e.g. 1. people can walk into houses & 2. houses are big -> cannot infer houses are bigger than people)


## Localized Linguistic Knowledge 
### BERT Embeddings
- The embeddings are contextualized
- These embeddings form clusters and can be used for word sense disambiguation
- Distill contextual word embeddings into static ones leads to better performance in word-level tasks
- BERT embeddings form more of a "cone" shape in vector space, which is less favored for static word embeddings

### Attention Heads

### Layers
- While lower layers have information about word order, higher layers obtain a more hierarchical sentence representation
- Syntactic information is best captured by the middle layers
- The final layers are more task-specific, and the middle layers are more transferable
- Some said that lower layers contain low-level syntactic information and higher layers encode high-level semantic information, much like a standard NLP pipeline; however, others suggest middle layers excel at both.

## Training BERT
### Model Architecture Choices
- Number of layers matters more than number of attention heads
- Attention heads often encode similar information; can tailor self-attention heads for specific needs to improve performance

### Improvements to Training 
- Use larger batches
- Train lower layers first and then retrain the whole model - faster training time

### Pretraining
Pretraining is beneficial to most tasks, but the exact reason is to be investigated. 

**Some improvements to data can be made:**

Larger pretraining datasets, longer training, including linguistic information in the data, and considering structured knowledge such as knowledge base or entites when training.


They also mentioned various alternative training schemes. Some change the masking, others tried to modify the text in ways other than masking, still others incorporate other tasks (e.g. latent knowledge retrieval).


### Improvements on Fine-tuning
- Considering more than just the output layer
- A separate supervised training phase in between pretraining and fine-tuning
- Other methods: Adversarial token perturbations, adversarial regularization, amd mixout regularization

## Overparameterization Problem

### Some proof of this:
- Could prune most of the attention heads without great performance loss
- Some observe positive effect from disabling attention heads
- In some task, more layers cause performance drops

### Solution: Compression Techniques
- knowledge distillation (e.g. DistillBERT), basically let a student network to learn from the activations of teacher (BERT)
- Quantization
- Pruning

## Suggestion on Future Work
- Create dataset that require more language skills to solve 
- Create a benchmark for comprehensive linguistic knowledge
- Should focus on how to reason over the information contained in BERT
- Learn what BERT actually do during test time instead of probing

## TL;DR
- BERT has learned a great amount of syntactic, semantic and even world knowledge, but the key to perform well is how to extract and reason with these information. 
- Different layers and attention heads of BERT seem to learn different kind of information during pretraining.
- BERT is overparameterized and does not fully utilize the parameters it has; thus it can be compressed without much performance loss. 
