---
title: GPU Architecture, CUDA and NCCL
tags:
  - gpu
  - performance
date: 21/5/25
---
### GPU Architecture
- CPU vs GPU characteristics:
	- CPUs are latency optimized ,GPUS are throughput optimized.
	- CPU => Sports Car -> minimize the total time of trip for one person 
	- GPU => bus -> optimize for the number of people moves per hour
		- We achieve higher throughput 
- Terminology:
	- CPU = "host"
	- GPU = "device"
	- Kernel = GPU function executed in parallel across many threads. Fundamental unit of execution in CUDA.

| Component       | CPU Time(ns) | GPU Time (ns) |
| --------------- | ------------ | ------------- |
| FMA             | 1            | 5.2           |
| Register Access | 0.3          | 5.2           |
| L1 Access       | 1            | 25            |
| L2 Access       | 2.5          | 260           |
| DRAM Access     | 63           | 520           |
#### CPU vs GPU High Level architecture 

![[Screenshot 2025-05-21 at 10.44.34 AM.png]]
- CPU cores are high performance cores that are optimized for low latency serial executions
	- Our true degree of parallelism is limited to the number of cores that are allowed.
	- DRAM , L3 Cache -> Common across the cores
	- Slighly bigger L2 cache than L1 cache.

- The GPUs have more higher number of cores -> small and can lead to higher latency -> but they are huge in number.
	- These indv cores are not as powerful as CPU cores -> but can achieve parallelism and higher throughput than CPU cores.
	- Shared L2 cache and shared memory in DRAM.


- Actually these exist in "streaming multiprocesser" -> higher the number is better.

#### Streaming Multiprocesser
![[Screenshot 2025-05-21 at 10.52.19 AM.png]]
- Composition:
	- An SM consists of multiple arithmatic logic units (ALUs), special function units,and memory (eg: registers,shared memory)
- Instruction Parallelism:
	- An SM executes threads in groups called  warps. A wrap is a group of typically 32 threads on NVIDIA GPUs.
	- All threads in a wrap execute the same instructions in the same order -> (SIMT - single instruction multi-threaded execution model).
		- SIMT is a generalization of strict SIMD in which threads can diverge in execution paths (due to conditional branching)
		- All 32 threads execute the same set of instructions, in the same order , but may operate on different data.
		- The GPU is not working with individual threads but dealing with warps. -> these are chunking through parllel group of computations through it. -> hides memory complexity.
- Control Logic:
	- The SM contains scheduling hardware to manage the execution of multiple wraps and switches between them to hide memory latency.

- We have specific tensor cores -> specialized cores that are specialized hardware for doing matrix multiplication . -> good for deep learning architectures.

- Warp Definition:
	- A warp is the smallest unit of execution within an SM. It consists of a set of threads (eg: 32 threads on NVIDIA GPUs) that execute the same instruction simultaneously but on different data (SIMD - Single Instruction, Multiple Data Model).
- Warp Execution:
	- The SM schedules warp for execution. At any given time, the SM might execute on warp, switch bw multiple warps, or stall if there are dependencies or resource constrainsts.
- Concurrency:
	- An SM can manage multiple warps concurrently, depending on the hardware's capability(eg: the maximum number of active warps per SM). The total number of active threads is constrained by resources like registers, shared memory, and the architecture's warp limit.
- Divergence Handling:
	- Within a warp, all threads must execute the same instruction. If threads within a warp diverge(Eg: due to an if-else branch), the SM handles each divergent path sequentially, potentially reducing efficiency.

#### latency comparision of memory/cache access versus computational operations.

- ![[Screenshot 2025-05-21 at 11.17.44 AM.png]]
- thing that we will grapple with training workloads/ ML workloads generally is that :
	- to scale well, try to overlap / hide our memory access latency - network computations.
	- find someway not do useful compuatations and not be blocked in some way.

#### ML at Scale and How GPUS fit in:
- System Diagram of GCP A3 VM with 2 H100s 80GB GPUs
	- ![[Screenshot 2025-05-21 at 11.20.52 AM.png]]
	- PCIe -> to move data to and from host memory and data memory.
	- NVLink -> how fast can interchip communication happen 
	- The slowest network is our DCN and is a resource constriant will designing our ML at Scale applications.
	- Infiniband -> specialized network link and network protocol that can give higher network bandwidth.
	- GPUDirect -> RDMA technology, allows to skip these steps of multiple copies ; allows the GPU and NIC to integerate directly.
	- GPU ->
		- Compute Constraints -> floating point 32 data type, 982 tflops/s, dwarfs many of the other numbers.with all these constraints , our network bandwidth and so on, we are gonna struggle to feed GPU data quickly enough , to use all that power unless we carefully arrange when and how we move data over the network -> overlap it with computation -> or maybe do compiler optimizations like kernel fusions.
		- or do more floating point operations that come in it.
	-  From the official NVIDIA developer docs, the imbalance grows with lower precision data types.