---
title: Introduction
tags:
  - ai
  - deep-learning
date: 6/1/25
---
- In the early days of AI, the field rapidlyb tackled and solved the problems that are intellectually difficult for human beings but relatively straight-forward for computers - problems that can be described by a list of formal, mathematical rules.
- By gathering knowledge from experience , this approach avoids the need for human operators to formally specify all of the knowledge that the computer needs. The hierarchy of concepts allows the computer to learn complicated concepts by building them out of simpler ones.
- Many of the early successes of AI took place in realtively sterile and formal environements and did not require computers to have much knowledge about the world.
- Devising a successful chess strategy is a termendous accomplishment, but the challenge is not due to the difficulty of describing the set of chess pieces and allowable moves to the computer. Chess can be completely described by a very brief list of completely formal rules, easily provided ahead of time by the programmar.
- A person's everyday life requires an immense amount of knowledge about the world. Much of this knowledge is subjective and intuitive and therefore difficult to articulate in a formal way. Computers need to capture this same knowledge in order to behave in an intelligent way. One of the key challenges in AI is how to get this informal knowledge into a computer.
- **Knowledge Base**: A computer can reason about statements in these formal languages automatically using logical inference rules. Eg: Cyc and Cycl (not successful)
- **Machine Learning**: Difficulties faces by system relying on hard-coded knowledge suggest that AI systems need the ability to acquire their own knowledge , by extracting patterns from the raw data.
	- This allowed computers to tackle problems involving knowledge of the real world and make decisions that appear subjective. A simple ml algorithm called logistic regression can determine whether to recommend cesarean delivery.
	- A simple ML algorithm like Naive Bayes can seperated email spams from legitimate emails.
- **Representation**: Performance of these simple ML algorithms depends of the representation of the data they are given.
	- Eg: when logistic regression used to recommend cesaren delivery, the AI system does not examine the patient directly.
- **Feature**: Each piece of the information included in repr of the patient.
- The dependence on repr is a general phenomenon that appears throughout CS and even daily life. In CS, operations such as searching a collection of data can proceed exponentially faster if the collection is structured and indexed intelligently.
- Many AI tasks can be solved by designing the right set of features to extract for that task, then providing these features to a simple ML algorithm.
	- Eg: a useful feature for speaker identification from sound is an estimate of the size of speaker's vocal tract. It therefore gives a strong clue as to whether the speaker is a man,woman or child.
- For many tasks it is difficult to know what features should be extracted. 
	- Eg: we would like to write a program to detect cars in photographs. We know that cards have wheels, so we might like to use the presence of a wheel as a feature. Unfortunately , it is difficult to describe exactly what a wheel looks like in terms of pixel values.
		- Solution: Use ML to discover not only the mapping from representation to output but also the representation itself. This approach is known as **representation learning**.

- **Autoencoder**: Biggest example of representation learning algorithm. An autoencoder is the combination of 
	- an **encoder** function that converts the input data into a different representation.
	- an **decoder** function that converts the new representaiton back into the original format.
- They are trained to preserve as much information as possible when an input is run through the encoder and then the decoder , but are also trained to make the new representation have various nice properties. Different kinds of autoencoders aim to achieve different kinds of properties.

