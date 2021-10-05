---
layout: summary
title: Summary
paper: sutskever2013on
# Please fill out info below
author: specfazhou
score: 9
---

TODO: Summarize the paper:
* What is the core idea? <br/>
The paper points that out classical momentum (CM) or Nesterov's accelerated gradient (NAG) can train DNNs and RNNs if initialization is well-designed and momentum coefficients are carefully chosen. Before this paper, people did achieved some successes by using first-order method together with good intializations, but that's still not as good as using HF optimization. However, this paper demonstrates that with use of momentum methods, the performance achieved is at the same level as using HF optimization, which shows us more potential of first-order method  <br/>

for reference, the followings are CM and NAG methods' <br/>
classical momentum (CM):<br/>
$$v_{t+1} = v_{t} - \epsilon \nabla f(\theta_{t})$$
<br/>
$$\theta_{t+1} = \theta_{t}+v_{t+1}$$
<br/>
Nesterov's accelerated gradient (NAG): <br/>
$$v_{t+1} = v_{t} - \epsilon \nabla f(\theta_{t}+\mu v_{t})$$
<br/>
$$\theta_{t+1} = \theta_{t}+v_{t+1}$$
<br/>





* How is it realized (technically)? <br/>
To show the performance achieved, the authors used CM and NAG to train deep autoencoders, which use sigmoid activication functions. They initialized parameters by using sparse initilization technique (SI), which makes each unit connect to 15 randomly chosen units in previous layer, and because input doesn't depend on the size of previous layer, they can't be easily saturated. the authors also chose momentum coefficient $$\mu_{t} = \min(1-2^{-1-log_{2}([t/250]+1)}, \mu_{max})$$ with $$\mu_{max} \in {0.999, 0.995, 0.99, 0.9, 0}$$. <br/>
To show the effectiveness of CM and NAG, the authors trained typical RNNs by using ESN-based initilization (ESN stands for Echo-State Network, which is one kind of RNNs whose recurrent connections are not learned but from a random draw from some distribution), and momentum methods with various different momentum coefficients and learning rates. One thing to notice is that in ESN-based initilization, it is important to carefully choose spectral radius of hidden-to-hidden matrix, and the scale of initial input-to-hidden connections to make the training effective. 

* How well does the paper perform?<br/>
From the results obtained from the training of Autoencoders, it seems if we use larger value of $$\mu_{max}$$, we will get better result, and NAG usually outperform CM. It is a surprise that the best results achieved by NAG is at the same level of best results gotten by HF. The authors also found that in the last several updates, it is beneficial to reduce momentum coefficient, but should be careful because if it happens too early, it can actually increase the error rates. <br/>
From the results obtained from the training typical RNNs, it seems RNNs can actually be trained by using ESN-based initialization, and momentum methods with large momentum coefficients and small learning rates. Better results can be achieved by NAG with larger momentum coefficient but not for CM probably because NAG has better tolerance of momentum coefficient. <br/>

* What interesting variants are explored? <br/>
The authors explains why NAG avoids oscillations (thus, more tolerant of large momentum coefficient) during training intuitively and theoretically in the paper.   

## TL;DR
1. Use momentums method with well-designed initialization to train DNNs and RNNs that previously thought impossible. But it turns out that first-order method just as good as truncated Newton methods like HF. <br/>
2. Compare the differences between classical momentum and Nesterov's accelerated gradient. <br/>
3. Large momentum coefficient will make momentum methods achieve better performance especially for NAG, because it has better tolerance for large momentum.
