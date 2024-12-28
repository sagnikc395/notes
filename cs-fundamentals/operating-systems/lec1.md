---
title: Lecture 1 - Operating Systems
tags:
  - operating-systems
date: 28/12/24
---
## Course Outline and Topics:
### Processes and Threads
### Memory Management 
### Storage and File Systems 
### Distributed Systems 

These 4 peices map to the resources that we see on any machine and managing each of them maps the things that the operating systems manages for each system.

We learn from these how the OS manages the machine for these.

## What is an Operating System ? 
- Definition has changed over the years:
	- Originally, very bare bones 
	- now includes more and more 
	- Essentially an interface between the user and the architecture.
	- Implements a virtual machine 
	- (hopefully) easier to program than raw hardware.
- A lot of the underlying details and the abstractions are dealt by the operating systems itself.
- A Traditional view of OS:
	- Interface between user and architecture:
		- Hides architectural details 
	- Implements virtual machine:
		- Easier to program than raw hardware.
	- Illusionist:
		- Bigger, Faster and reliable
	- kinda like govt. -> managed centrally to allocate resources and do resource management -> some overhead like taxes like govt.
- New Development in OS:
	- Operating Systems: An Active Field of Research:
		- Demands on OS's growing 
		- New application spaces(web,grid,cloud)
		- Rapidly evolving hardware
	- Advent of open source operating systems:
		- Linux etc.
		- Excellent research platform.

### Operating Systems : Salient Features:
- **Services**: OS provides standard services(interface) which the hardware implements.
	- Ex: the file system, virtual memory, networking, CPU scheduling and time-sharing (run more than one application at a time -> time share an application bw the common hardware.)
- **Coordination**: OS Coordinates multiple applications and users to achieve fairness and efficiency(throughput).
	- Ex: concurrency, memory protection, networking and security.
- Major goal for most operating systems development is to design an OS so that the machine is convenient to use(a software engineering problem) and efficient(a system and engineering problem).
	- Ideally we want both, but we necessarily wont be able to make both work.
	- Designing a operating system is a tradeoffs and to make correct tradeoffs worth the cost.
	- The decisions do matter as it is thousands of lines of codes -> system needs to be efficient and fast.

### Why study Operating Systems ?
- **Abstraction**: OS gives users an illusion of infinite memory, CPUs, resources , WWW etc.
	- How to scale this up for larger machines and services ?
- **System Design**: How to make tradeoffs bw:
	- performance and the convenience of OS abstractions.
	- performance and the simplicity of OS Design and 
	- putting functionality in hardware or software.
- **System Level Understanding**: The OS provides the services that allow application programs to work at all.
- **System Intersection Point**: The OS is the point where hardware and software meet. OS exports the system call interface (the API) for the application , which the end-user applications uses to interact with hardware. Higher level interfaces/libraries exist that further make it easier to program on top of the system call.

- Think of building OS as an example of building a large scale system design.
- Goals: Fast,Reliable and large scale.
- To build these systems, we need to know about:
	- Each computer:
		- Architectural details that matter 
		- C/C++ (systems knowledge and nitty gritty)
		- Memory management and locality 
		- Concurrency and scheduling 
		- Disks, networks and file systems 
	- Across Cluster:
		- Server architecture 
		- Distributed Computing, File Systems 

## Historical Context of Operating Systems:
- An overview of operating systems from mainframes to web based software.

### Single User Computers:
- 1960s 
- hardware capital was expensive, human capital was cheap.
- one user at a time on console:
	- interacting with as program runs 
- computer executes one function at a time:
	- no overlap: computation and I/O 
- User must be at console to debug 
- Uni-programming : one process at a time operating systems 
- Multiple Users = inefficient use of the machine , CPU more idle and more IO devices are sitting idle.
### Batch Processing (feature of OS):
- Early OS did not have fancy user interface, had to load program using punch cards and machine read them and executed them linearly.
- An method developed to batch the programs(cards) together to produce an output.
- Execute multiple "jobs" in batches:
	- Load the program 
	- Run 
	- Print the results, dump machine state 
	- Repeat 
- Users submit jobs(on cards or tape)
- human schedules jobs 
- Operating system loads and runs the jobs 
- A slightly efficient use of the machines.
- Eg: Data Processing for Payroll for employees.
### Overlap I/O and Computation:
- Both batch processing and uni-programming is an ineffective use of our resources for the program to run.
- We want some sort of continuous program to run in background processes.
- The CPU cycles are getting wasted waiting for the machine for I/O to complete.
- New approach:
	- Allow the CPU to execute while waiting 
	- Add a buffering layer:
		- Data fills the "buffer" and then outputs
	- and interrupt the handling:
		- I/O events trigger a signal("interrupt")
- Leads to a more efficient use of the machine:
	- however we are still limited to one job at a time.
	- leads to multi-programming of OS.
### Multiprogramming:
- A huge achievement if Operating System Design and led to its popularity.
- Several program can now run simultaneously:
	- Run one job until I/O
	- Run another job etc.
- OS can now manage interactions:
	- Which jobs to run (schedule)
	- Protects the program's memory from others ,so as to prevent memory protection and so that processes are not crashed.
	- Decides which program to resume when the CPU is available.
### OS Complexity:
- Over the 60s-70s and 80s led to increased functioanlity and complexity of writing such code bases.
- Led to interesting challenges and first OS failures were also reported:
	- Multics(GE and MIT) announced in 1963,released in 1969
	- OS/360 released with 1000 known bugs.
- Need arose to treat OS design scientifically.
- Managing complexity becomes the key to development of UNIX (from the failures of Multics.)
- Rather than making the OS very complex, make small utlities than do them well and make bigger programs by composition rather than making the core very big.

### The Renaissance(1970s)
- Hardwre had become cheaper, humans have become expensive.
- Users share system via terminals.
- The UNIX era:
	- Multics:
		- army of programmers, six years to complete.
	- Unix:
		- 3 guys, 2years to complete.
		- "shell" -> composable commands 
		- no distinction between programs and data 
- Introduced the concepts of response time and thrashing in UNIX.

### Industrial Revolution(1980s):
- PCs started being manufactured and hardware design became very very cheap as compared to human cost.
- Led to widespread use of PCS:
	- IBM PC: 1981, Macintosh: 1984.
- Simple OS (DOS,MacOS):
	- No multiprogramming, concurrency, memory protection, virtual memory.
	- Later: added netwokring, file-sharing, remote printing.
	- GUI added to OS(WIMP)
	- MSDOS was a uni-programming environment.

### Modern Era (1990s-now):
- Hardware became extremely cheap, processing demands increased.
- "Real" operating systems on PCS:
	- NT(1991), Mac OS X,Linux 
- Different modalities:
	- Real-time : strict or loose deadlines 
	- Sensor/Embedded : Many small computers 
	- Parallel: multiple processors, one machine 
	- Distributed: Multiple networked processors
		- P2P,Web,Google,Cloud etc.
	- OS for phone, tablets, watches,TV.

## Architectural Trends:
- 9 orders of magnitudes of CPUs change and increasing of Moore's law.
- Big Changes:
	- In 50 years,almost every computer component now, 9 orders of magnitude faster,larger and cheaper.
	- OS Design has kept up the increasing demands,architecture changes and multi-core systems.
- Moore's Law = running out of steam.
- New "features" coming:
	- Multiple cores
	- Unreliable memory 
	- serious power/heat constraints 
- Other Tradeoffs possible:
	- Computing power is reliability.
- OS is the abstraction layer , that splits bw the software and the hardware. OS reacts to changes in hardware, and can motivate changes.

## Core Ideas of Operating Systems Principles:
1. **OS as juggler/virtualizer**: providing the illusion of a dedicated machine with infinite memory and CPU.
2. **OS as government**: protecting users from each other, allocating resources efficiently and fairly, and providing secure and safe communication.
3. **OS as complex system**: Keeping OS design and implementation as simple as possible is the key to getting the OS to work.
4. **OS as history teacher**: Learning from past to predict the future i.e OS Design tradeoff's change with technology.


