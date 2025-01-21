---
title: OS and Computer Architecure
tags:
  - operating-systems
  - computer-architecture
date: 28/12/24
---

(continue from 12:10)
## OS and Computer Architecture:
### Modern OS Functionality 
- **Process and Thread Management**
- **Concurrency**: 
	- Doing many things simultaneously (I/O, processing, multiple programs etc.)
		- Several users work at the same time as if each has a private machine.
		- Threads (unit of OS control) - one thread on the CPU at a time, but many threads active concurently.

- **I/O devices**: Let the CPU work on compute while a slow I/O device is working.
- **Memory Management**: OS coordinates allocation of memory and moving data bw disk and main memory.
- **Files**: OS coordinates how disk space is used for files, in order to find files and to store multiple files.
- **Distributed Systems and Networks**: allow a group of machines to work together co-operatively on distributed hardware.

### Basic Architecture Refresher
- ![[Screenshot 2024-12-28 at 3.07.26 PM.png]]
- Generic Computer Architecture: ![[Screenshot 2024-12-28 at 3.08.44 PM.png]]
- Core pieces of the Computer Architecture:
	- **CPU** : the processor that performs the actual computation.
		- multiple "cores" common in today's processors.
	- **I/O devices**: terminal, disks,video bound, printer etc.
		- Network card is key component, but also an I/O device.
	- **Memory**: RAM containing data and programs used by the CPU.
	- **System Bus**: Communication medium between CPU,Memory and peripherals. How the CPU will fetch instructions from the memory.

### What the OS can do is dictated in part by the architecture and Architectural support can greatly simplify or complicate the OS



