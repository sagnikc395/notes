---
title: Introducing Deep Learning and PyTorch Library
tags:
  - ai
  - pytorch
date: 6/1/25
---
### AI and Deep Learning:
- AI essentially is a general class of algorithms that are able to approximate complicated , non-linear processes very,very effectively, which we can use to automate tasks that were previously limited to humans.
- The ability to perform these formerly human-only tasks is acquired through examples, rather than encoded by a human as a set of handcrafted rules. In a way, we are learning that intelligence is a notion we often conflate with self awareness, and self-awareness is definitely not required to successfully carry out these kinds of tasks.
- Deep Learning uses large amounts of data to approximate complex functions whose inputs and outputs are far apart, like an input image and as output a line of text describing the input or a written script as input etc.
- Until the last decade, the broader class of systems that fell under the label ML relied heavily on **feature engineering**. Features are transformations on input data that facilitate a downstream algorithm, like a classifier,to produce correct outcomes on new data. Feature engineering consists of coming up with right transformations so that the downstream algorithm can solve a task.
- Deep learning on the other hand. deals with finding such representations automatically , from raw data, in order to successfully perform a task. However, the ability of a neural netowrk to ingest data and extract useuful representation on the basis of examples is what makes deep learning so powerful. The focus of deep learning practitioners is not so much on handcrafting those representations, but on operation on a mathematical entity so that it discovers representations from the training data autonomously. Often, these automatically created features are better than those that are handcrafted.
- Successful way of executing deep learning:
	- We need a way to ingest whatever data we have at hand.
	- We somehow need to define the deep learning machine.
	- We must have an automated way, training, to obtain useuful repr, and make the machine produce desired outputs.
- During training , we use **criterion**, a real valued function of model outputs and reference data, to provide a numerical score for the discrepancy between the desired and actual output of our model. Training consists of driving the criterion towards lower and lower scores by incrementally modifying our deep learning machine until it achieves low scores, even on data not seen during training.

### About PyTorch:
- PyTorch is a library for Python programs that facilites building deep learning projects. It emphasized flexibility and allows deep learning models to be expressed in idiomatic Python.
- PyTorch provides an excellent intro to deep learning. At the same time, PyTorch has been proven to be fully qualified for use in professional contexts for real-world, high-profile work.
- To facilities expression the complex mathematical function , PyTorch provides a core data structure, the tensor, which is a multidim array that shares many similarities with NumPy arrays.
- PyTorch also comes with features to perform accelerated mathematical operations on dedicated hardware, which makes it convinieent to design neural network architecture and train them on ind. machines of parallel computing resources.
- Main reasons:
	- Simplicity, used my many researchers and practioners and deployed on prod. Easy to learn,use and extend and debug.
	- Deep learning machine is very natural in PyTorch. PyTorch gives us a data type, the Tensor, to hold numbers, vectors, matrices, or arrays in general. In addition, it provides functions for operating on them.
	- Particularly relevant for deep learning:
		- Provides accelerated computation using GPUs
		- Provides facilities that support numerical optimization on generic mathematical expressions, which deep learning uses for training.
	- Expresseivety , allowing a developer to implement complicated models without undue complexity being imposed by the library.
	- PyTorch also has a compelling story for the transition from research and develop- ment into production. While it was initially focused on research workflows, PyTorch has been equipped with a high-performance C++ runtime that can be used to deploy models for inference without relying on Python, and can be used for designing and training models in C++.
### Overview of how PyTorch supports deep learning projects:
- For performance reasons, most of PyTorch is written in C++ and CUDA(NVIDIA) that can be compiled to run with massive parallelism on GPUs.
- Python API is where PyTroch shines in terms of usuability and integration with the wider Python ecosystem.
- At its core, PyTroch is a library that provides mutlidimensional arrays, or tensors (PyTorch vocab) and an extensive library of operations on them, provided by the torch module.
	- Both tensors and the operations on them can be used on CPU or GPU. 
	- Moving computations from CPU to the GPU in Pytorch doesnt require much effort.
- PyTorch proides the ability of tensors to keep track of the operations performed on them and to anlytically compute derivatives of an output of a computation with respect to any of its inputs. Used for numerical optimization, and it is provided natively by tensors by virtue of dispatching through PyTorch's autograd engine under the hood.