---
title: Ownership in Rust
tags:
  - PL
  - rust
  - ownership
  - memory-management
  - memory-safety
date: 5/7/25
---
- Ownership is the most unique feature in Rust and has deep implications for the rest of the language.
- It enables Rust to make memory safety guarantees without needing a garbage collector, so important to understand how ownership works.
- Also cover several related features like:
	- borrowing 
	- slices 
	- how Rust lays data out in memory

### What is Ownership ?
- Ownership is a set if rules that govern how a Rust program manages the memory.
- All programs have to manage the way they use a computer's memory while running.
	- Some languages have GC that regularly looks for no-longer-used memory as the program runs.
	- In other languages, the programmer must explicitly allocate and free the memory.
- Rust uses a **third approach**
	- Memory is managed through a system of ownership with a set of rules that the compiler checks.
	- If any of the rules are violated -> the program won't compile. 
	- None of the features of ownership will slow down our program while its running.

### Stack and Heap:
- For most programming lang, they dont require us to think about the stack and the heap very often.
- Rust being a systems programming language, whether a value is on the stack or the heap affects how the language behaves and why we would have to make certain decisions.
- Both stack and the heap are parts of memory available to our code to use at runtime , but they are structured in different ways.
- **Stack**:
	- Stores values in the order it gets them and removes the value in the opposite order. LIFO policy.
	- Adding data is called pushing onto the stack , and removing data is calling popping off the stack.
	- All the data stored on the stack must have a known , fixed size. 
	- Data with a unknown size at compile time or a size that might change must be stored on the heap instead.
- **Heap**:
	- Less organized , when we put data on the heap, we request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough , marks it as being in use, and returns a pointer - address of that location.
	- Since the pointer to the heap is a known, fixed size, we can store the pointer on the stck, but when we want the actual data, we must follow the pointer.

- Pushing to the stack is faster than allocating on the heap since the allocator never has to search for a plate to store new data -> that location is always at the top os the stack.
- Allocating on the heap requires more work since the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.

- Keeping track of what parts of code are using what data on the heap, minimizing the amount of duplicate data on the heap, and cleaning up unused data on the heap so we don't run out of space are all problems that ownership addresses.


### Ownership Rules:
- **Each value in Rust has a owner**.
- **There can only be one owner at a time**.
- **When the owner goes out of scope, the value will be dropped**.

### Variable Scope
```rust 

{ //s is not valid here , as not yet declared 
let s = "hello"; // s is valid from this point onward 
} // this scope is now over, and s is no longer valid 
```
- In other words, there are 2 important points in time here:
	- When s comes into scope, it is valid.
	- It will remain valid until it goes out of scope.

### String type:
- String type Stored on the heap and explore how Rust knows when to clean up that data.
- String literals are convinient but they aren't suitable for every situation in which we may want to use text. 
	- One reasons is that they are immutable.
	- Not every string value can be known when we write our code: eg: what if we want to take user input and store it ?
- `String` type useful for these kind of cases. This type manages data allocated on the heap and is such is able to store an amount of text that is unknown to us at compile times.
```rust
let s = String::from("hello");
```
- Double colon :: operator allows us to namespace this particular form function under the String type rather than using some sort of name like `string_from`.
- This type of string can be mutated , as:
```rust 
let mut s = String::from("hello");
s.push_str(", world!");
println!("{s}");
```

### Memory and Allocation:
- With the `String` type , in order to support a mutable , growable piece of text, we need to allocate an amount of memory on the heap, unknown at compile time, to hold the contents. This means:
	- The memory must be requested from the memory allocator at runtime.
	- We need a way of returning this memory to the allocator when we are done with our `String`.
- The first part is done by us i.e we call `String::from` , its implementation will request the memory it needs.
- For the second part it is different.
	- For languages, with GC (garbage collector), the GC will keep track of and clean up memory that isn't being used anymore, and we don't need to think about it.
	- In most other programming languages without a GC, it's our responsibility to identify when a memory is no longer being used and to call code to explicitly free it, just as we did to request it. Doing this correctly has historically been a difficult programming problem. If we forget it, we'll waste memory. If we do it too early, we'll have an invalid variable.
- **Rust takes a different part; memory is automatically returned once the variable that owns it goes out of scope.**
	- in the scope function example above, there is a natural point at which we can return the memory our `String` needs to the allocator : when `s` goes out of scope.
	- When a variable goes out of scope, Rust calls a special function for us. This function is called `drop` , and it's where the author of `String` can put the code to return the memory.
	- Rust calls `drop` automatically at the closing curly bracket.
- `drop` is similar to how RAII works in C++.
