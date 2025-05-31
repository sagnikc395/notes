---
title: History of Deep Learning and Progress till 2022
tags:
  - ai
  - deep-learning
  - history-of-dl
date: 22/5/25
---
#### Small History of Deep Learning:
1. 1943 -> McCulloch and Pitts, networks of binary neurons can do logic; if we have binary elements, can do logical computations and inference - for reasoning 
2. 1947 -> Donald Hebb, Hebbian Synaptic Plasticity -> by changing the strengths of the neurons in the brain , they can change the strength of the networks
3. 1948 -> Norbert Wiener, Cybernetics -> Systems Theory now, Optimal Filter, Feedback,Autopoises, Auto Organization; Very complex phenomenon emerging from simple systems. Connecting lots of lots of simple things and rules -> they can self organize into rules (seen in biology)
4. 1957 -> Frank Rosenblatt ; Perceptron -> simple idea -> supervised learning ; having a system that can classify ->  patterns by adjusting weigths -> synapses on a neuron.
5. 1961 -> Bernie Widrow -> Adaline -> very similar to perceptron -> neuro classifier
6. 1962 -> Hubel and Wiesel -> Visual Cortex Architecture -> architecture of the visual cortex -> lead to a Nobel Prize.
7. 1969 -> Minsky and Papert -> Limits of the Perceptron. -> lead to Winter of AI -> killed the whole field in the late 70s.
8. 1970s -> statistical pattern recognition -> Duda and Hart / adpative filters 
9. 1979 -> Kunihiko Fukushima , Neocognitron -> neural nets and cognitron 
10. 1982 -> HopField Networks -> physicists ; 
11. 1982 -> Hinton and Sejnowski -> Boltzmann Machines -> Physicsist
12. 1985/86 -> Practical Backpropogation for neural net training 
13. 1989 -> Convolutional Networks -> started the NIPS conference; and brought back the attention to neural networks.  
14. 1991 -> Bottou and Gallinari -> module based automatic differnetiation 
15. 1995 -> Hochreiter and Schmidhuber -> LSTM recurrent net 
16. 1996 -> Structured prediction with neural nets -> graph transformer nets 
17. 2003 -> Yoshua Bengio -> Neural Language Model
18. 2006 -> Layer-wise unsupervised pre-training of deep networks.
19. 2010 -> Collobert and Weston -> self-supervised neural nets in NLP
20. 2012 -> AlexNet /convent on GPU/ Object classification 
21. 2015 -> I. Sutskever  -> Neural machine translation with multilayer LSTM 
22. 2015 -> Weston, Chopra and Bordes -> Memory Networks 
23. 2016 -> Bahdanau,Cho,Bengio -> GRU, Attention Mechanism 
24. 2016 -> Kaiming He -> ResNet 

#### Supervised Learning goes back to the Perceptron and Adaline: 
- Main thing was the McCullough-Pitts Binary Neuron where the perform weighted avergeas and compared to a threshold and turns off if less than a threshold.
- ![[Screenshot 2025-05-22 at 3.12.56 PM.png]]

- Perceptron-> weights are motorized potentiometers.
- Adaline -> Weights are electrochemical "mimstors"
$$
y = \text{sign}\left(\sum_{i=1}^{N} W_{i} X_{i} + b\right)
$$

#### Hot Topics in AI:(2022 version)
- Self Supervised Learning - learning without looking into the data before -> pretrain a neural net to understand the data without fine tuning for processing. Then fine tune of what thing we would want to optimize. Improved a lot of computer vision.
- Machine Based Reasoning - learning like humans -> Animals and Humans can do perceptions, navigating etc that dont require reasoning -> for long chains of reasoning and planning -> how to modify our architectures for reasons. Machine networks -> reason on it and then change the basis of the underlying networks.
- How to train systems to train on action plans and stuff ?

#### Limitations and Quantum Computing and Non binary states
- one big challenge, can we come up with paradigms that will allow the  machines to come up with reasoning on its paradigms by observing and common sense. No machine has common sense yet ! AI systems have very narrow intelligence.
- Quantum Computing and AI is still much up in the air , and in a academic research subject it is interesting to observe.