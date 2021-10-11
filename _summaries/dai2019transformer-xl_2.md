---
layout: summary
title: Summary
paper: dai2019transformer-xl
# Please fill out info below
author: elampietti
score: 9.5
---

Langauge modeling problems have been limited in performance due to the difficulty of building models that can capture long-term dependency. 
Solutions have included recurrent neural networks (RNNs) such as long short-term memory (LSTM) networks that use predefined context length segments.
However, due to their fixed-lengths and lack of information flow between segments, they do not respect semantic boundaries and do not have enough context to predict the beginning of a sentence.
This problem of context fragmentation is addressed in this paper with their novel architecture called Transformer-XL.

This paper improves upon the vanilla transformer language model which splits up sequences into same-sized segments for training while ignoring information from previous segments as seen in the figure below.
This constrains long-term dependencies by the segment length and can lead to context fragmentation by just dividing each sequence into fixed-length segments.

![vanilla_transformer](https://user-images.githubusercontent.com/7085644/135945858-51368548-2b71-4f03-8ce9-6240bd2dffbf.PNG)

To improve information flow between segments, the hidden states for each segment are not completely re-computed and instead are built using information on the hidden states for previous segments.
This allows the model to capture long-term dependencies through these recurrent connections and the largest dependency length now increases based on the number of layers and segment length.

![xl_transformer](https://user-images.githubusercontent.com/7085644/135946726-baff9230-7e7d-43f3-bcb3-6d517efb1e4d.PNG)

Additionally, the Transformer-XL mitigates temporal confusion while achieving state re-use by using relative positional encodings instead of absolute ones.
If the absolute positions were used in segments, then the recurrence mechanism in the Transformer-XL would not be able to distinguish positional differences between segments.
Instead, relative positions are encoded in hidden states and injected into the attention scores so that the state re-use mechanism can be used and distinguish positional differences.
This difference in computing absolute vs. relative attention scores can be seen below.

![attention_standard](https://user-images.githubusercontent.com/7085644/135948745-83daedd3-57f1-418f-96fb-f3dd30fe5a39.PNG)
![attention_relative](https://user-images.githubusercontent.com/7085644/135948753-119d30e9-3418-4c7a-979d-4d751ed3c5ee.PNG)

The absolute positional embeddings U_j are replaced with the relative embeddings R_i-j and trainable parameters 'u' and 'v' are added to ensure the attentive bias is constant regardless of query position.
Also the weights matrices 'W' are separated into content and location key vectors.

The Transformer-XL model performed well against the state-of-the-art systems with results displayed below. 

![performance_1](https://user-images.githubusercontent.com/7085644/135950392-ebcac12e-66b1-45e2-8b24-6ede02b677e2.PNG)

The previous state-of-the-art model, Adaptive Input, achieved a perplexity of 20.5 while the Transformer-XL achieved 18.3.
The 12-layer Transformer-XL also outperforms the 12-layer vanilla Transformer by 0.05 and matches the 64-layer performance.
Variations include increasing the model size to 18 and 24 layers which resulted in even better performance and achieve 0.99 on known character level benchmarks.
Finally, evaluation speed of the Transformer-XL improved by 1,874 times against the vanilla Transformer model.

## TL;DR
* Capturing long-term dependences is a crucial step towards improving performance in language modeling that LSTM and vanilla transformer models struggle with.
* Traditional fixed-length segmenting during training constrains the longest dependency length by the segment size and can lead to context fragmentation.
* The novel Transformer-XL architecture address these issues with reccurence that allows for information flow between segments and a new relative positional encoding scheme.
