---
title: Flash Attention
tags:
  - flash-attention
  - ml-algorithms
  - ai
  - performance
date: 31/5/25
---
### Motivation:
- The basic motivation for flash attention is that past a certain context, training with long context gets very very difficult with quadratic attention.
- It has so many attention heads and so many decoder blocks that each head has to be have this big matrix of attention scores stored in GPU memory and the work and memory, trying to store all of this and to load and compute all of them gets insane.
- Past a certain point it is impossible and would get out of device memory and its brutal and it takes really , really long time -> really really painful.

### Flash Attention 
- Key Idea: be I/O aware, with respect to HRAM access 
- Sometimes it's faster to recompute than to load from memory.
	- Ideally do as few loads as possible and do as much work done as possible per byte we have to load per GPU memory.
 $$ 
 Arithmatic Intensity = Floating Point Operations \div{Memory Accesss}
 $$
 - We really need to be judicious with our loads -> and when we do load something , we dont want to be doing something like saves which are unnecessary. 
 - Arithmetic Intensity is basically reduce the number of floating point accesses per memory access.
	 - We try to increase arithmetic intensity to the level to which we are compute bound, and once we cross the threshold where we are compute bound , then there is frankly nothing we can do.
	 - We just to have get more GPUs at that point.
- Attention Formulation:
	- **Require**: Matrices Q,K,V \belongs