---
title: Stable Diffusion Paper Discussion
tags:
  - text-to-image
  - ai
  - diffusion
date: 18/2/25
---
### Main topics discussed:
1. Latent Diffusion Models 
2. Maths of Diffusion Models 
3. Classifier-Free Guidance 
4. Text - to - Image 
5. Image - to - Image 
6. Inpainting 

### What is a generative Model ?
- SD is a text-to-image deep learning model, based on diffusion models. Introduced by CompViz group at LMU Munich.
- Diffusion models are generative model. A generative model learns a probability distribution of the data set such that we can then sample from the distribution to create new instances of data. 
	- Eg: if we have many pictures of cats and we train a generative model on it, we then sample from this distribution to create new images of cats.

### Why do we model data as distributions ?
- Imagine you are a criminal, and you want to generate thousands of fake identities. Each fake identity, is made up of variables, repr. the characteristics of a person(Age,Height).
- We can ask the Stats dept of govt. to give us statistics about the age and the height of the population and then sample from these distributions.
	- what does it meean to sample ? 
		- throw a coin that has a very very high change to fall in the median area and a very low chance to fall in the extremes.
- 