---
title: Understanding Ownership
tags:
  - rust
  - rust-ownership
  - compilers
d: 28/12/24
---
### What is Ownership ?
- Ownership is a set of rules that govern how a Rust program will manage the memory. Since all programs have to manage the way they use a computer's memory, some pl have garbage collection in their runtimes , in other languages , the programmer must explicitly allocate and free the memory.
- Rust manages the memory through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program then wouldnt compile.
- Before understanding ownership, we must first understand the differences bw stack and heap and how is memory managed.
### Stack and Heap:
- Both stack and the heap are parts of memory available to our code to use at runtime, but they are structured in different ways. 
- Stack stores the values in the order it gets them and removes the values in the opposite order.(LIFO fashion)
	- All the data stored on the stakc must have a known ,fixed size.
- Data with unknown size at compile time or a size that might change(think vectors, maps etc.) must be stored on the heap instead.
	- heap is less organized : when you put data on the heap,you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough,marks it as being in use, and returns a pointer, which is the address of that location.
	- This is called as allocating on the heap.
	- Since the pointer to the heap is known fixed size, we can store the pointer itself on stack, but when we want the actual data, we must follow the pointer.
- Pushing on the stack is faster than allocating on heap because the allocator never has to search for a place to store new data : the location is always at the top of the stack.
- Similarly allocating space on the heap requires more work because the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.

- Ownership addresses the problems of keeping track of what parts of code are using what data on the heap,minimizing the amount of duplicate data on the heap, and cleaning up unused data on the heap so that we don't run out of space are all problem that ownership addresses.

### Ownership Rules:
- The rules are:
	- Each value in Rust has a owner.
	- There can only be one owner at a time.
	- When the owner goes out of scope, the value will be dropped.
- 