---
layout: summary
title: Summary
paper: brown2020language
# Please fill out info below
author: mattkelleher
score: 8
---
# Core Idea
By increasing their size it is possible to build language models that are task agnostic and are able to perform tasks well with zero-shot, one-shot, and few-shot learning.

# Context


**Fine-Tuning:** Traditional learning. Start with pre-trained model and update weights by training for a specific task.
Requires a labeled dataset for each new task to be learned.

**Zero-Shot:** Start with general model. Model is only given a description of the desired task in natural language. 
No examples or demonstrations. 
Network is given:

- task description
- a context (input) (to complete task on)
# example: translation, you would expect a person the understand to do without an example.
  
**One-Shot:** Similar to Zero-Shot except the model is given a single demonstration of the task.
 The network uses the example at inference time to 'see' the task and will use this information along with the natural language description of the task provided. 
Note that NO weights will be updated.
Network is given:

- task description in natural language
- 1 context output-pair 
- a context (to complete task on)   

**Few-Shot:** Similar to One-Shot with the addition of more demonstrations of the desired task. Note that while this does require making a dataset for each task, this dataset is much easier to make as it usually consists of 10-100 examples as opposed to the thousands or millions of examples needed for most tasks for the fine-tuning approach.

Network is given:

- task description in natural language
- a few (usually 10-100) context-output pairs
- a context (to complete task on)

# Technical Details

# Results 

# Other Experiments 

**Data Contamination**

TODO fill in

**Model Scaling**


TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
