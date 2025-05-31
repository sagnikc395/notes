---
title: Gradient Descent and Backpropogation algorithm
tags:
  - ai
  - gradient-descent
  - backpropogation
  - shallow-networks
  - loss-function
date: 31/5/25
---
### SuperVised Learning 
- Training a machine by showing examples instead of programming it explicitly.
- When the output is wrong, tweak the parameters of the machine.
- Works well for:
	- Speech -> words 
	- Image -> categories 
	- Potrait -> name 
	- Photo -> caption 
	- Text -> topic 
- Most of the practical applications of deep learning and AI in general use this paradigm.
- Eg: differentiation of images from car and airplanes.
- Works really well when we have lots of data to train our examples for.

### Standard Paradigm of Pattern Recognition and ML
- Born in the 1960s.
- part of the traditional Machine Learning 
	- until the Deep Learning Revolution (2012)
	- ![[Screenshot 2025-05-31 at 6.08.16 PM.png]]
	- The trainable classifier is where the learning takes part 
	- Still popular , but superseeded by new algorithms using deep learning.
### MultiLayer Neural Nets and Deep Learning 
- Deep Learning has replaces the manual hand enigneered way of feature extractor using multi layers of neural networks which are trainable -> hence called deep as the stack transforms the input into something else and then we train the entire system end to end.
- ![[Screenshot 2025-05-31 at 10.04.10 PM.png]]
- The practical methods for this go back to a long time -> the backpropogation algorithm.
- Took some time for this idea to percolate and for people to build machine learning system.

### Parameterized Models:
- Parameterized Model -> learning model, is basically a parameterized function.
$$ 
	 \overline{y} = G(x,w)
$$
- ![[Screenshot 2025-05-31 at 10.08.45 PM.png]]
- This parameterized model produces a single output lets say a vector, matrix or tensor -> generally something multidimensional or something like a sparse array representation or something like a graph.
- Both the input x, and output $\overline{y}$ are multidimensional arrays / tensors and these are parameterized by some parameters $w$ which are some knobs that we are going to adjust during training and these are basically going to determine the input/ output relationships bw input $x$ and predicted output $y$.
- **Cost Function**:
	- If any machine learning algorithm it will have an cost function.
	- The cost function in supervised learning as well as in other algorithms will compute the discrepencies, distance , divergence bw desired output $y$ and the $\overline{y}$ .
	- Eg: Linear Regression 
		$$
		\overline{y} = \sum_{i}{w_{i}x_{i}}\space{C(y,\overline{y})} = || y - \overline{y} ||^{2}
	  $$ 
		- here we are computing the square distance bw $y$ and $\overline{y}$. 
		- This G may not be something simple to compute and something fixed number of steps and may involve minimizing the value wrt some other values.
	- **Computing function G may involve complicated algorithms**.

#### Block Diagram Notations for computation graphs 
- Variables (tensor, scalar, continuous, discrete...)
	- observed: input, desired output...
		- ![[Screenshot 2025-05-31 at 10.21.37 PM.png]]
	- computed variable: outputs of deterministic functions 
		- ![[Screenshot 2025-05-31 at 10.22.02 PM.png]]
- Deterministic Function:
	- ![[Screenshot 2025-05-31 at 10.22.20 PM.png]]
	- Multiple Inputs and outputs (tensors,scalars,...)
	- Implicit parameter variable (here: w) that are tunable by training 
- Scalar Valued Function(implicit output) -> Cost Function :
	- ![[Screenshot 2025-05-31 at 10.23.05 PM.png]]
	- Single Scalar Output (implicit) 
	- used mostly for cost functions 
- Symbolism kinda similar to graphical models -> Factrographs
	- Graphical models dont care about the fact that you are directed models in one direction or the other.
	- Here we care about it.

### Loss Function, Average Loss:
- Machine learning consist in finding the $w$ that minizimizes the cost function averaged over the training set.
- A simple per-sample loss function:
$$
	L(x,y,w) = C(y,G(x,w))
$$
- **Training Set**: Set of pairs, $x,y$ indexed by a index $P$ training samples and overall loss function that we have to minimize is equal to the discrepancy over the model $y$ and its output $\overline{y}$ . 
- ![[Screenshot 2025-05-31 at 10.51.37 PM.png]]
- A set of examples: 
$$ 
	S = \{(x[p],y[p]) / p = 0 .... P -1\}
$$
- So the average loss over the set:
$$
L(S,w) = 1/P\sum_{(x,y)}L(x,y,w) = 1/P\sum_{p=0}^{P-1}L(x[p],y[p],w)
$$
- The avg operation computes the loss, we can write in terms of the graphs.

### Supervised Machine Learning - Function Optimization 
- Supervised machine learning and a lot of other machine learning can be just viewed as function optimizations.
- ![[Screenshot 2025-05-31 at 10.57.39 PM.png]]
- It's like walking in the mountains in a fog and following the direction of steepest descent to reach the village in the valley.
- But each sample gives us a noisy estimate of the direction. So our path is a bit random each time.
- ![[Screenshot 2025-05-31 at 10.58.52 PM.png]]
$$
 W_{i} = W_{i} - \eta(\delta L(W,X)/(\delta W_{i}))
$$
- 