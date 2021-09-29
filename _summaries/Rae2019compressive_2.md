---
layout: summary
title: Summary
paper: Rae2019compressive_2
# Please fill out info below
author: specfazhou
score: 8/10
---

## core idea
In this article, the authors proposed Compressive Transformer, a variant of Transformer, which achieved the-state-of-art resutls on character-based language modelligng and word-level language modelling.
Compressive Transformer also performed very well on the book-level language modelling. The Compressive Transformer, neither like Transformer that computationally expensive, nor like TransformerXL that discard old enough activations, it compress past activations into compressed memory.
The Compressive Transformer not only achieved computational and storage efficiency, but also remember all the past activations. 

## how is it realized?
The Compressive Transformer only uses attention to propagate information, and it has two parts of memories --- normal memory and compressed memory. With sequences coming in, they first 

