---
title: Introduction of Reinforcement Learning
tags:
  - ai
  - rl
  - cs234
date: 5/2/25
---
### what is RL?
- learning through experience/data to make good decisions under uncertainty.
- Essential part of intelligence to make decisions - and has to be the general idea under general intelligence.
- Builds strongly from theory and ideas starting from the 50s with Richard Bellman.
- Practical and has a number of impressive success in the last decade.
	- Beyond Human Performance on the Board Game Go - Google DeepMind and Monte Carlo Tree Search 
	- Learning Plasma Control for Fusion Science -> Potential approach for sustainable energy 
	- Efficient and targeted COVID-19 border testing via RL.
	- ChatGPT -> 
		- Collect demonstrattion data and train a supervised policy (Behaviour Cloning / Imitation Learning)
		- Collect comparision data and train a reward model. -> Model of a reward (model based RL)
		- Optimize a policy against the reward model using the PPO reinforcement learning algorithm.
		- ![[Screenshot 2025-02-05 at 1.42.16 AM.png]]

### Skeptics of RL (Yann Lecun -2016)
#### "Pure" Reinforcement Learning(cherry)
- the machine predicts a scalar reward given once in a while 
- a few bits for some samples 
#### supervised learning (icing)
- the machine predicts a category or a few numbers for each input
- predicting human-supplied data 
- 10 -> 10,000 bits per sample

#### unsupervised/predictive learning (Cake)
- the machine predicts any part of its input for any observed part
- predicts future frames in video
- millions of bits per sample