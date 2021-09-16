<table> 
   <tr>
     <th> layout</th>
     <th> title</th>
     <th> paper</th>
     <th> author</th>
     <th> score</th>
   </tr>
   <tr> 
     <td> Summary</td>
     <td> Summary</td>
     <td> ADADELTA: AN ADAPTIVE LEARNING RATE METHOD, Zeiler1; 2012 - Summary</td>
     <td> Shivi Agarwal</td>
     <td> 8/10</td>
   </tr>
</table>

ADADELTA 


•	What is the core idea?
The paper introduces ADADELTA a learning rate used in gradient descendent algorithm for optimization of neural network.
ADADELTA is computed on a per-dimension basis using only first order information.
ADADELTA is better to other learning rates because it is robust to large gradients, noise and architecture choice and it requires minimal calculation over gradient descent.
ADADELTA performs better than ADAGRAD as it doesn’t decay the learning rate. In ADAGRAD due to continuous accumulation of squared denominator the learning rate eventually decreases to zero and stops training. ADAGRAD also requires to manually select the global learning rates which is not needed in ADADELTA.
ADADELTA uses the window of past gradients that are accumulated to be some fixed size.

•	How is it realized (technically)?
The ADADELTA is defined by the function:
Using accumulation over window it is defined as : 
       ∆xt = − η /RMS[g]t g 
	   
	 where gt is the gradient of the parameters at the t-th iteration
    and η is a learning rate,
	∆x is the set of parameters,
	
       
Using Correct Units with Hessian Approximation:
		∆xt = − RMS[∆x]t−1 /RMS[g]t gt
		∆x is the set of parameters
		gt is the gradient of the parameters at the t-th iteration
	
•	How well does the paper perform?
The ADADELTA Learning Rate was  tested on multiple tasks, such as the MNIST classification (handwritten digits dataset), Speech Data and 
outperformed other methods like SGD, Momentum, ADAGRAD in all tasks.

•	Experiments to test this learning rate:
    Task: Validate ADADELTA over Speech Recognition.
    Data: 26 frames of audio, each consisting of 40 log-energy filter bank output
    Model: r logistic or rectified linear nonlinearities 
    Evaluation metric: training issues and divergence in deeper architects.
    Side note: The ADADELTA method performs well, quickly converging to the same frame accuracy as the other methods.
    
    


<img src="ADADelta1.png">

<img src="Adadelta2.png">


TL;DR

•ADADELTA is a learning rate used in gradent decent algorithm.

•It outperformed all other learning rates across multiple classification tasks because it uses fixed window size (w).

•Due to the window size the laering rate decays at slower rate but the learning doesn't stop.


```python

```
